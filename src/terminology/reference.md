# Reference (參照/參考)

## Layer References (圖層外部參照)
除了 sublayers (子圖層疊加) 機制之外，Layer 也可以被掛載 (grafted) 於單一的 prim 之下。延續在 [Local/Sublayer (本地與子圖層)](./local_sublayer.md) 中提及的 Cube 與 Sphere 範例，我們可以建立多個新的 prim，並讓它們各自指向 (point to) 這些外部的 layer 檔案。

> **🖼️ Layer referencing 圖層外部參照**
>
> ![reference_1](../images/terminology/reference_1.png)
> ![reference_2](../images/terminology/reference_2.png)


## Local References (本地圖層內部參照)
雖然 referencing 通常適用於參照外部檔案 (file paths)，但它同樣支援內部圖層的參照。您可以將參照屬性關係指向「與當前 prim 身處於同一層 Layer」的另一個物件進行定義。這種方式被稱為 Local Reference (本地參照)。

> **🖼️ Local referencing 本地參照**
>
> ![reference_3](../images/terminology/reference_3.png)
> ![reference_4](../images/terminology/reference_4.png)


您只需透過 Reference 將目標指向特定的 prim（如 `</foo>`），接著該目標下的所有 hierarchy (階層結構) 將會被完整載入並置於當前的 prim 之下：

```usd
def "ReferenceToFoo"(
        prepend references=</foo>
) {
}
```

# Layer Prim References (圖層中指定 Prim 參照)
Composition (合成機制) 是建立在 Layer stacks 之上的。這表示您不僅可以參照整個圖層，甚至可以從其他 Layer 的 layer stack 中精準參照一顆特定的 prim！即使這些被參照的 prims 本身也是來源端 Layer stack 經過合成運算後的產物，皆能順利被參照引入。

> **🖼️ Layer Prim referencing 圖層中指定 Prim 參照實作**
>
> ![reference_5](../images/terminology/reference_5.png)
> ![reference_6](../images/terminology/reference_6.png)


```usd
def "ReferenceToPrim"(
    prepend references= @./several_prims.usd@</A_Capsule>
) {
    float3 xformOp:translate = (3, 0, 0)
    uniform token[] xformOpOrder = ["xformOp:translate"]
}
```

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Reference](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-reference)
