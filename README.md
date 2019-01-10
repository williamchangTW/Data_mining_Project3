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
  - - `HIT_1` 
      - 圖表只匯聚於一點(hub = Aut), 根據資料特性呈現一直線的參考, 所以在圖表的表現上, 會只單一匯聚在一個點, 也就是經過計算後每個點的排名都一樣, node 1 順序性的參考到 node 6 所以根據規則只有 node 1 hub = 0, node 6 aut = 0
    - `HIT_2`
      - 經過圖表的呈現也跟第一張圖一樣, 根據資料原始陳述, 若以 DAG 的特性去解釋, 會繞成一個圓形, 這在 HIT 演算法下也代表全部的節點同一排名, 每個點的參考別人與被參考的是一樣的, 所以 hub = aut
    - `HIT_3`
      - 這張圖比較有趣, 經錯8次迭代後hub & aut收斂在一個點, 位於 0.6~0.6025, 資料本若用圖呈現會呈現一個麻花捲的形狀, 這也代表在這幾個資料點會各自參考各自的強連結關係, 重要的是, 這張圖所陳述的像前兩張圖的合體, node 1 及 node 6 HIT 篹出來的分數沒有前兩個高, 因為中間的都有兩條指入線和指出線, 而 node 1 及 node 6 都是只有各一條
    - `HIT_4`
      - 這張圖沒有交集但看hub 是往下降的, aut 是相對往上升的, 代表被參考的少於參考別人的, 但經過運算排名後, 因為參考 node 1 及 的也佔多數, 所以得到的分數也很高, 而所有 nodes aut 分數其實差不多的, 也可以顯示出整體的狀況
    - 'HIT_5`
      - 這結果運算花了 28 秒才作完, 相對花很大量的時間在處理大量的資料, 因為相對於前面幾個資料集, 這個資料集提升10倍左右, 這個圖表表示一件事, 點一再一開始擁有參考許多別的節點資料, 根據多次迭代後降到跟一開始的 aut 差不多的範圍, 推測應該是其他節點的提升造成邊數的量提升, 相對的就沒有這麼高的 hub 數, 被分攤掉, 這份資料出線的原因我覺得是要跟下一張圖做比較, 因為下一張圖要調整參數才有辦法找到關聯性
     - `HIT_6`
        - hub 一直呈現 0, 這邊是依照資料特性作解釋, 我覺得第一個原因是因為資料量太多, 很多資料都呈現 0, 且因為 HIT 演算法的特性, 是根據邊的數量去運算每個節點的 aut 及 hub, 在這個概念下, 若線非常多且沒有什麼強連結性存在的話, 會造成整體的 HIT 值很低, 以至於**找不出任何關連性**, 算出來的結果能參考的價值也非常低, 因此, 有這樣的結果單純是因為原始資料並不是很好的判斷數據集, (註: 可以參考在上課講義中所提到的 **Topic drift**
     - `PR_1`
        - 為單向圖, 所以最後一個點的 PR 值會最高
     - `PR_2`
        - 類似於環的結構, 在這樣情況下 PR 值每個點趨於一致
     - `PR_3`
        - 麻花捲結構, 迭代多次每個點之間的 PR 值相同
     - `PR_4`
        - 資料量相對較大, 其中有幾個點 PR 值較高是因為有被參考到, 沒有特別的規律情況
     - `PR_5`
        - 如同 PR_4 一樣, 資料量相對更大且沒有很強的連接關係, 非常分散, 若阻尼係數沒有設定好會讓整個程式結果跑不出來, 因為點之間關係薄弱
     - `PR_6`
        - 如同 PR_5 一樣, 但是情況更加嚴重, 幾乎沒有關係
     - `SR_1`
        - 沒有任兩不相同的點, 同時參考到同一個點, 結果為 6*6 的單位矩陣
     - `SR_2`
        - 同 SR_1 結果, 為 5*5 的單位矩陣
     - `SR_3`
        - 在矩陣結果下, 對角線 (1, 3) 及 (2, 4) 會出現關聯性為 1, 其他為 0
     - `SR_4`
        - 計算量大, 只要任意兩點有相連結就會在矩陣上產生 1
     - `SR_5`
        - 同上解釋, 差別在於幾乎為 Spare matrix 浪費太多計算時間計算空連結
- `Computation performance analysis`
  - 執行效能上, 出現延遲最嚴重的讚於 `Simrank` 的演算法上, 因為該演算法會計算所有組合, 而在這樣的情況對於運算資源的消耗相當大, 而導致計算時間拉長, 而另外兩個演算法的方式不同在於只要找到收斂條件就不會再進行運算, 顯著地降低了許多運算
- `Discussion`
  - 全部寫在 **Note of Link analysis**，請參考下方

        
#### Qusetion & Discussion
- More limitations about link analysis algorthm
  - A: Topic drift, 
- Can link analysis algorithms find important page from Web?
- What issues from implement in a real web(performance, time cost)
  - A: 分成三個演算法說明
    1. 在 `HIT` algo 的情況下, 沒有辦法及時性的反應, 只有有增加網頁的 citation 或被 citation 都會影響整體的排名, 也很容易受到爬蟲的影響, 因為**爬蟲**會對所有相關標題進行搜尋, 所以相關路徑都會被影響, 整體效果會被影響, 也不具代表性
    2. 在 `PageRank` 的情況是依據點所佔的分數, 把分數在分散給每個參考這個節點的子節點, 
    3. 在 `SimRank`
- Design a new link-based similarity measurement
- What is the effect of C parameter in SimRank
  - A: 根據公式所呈現的, C 的增加或者是減少是不會影響整體比例, 但如果單純以 C 會造成什麼影響來看, 根據我所找的論文解釋, C 這個參數會影響迭代次數, 當 C 越大會讓結果偏差值變小, 換句話說, 是讓精準度越高, 而如何去衡量選擇 C, 簡單來說, 根據不同應用而定, 當 C 越大需要迭代次數越多, 運算時間越久, 好處是得到精準度(但有可能大於某種數值結果都一樣), 若 C 越小, 則迭代次數越少, 運算效能也比較少, 但犧牲準確度(也有可能在很低的迭代次數就有很好的結果)
- Any new idea about the link analysis algorithm
  - 整體看起來似乎是 `SimeRank` 對於 `Link analysis` 的效果是比較好的, 然而, 在我所參考的文獻中, 有提到 `Simrank` 所發生的缺點, 
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
Tutorial
- [協同過濾推薦算法總結](http://www.cnblogs.com/pinard/p/6349233.html)
- [SimRank 協同推薦算法](https://cloud.tencent.com/developer/article/1184560)
- [大規模社會網路中個體之間影響力度量](https://blog.argcv.com/articles/4534.c)
- [上課講義]()
- [菜鳥數位行銷企劃學習筆記](http://marketing.bankshung.net/2012/03/hitspagerank.html)
Github
- [pagerank.py](https://gist.github.com/diogojc/1338222)
- [hits.py](https://github.com/DevSinghSachan/HITS-Hyperlink-Induced-Topic-Search/blob/master/hits.py)
stackoverflow
- [Calculating SimRank using NetworkX?](https://stackoverflow.com/questions/9767773/calculating-simrank-using-networkx)
