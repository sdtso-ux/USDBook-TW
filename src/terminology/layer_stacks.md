# Layer Stack (圖層堆疊)

每一個 [Layer (圖層)](./layer.md) 內部都會跟蹤紀錄屬於自己的那一份「local (本地)」圖層堆疊清單，這份清單上紀載了所有對該 Layer 產生貢獻的圖層們。您可以把這份 stack 視為一組「經過排序與羅列好的圖層集合體」，這些被堆疊進來的圖層將會共同合作並決定出該 Layer 的 hierarchy 結構以及 [Composition (合成)](./composition.md) 結果。

> **🖼️ furniture_workbench01.usda 的 layer stack 範例**
>
> ![](../images/terminology/layer_stack.png)
> 
> 在上圖中，`furniture_workbench01.usda` 這層 layer 實際上是由「另外三層 layer 加上它自己」共同組網而成的。在這個案例裡，它依序把 `furniture_workbench01_modelling.usda`、`furniture_workbench01_surfacing.usda` 以及 `furniture_workbench01_rigging.usda` 用這個秩序疊加在它的 Layer Stack 之中。若您從視覺上的清單來看這個順序可能是反過來的，畢竟它是個「堆滿東西的高塔 (stack)」嘛！只要記住一個鐵則：在這個堆疊裡樓層爬得越高，那一層 layer 的「權重與話語權 (important)」就越大。


> **ℹ️ 提示**
>
> 對於某個 Layer 專屬的 Layer Stack 而言，它永遠會把「自己的 data」給強壓在整座 stack 大權在握的最頂層，這也意味著它對「自己」的覆寫權限永遠是最至高無上且最重要 (most important) 的。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - LayerStack](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-layerstack)
