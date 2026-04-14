# VariantSet (變體集)

VariantSets (變體集) 與其包含的 variant (變體分支)，賦予了圖層中的 prim 提供多層「可切換 (switchable)」狀態與組態的能力。在下方的範例中，一顆位於最頂層 (top-level) 名為 `Implicits` 的 prim 掛載了一組名為 `Shape` 的 VariantSet。此組 VariantSet 內部結合了多個不同獨立設定的 variant 選項，它們確保使用者在切換不同的支線選項時，能載入截然不同的型態設定與層級樹變更。

當使用者切換至不同的 active variant 取代當下預設值時，USD 會將該變體內所記錄的所有屬性與設定，直接匯入注射 (inject) 至系統主流的 composition (合成) 流程之中。在此具體範例中，各個 variant 分別為 `Implicits` 提供了不同 type 設定的子物件參與構成。選擇不同的 variant 便能手動切換生成為 Capsule (膠囊體)、Cube (方塊) 或是 Sphere (球體)。

> **🖼️ Variant/VariantSet 切換範例**
>
> ![Variant Sets](../images/terminology/variant_switching.gif)


在撰寫與定義 variant 時，您在架構上享有極大的開發彈性。您可以在單個 variant 模塊中建構全新的層級樹 hierarchy、利用 reference 參照外部的圖層檔案、追加屬性覆寫 (opinion) 或是設定 metadata。但在使用這項機制時遇到多個可選變數環境，有一個要點務必銘記在心。

> **⚠️ 警告**
>
> 對於任何單獨的 VariantSet 而言，無論內部定義了多少可選的 variant (變體分支)，它的規矩是：『**同一個時間內絕對僅允許有一個 Variant 是處於啟動 (active) 狀態的！**』。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - VariantSet](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-VariantSet)  
> ↪ [USD Glossary - Variant](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-Variant)
