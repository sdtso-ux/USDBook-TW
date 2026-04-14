# Default Prim (預設 Prim 設定)

撰寫新層級圖層 (layer) 時，可以順帶賦予並綁定一顆名為「default prim (預設主物件)」的指標。這項設定可視作是被寫入該層 layer 裡的預設中繼資料 (metadatum)。內部記錄了該圖層當中最能作為主體代表的那顆 prim 名稱資訊；此舉使得這張 layer 在日後被其他的 reference 或是 payload 掛載時，若呼叫方沒有明確指定想參照哪一個特定的 prim path 節點路徑，系統就能「自動地」去調出這位被註冊為 default prim 稱號的物件代表出席。  

這項作為圖層代表呼叫的目標，所指向的目標必須是位於層級樹最頂級 (root level) 路徑下的 prim 節點。也就是能夠直屬於最高 `PseudoRoot` 層級的直系子物件。受限於這條硬性定義的規則，嘗試賦予一個深層且迂迴的「路徑 (path)」成為預設標的是絕對不允許的行為。

> **🔰 \*\*撰寫在 Layer Metadata 中的 `defaultPrim` 合法範例\*\***
> 
> ```usd
> #usda 1.0
> (
>     defaultPrim = "PrimName"  
> )
> 
> def "PrimName" {}
> ```

> **🛑 \*\*這是不合法的 `defaultPrim` 寫法\*\***
> 
> ```usd
> #usda 1.0
> (
>     defaultPrim = "PrimName/NestedPrim"  
> )
> 
> def "PrimName" {
>     def "NestedPrim" {}
> }
> ```

如果 `defaultPrim` 的目標沒有具體撰寫，或指向了未能符合規則的深層物件，USD 編譯器將會拋出錯誤訊息，並亮出 "unresolved reference prim path (無法解析的參照 prim 路徑)" 的警告。這也將導致以其作爲目標對象的合成作業在途中斷線崩潰。

```
Warning: ... In </reference>: Unresolved reference prim path @.../defaultPrim.usda@<defaultPrim> ...
```

> **💡 提示**
>
> **重要規則：若您預設這層 layer 在日後將被作為其他人的 reference 或是 payload 的目標素材來源，那該名稱的屬性對象 `defaultPrim`，務必將其完整設置與指定。**


## 實戰範例
在這次的示範場景中包含兩張圖層：第一張在最高根目錄 (root) 路徑下定義了多個物件 prims (名為 `defaultPrim.usda`)，第二張圖層則透過參照引入了第一張圖層 (名為 `reference.usda`)。

> **🖼️ defaultPrim.usda**
>
> ```usd
> #usda 1.0
> (
>     defaultPrim = "CubePrim"  
> )
> 
> def Cube "CubePrim" {}
> def Sphere "SpherePrim" {}
> def Cone "ConePrim" {}
> ```


請注意，圖層 `reference.usda` 的內容單純僅參照了圖層檔案此一「整體概念」，並未明確點名欲匯入 `defaultPrim.usda` 內部這堆 prims 名冊裡的哪位特定對象：
> **🖼️ reference.usda**
>
> ```usd
> #usda 1.0
> 
> def "reference"(
>     prepend references= @defaultPrim.usda@
> ) {
> }
> ```


一旦我們開了個 `usdview` 舞台，把這張作威作福的 `reference.usda` 圖層攤開來檢視時我們便會驚訝地發現：唯有那個最幸運、最關鍵的 prim 得以被拔擢進它層高高在上的 Layer Stack 當中，此人不是別人，正是那位傳說中的方塊君 `Cube`。

> **🖼️ 顯示出來是 Cube**
>
> ![](../images/terminology/defaultPrim_cube.png)


若是我們翻臉不認人，回去把出廠設定上的那個 default prim 中繼標籤給硬生生換成了例如： `defaultPrim = "SpherePrim"` 時，這回該位身形圓潤的球體 `Sphere` 就會雀屏中選，取而代之被當成被參考的對象拉過來了。

> **🖼️ 變成了 Sphere**
>
> ![](../images/terminology/defaultPrim_sphere.png)


倘若您有顆熊心豹子膽，手起刀落直接乾脆俐落地把 `defaultPrim` 身上掛的那些中繼標籤整個根除了，那它能還您的也就只有無盡的空虛了 —— 留下一條空空蕩蕩啥屁都生不出來的參照死路 (empty reference arc)。即使「這張 layer 本身」理論上依舊處於被拉近去參考掛載的進行式當中，但是那層裡頭原先安穩住著的那些 prims，就一個也不會被抓出來陪葬出現在您的舞台裡組成結構 (composed) 了。

> **🖼️ 結果啥都沒有**
>
> ![](../images/terminology/defaultPrim_empty.png)


---

> **💡 提示**
>
> ↪ 本文內容在 USD Glossary 官方字典中無編列字條！
