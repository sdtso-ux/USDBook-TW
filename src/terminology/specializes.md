# Specializes (特化)
「Specializing (特化)」是一種以 prim 及旗下 hierarchy 為基礎定義，並進行進階精煉 (refining) 來產生特定客製化分身 (specialized version) 的機制。舉例來說，您可以將一個標準的 Metal 金屬材質予以特化，修改部分屬性後創造出一個獨立的 CorrodedMetal (腐蝕金屬) 材質。這種「特化與精專」的應用層面廣泛，從調整材質基礎數值，甚至到重新定義整組 shaders 或是貼圖結構皆可達成。總體來看，這機制與 Inherits (繼承) 具有高度的相似性！然而，兩者之間存在著一項最核心的差異（key difference）。

> **💡 提示**
>
> 「不論面臨何種層級的系統覆寫，只要本身被寫入定義為 Specializations (特化) 的 Opinions (意見/主張)，它**永遠擁有最高順位的優先權勝出**。」


一旦有其他的 Opinion 試圖對已處於 specialized (特化) 狀態下的屬性提出覆寫挑戰時，該特化屬性仍會維持原判，並主動略過及捨棄這些外部的覆寫請求。這項判定邏輯若放到 [Inherits (繼承)](./inherits.md) 的規矩脈絡中，結果則會完全反過來。

> **⚠️ 警告**
>
> 您無法將某顆 prim 單位的「直系先祖 (ancestor)」或是「子代 (descendant)」作為它的「特化來源 (source)」。能夠作為被特化來源 (bases) 指標的基準物件，僅能是旁系的階層物件 (siblings)，或者是存在於本目標原生階層定義之外的其他獨立 prim 體系。



## 實戰範例 → 產生腐蝕痕跡的金屬特化材質

此範例中包含兩張圖層：`robot.usd` 還有 `world.usd`。 

### Robot.usd
`robot.usd` 圖層中定義了一顆 `Robot` prim，並包含著三個做為材質的 prims：`Metal`、`CorrodedMetal` 以及 `InheritedMetal`。其中 `Metal` 材質身上被賦予了兩種基礎的屬性：分別是 `inputs:diffuseGain` 與 `inputs:specularRoughness`。

> **🖼️ robot.usd**
>
> ![](../images/terminology/robot_usd.png)


其中，`CorrodedMetal` 即為 `Metal` 因應特化 (specialization) 而產生的變體。為達成這項目標，我們對 `inputs:specularRoughness` 屬性進行特化，明確宣告並鎖定其數值為 `0.2`。

> **🖼️ 遭到特化宣示的 metal**
>
> ![](../images/terminology/specializes_1.png)


```usd
def Material "CorrodedMetal" (
    specializes = </Robot/Materials/Metal>
)
{
    # 取出粗糙度來進行特化專精...
    float inputs:specularRoughness = 0.2
}
```

相反地，`InheritedMetal` 是單純透過 inherits arc 對 `Metal` 進行標準繼承的物件。值得留意的是，不論是採用 `inherits` 繼承法還是透過 `specializes` 特化法，最終呈現出的文字結果是一致的！`CorrodedMetal` 與 `InheritedMetal` 同樣完美獲取與繼承了來自 `Metal` 攜帶的資產參數，但對於 `inputs:specularRoughness` 卻也同時有著強勢覆寫的主張意見 (opinion)。

> **🖼️ Inherited metal**
> 
> ![](../images/terminology/specializes_2.png)


### world.usd

而在 `world.usda` 中，此圖層透過 reference 參照整併了 `robot.usda` 檔案，並且對已經存在著的源頭 `Metal` 提出了 Opinion 意圖覆寫它的基礎。其內部宣示了 `inputs:diffuseGain` 和 `inputs:specularRoughness` 皆須被變更為 `0.3` 與 `0.1`。
 
> **🔰 \*\*world.usd\*\***
>
> ```usd
> #usda 1.0
>  
> def Xform "World"
> {
>     def "RosieTheRobot" (
>         references = @./robot.usda@</Robot>
>     )
>     {
>         over "Materials"
>         {
>             over "Metal"
>             {
>                     float inputs:diffuseGain = 0.3
>                     float inputs:specularRoughness = 0.1
>             }
>         }
>     }
> }
> ```

### 所以 `Inherits` (繼承) 和 `Specializes` (特化) 兩者的差異？
當我們仔細檢視 `world.usd` 歷經合成後的 opinions 結果，您將會發現：那些原先意圖覆寫在 `Metal` 身上舊有數值（`inputs:diffuseGain` 與 `inputs:specularRoughness`）的意圖以及力量，確實被延展發散並反應到了普通的 `InheritedMaterial` 身上，但對於那顆受到「特化位階」保護傘防衛之下的 `CorrodedMaterial` 則並未受到任何的影響與改變。

| 源自 Base Metal 的外部強制覆寫         | 作用在 `InheritedMaterial` 的檢視結果     | 作用在 `CorrodedMaterial` 上的檢視結果 |
|--------------|-----------|------------|
| <pre>over "Metal"</br>{</br>&nbsp;&nbsp;&nbsp;&nbsp;float inputs:diffuseGain = 0.3</br>&nbsp;&nbsp;&nbsp;&nbsp;float inputs:specularRoughness = 0.1</br>}</pre> | ![../images/terminology/specializes_3.png](../images/terminology/specializes_3.png)       | ![](../images/terminology/specializes_4.png)         |

如同在上方過程所見，即便我們透過了最極端與強大的優先權去嘗試將源頭 `Metal` 及其旗下的任何直系關聯進行覆寫，系統仍會遵守該條鐵則： _一旦掛上了特化 (specializations) 標籤，該意見將會恆定成為最高優先順位的贏家_。

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Specializes](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-specializes)
