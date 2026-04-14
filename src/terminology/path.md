# Path (路徑)

[Prim](./prims.md) 與 [Property](./properties.md) 都是藉由在 scene hierarchy（場景階層）中的唯一 `path` (路徑) 來進行識別的。它們是 hierarchy 的純文字表達形式——這就好比我們在絕大多數作業系統中習慣使用的資料夾路徑一樣——只不過在這裡，每一個 Prim 與它的 parent 或是 child 之間，是透過 `/` 作為分隔符號 (delimiter) 來標示的。

就如同資料夾一樣，path 可以是相對 (relative) 的也可以是絕對 (absolute) 的。絕對的 path 永遠會以 `/` 作為開頭。

> **ℹ️ 提示**
>
> `/` 在 USD 中是一個極度特殊的 path。它被稱作為 [PseudoRoot (偽根節點)](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-pseudoroot)。


在下方的範例中，被強光標記出來的 path `/root/remi/head_M_hrc/GEO/head_M_hrc/eyeScrew_L_geo`，就是一條指向名為 `eyeScrew_L_geo` 的 Prim 之路徑。這條路徑是由以下 hierarchy 逐層建構出來的： `/` → `root` → `remi` → `head_M_hrc` → `GEO` → `head_M_hrc` → `eyeScrew_L_geo`。

> **🖼️ Prim Path 範例**
>
> ![](../images/terminology/prim_path.png)


若是換成 Property 的狀況，我們沿用剛才的例子，點進去檢查名叫 `points` 的 attribute (數值屬性)，它就會回傳 `/root/remi/head_M_hrc/GEO/head_M_hrc/eyeScrew_L_geo.points` 這樣一段 path。Property 的 path 是透過將 Property 的名稱用 `.` 符號作為分水嶺，銜接在上一個 Prim path 之後所建構而成的。

> **🖼️ Property Path 範例**
>
> ![](../images/terminology/property_path.png)


> **⚠️ 注意**
>
> USD 中的 path 全部都是基於 name (名稱) 所產生的，這代表您無法定義出兩條完全相同的 path。套用到實務層面上，這代表您無法擁有兩個或兩個以上「名稱一模一樣」的 _同層級 (sibling)_ Prim。


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Path](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-path)

