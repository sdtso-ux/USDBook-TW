# Specifier (識別定義子)

在定義 scene graph (場景圖層樹) 中的 prim 時，總共有三種宣告方式可供選擇。

> **ℹ️ 提示**
>
> 為了解釋方便，在下方我們展示的數個例子中都將採用純文字格式的 USD text 組成結構作為教材，因為 `usdview` 的基礎軟體介面無法直接將這種虛擬的定義概念視覺化。


> **🔰 \*\*def\*\***
> 
> 這是一種具體的實體定義宣告。這種語法格式通常在兩種情況下出現：第一，當您首次建立並定義一顆全新的 prim；第二，當某顆現存的 prim 出現變動且需要被「重新定義」時。在場景架構中，`def` _永遠_ 會對您的場景最終 composition (合成) 成果構成實際的影響與改變。
>   ```usd
>   def Xform "MyTransform"
>   {
>     # ...
>   }
>   ```
> 
>   `def` 也能夠以不帶任何 type 型別標籤的 (`type-less`) 方式宣告！通常當您遇到這類寫法時，代表這顆 prim 參與了複雜的 composition 作業。在未來的合成運算過程中，別的圖層將會為主動提供並補上它真正該有的 type 屬性。
>   ```usd
>   def "MyPrim" {
>     # ...
>   }
>   ```

> **🔰 \*\*over\*\***
> 
> 這代表向 USD 宣告該 prim 將被覆寫。只要在名稱前綴加上這個字，即表示該 prim 預期要在底層架構中被「覆寫（overridden）」。一旦掌事系統的 composition engine (合成引擎) 在沿著階層尋找時，卻在指定的區域找不到被對應覆寫的來源物件時，這個由 `over` 構成的宣告就會被系統忽略，這也代表著它不會對最終的場景合成產生任何影響。
>   ```usd
>   over "SomethingThatAlreadyExists"
>   {
>     # ...
>   }
>   ```

> **🔰 \*\*class\*\***
> 
>  這代表宣告定義了一種抽象（abstract）物件。在預設情況下，帶有此標籤的 prim 是會被 [stage traversal](./stage_traversal.md) (場景遍歷) 給忽略的。這意味著，當您展開整個 stage hierarchy 檢視時，並不會看到該物件直接顯示出來；儘管它是不可見的，但其他正常的 prim 卻能夠「擷取並繼承 (inherit)」這尊 class 所定義的任何屬性與規則（詳情將在後續的 Composition 章節中深入探討）。
>   ```usd
>   class "_MyClass"
>   {
>     # ...
>   }
>   ```

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Specifier](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-specifier)
