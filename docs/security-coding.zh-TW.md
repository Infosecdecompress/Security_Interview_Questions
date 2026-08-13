# 資安相關的程式設計與演算法

- 基礎
  - 條件判斷（if、else）。
  - 迴圈（for 迴圈、while 迴圈）。
  - 字典（dictionary）。
  - 切片（slice）/清單（list）/陣列（array）。
  - 字串/陣列操作（split、contaings、length、正規表示式）。
  - 虛擬碼（pseudo code，簡潔地描述你解題的思路）。

- 資料結構
  - 字典 / 雜湊表（hash table，鏈結串列的陣列，有時也用 BST）。
  - 陣列。
  - 堆疊（stack）。
  - SQL/資料表。
  - Bigtable。

- 排序
  - Quicksort、merge sort。

- 搜尋
  - 二分搜尋（binary）與線性搜尋（linear）的比較。

- Big O
  - 針對空間與時間複雜度。

- 正規表示式
  - 通常比對是 O(n)，但採用回溯（backtracking）的引擎在最壞情況下可能達到指數等級 O(2^n)（災難性回溯，catastrophic backtracking）。
  - 熟悉基本的 regex 語法也很有用。

- 遞迴
  - 以及何時該改用迭代（stack 深度 / 效能考量）。

- Python
  - 串列生成式與生成器（generator）[ x for x in range() ]。
  - 迭代器（iterator）與生成器。
  - 切片 [start:stop:step]。
  - 正規表示式。
  - 型別（動態型別）、資料結構。
  - Python 與 C、Java 等語言相比的優缺點。
  - 對常用函式要非常熟悉，並對這個語言運用自如。

## 資安主題的程式設計挑戰

- 加密法 / 加密演算法
  - 能夠實作基本的加密法（cypher）。

- 解析任意的日誌
  - 練習文字解析。

- 網路爬蟲（web scraper）
  - 另一種練習文字解析的方式。

- 連接埠掃描器（port scanner）
  - 練習解析網路資訊。

- 殭屍網路（botnet）
  - 你會如何建立一個 ssh 殭屍網路。

- 密碼暴力破解器（bruteforcer）
- 從 PDF 抓取中繼資料（meta data）
- 用來還原已刪除項目的腳本
- 一支在二進位檔 / 程式碼樣本中尋找惡意程式特徵碼（malware signature）的程式
