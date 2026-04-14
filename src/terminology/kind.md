# Kind (分類層級)

_Kind_ 是一種掛載在 Prim 層級的 metadatum，它的功用是能將數顆 prim 以及所有它底下的子子孫孫直接提升至比它們自身實體定義（像是 `Mesh`, `Sphere`, `Cube` 等）還要高出一個次元的「宏觀概念定位」。

> **🖼️ 套用 Kind 分類的實戰**
>
> ![kind](../images/terminology/kind.png)


皮克斯原廠隨附出貨時，USD 裡就自帶了幾種不同位階的 `kind` 等級來給這群 prims 當作身分標記：

| Kind 分級         | 它的工作是什麼？     |
|--------------|-----------|
| **model** | 所有模型 kind 中最基礎的父層級。`model` 本身被視為一個極度抽象的原型特質，它永遠不應該被拿來作為「任何單一 prim 身上的唯一實體標籤」使用。|
| **group** | 就是個把其他一群 model 給「圈起來」的模型群組|
| **assembly** | 這是一個具備極度重要地位的打包模型，它通常代表了一個「對外發布的完成體 asset」，或者是由外部 reference 進來的組裝模型 |
| **component** | 想像它是一片「長滿葉子的終結點基底模型 (leaf model)」，它不再允許自己的肚子裡裝載任何其他的模型|
| **subcomponent** | 一個 component 身上被獨立指認出來、有著特殊任務的「子零件」模型|

> **💡 提示**
>
> 您絕對可以透過各種客製的 USD Plugins 來隨心所欲地擴增那些清單上沒有的 `kind` 出來！



為模型標注 kind 最大的實質意義，在於能夠在進行系統 Stage Traversal 的期間「神速」找出那些符合您「心儀身分」的 prim 類型。比方說，系統可以靠著掃過一遍 kind 的標記籤章，去有選擇性地一舉抹除 (prune) 整個特定位階底下的老少婦孺物件樹！


## 所以 Kind 到底實際是如何參與生產的？

讓我們來檢視 [Animal Logic ALab](https://animallogic.com/alab/) 提供的根圖層為例，我們可以看到身處體系最高層級的那些金字塔頂端 prim，每一個都被莊嚴地標注上了 `assembly`（組裝體）的頭銜。這使得我們在極其龐大的場景中依然能輕鬆依層級定位出所有的「實體道具 asset」。在下圖的展示中，無論是 `lab_workbench01_0001` 或甚至是它的父物件 `alab_set01` 都被賦予了 assembly 的最高階層授權。

> **🖼️ lab_workbench01_0001**
>
> ![](../images/terminology/kind_assembly.png)


一個只要是被標注擁有 `assembly` 頭銜的孤獨 prim 肚子裡，理所當然包含了成千上萬掛有各式各樣不同等級 `kind` 標注的其餘 prim。我們接著往深處挖掘剛才的第一個範例，我們可以看到光是那張工作桌在 `/root/alab_set01/lab_workbench01_0001/workbench01` 這個位置本身，也僅僅是被標示為一個單純的 `group` 而已。

> **🖼️ workbench01**
>
> ![](../images/terminology/kind_group.png)


接著如果我們潛入海底的更深處，看見了 `/root/alab_set01/lab_workbench01_0001/workbench01/furniture_workbench01_0001` 這顆孤獨的 prim 則被徹底標示了 `component` 的結案標籤。按照規矩，但凡只要是標注為 Component 的這群傢伙，基本上裡面就不應該再繼續包山包海地去儲藏任何同樣是從 `model` 血統衍生出來的那些複雜 `kind` 類型了，但是，它還是可以容許少數擁有 `subcomponent` 這種最微末階級身分的朋友出現。

> **🖼️ furniture_workbench01_0001**
>
> ![](../images/terminology/kind_component.png)


透過上述這種把身分都給標明的層層階級化之後，針對那些龐大複雜的物件，我們只需要透過尋找底層這類的 `component` 物件們，就可以在不必勞心費神去層層過濾底層那萬丈深淵般 hierarchy 結構的前提下，達成非常有效率且強大的物件資產搜索以及 [instancing (實例化)](./instancing.md) 調用。

> **📝 備註**
>
> 每個視效生產環境的體系都不太一樣，因此對某間特效工作室而言，什麼才算是一顆 `asset`，到了另一間可能標準又是南轅北轍。然而，這種透過 `kind` 來建立階級金字塔分類的思想哲學，在工業界實務上依然能創造出無與倫比的巨大產能價值！


---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Kind](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-kind)
