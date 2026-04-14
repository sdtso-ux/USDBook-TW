# Schemas (圖解架構綱要)

Schemas (模組綱要) 用於「描述與定義」 Prims、properties (屬性)、metadata (中繼資料) 等元素。Schemas 賦予了 USD 理解 Prim 或是特定屬性背後涵義與行為模式的能力。 
透過掛載 Plugins 套件，USD 允許擴展並套用全新的 schemas 以延伸其核心功能，進而自訂全新的屬性組合、建立全新的 prim 型別、以及定義自訂的 metadata 等。 

若要建立新的 Schemas，通常需要使用 `.usda` 檔案格式來撰寫 schema definition (綱要定義檔)，這些定義隨後可用來自動生成對應的原始碼 (source code) 與 plugin 執行檔。  
簡而言之，USD 預設提供的 default prims 與 default properties，在本質上也是由 Pixar 開發團隊在系統底層所建立的標準 Schemas！

> **💡 提示**
>
> 自 USD 21.08 版本起，Schemas 不再強制依賴預編譯的機器代碼 (code) 才能運作。這意味著現在僅需 plugin 本身的存在即可發揮效用，這種機制被稱為：`codeless schemas`。


一般來說，使用者在撰寫 (author) schemas 時所建立的類別，大致上分為以下兩種：

> **🔰 \*\*IsA Schemas\*\***
>
> [IsA Schemas 解析](./isa_schemas.md)


> **🔰 \*\*API Schemas\*\***
>
> [API Schemas 解析](./api_schemas.md)


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Schema](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-schema)
