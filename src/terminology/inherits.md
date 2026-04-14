# Inherits (繼承)

這與軟體開發領域中的「繼承 (inheritance)」概念雷同。Prims 可以「繼承」自其他的 prims (無論被繼承方是實體 prim 或是 abstract 抽象類別)，並忠實反映出該被繼承目標的所有 hierarchy 與屬性特徵。這表示，只要作為繼承源頭的物件 (base prim) 被修改了，所有繼承自該源頭的子代 prims，皆會在第一時間自動套用並繼承這些聯動的變更。

若在單一圖層 (Layer) 的環境下，Inherits 與 Local Reference 的作用十分相近。然而，在多圖層的 Composition (合成) 結構中，Inherits 展現出了獨特的優勢。普通的 References 在引入 Layer stack 之後通常會直接定型成為封裝體。這表示若 references 被遷移至其他的 Layer stack 時，便會喪失對源生圖層的繼承連帶羈絆關係。而 Inherits 則是維持「即時連線 (live)」狀態，無論在 composition 的過程中歷經多少次巢狀結構，或是目標 prim 被後續的圖層所覆寫，帶有 Inherit 的 prim 都能夠確保回溯 (backtrack) 至最初的源頭本尊 (base) 位置，無視合成層級的隔閡。

> **⚠️ 警告**
>
> 注意：Prims 無法繼承自身的「直系先祖 (ancestor)」或「子代 (descendant)」。用作被繼承來源的物件 (bases)，必須定義在同一階層的旁系 (siblings) 位置上，或是完全獨立於目標 prim 原生的樹狀階層與架構之外 (例如定義於最頂層 root 位階)。


## 實戰範例

在此案例中，`SomeScope`、`SomeMesh` 以及 `SomeTransform` 各自被實體定義且帶有專屬的型別。同時，它們也共同繼承了一顆名為 `_Base` 且狀態為 abstract (抽象類別) 的 class prim。而 `_Base` 本身底端定義了兩個獨立名為 `Foo` 及 `Bar` 的 Xform 子節點。  
因 `_Base` 屬於 `class` 類型，並不會主動參與於常規的 [Stage Traversal (場景遍歷)](./stage_traversal.md) 中，自然也不會顯示於常規的層級樹內。要檢視其結構，必須在 `USDView` 中開啟顯示 `Abstract Prims` 功能。

> **🔰 \*\*`_Base` 是如何被定義的？\*\***
>
> ![](../images/terminology/inherits_base.png)

繼承 `_Base` 的結果，會使 `_Base` 旗下的所有子節點 hierarchy，完美轉移並複製至所有繼承它的目標 prim 體系之內。

> **🖼️ Simple inherits (單純繼承範例)**
>
> ![](../images/terminology/inherits_1.png)


若日後我們修改了 `_Base` 源頭，這些變更將立即反應在所有繼承它的所有 prim 系列上，無需對個別的繼承實體進行額外的介入。以下方範例做展示，我們在源頭 `/_Base/Bar` 路徑之下新增了一個名為 `Baz` 的 prim 參數節點：

> **🔰 \*\*歷經更動後的 `_base`\*\***
>
> ![](../images/terminology/inherits_2.png)


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Inherits](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-inherits)
