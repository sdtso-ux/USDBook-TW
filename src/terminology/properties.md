# Properties

[Prims](./prims.md) 可以擁有 Properties (屬性)，本質上它們就是具名且帶有 type 的 data。

USD 裡的 `Property` 實際上是兩種截然不同型態 Property 的統稱：

> **🔰 Attributes**
> 
> Attributes (數值屬性) 是帶有直接 value (數值) 的 Property，且這些數值可能會隨時間產生變化。  
> ![](../images/terminology/attributes.png)

> **🔰 Relationships**
> 
> Relationships (關聯) 則是負責指向其他 Property 或 [Prim](./prims.md) 的 Property。  
> ![](../images/terminology/relationships.png)

從上述例子中，您可以看到 Property 是由 `name` (名稱) 以及帶有 type 的 `value` 所組成的。

這些 Property name 也能夠加上 namespace (命名空間)。一個 Property name 可以擁有一或多個以 `:` 隔開的 namespace 標識符。  
再仔細端倪 Relationship 的範例，`material:binding` 這個 Property name 實際上就是使用了 namespace。這個 Property 的名稱本身是 `binding`，而它是從屬於 `material` 這個 namespace 裡。

Namespace 可以用來將多個 Property 進行歸類或群組化。

---

> **📝 延伸閱讀**
> 
> ↪ [USD Glossary - Property](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-property)