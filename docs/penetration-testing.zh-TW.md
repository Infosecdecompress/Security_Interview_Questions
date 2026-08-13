# Penetration Testing

### 三種攻擊方式 - 社交、實體、網路

- **社交（Social）**
  - 向對方索取存取權、網路釣魚（phishing）。
  - 認知偏誤（Cognitive biases）- 觀察這些是如何被利用的。
  - 魚叉式網路釣魚（Spear phishing）。
  - 水坑攻擊（Water holing）。
  - 誘餌攻擊（Baiting，散布 CD 或 USB 隨身碟並期望人們去使用它們）。
  - 尾隨進入（Tailgating）。
- **實體（Physical）**
  - 取得硬碟存取權，它會被加密嗎？
  - 從 linux 開機。
  - 暴力破解密碼。
  - 鍵盤側錄程式（Keylogger）。
  - 頻率干擾（bluetooth/wifi）。
  - 隱密的竊聽裝置。
  - 隱藏的攝影機。
  - 磁碟加密。
  - Trusted Platform Module（TPM）。
  - 透過非預期的無線電或電子訊號、聲音與振動進行窺探（TEMPEST - NSA）。
- **網路（Network）**
  - Nmap。
  - 為任何執行中的服務尋找 CVE。
  - 攔截攻擊（Interception attack）。
  - 從網路上取得未受保護的資訊。

### 漏洞攻擊套件（Exploit Kit）與偷渡式下載（drive-by download）攻擊

漏洞攻擊套件是託管在惡意或遭入侵網站上的工具組，會自動偵測辨識訪客的瀏覽器與外掛程式（plugin），並發動相符的漏洞攻擊。偷渡式下載就是其結果：只要造訪該頁面，惡意程式便會被安裝，無須任何點擊，方法是利用未修補的弱點。防禦方式：修補、停用不需要的外掛程式，以及瀏覽器沙箱化（sandboxing）。

### 遠端控制

遠端程式碼執行與權限。

Bind shell（開啟連接埠並等待攻擊者）。

Reverse shell（連線到攻擊者 C2 伺服器上的連接埠）。

### 偽冒（Spoofing）

電子郵件偽冒（Email spoofing）。

IP 位址偽冒（IP address spoofing）。

MAC 偽冒（MAC spoofing）。

生物特徵偽冒（Biometric spoofing）。

ARP 偽冒（ARP spoofing）。

### 工具

Metasploit。

ExploitDB。

Shodan - 有如 Google，但針對連接到網際網路的裝置／伺服器。

在 Google 上搜尋任何東西的版本編號以尋找漏洞攻擊。

Hak5 工具。

### 參閱 MITRE attack matrix

https://attack.mitre.org/

### 滲透測試經驗問題

#### 你會如何開始一個新的滲透測試？

從界定範圍（scoping）與取得授權開始：定義目標、交戰規則（rules of engagement）與時程，並取得書面許可。接著遵循標準階段——偵查（reconnaissance，OSINT、被動／主動）、掃描與列舉（scanning and enumeration，Nmap、服務／版本探索）、弱點辨識、透過漏洞利用（exploitation）來證明衝擊、在範圍允許下進行後滲透／橫向移動（post-exploitation/pivoting），最後撰寫附有可重現步驟與修補建議的報告。事先確認它是黑箱／灰箱／白箱測試、系統是正式（production）還是測試環境，以及在你動手之前是否已有備份。

#### 你歷來最喜歡發現過的漏洞（bug）是什麼？

#### 你最喜歡的工具是什麼，為什麼？

#### 你最不喜歡的工具是什麼，為什麼？

#### 你有沒有自己寫過的工具？

#### 你有參加過任何漏洞獎勵計畫（bug bounty program）嗎？

### 惡意程式與逆向工程

#### 有趣的惡意程式

Conficker。

Morris worm。

Zeus malware。

Stuxnet。

Wannacry。

CookieMiner。

Sunburst。

#### 惡意程式的特徵

各種取得遠端程式碼執行的方法。

Domain-flux。

Fast-Flux。

隱密的 C2 通道。

規避技術（例如反沙箱）。

Process hollowing。

Mutex（互斥鎖）。

多向量與多型（polymorphic）攻擊。

RAT（remote access trojan，遠端存取木馬）的特徵。

#### 反編譯／逆向工程

程式碼混淆（Obfuscation）、獨特字串（可用於辨識程式碼）。

IdaPro、Ghidra。

#### 靜態／動態分析

描述其差異。

Virus total。

Reverse.it。

Hybrid Analysis。
