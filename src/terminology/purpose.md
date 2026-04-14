# Purpose (渲染標記)


_Purpose_ 是一種可以被利用來賦予某一顆 prim 及它所有次代們一個極高層級身份的「顯示權限旗標 (visibility flag)」用的 attribute，通常都是指在針對 Render (算圖) 的最後把關脈絡中應該如何被顯現這件事來作為它的宿命。

舉例來說，如果有一顆 prim 上面的 `purpose` attribute 就已經擺明車馬被設定為了 `render` 模式，那只要當它遇上那種被使用者嚴格要求只需把 `proxy` 替身 prim 給畫出來的渲染引擎時，它就會被系統狠狠地排除在渲染清單之外。

在某種程度上來說，去決定與干預場景顯示的 purpose 設定操作，其實可以被廣泛地想像成是一種針對 Render (渲染) 工作的 [Stage Traversal](./stage_traversal.md) 操作。


就目前現狀而言，系統為 `purpose` attribute 只開出了四種可用的鐵血屬性價值：

| Purpose 種類    | 描述 | 
|--------------|-----------|
| `default` | 只要沒被設定任何標示就算這個。它代表這顆 prim 沒有任何背負特殊的渲染宿命考量，這使它會在無腦在每一次所有的渲染通道中被看見並繪製出來。      |
| `guide`      | 一旦被打上這類特殊的標籤，通常都是因為某些在進行互動溝通時的商業軟體需要去畫出「視圖導向的輔助幾何物件」。您可以把它想像成：當我們為了展示某些像是綁定的骨架控制器幾何 (controller geometry for rigs)、關節軸向等工具而發出請求的專利。  |
| `proxy`      | Proxy (代理) 這個記號通常只被允許打在那些「為了被放置在視窗 viewport 級別環境下能流暢互動」而產生的「另一組具備輕量型面數與細節代替品 (lightweight representation)」模型身上。  |
| `render`      | 這些是即將被轉換成圖片的「最純、最高無上」的海量面數資料模型。通常為了解決在 offline (非實時渲染，例如算電影畫面) 環境下進行最極限的成像渲染結果才會去把這開關給對齊過來。 |


> **⚠️ 警告**
>
> 請特別注意，跟那些百花齊放的 [Kind](./kind.md) 完全不同，`purpose` 這種屬性可容不得您在開發中隨意任性地加添任何 custom values！



> **🖼️ 範例： 在 proxy 模式與 render 模式兩種 Purpose 之間進行暴力切換**
>
> ![purpose](../images/terminology/purpose.gif)


> **📝 備註**
>
> 就像您在上方的展示中看到的那樣被重塑的操作結果一樣，`purpose` 就連存在本身都不是個能用非黑即白定義的鐵則！它無比大氣地允許您在場景中同時啟動著 `proxy` _與_ `render` 兩種目的，並把這兩者的視覺結果一併重疊顯示在您的實體主宰畫面上。



在這裡我們將 `/root/GEO` 的 purpose 給強行改寫設定為 `render` 模式，這下子除非那台辛勤工作的渲染器有去特別請託（要求回傳所有標記有 `render` purpose 名牌的傢伙）給它看，這顆物件才會有被看上的價值：
> **🖼️ Render 的目的**
>
> ![renderpurpose](../images/terminology/purpose_render.png)


若是我們如法炮製將 `/root/GEO_PROXY` purpose 也改為 `proxy`；除非當下活躍中的渲染對象強迫徵召顯示所有帶有 `proxy` 標記的傢伙們出面，否則您將永遠見不到它的殘影：

> **🖼️ Proxy 的目的**
>
> ![proxypurpose](../images/terminology/purpose_proxy.png)




---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Purpose](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-purpose)

