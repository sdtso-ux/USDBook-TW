# Overrides (覆寫)


當您在 Layer 中表達意見 (opinion) 時，有一種做法是把該 property 早就已經定義好的舊數值給「重新定義 (redefine)」一番。這個無情的機制就叫做 `overrides`，顧名思義，因為您正在 _覆寫 (overriding)_ 掉前人留下來的遺產。
然而，千萬要牢記一件在 USD 中至關重要的底線：_最一開始的原始 data (original data)_ 自始至終都能保持純淨完整、未曾受過任何一絲的改變。**這種「覆寫」的作為，只會而且永遠只存在於「您提出這個覆寫行為當下的那一層 Layer」裡面而已！**

毫無懸念的，這是您在學習 USD 的漫漫長路中 _最首要_ 去建立及領會的概念。各種各樣的意見 (Opinions) 加上與它們的「數值解析 (value resolution)」（也就是去解析到底最後是哪一條數值能在層層堆疊的大逃殺中脫穎而出、被真正實踐），這兩者正是驅動起整個 Composition 機制的關鍵齒輪。

以下是一個非常經典的案例，展示了一條被前人定義過的 attribute opinion 是怎麼硬生生被覆蓋掉的。

> **🖼️ override 範例**
>
> [![schematic](../images/terminology/overrides.png)](../images/terminology/overrides.png)
> 
> 1. 上圖展示了 `cube_sphere_torus.usda` 這層 layer 裡面，因為某個 attribute 第一次被建立而產生出的 [opinion (意見/主張)] (`/GEO/Cube.size`)
> 2. 接著展示了 `referenced.usda`，在這個環境中發生了：
>    * 利用了一種名為 `referencing` 的 [composition (合成)] 機制，將剛剛的 `cube_sphere_torus.usda` 整層打包請進了 `referenced.usda` 這個檔案中
>    * 針對那個在上游就已經被定義過的 `/GEO/Cube.size` attribute 提出了強烈的意見，但在這個語境之下，這一切都只發生在我們剛才引進的 `cube_sphere_torus.usda` 脈絡裡，本質上這就是去硬生生蓋掉它原先的大小
> 3. 最後展示了經過層層交疊與剝削後，最後合成輸出的終極結果，也就是所謂的 [stage (舞台)]


[composition]: composition.md
[opinion]: opinions.md
[stage]: stage.md

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - Override](https://graphics.pixar.com/usd/release/glossary.html#usdglossary-override)

