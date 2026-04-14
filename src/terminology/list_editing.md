# List-Editing (清單編譯作業)

List editing (清單編譯作業) 是 USD 內部的一項功能機制，允許創作者以非破壞性 (non-destructively) 的方式，對場景圖 (scenegraph) 裡屬於「清單類型」的元素進行編輯。您可以在 composition (合成) 的運算過程中，無縫地在清單中安插 (append、prepend) 或移除 (delete) 項目；甚至能夠以顯式的語法，強制覆寫 (explicitly override) 整個清單內容。這類操作通常適用於以下元素：references、relationships、custom metadata、inherits、specializations 以及 variantsets。需要特別注意的是，被標記為清單型別 (list-type) 的屬性 (Attributes) 無法使用 list-edited。

在下方的範例中，我們覆寫 (override) 了一顆 prim 身上的 references 清單，在其清單最前方 (prepend) 加入了一個指向另一個圖層的全新 reference 參照連結。這種操作會使該 prim 同時參照兩個不同的圖層（在假設套用覆寫前原始的定義僅指向單一圖層的情況下）。

> **🔰 \*\*操作 references 參考的清單編輯範例\*\***
> 
> ```usd
> #usda 1.0
>  
> over "World"
> {
>     over "Foo"
>     {
>         # 覆寫 "Bar"，使其除了原本的 references 之外，額外增加參照 baz.usd
>         over "Bar" (
>             prepend references = @./baz.usd@
>         )
>         {
>         }
>     }
> }
> ```

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - List-Editing](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-list-editing)
