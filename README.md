# Book of USD (繁體中文版)

![Preview with Frappe styling of the book](./preview.png)

## 關於本中文翻譯專案

基於對 Universal Scene Description (USD) 格式的熱愛與學習熱忱，我在近期偶然發現了 **Book of USD** 這個優秀的開源計畫。為了讓更多台灣及中文語系的 CG / VFX / Pipeline 從業人員能夠無痛跨越語言的門檻，一窺 USD 的強大技術底層，我立刻萌生了將其在地化翻轉為繁體中文版的想法。

在人工智能 **Gemini** 的高效協助下，我迅速且專業地對原有文件進行了審閱與中文在地化的翻譯。期望這份文件能成為大家踏入 USD 宇宙的優質起點！

## 關於這本書 (About)

這本線上電子書的宗旨在於提供一個更具人類可讀性、且對設計師與藝術家 (artist-friendly) 更加友善的方式，來幫助大家學習 Universal Scene Description (USD) 以及其背後龐大的專業術語。它並非用來取代[官方的 USD Glossary 字典](https://graphics.pixar.com/usd/release/glossary.html)，而是作為任何剛接觸這項技術的新手或初學者的起點。

---

## 建置與安裝說明

### 安裝 Rust 語言與依賴套件

- 請遵循官方教學 [https://www.rust-lang.org/learn/get-started](https://www.rust-lang.org/learn/get-started) 的指示，為您的系統安裝 Rust 語言環境。
- 執行 `rustup update` 指令，將您的 rust 更新至最新版本。
- 執行以下指令安裝 [`mdbook`](https://rust-lang.github.io/mdBook/) 以及額外的擴充主題（視您的需要）：
  ```bash
  cargo install mdbook mdbook-catppuccin mdbook-admonish
  ```
  *(註：此繁中分支版本已將舊有標籤語法重構為原生 mdbook 支援的格式，基本上您只需確保安裝 `mdbook` v0.5 以上的版本即可順利編譯。)*

### 編譯輸出 (Building)
專案的建置非常簡單，只需執行：
```bash
mdbook build -d <欲輸出的資料夾路徑>
```

建議您偶爾也執行一次 `mdbook clean -d <欲輸出的資料夾路徑>` 來清理編譯快取檔，確保每次編譯輸出的整潔。

### 網站預覽 (Previewing)
您可以隨時透過以下指令啟動本地端的開發伺服器來預覽這本書。這個指令除了會自動編譯書籍，還會直接幫您在網頁瀏覽器中打開它！
```bash
mdbook serve --open
```
