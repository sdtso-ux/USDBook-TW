# Payload (酬載延遲載入)

Payload 是一種支援「延遲載入 (lazily loaded)」的進階 reference (參照引用) 機制。當某顆 prim 透過 Payload 掛載圖層資源時，USD 會在預設情況下不主動載入這些圖層資料，直到使用者後續手動要求載入為止。

當被引用的外部圖層檔案包含龐大的資料量或極度複雜的 hierarchy，導致整體檔案沉重時，將其轉換為 Payload 讓使用者在 stage (舞台) 中視需求分批載入，可帶來莫大且直接的效能與流暢度收益。整體而言，被歸類為「非場景核心優先」的物件或圖層，都建議透過 Payload 的形式來進行掛載防護。未被載入的 Payload 將不會參與系統的場景遍歷 (stage traversal)，因此在決定哪些資料為必備的「核心關鍵 (important)」內容時，必須端看當下的專案需求而定，以防重要資料遭遇載入延遲。


## 實戰範例 → 透過 Payload 延遲載入高面數模型

當我們選擇預設不載入 (unloaded) Payload 的時候，hierarchy 的結構顯示看起來會如下圖這般空洞：
> **🖼️ 未載入的 Payload**
>
> ![unloaded](../images/terminology/payload_1.png)


然而這個 Payload 會保留其 prim 的節點標示，允許使用者在載入 stage 之後，隨時能像開關一樣進行載入狀態切換 (toggled on/off)。

> **🖼️ 切換 Payload 的載入/卸載狀態**
>
> ![loaded](../images/terminology/payload_example.gif)


一旦開啟載入，完整的 hierarchy 層級樹就會被全數讀取進來：

> **🖼️ 成功載入 Payload 後的結果**
>
> ![unloaded](../images/terminology/payload_2.png)


> **🔰 \*\*simple_payload_example.usd\*\***
> 
> ```usd
> #usda 1.0
> (
>     defaultPrim = "Asset"
> )
>  
> def Scope "Asset"
> {
>     def Xform "Geometry"
>     (
>         prepend payload=@./highres_model.usd@
>     )
>     {
>     }
> }
> ```

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Payload](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-payload)
