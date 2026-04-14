# 如何取得 USD

USD 是當今世上一套強大得令人髮指的技術生態系 (technology stack)，但不幸的是，這也是導致初學者極度難以上手的主因。它是由一連串巨大的資料庫與工具所組成，所有子項目結合成了一套構築起 USD 的生態系統。隨著第三方工具整合的成熟度越來越高，單純想要「取得並安裝 USD」這件事有時候也變成了一門學問。

身為最核心推手，皮克斯動畫工作室 (Pixar Animation Studios) 選擇在 [GitHub 上公開完整的原始碼](https://github.com/PixarAnimationStudios/USD)。對於許多軟體開發者來說，這通常會是進入這個世界的最一開始的起點。他們會將整個儲存庫 clone 回來，掛上這套生態系指定的 Python 版本與對應的編譯器，這時他們可以泡杯咖啡，讓電腦花上好幾個小時瘋狂運作，將所有的軟體工具鏈與程式庫在他們的系統底層給組裝並編譯起來。

想當然耳，這麼硬核的玩法絕對不是適用所有人的。非常慶幸地，這也絕對**不是**取得與踏入 USD 世界的唯一方法。

身為一名初來乍到的新人，通常有另外兩條路可以帶您進入 USD 的大門。

> **🔰 透過宿主應用程式 (Host Application)**
>
> Host Application 指的是那些選擇在自家的商業軟體生態系中原生植入 USD 工具庫،甚至是在誕生之初，就整間公司重構，將底層核心徹底建立在 USD 規範上的第三方軟體。
> 
> 以下是一份簡要的列表，列出了業界較為知名、且具備深度整合 USD 的宿主軟體：  
> - [NVIDIA Omniverse Create](https://www.nvidia.com/en-us/omniverse/apps/create/) - 這是一款由 [NVIDIA Omniverse](https://www.nvidia.com/en-us/omniverse) 完全基於 USD 所打造的超強視效組裝軟體，這款軟體能讓您無縫體會並接近最原汁原味的 raw USD 操作體驗。
> - [Autodesk Maya + MayaUsd](https://www.autodesk.com/products/maya) - 全球頂尖的工業級 3D 動畫軟體，Maya 提供的 USD 整合是以外掛元件形式存在，可以在安裝主程式的過程一併安裝。
> - [SideFx Houdini + Solaris](https://www.sidefx.com/products/houdini/solaris/) - 頂尖特效視覺合成 3D 軟體，其內建的視覺開發模組 (Look Development Suite) 被稱為 **Solaris**，該模組也是徹底依託並打造於底層最厚實的 USD 協議之上。


> **🔰 獨立運行版本 (Standalone)**
> 
> 就現狀來說，這大概是對一般單純想要畫圖的 Artist 最不友善的一個選項。但如果想單純享受由皮克斯官方最原汁原味打造的 USD 體驗，不妨可以挑戰看看這個路線。這條路線又分為兩種：
> 
> * **已編譯安裝檔 (Prebuilt binaries)**  
>   雖然官方放出的編譯後安裝檔案極其稀有，但在業界致力推廣這項技術的最大軍火商 NVIDIA 其實為大家默默準備了不少，您可以在 [developer.nvidia.com/usd](https://developer.nvidia.com/usd#bin) 取得。  
> 
> * **無中生有：自己親自編譯 (Compile-it-yourself)**  
>   這就是我們上面提過的，最傳統、也最地獄的 USD 開局方式。就像文章開頭所說的那樣，這對不是工程師背景出生的使用者來說，無疑是個極度令人恐懼的過程。但如果您依然對這件事充滿著濃厚的狂熱，想親手挑戰看看；皮克斯官方真的提供了一份非常詳盡且不可思議的[超強編譯指南](https://github.com/PixarAnimationStudios/USD)！


如果您是 USD 世界的新人，且目的很單純地「我只是想學習架構出一個 USD 的專案結構並與它互動」；我們會強烈建議您直接將您的 USD Composition (合成) 專題與 Layer 建立在市面上任何一款您熟悉的「宿主應用程式 (Host Application)」裡。儘管每一款宿主都有它各異的學習曲線跟獨特的挑戰性，但這絕對是幫助您飆速無痛進入狀況的最佳途徑。

> **📝 關於本書的宣告**
>
> 為了提供沒有受任一宿主框架污染的觀念，這本書當中出現的所有截圖畫面與展示，皆採用最原始的 `Compile-it-yourself` 原生版本，且絕大部分的操作也都是透過其內附的 `usdview` 工具軟體來進行展示。
