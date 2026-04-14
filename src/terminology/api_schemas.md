# API Schemas (應用介面綱要)

API Schemas 提供了一種能夠為 prim 「宣告定義 (definition)」進行擴充的機制。它可以打包一組預設屬性 (properties) 與中繼資料 (metadata) 供物件掛載套用，或者提供專屬的程式介面管道用以提取這些資訊。

一般來說，API Schemas 的運作可劃分為兩種主要類型：`Non-applied API Schemas` (非掛載式) 以及 `Single or Multiple-applied API Schemas` (單一或多重複數掛載式)。

## Non-Applied Schemas (非掛載式綱要)
這類綱要主要用於協助開發人員，提供從較高階的抽象層次來讀取、操縱屬性與中繼資料 (metadata) 的手段。

這類型別的綱要通常不會自行定義出任何屬性，它們的作用純粹是提供讀取與操作的介面通道。

```python
# 以下的 Python 範例展示了如何透過 UsdModelAPI (一種非掛載式的 API schema)，簡潔地將 prim 的 Kind 型別設定完成。
Usd.ModelAPI(prim).SetKind(Kind.Tokens.subcomponent)
```

> **ℹ️ 資訊**
>
> 一般使用者通常不需要直接與這類 schemas 打交道，因為這些往往僅在程式開發操作 (programmatically) 的設計情境中才會被廣泛呼叫使用。


## Single or Multiple-applied API Schemas (單一或複數掛載式綱要)

這種類型的 schemas 是使用者在建立結構時最常遇到的。  
如同其名 (Applied)，當系統將這類 API Schemas「掛載套用」到某顆 prim 時，該 prim 的原始定義清單內就會自動加入由這組 Schema 所預先宣告搭載的屬性參數群。

舉例來說，若某個掛載式的 schema (我們稱之為 `FooAPI`) 內部定義了一個名為 `foo` 的浮點數 (`float`) 屬性，一旦我們將該 schema 掛載至指定 prim，這該 prim 上便會立即新增出 `foo` 這個屬性，並允許使用者直接針對其寫入設定與覆寫宣告 (express opinions)。如果使用者沒有對其寫入任何參數，`foo` 則會退回並保持其 schema 原預設的系統底線值 (fall back to its default value)。  

我們再來看一個更具體的實例：能夠負責定義出材質連接屬性的 `MaterialBindingAPI`。  
位於路徑 `/Sphere/Mesh` 的 prim 之所以能夠連接材質，正是因為其本身的 `apiSchemas` 中繼資料欄位中已被掛載套用了 `MaterialBindingAPI`。 (順帶一提，`apiSchemas` 這筆資料屬性也支援 [清單編輯 List-Editable 機制](./list_editing.md)，這意味著使用者有權限能夠自行編輯或覆寫指定 prim 所掛載的 API Schemas)。

> **🖼️ Applied Schemas 已掛載生效**
>
> ![](../images/terminology/schemas_1.png)


搞明白上述機制後，我們就可以順利地針對這個 prim 所擴充附帶名為 `material:binding` 的屬性進行了編輯修改。在這裡有一個需要特別注意的特點：您會發現這筆屬性身上註記了一個名為 `custom` (自訂) 的中繼資料標籤（metadatum）。這個標籤是用來明確宣告該屬性存在且合法歸屬於某個 schema 綱要的管轄之內。整體來說，如果系統發現某個屬性上的 `custom` 遭人為手動寫死為 `True`，那麼該屬性在系統中通常只會被判定為是不具合法綱要效力的外部孤立擴充屬性（out-of-schema）。

> **🖼️ 透過 Schema 預定義而擴充出的新屬性**
>
> ![](../images/terminology/schemas_2.png)


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - API Schema](https://graphics.pixar.com/usd/release/glossary.html#api-schema)
