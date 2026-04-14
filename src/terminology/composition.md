# Composition (合成)

說白了，這就是一種將各式各種的 Layer 與散落其上的 Prim、Property 以及 Metadata，透過被稱為 [Composition Arcs (合成弧)](./composition_arcs.md) 的機制媒介，強行組合與揉捏在一起的偉大行為。

雖然說把各圖層集結在一起這個動詞可以被稱作是在「合成 (composing)」它們；但在底層架構上，USD 的合成引擎真正在調用的東西，其實是各個 layer 背後深藏不露的 [Layer Stack (圖層堆疊)](./layer_stacks.md) 們。

> **⚠️ 警告**
>
> 清楚釐清這件事的定義是非常、非常重要的！因為這意味著：當我們嘗試去 target (指定目標) 到某一個 Layer Stack 時，這也代表著「在那個目標 Layer Stack 內部所孕育出的所有 Composition 合成結果」，全都會一併被牽連並算進最後的貢獻 (contribution) 當中。


> **🖼️ `furniture_workbench01.usda` 裡 `/root` prim 的合成範例**
>
> ![](../images/terminology/composition.png)
>
> 這個範例結構第一眼看起來可能會讓您覺得龐雜且無比困惑，但它其實想表達的事情只有一件：「位於 `/root` path 下的這顆 prim，是受惠於清單表上所有羅列的 Layer (更準確地說，是靠呼叫它們背後的 Layer Stacks) 共同貢獻 (contributions) 結合成的產物」。  
> 表格最前面的 `Arc Type` 這一欄，則標示了這些 Layer 到底是 _如何 (how)_ 將這份貢獻推進給 `/root` 並長成您現在看到的最終「規格 (specification)」的（更多細節稍後再談）。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Composition](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-composition)
