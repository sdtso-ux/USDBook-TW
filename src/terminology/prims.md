# Prims

它是 _Primitive_ 的縮寫，同時也是 USD 當中最不可或缺的核心組件。  
Prim (基礎物件) 也就是 hierarchy 中的 node，因此能與其他 Prim 之間建立 parent/child 關係；這意味著一個 Prim 可以擁有多個子 Prim 或同層級的 Prim (siblings)，本身也能夠從屬於另一個父 Prim。

在下圖中，hierarchy 裡的每一個 node 都是一個 Prim。  

> **💡 Prim 範例**
> 
> ![Prims in USD View](../images/terminology/prim.png)

眼尖的讀者可能會注意到，Prim 可以擁有特定的 _type_。例如 `Xform`、`Mesh`、`Scope` 以及 `Material` 都是特定的 Prim type。
這些 type 自帶有預設行為與相關的 data，其運作體系我們會在後續章節中詳述。

> **ℹ️ 提示**
> 使用者也能夠定義專屬於自己的 Prim type。

儘管 Prim 本身標示了它們是什麼 type 的場景元素，但它們並不一定確實握有 data。然而，它們可以被視為具名 data 的「載體 (containers)」，而這些 data 通常是以 [Properties (屬性)](./properties.md) 的形式來呈現。

---

> **🔗 延伸閱讀**
> ↪ [USD Glossary - Prim](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-prim)
