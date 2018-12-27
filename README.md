# Data_mining_Project3
as title(just for Project3)
contributed by <`williamchangTW`>

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
  
## 題目
- Please implement
  - HITS and PageRank (Lecture 7, P37, random jumping probability, i.e., damping factor=0.15) and calculate authority, hub and PageRank values for the following 8 graphs
    - 6 graphs in project3dataset
    - 1 graphs from project1 transaction data (connect items in each row, bidirected or directed)
  - SimRank to calculate pair-wise similarity of nodes (choice any parameter C you like) , using
    - first 5 graphs of project3dataset.
    - 答案:根據每個圖檔標示數字代表實作該圖檔(依序)
    - `HIT_1` 
      - 圖表只匯聚於一點(hub = Aut), 根據資料特性呈現一直線的參考, 所以在圖表的表現上, 會只單一匯聚在一個點, 也就是經過計算後每個點的排名都一樣, node 1 順序性的參考到 node 6 所以根據規則只有 node 1 hub = 0, node 6 aut = 0
    - `HIT_2`
      - 經過圖表的呈現也跟第一張圖一樣, 根據資料原始陳述, 若以 DAG 的特性去解釋, 會繞成一個圓形, 這在 HIT 演算法下也代表全部的節點同一排名, 每個點的參考別人與被參考的是一樣的, 所以 hub = aut
    - `HIT_3`
      - 這張圖比較有趣, 經錯8次迭代後hub & aut收斂在一個點, 位於 0.6~0.6025, 資料本若用圖呈現會呈現一個麻花捲的形狀, 這也代表在這幾個資料點會各自參考各自的強連結關係, 每個點的 hub = aut
    - `HIT_4`
      - 這張圖沒有交集但看hub 是往下降的, Aut 是相對往上升的, 代表被參考的少於參考別人的, 但經過運算排名後, 因為參考節點一的也佔多數, 所以得到的分數也很考
    - 'HIT_5`
      - 這結果運算花了 28 秒才作完, 相對花很大量的時間在處理大量的資料, 因為相對於前面幾個資料集, 這個資料集提升10倍左右, 這個圖表表示一件事, 點一再一開始擁有參考許多別的節點資料, 根據多次迭代後降到跟一開始的 Aut 差不多的範圍, 推測應該是其他節點的提升造成邊數的量提升, 相對的就沒有這麼高的 hub 數, 被分攤掉
     - `HIT_6`
        - hub 一直呈現 0 的狀態是因為, 他只有參考別人的數量
     - `PR_1`
     - `PR_2`
     - `PR_3`
     - `PR_4`
     - `PR_5`
     - `PR_6`
     - `SR_1`
     - `SR_2`
     - `SR_3`
     - `SR_4`
     - `SR_5`
      
- Find a way (e.g., add/delete some links) to increase hub, authority, and PageRank of Node 1 in first 3 graphs respectively.    
    - 答案: 依據 HIT 特性只要刪除節點伊以外的節點邊就可以達到相同效果
    - 以下是根據圖檔變換裡面資料(檔名為HIT_ch_X, PR_ch_X)
      - graph_1
        - 1,2
        - 2,3
        - 3,4
        - 4,5
        - 5,6
        - (增加所有能加的邊到 `node1`)
        - 1,3
        - 1,4
        - 1,5
        - 1,6
        - 2,1
        - 3,1
        - 4,1
        - 5,1
        - conclusion:
          - Hub increase from 0.4472136 to 0.70705751
          - Auth increase from 0 to 0.53460939
          - Pagerank increase from 0.02773825 to 0.38159199
      - graph_2
        - 1,2
        - 2,3
        - 3,4
        - 4,5
        - 5,1
        - 2,4
        - 2,5
        - 3,5
        - 1,3
        - 1,4
        - 1,5
        - 2,1
        - 3,1
        - 4,1
        - conclusion:
          - Hub increase from 0.4472136 to 0.49711279
          - Auth increase from 0.4472136 to 0.49717426
          - Pagerank increase from 0.4472136 to 0.46201128
      - graph_3
        - 1,2
        - 2,1
        - 2,3
        - 3,2
        - 3,4
        - 4,3
        - 3,1
        - 4,1
        - 1,3
        - 1,4
        - conclusion:
          - Hub increase from 0.37175742 to 0.63232892
          - Auth increase from 0.37172346 to 0.55737738
          - **Pagerank from 0.5 to 0.5**

## Requirement
- `Implementation detail`
  - 參考講義的演算法，程式碼部分參考多線上資源及他人的 Github
- `Result analysis and discussion`
  - 
- `Computation performance analysis`
  - 
- `Discussion`
  - 全部寫在 **Note of Link analysis**，請參考下方

        
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
    document in another host 
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
