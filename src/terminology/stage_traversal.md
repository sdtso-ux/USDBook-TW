# Stage Traversal (場景遍歷)

通常這是一個在使用 USD 進行程式開發寫扣時才會遇上的概念，但對於一般用戶而言，理解它也是百利而無一害的。Stage Traversal (場景遍歷) 指的是在 Stage 中開啟並讀取了 Layer 之後，USD 系統需要「一路爬梳過」這個層層疊疊的場景樹 (scene graph) 的過程。這個遍歷的過程是可以靠著下達特定的「規則（或稱述語 predicates）」來進行篩選與過濾的，例如限制它只能爬梳某幾支從屬的子樹幹線 (sub-trees)，或者乾脆在遍歷期間豪邁地直接斬草除根、抹掉某部分的 hierarchy 不讓它顯示出來等等。

在預設狀態中，USD Stage Traversal 是只會考慮讀取並爬梳那些顯示狀態為活躍 (active)、具備實體定義 (defined)、已經被裝載進來 (loaded)，且並非抽象類型 (not abstract) 的 prims 而已。取決於您使用的是市面上哪一款軟體或工具，使用者通常可以透過介面來手動改變這種運算條件。但若您是一個開發者，您當然能夠透過呼叫相關程式介面來對這種機制進行完全的掌控。

> **🖼️ 在 USDView 中切換顯示 Abstract prims (抽象物件)**
>
> ![](../images/terminology/stage_traversal.gif)
> 
> 這裡有一顆 `_root_type` 的 prim 被宣告並定義成為 `class` 等級，這在 USD 的體系中是會被視為是一種 _abstract (抽象)_ 狀態的特洛伊節點。在通常狀況下，若您使用 USDView 讀入這層 Layer，它會神隱且絕對不會顯示在 hierarchy 列表上。  
> 然而，一旦您至 hierarchy 視窗選單中的 `Show` 分頁去開啟 `Abstract Prims (Classes)` 顯示條件時，那些所有被歸屬為像是 `_root_type` 這種抽象狀態的 prims 就會無所遁形地全部被攤在陽光下。在系統底層，這一切的操作就是靠著去竄改 Stage Traversal（場景遍歷）中的 predicate (述語條件) 來達成的。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Stage Traversal](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-stage-traversal)
