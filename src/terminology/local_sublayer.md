# Local/Sublayer (本地與子圖層)

每一層 Layer 皆能夠透過 sublayer (載入子圖層) 的方式納入其他 Layers。這種機制 (grafting) 可將來自多個來源的獨立 layer stacks 無縫串接為單一體系。實際上，USD 中的 Layer Stacks 便是透過 sublayering (疊加子圖層) 逐步堆疊而成的。

> **🛑 警告**
>
> 在進行 sublayering 操作時，_檔案載入的先後順序非常重要 (Order matters)_！


例如：假設我們在 `layer_a.usd` 中的 `/Foo` 路徑下定義了一顆 `Cube` prim；而在 `layer_b.usd` 中，我們在相同的 `/Foo` 路徑下定義了一顆 `Sphere` prim。當我們在 `layer_c.usd` 中同時將這兩者以 sublayer 方式引入時，`/Foo` 最終會是方塊還是球體？這會取決於匯入 `layer_a.usd` 與 `layer_b.usd` 時的 _載入順序 (order)_。

> **🖼️ Sublayering 實機範例**
>
> 在此範例中，包含 `a_cube.usd`、`a_sphere.usd` 以及用於整合收尾的 `cube_and_sphere.usd`。
> 
> `a_cube` 與 `a_sphere` 各自分別定義了一顆獨立的 Cube (方塊) 與 Sphere (球體) prim。在 `cube_and_sphere` 圖層中，雖然自身未定義任何實體，但藉由 sublayer 將前述兩個圖層疊加，本質上即是將兩個 hierarchy 體系融合，最終匯集成為專屬於 `cube_and_sphere` 自身 Layer Stack 裡的一部分。
> 
> ![](../images/terminology/sublayer.png)


> **⚠️ 注意**
>
> 請注意，Sublayering 這種行為是在「圖層的根節點 (roots)」進行疊加貼合。如果您的目的是在 hierarchy (階層樹) 的「特定位階或子節點上」插入並組合不同的圖層，則應該使用的是名為 [reference (參照引用)](./reference.md) 這種 composition arc。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - SubLayers](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-sublayers)

