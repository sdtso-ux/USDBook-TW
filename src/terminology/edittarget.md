# EditTarget (編輯目標層)

當在 stage (舞台) 中開啟並檢視某個 layer 圖層，並對場景樹 (scene graph) 進行編輯修改時，這些編輯操作在預設情況下都會被寫入並記錄於「Root Layer」(即最初建立 stage 時所使用的基礎圖層)。

但在一個多重圖層與 composition arcs 交雜的複雜專案中，通常會有需要單獨針對某一層特定的 layer 進行內容編輯的情境。與其單獨將該層 layer 給單獨開啟出來編輯，USD 提供了一項名為 `EditTarget` 的功能機制。透過 `EditTarget`，使用者可以直接指定接下來所有的編輯變更 (例如：強制覆寫 overrides、修改階層架構等...) 應該被明確記錄至 _哪一層指定的 Layer_ 上。

憑藉這個機制，使用者可以在「經過完整合成運算的大型場景 (fully composed scene)」中持續檢修畫面，並同時確保這些編輯變更精準寫入構成該場景的特定原始圖層中。這種工作流大致上就像是在擁有多層圖層的 Photoshop 檔案中，切換選擇 Active Layer 以確保下筆能落在正確位置的概念一般。

> **💡 提示**
>
> 這是 USD 架構下的核心工作流 (Core workflow) 要素之一。


> **🔰 \*\*Session Layers 暫存任務快照編輯層\*\***
> 
> 當每次 USD 建立並載入 stage 的同時，其底層系統預設也會建立一個被稱為 "Session Layer" 的圖層空間。  
> 
> 這個空間可視作隨附的一塊「獨立塗鴉板區 (scratch space)」，它相當適合被指派為 `EditTarget` 來將任何草稿型的變更完整記錄下來，且確保這些實驗性修改不會污染到場景中原始被引入的圖層 (original layers)。  
> 
> Session Layer 在整個 stage 的 layer stack (圖層堆疊) 中會被永遠錨定於最高點位置 (在系統底層，每個 stage 自行保有一套獨立的 layer stacks 架構)。它就像在 layer stack 裡的其他圖層一樣履行各種圖層職責。一旦在該 session layer 中寫入了修改與宣告 (opinions)，由於其高高在上的優先級，它產生的意見將會永遠擁有最強的力量 (strongest)，能夠覆蓋下方所有其他圖層的同值屬性。

![](../images/terminology/edittarget.png)

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - EditTarget](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-edittarget)
