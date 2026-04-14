# Metadata (中繼資料)

Prim、Property，甚至是它們所從屬的 Layer 本身，全都可以加上 Metadata (中繼資料)。這是一種額外的_靜態_資料（static data，意味著它不能隨著時間而產生數值上的動態變化），不僅可以提供給 USD 系統看，也能讓使用者自由讀取、利用或宣告定義。

Metadata 可以用來描述各種系統行為、賦予特定意義、或者是呈現成文件。USD 出廠時就已經內建了一套極度強大且全面的 Metadata 架構供大家使用。

> **💡 提示**
>
> 開發人員也可以透過撰寫 USD Plugin 的方式來自定義全新的 Metadata！


## 簡單的 Metadata 範例

### Layer Metadata

> **🖼️**
>
> ![StageMetadata](../images/terminology/metadata_stage.png)


在上方的截圖中，我們選取了位於 path `/` 的 [PseudoRoot](./path.md)，此時 `usdview` 中關於 Metadata 的介面面板會亮起高光。這個 Root 代表了來自 [Animal Logic ALab](https://animallogic.com/alab/) 場景的 `entry.usda` 這層 Layer。`entry.usda` 定義了諸多 Metadata 供人檢驗，向使用者呈現了有關於它自己的以下情報：
- 這層 Layer 所採用的線性長度單位是 `0.01` 公尺（即為公分） → `metersPerUnit = 0.01`
- 這個場景的朝上軸向為 `Y` 軸 → `upAxis = Y`
- 還有另外兩層 Layer 參與貢獻了這個場景（這部分我們晚點會在 [Local/Sublayer (本地子圖層)](./local_sublayer.md) 中進一步探討） → `subLayers = [...]`
- 該檔案在 time code `1004.0` 到 `1057.0` 之間擁有 Animation (動畫) 資料，且每一秒配備有 `24.0` 幀的速度 (framesPerSecond) 以及等同的 timeCodesPerSecond 配置。
  - `startTimeCode = 1004.0`
  - `endTimeCode = 1057.0`
  - `framesPerSecond = 24.0`
  - `timeCodesPerSecond = 24.0`

> **⚠️ 警告**
>
> 請務必注意，雖然這當中有很多的 Metadata 單純只是用來「告知資訊」，但在核心的 Metadata 架構裡仍然有非常大一部分的資料，可是會對內部運作產生極為嚴重的「副作用 (side effects)」，它們甚至左右了 USD 在底層究竟該如何建構世界。
> 
> 舉例來說，`metersPerUnit` 是單純作為情報的存在；但是反觀 `subLayers`，一旦您編輯修改了它的數值，整個天下可是會為之震動的！



> **📝 備註**
>
> 其他像是 Autodesk Maya 或是 Sidefx Houdini 這類型的 USD 宿主軟體，也可以自己選擇要去抓出並解讀某個 Metadata 裡的關鍵屬性來產生動作，即便 USD 本地環境可能不會對此做出任何反應。


### Prim Metadata

> **🖼️**
>
> ![StageMetadata](../images/terminology/metadata.png)


Prim 身上的 Metadata 可以推論出大量跟這顆 Prim 本身有關的情報身世，包含它在這個場景裡具體是怎麼被使用的（請參見 [Composition (合成)](./composition.md)）、它擁有哪種 Property 等等。

從上圖中我們可以得知位在 `/root/alab_set01/lab_electronics01_0001/bench01/decor_paper_notej01_0001` 的這顆 Prim：

- 是一個 `Xform` 類型 → `typeName = Xform`
- 此物件被轉換為實例 (instanced) 如分身般存在著（關於這點，稍後會在 [Instancing (實例化)](./instancing.md) 章節詳解） → `instanceable = true`
- 擁有兩個 VariantSet (變體集)（這也會在稍後 [VariantSets](./variantset.md) 詳解）→ `geo` 跟 `geo_vis`
- 被歸類標記為 `component` 這個階級（我們會在詳談 [Kind (分類層級)](./kind.md) 這個 metadatum 時一併討論） → `kind = component`
- 諸如此類不勝枚舉。

### Property Metadata

> **🖼️**
>
> ![StageMetadata](../images/terminology/metadata_prop.png)


最後我們來看 Property 的 Metadata。這類資料的作用是用來揭露跟這個 Property 數值自身相關的最細緻情報，例如：

- 它是什麼 type 型別 → `typename = double3`
- 它的數值是否會隨著時間變化（動畫） → `variability = Sdf.VariabilityVarying`
- 它是某個客製化的 "out-of-schema" 屬性嗎（請見稍後的 [Schemas](./schemas.md) 篇章）→ `custom = false`

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Metadata](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-metadata)
