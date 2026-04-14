# Instancing (實例化技術)

Instancing (實例化技術) 是 USD 中的一項機制，允許特定結構在讀取與操作時降低記憶體用量與合成 (composition) 複雜度。
舉例來說，當某層 layer 被參照 (reference) 指定到某顆 prim 時，USD 預設會為該 layer 所涉及到的 _每一條_ reference，重新去進行一次完整的結構合成編譯 (re-compose)；即使所有引用的參考皆是指向同一層 layer。

然而，當使用 Instancing 機制時，USD 會在背景建立一個以參照結果所構成的『原型 (Prototype)』。接下來凡是指向該來源 layer 的參照連結，都會被置換成一種專門對應到該 Prototype prim 的小型連線模式 (local-reference)。此舉優化了 USD，使系統只需對被當作參照物的 layer 其背後的 layer stack 合成運算『一次 (only once)』即可。

> **⚠️ 警告**
>
> 這種架構伴隨著一個運作限制：_若在身上掛有參照層的那個實例化 prim (instance prim) 之下，你對其更底層的子物件所進行的任何屬性覆寫變更 (overrides) 皆會被 USD 無視並忽略 (ignored)_。


> **🖼️ 大量實驗瓶參照著相同的原始層 layer**
>
> ![](../images/terminology/instancing_1.png)


在上圖範例之中，所有被選取的實驗瓶 prims 皆是參照自 `chemistry_bottle01.usda` 檔案為原始樣板，且這幾筆參照同時都被加入了 `instanceable = true` 的中繼資料 (metadatum)。這筆標記資料告訴了 USD，它只需要針對 `chemistry_bottle01.usda` 合成一次對應至 `__Prototype` 的 prim 中即可。而在完成之後，所有指向 `chemistry_bottle01.usda` 的參考連線，在內部機制上實際上皆轉換成了指向 Prototype prim (在本範例中被命名為 `__Prototype_37`) 的本機內部參照連線 (local prim reference)。

> **🖼️ 對應 Bottle prototype 的主 prim**
>
> ![](../images/terminology/instancing_2.png)


> **⚠️ 警告**
>
> 當一顆 prim 被標記成 instance 時，[Stage Traversal 機制](../intermediate/stage_traversal.md) (場景遍歷) 會在此 prim 節點前止步，並不會往下遍歷其子層架構。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Instancing](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-instancing)
