# 前言與動機

通用場景描述 (Universal Scene Description, USD) 上市至今已經在 VFX/電影與遊戲產業掀起巨大的波瀾，這包含了業界的幾家巨頭例如 [NVidia](https://www.nvidia.com/en-us/omniverse/)、[Apple](https://opensource.apple.com/projects/usd/) 以及 [Autodesk](https://makeanything.autodesk.com/usd) 也全數投入這項技術的開發與整合中。但如果您是一位初學者，跨入這個領域絕對會是一趟讓人感到極度怯步且充滿挫折的旅程。

這本書誕生的核心動力，正是希望能提供一個**更簡潔、對新手友善且具備結構化**的學習途徑，幫大家深入淺出地介紹 USD 及其核心邏輯與術語。目前本書會將重心大量擺在 USD Terminology (術語字典) 上，但未來我們將持續擴增更多工作流的實際範例。

> **❓ 讀到這邊，您也許會想問**
>
> _我為什麼要看這本書，而不是直接去看[官方 USD 術語表 (Glossary)](https://graphics.pixar.com/usd/release/glossary.html) 與[官方教學](https://graphics.pixar.com/usd/release/tut_usd_tutorials.html)？_


一頭栽進[官方 USD 術語表](https://graphics.pixar.com/usd/release/glossary.html)或[官方教學](https://graphics.pixar.com/usd/release/tut_usd_tutorials.html)絕對是非常正確的學習策略；不幸的是，現實情況是 USD 是一台結構極其複雜的巨型機器，內部擁有無限多個盤根錯節的運作機制。如果您本身不是軟體工程師，光是想要打開 USD 官方內建的軟體如 `USDView`，就已經會搞得您一個頭兩個大了。  
許多概念也是彼此深度綑綁的，因此初學者極度容易在字海中溺水。這種「跌入愛麗絲夢遊仙境兔子洞」般的學習法，只會帶來成噸的困惑與壓力。

這本書正是為了解決這個痛點而準備的另一條避坑捷徑。


------- 

> **📝 原著作者的備註**
>
> 在 [Remedy Entertainment](https://www.remedygames.com) 工作室中，我們絕對是 100% <font color=Red>❤</font> USD 的！我們甚至辦過[一場實體演講](https://www.youtube.com/watch?v=FI2pyzTOvaQ)來分享我們是如何利用它來製作 AAA 級遊戲大作！
> 
> 在那場演說之後，我們被要求公開內部在使用 USD 時撰寫的文件，因為我們為團隊寫了一份更簡易版的[官方 USD 術語翻譯版](https://graphics.pixar.com/usd/release/glossary.html)。這本書就是那份內部文件，經過修飾、改寫，並調整為相容於 `mdbook` 的公開發行版本。
> 
> 我們選擇了一個非常寬鬆的開源授權釋出這本心血結晶，因此您可以隨心所欲地視您的需求 fork / copy / change 您專屬的書籍版本。
