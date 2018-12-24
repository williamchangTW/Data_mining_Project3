# Data_mining_Project3
as title(just for Project3)
contributed by <`williamchangTW`>

### Requirement
- 實作細節
- 結果分析與討論
- 計算效能分析
- 從中學到什麼?
#### Link Analysis Pratice
- `HITS` & `PageRank`(Lecture 7,P_37, random jumping probability, damping facto=0.15)
  - caculate(8 graphs->6 graphs from file, 1 graph from Project1 transaction data):
    - authority
    - hub
    - PageRank
- `SimRank` first 5 graphs(from file), choice any parameter C
- add/delete some links to increase(Node 1 in first 3 graphs) 
  - hub
  - authority
  - PageRank
#### Qusetion & Discussion
- More limitations about link analysis algorthm
- Can link analysis algorithms find important page from Web?
- What issues from implement in a real web(performance, time cost)
- Design a new link-based similarity measurement
- What is the effect of C parameter in SimRank
- Any new idae about the link analysis algorithm
## Note of Link Analysis

- 目的:
  - 根據瀏覽次數分析關聯性或重要性

- 早期成果

  - 超連結會呈現人的判斷

  - 越多人參考的連結，連帶地會有更強的參考依據
  - 舉例：
    - 節點為 `person` or `organizations`
    - 編為 `social interaction`

- 遇到的問題: 在 `indegree` 和 `outdegree` 中的考量因素不一樣，對處理結果的影響可能會有限制（難以處理連節相關性）

### HITS - Algorithm

- HIT disadvantage
  - 當非常少的 edge，點上有大量的分數會被分離
  - 真正 authoritative pages 沒有被包含在 root 中
  - The document can contain many identical links to the same
    document in another host (ಭ纏蟂褧)
  - Links are generated automatically (e.g. messages posted
    on newsgroups)
    • Containing human’s opinion ? 
  - Non-relevant Nodes
    • Topic drift 

### PageRank

- 透過 `Title` 標籤和 `Keywords` 等標籤因素, google 透過 `Page Rank` 來調整網站關鍵字排名結果，使真正的關鍵字獲得排名的提升
  - 藉由此提高搜尋 **相關性** 和 **品質**
  - 如何作業
    - 根據搜尋關鍵字匹配網頁
    - 標題關鍵字密度等級排序
    - 計算導入連結的連結關鍵字
    - 透過 `PageRank` 分數調整關鍵字排名結果
- 判定依據?
  - 若 B 網頁參考 A 網頁連結，說明 B 認為 A 網頁有參考價值，是一個重要的網頁，若 B 網頁經由 `PageRank` 的計算分數高的話，就可以平均給 A 網頁
  - 

#### HIT algorithm v.s. PageRank 

- `HIT` 演算法
  - 用戶輸入的查詢請求密切相關(可以 **單獨作為相似性計算評價標準**)
  - 必須要收到用戶資料進行即時的運算(運算 **效能差**)
  - 計算物件較少，只需擴展集合內的網頁鏈結關係
  - 適合部屬在用戶端
  - 存在主題氾化問題，更適合處理具體化的用戶查詢
  - 對每個頁面都要求兩個值(`Authority` 和 `Hub`)
  - 容易受到鏈結作弊影響
  - 在集合內作些微的改變會對排名產生劇烈的改變
- `PageRank` 演算法
  - 與查詢請求無相關(必須 **結合相似性運算** 才能對網頁行評價)
  - 可以用爬算的計算結果直接計算（運算 **效率高**)
  - 全局演算法，對所有網頁進行處理
  - 適合部屬在伺服器端
  - 處理廣泛的用戶查詢有優勢
  - 只需要一個值
  - 不容易受到鏈結作弊影響
  - 遠端跳轉

### SimRank - Algorithm

- 基於圖論
- 基本概念: 若 A 使用者與 B 使用者相似，用的東西也會相似，根據用戶性格相似或參考節點
- 若二分圖為  $G(V,E)$
  - 其中 $V$ 是節點的集合
  - $E$ 是邊的集合
  - $s(a, b)$ a 與 b 可以用來表示節點的相似度
    - 即 $$s(a,b) = \frac{C}{|I(a)||I(b)|}\sum\limits_{i=1}^{|I_(a)|}\sum\limits_{j=1}^{|I_(b)|}s(I_i(a),I_i(b))$$
    - `C` 為一個常數
- **SimRank** 算法流程
  - 輸入: 
    - 二分圖對應的轉置矩陣 `W`
    - 阻尼常數 `C`
    - 最大迭代次數 `k`
  - 輸出:
    - 子集相似度矩陣 `S`:
      - 一開始設為單位矩陣 `I`
      - 對於 i = 1~k
        - $temp = CW^TSW$
        - $S = temp + I - Diag(diag(temp))$
- **SimRank++** 算法原理( `SimRank` 針對弱點加強版)
  - 做到兩點改進
    - 考慮 `Edge` 的加權值
    - 考慮 `子集 Node 相似度` 的證據
  - 對於**邊** 的改進
    - 在 `SimRank` 的演算法
      - 用**關聯邊數分之一** 作為權重計算方法
      - 並沒有考慮到不同邊可能有不同的權重
    - `SimRank++` 則是考慮到**每個編的不同權重** 在 **轉置矩陣 W** 中
  - 對於 **子集 node 相似度** 的確認
    - 在 `SimRank` 演算法中
      - 認為只要 **邊有相連就為相似**
      - 沒有考慮到 **共同相連邊越多** 代表兩點就越 **相似**
    - 在 `SimRank++` 中
      - 經過迭代多次就會修正，得到最後的相似值
- **如何加快運算速度**
  - 有兩種方法
    - 將大數據進行分散式的平台運算
      - 如: `Spark`, `Hadoop`, `MapReduce`
      - 或者將矩陣平行化運算
    - 用`蒙地卡羅(Monte Carlo, MC)` 相似
      - 將兩節點 `SimRank` 設為期望值(即為兩點隨機再圖上走相遇的時間)
      - 複雜度會降低, 但精確度會下降(因為**隨機**)
- **與 PageRank 之間的差別**
  - `PageRank` 指得到單一節點的權重
  - `SimRank` 得到兩兩之間的權重度量

###### Reference

- [協同過濾推薦算法總結](http://www.cnblogs.com/pinard/p/6349233.html)
- [SimRank 協同推薦算法](https://cloud.tencent.com/developer/article/1184560)
- [大規模社會網路中個體之間影響力度量](https://blog.argcv.com/articles/4534.c)

- [上課講義]()

- [菜鳥數位行銷企劃學習筆記](http://marketing.bankshung.net/2012/03/hitspagerank.html)
