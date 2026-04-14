# Strength Ordering (優先權強弱排名 LIVRPS)

Composition (合成) 機制與 opinion (意見/主張) 覆寫時的權重判定有著密不可分的關係。USD 為此制定了一套嚴謹的判定規則。每一種特定的 composition arc 都被系統賦予了對應階級的「權重值 (strength)」。舉例來說，當系統中有針對同單一屬性發出多個衝突意見 (例如分別來自同一份 layer stack 中三條不同的 composition arcs) 時，系統將依據「誰的權重名次最重 (strongest)」來仲裁，並採納該對象的值為最終定案。此規則的排列字首縮寫即為技術圈常稱呼的：`LIVRPS` (讀音似 Liver Peas)。

首字母縮寫 LIVRPS 代表了以下 6 大門派位階，權重順序由上而下遞減：
- `L`ocal (本地圖層)
- `I`nherits (繼承)
- `V`ariants (變體)
- `R`eferences (參照)
- `P`ayloads (酬載延遲載入)
- `S`pecializes (特化)

這個階層式的清單，可視作一個由上而下遞減檢索的結構 (top-down stack)。當 USD 需要對指定的屬性 (property) 或 metadatum 進行 opinion 衝突排解時，系統將遵循上方羅列的順序位階，由高至低逐一掃描各層 composition arcs。掃描途中一旦發現其中包含有效定義的 opinion，該往下的探尋流程便會立刻中斷，直接採納並沿用該節點的值。如果直至底層整個流程都沒有搜尋到任何使用者編寫的 authored opinion，USD 將會退回採用該屬性或資料所指定的出廠預設值。

除了最頂階的 Local 以外，當其他的 composition arcs 被調用觸發時，皆會啟動深度遞迴式的 LIVRP(S) 權重重新尋訪與驗證流程。然而在這反覆的驗證探尋迴圈中，位處名單底端的 `S`(pecializes) 基於系統設計考量將預設被系統略過並隱藏。除非當下的檢索評估本來就是為了處理 [Specializes](../intermediate/specializes.md) 中相關的元件事件，這才會啟動涵蓋並呼叫完整包含 `S` 的 `LIVRPS` 調查名單。

下方的決策流程圖展示了在特定條件下，如何決定並取用不同的 opinion values。

![](../images/terminology/livrps.png)

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - LIVRPS Strength Ordering](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-livrps-strength-ordering)
