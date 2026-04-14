# Layer (圖層)

Layer 是一個用來網羅 Prim 及其 Property 的集合體，它可以被儲存進硬碟中，或是被載入到記憶體裡供人讀取。正因如此，它其實可以被視作是一個「具備存檔能力的 hierarchy」。

業界標準的 USD Layer 可以透過以下這幾種實體檔案存在於硬碟中：

| 副檔名 (Extension)    | 描述 (Description) |
|--------------|-----------|
| `.usda` | ASCII 純文字，人類可以直接閱讀的結構    |
| `.usdc`      | USD Crate 檔案格式。這是一種為了追求極致效能而生的高效能二進位檔 (binary file)，人類無法閱讀  |
| `.usd`      | 可能是 Crate 也可能是純文字格式  |
| `.usdz`      | 無壓縮的打包封裝格式 (.zip)  |

> **ℹ️ 提示**
>
> USD 允許您透過一種極度特殊的 plugin 形式（即 `SdfFileFormat`）來無上限擴展那些能被作為「Layer」載入的檔案。說穿了，上面羅列的那些預設檔案類型，本質上也都是實作了這類型 plugin 的產物。  
> 若您掌握了這種 `SdfFileFormat` plugin 的開發邏輯，您甚至可以實做出讓 USD 原生支援並載入諸如 `.fbx`、`.abc`、`.obj` (甚至是任何東西) 的強大整合能力。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Layer](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-layer)
