# 所以，到底什麼是 ![](./images/usd_icon_small.png) USD？

簡而言之，USD 是一種用來描述 3D 場景 hierarchy (階層) 的方法。

> **🖼️ USD 場景範例**
>
> ![](./images/alab2.png)
> <sub>[Animal Logic ALab](https://animallogic.com/alab/) USD 場景，於 USDView 中的畫面</sub>


一般來說，hierarchy 包含了數個實體（即 `node` 或節點），這使得這些 node 能與其他 node 建立 parent / child / sibling（父子或相鄰）的層級關係。  
在 USD 中，這些 node 可以是具備「物理實體」的東西（您可以想像成 Geometry 幾何體、Animation 動畫 data 等...）或者是更抽象的東西，諸如群組物件、materials、shaders，甚至連「設定值」本身都可以被表達為 hierarchy 裡的一個 node。

USD 與其他傳統場景描述技術存在巨大落差的地方在於，它具備了「將多個 hierarchy 搭配不同的行為規則組合在一起」的超強能力（這項能力又被稱為 [Composition (合成)](./terminology/composition.md)）。在 USD 中，您總是以非破壞性 (non-destructively) 的方式去參照 (refer) 或是嫁接另外幾個 hierarchy 到當前的檔案中、重新定義先前就已定義過好的 data、又或者是讓一整個超大團隊在「同一個 hierarchy」上進行天衣無縫的協作開發。

> **🖼️ USD 場景的 Composition (合成) 範例**
>
> ![](./images/alab_root_layer_stack.png)  
> <sub>構成 [Animal Logic ALab](https://animallogic.com/alab/) USD 場景合成系統（於 USDView 顯示）的 USD 子場景清單片段</sub>


## 等等，不只這樣！

除了前述「非破壞性地合成 hierarchy」之外，USD 更是以極高擴展性 (extensible) 為初衷所打造的。  
舉例來說，您可以開發一款 plugin 來擴展 USD 功能，讓它能夠自動解析某種客製化或是商用專屬檔案格式，並允許您直接在 USD 環境去「原生地」使用那些檔案。

> **📝 備註**
>
> 業界一個最經典的實例，就是實現在 USD hierarchy 當中原生且直接地調用與讀取 FBX 檔案格式。


總體來說，USD 透過定義一套共通且共享的溝通「語言」來描述場景與 3D data，藉此達到成為一個高度可攜帶且流通的交換格式。  
這個概念雖然不算新穎，但在這一切優勢之上，它還同時附帶提供了一個強大無比的方法來統一繪製 (draw)／渲染 (render)／成像 (image) 這些複雜的場景。這個渲染成真的一切，都要歸功於 USD 御用的後端渲染框架：`Hydra`。

> **⚠️ 注意**
>
> 本書目前尚未涵蓋跟 Hydra 相關的進階概念，未來隨著版本的更新可能才會考慮補齊。

