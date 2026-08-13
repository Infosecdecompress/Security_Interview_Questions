# 基礎網路與網路安全

### OSI 模型

- 應用層（Application）；第 7 層（基本上也涵蓋第 5 與第 6 層）（包含 API、HTTP 等）
- 傳輸層（Transport）；第 4 層（TCP/UDP）
- 網路層（Network）；第 3 層（路由）
- 資料連結層（Datalink）；第 2 層（錯誤檢查與訊框同步）
- 實體層（Physical）；第 1 層（透過光纖傳輸位元）

### 常見協定與連接埠

- HTTP/S
  - 連接埠 80、443

- SSL/TLS
  - 連接埠 443
  - 這部分非常重要，務必學習，包含了解交握（handshake）、加密、簽章、憑證授權單位（certificate authority）以及信任系統。荷蘭資安中心提供了[一份涵蓋這些概念與演算法的優良入門文件](https://english.ncsc.nl/publications/publications/2019/juni/01/it-security-guidelines-for-transport-layer-security-tls)。
  - 針對舊版 SSL/TLS 的各種攻擊（都有琅琅上口的名稱），可參考 [Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security#Attacks_against_TLS/SSL)

- ICMP
  - Ping 與 traceroute

- 郵件
  - SMTP（連接埠 25、587、465）
  - IMAP（連接埠 143、993）
  - POP3（連接埠 110、995）

- SSH
  - 連接埠 22
  - 交握使用非對稱加密來交換對稱金鑰

- Telnet
  - 連接埠 23、992
  - 允許與主機進行遠端通訊

- ARP
  - Who is 0.0.0.0? Tell 0.0.0.1.
  - 將 MAC 位址與 IP 位址配對以建立 IP 連線。會先查看快取。
  - 這是一種用於將 IP 位址對應到連接在區域網路（LAN）上的電腦的協定。由於每台電腦都有一個稱為 MAC 位址的唯一實體位址，ARP 會將 IP 位址轉換成 MAC 位址。這確保每台電腦都有唯一的網路識別。
  - ARP 是 UDP 還是 TCP？兩者都不是

- DHCP
  - 連接埠 67、68、546、547
  - 自動（租用 IP 位址，並在表格中記住 MAC 與 IP 的配對）
  - 手動（由管理員設定的靜態 IP）
  - 動態（租用 IP 位址，非永久性。由路由器配置）。
  - `DHCPDISCOVER` -> `DHCPOFFER` -> `DHCPREQUEST` -> `DHCPACK`
  - 惡意 DHCP（Rogue DHCP）：惡意的 DHCP 伺服器可以重新導向 IP 位址的指派，讓駭客得以識別並將客戶端電腦重新導向到另一個網路區段。駭客接著便能從目標機器竊聽網路流量。

- IRC
  - 了解駭客的使用方式（殭屍網路，botnet）

- FTP/SFTP
  - 連接埠 21、22

- RPC
  - 一組預先定義、可供遠端客戶端執行的任務
  - 在組織內部使用

- 服務連接埠
  - 0 - 1023：保留給常見服務——需要 sudo 權限
  - 1024 - 49151：註冊連接埠，供 IANA 註冊的服務使用
  - 49152 - 65535：動態連接埠，可用於任何用途

### TCP / UDP

#### 說明 TCP 與 UDP 的差異。

TCP 透過為封包（packet）編號來保證接收方會依序收到封包。

使用 UDP 時，封包只是單純被送往接收方。傳送方不會等待確認接收方是否已收到封包——它會直接繼續傳送下一批封包。

#### 哪一個較安全？TCP 還是 UDP？為什麼？

TCP，因為 TCP 必須建立連線。

### DNS

連接埠 53

對 DNS 的請求通常是 UDP，除非伺服器發出重新導向通知要求建立 TCP 連線。會先查看快取。DNS 資料外洩（exfiltration）。使用原始 IP 位址代表不會有 DNS 記錄檔，但仍會有 HTTP 記錄檔。DNS 沉洞（sinkhole）。

在反向 DNS 查詢中，PTR 可能包含 2.152.80.208.in-addr.arpa，其對應到 208.80.152.2。DNS 查詢從字串的尾端開始並往回處理，這就是為什麼 PTR 中的 IP 位址是反向的。

#### DNS 資料外洩

- 將資料以子網域的形式傳送
- 26856485f6476a567567c6576e678.badguy.com
- 不會出現在 http 記錄檔中

#### DNS 設定

- 授權起始（Start of Authority，SOA）
- IP 位址（A 與 AAAA）
- SMTP 郵件交換器（MX）
- 名稱伺服器（NS）
- 反向 DNS 查詢的指標（PTR）
- 網域名稱別名（CNAME）

#### 為什麼需要 DNS 監控

網域名稱系統（DNS）將你的網站配置在一個容易辨識的特定網域下，同時也保存了其他網域名稱的資訊。

它的運作就像網際網路上所有事物的目錄。

因此，DNS 監控非常重要，因為你可以輕鬆造訪網站，而無需實際記住它們的 IP 位址。

#### 權威 DNS 伺服器 vs. 遞迴 DNS 伺服器

權威名稱伺服器（Authoritative name server）儲存 DNS 記錄資訊——通常是 DNS 代管供應商或網域註冊商。

遞迴名稱伺服器（Recursive name server）是權威伺服器與終端使用者之間的「中間人」，因為它們必須沿著 DNS 樹向上遞迴，才能抵達負責儲存該網域記錄的權威名稱伺服器。

#### 什麼是 DNS 欺騙（快取毒化，cache poisoning）？它如何運作？

攻擊者讓 DNS 解析器快取一筆偽造的記錄，使某個網域解析到攻擊者控制的 IP。由於傳統 DNS 在沒有驗證的情況下透過 UDP 運作，能夠猜測或觀察到查詢的交易 ID（transaction ID）與來源連接埠的攻擊者——或者單純在與真實回應的競賽中勝出——便能傳送一筆偽造的回應，讓解析器接受並快取。該解析器的每一位使用者接著都會被重新導向，直到該記錄的 TTL 到期為止。緩解措施：DNSSEC（以密碼學方式簽署記錄）、隨機化的來源連接埠與交易 ID，以及 0x20 位元查詢編碼。

### 什麼是子網路（subnet），它在安全上有何用處？

你可以使用 ACL、QoS 或 route-map 來控制流量的走向，讓你更容易識別威脅、封閉進入點，並更精準地鎖定你的因應措施。

限制無線客戶端對資源的存取，確保有價值的資訊在遠端位置不會輕易被存取。

### Ping 是透過哪個連接埠運作的？

ICMP 不使用連接埠。

### 防火牆 / IPS / IDS

用來防止傳入與傳出連線的規則。

防火牆是一種扮演守門員角色的裝置或服務，決定什麼可以進出網路。它透過檢查封包標頭與資料來分析經過它的流量。防火牆接著會依據其設定，據以決定是否拒絕或允許流量通過。

#### 在防火牆上，你偏好過濾（filtered）連接埠還是關閉（closed）連接埠？為什麼？

過濾（靜默丟棄，不回覆）通常比關閉（會送出 TCP RST 或 ICMP unreachable）更受青睞。關閉的連接埠仍會回應，等於確認了主機存活且連接埠可達；而過濾的連接埠不回傳任何東西，因此掃描者所能得知的較少，且必須等待逾時，拖慢了偵察的速度。取捨在於：全部丟棄可能會使正當的網路疑難排解變得複雜。

#### IPS vs 防火牆

防火牆的主要功能是防止／控制來自不受信任網路（外部）的流量走向。防火牆無法偵測資料偏離其常規模式的攻擊，而 IPS 因為內建異常偵測，能夠偵測到並重置該連線。

#### NIDS

NIDS（網路入侵偵測系統，Network Intrusion Detection System）是一種嘗試偵測駭客活動、阻斷服務攻擊或針對電腦網路或電腦本身進行連接埠掃描的系統。NIDS 監控網路流量，並透過識別傳入封包中的可疑模式來協助偵測這些惡意活動。

### HTTP

#### HTTP 標頭

- | 動詞（Verb） | 路徑（Path） | HTTP 版本 |
- 網域（Domain）
- Accept
- Accept-language
- Accept-charset
- Accept-encoding（壓縮類型）
- Connection——close 或 keep-alive
- Referrer
- 回傳位址（Return address）
- 預期大小？（Expected Size）

#### HTTP 回應標頭

- HTTP 版本
- 狀態碼：
  - 1xx：資訊性回應
  - 2xx：成功
  - 3xx：重新導向
  - 4xx：客戶端錯誤
  - 5xx：伺服器錯誤
- 回應中的資料類型
- 編碼類型
- 語言
- 字元集（Charset）

#### 常見的 HTTP 攻擊

- SQL injection
- URL 解讀（URL interpretation）
- 冒充（Impersonation）
- 緩衝區溢位（Buffer overflow）
- 工作階段劫持（Session Hijacking）
- 跨網站指令碼攻擊（Cross-Site Scripting）

### 什麼是 DDoS？

一種意圖使伺服器或網路資源對使用者無法使用的惡意嘗試。

它是透過使某項服務飽和來達成，導致該服務暫時中止或中斷。

阻斷服務（DoS）攻擊使用單一機器，來針對軟體弱點或以封包、請求或查詢淹沒目標資源。

然而，分散式阻斷服務（DDoS）攻擊則使用多台連網裝置——通常由殭屍網路執行，偶爾也由協調彼此行動的個人執行。

### Traceroute

通常使用 UDP，但也可能使用 ICMP Echo Request 或 TCP SYN。TTL，即跳躍限制（hop-limit）。

初始跳躍限制在 Windows 上為 128，在 *nix 上為 64。使用預設的 UDP 探測時，目的端會回傳 ICMP Port Unreachable（Destination Unreachable）；中繼跳點則回傳 ICMP Time Exceeded。ICMP 變體（例如 Windows 的 tracert）則是從目的端得到 ICMP Echo Reply。

#### Traceroute 如何運作？

Traceroute 透過封包傳送很小的存活時間（Time To Live，TTL）值。這個過程可防止封包陷入迴圈。路由器從給定封包的 TTL 減去數值後，當 TTL 抵達絕對零值時封包便立即失效。之後傳送方會收到來自 Traceroute 的逾時訊息。當使用很小的 TTL 值時，失效會很快發生，因此 traceroute 會產生用於識別路由器的 ICMP 訊息。

#### traceroute/tracert 在協定層級上究竟如何運作？

它其實是不斷地將封包傳送到最終目的地；唯一改變的是所使用的 TTL。額外的加分項在於：Windows 預設使用 ICMP，而 Linux 使用 UDP。

### Nmap

網路掃描工具

#### nmap -sS 的作用是什麼？

TCP SYN（隱匿式，Stealth）掃描 https://nmap.org/book/synscan.html

#### nmap -sT 的作用是什麼？

TCP connect 掃描 https://nmap.org/book/scan-methods-connect-scan.html

### 憑證

參考 DigiNotar。

### 憑證包含哪些資訊，它們是如何簽署的？

一份 X.509 憑證包含主體（CN 與 Subject Alternative Names）、主體的公鑰、簽發者、有效期間（not-before/not-after）、序號、金鑰用途／延伸金鑰用途（key-usage/extended-key-usage）限制，以及簽發 CA 的簽章。簽署方式：CA 對憑證的待簽署內容進行雜湊，並以 CA 的私鑰簽署該雜湊值。客戶端則透過對相同內容重新進行雜湊，並以 CA 的公鑰檢查簽章來驗證，一路沿著任何中繼憑證向上串連到其根憑證存放區中已受信任的根 CA。

#### 用於 HTTPS 的網站憑證如何運作？

CA（憑證授權單位，Certificate Authority）、CRL（憑證撤銷清單，Certificate Revocation List）、線上憑證狀態協定（Online Certificate Status Protocol，OCSP）。

#### 什麼是憑證固定（certificate pinning）？

客戶端將它預期從伺服器取得的確切憑證或公鑰（通常以雜湊形式）硬編碼（「固定」）下來，並拒絕任何其他憑證，即使是由受信任 CA 有效簽發的也一樣。這可防禦惡意或遭入侵的 CA 為該網域簽發偽造憑證，在行動應用程式中很常見。缺點在於營運層面：如果被固定的金鑰在未更新客戶端的情況下輪替，連線就會中斷——這也是為什麼透過 HTTP 標頭的固定機制（HPKP）已被棄用。

#### 什麼是憑證透明度（Certificate Transparency）？

可以根據公開的記錄（log）來驗證憑證。

### 單一登入（Single Sign-On）如何運作？

Bearer 權杖（token），這可能被竊取並被使用，就像 cookie 一樣。

![SSO](assets/images/SSO.png)

### NAT

有助於理解 IPv4 與 IPv6 的差異。

### 多工（Multiplex）

分時共享、統計式共享，知道它的存在就很有用。

### 攔截（MITM）

理解 PKI（公開金鑰基礎建設，public key infrastructure）與此的關聯。

### VPN

對 ISP 隱藏流量，但將流量暴露給 VPN 供應商。

### Tor

流量在網路上是明顯可見的。

組織犯罪調查人員如何在 tor 網路上找出人。

### 代理伺服器（Proxy）

為什麼 7 層代理救不了你。

### BGP

邊界閘道器協定（Border Gateway Protocol）。

它是撐起整個網際網路的基礎。

### 網路流量工具

Wireshark

Tcpdump

Burp suite

### UDP 標頭

來源連接埠

目的連接埠

長度

檢查碼（Checksum）

### 廣播網域（broadcast domain）與碰撞網域（collision domain）。

碰撞網域是一個網路區段，其中同時進行的傳輸可能會碰撞（如同在舊式的共享集線器上）；交換器（switch）會將每個連接埠放入各自的碰撞網域。廣播網域則是彼此接收對方廣播訊框的裝置集合；路由器（或獨立的 VLAN）界定了廣播網域的範圍。簡言之：交換器切分碰撞網域，路由器／VLAN 切分廣播網域。

### 根憑證存放區（Root stores）

隨作業系統或瀏覽器一同出貨的受信任根 CA 憑證集合。一份 TLS 憑證唯有在其憑證鏈終止於此存放區中的某個根憑證時，才會被信任。掌控根憑證存放區者即掌控信任決策，因此新增與移除（例如不再信任行為不當的 CA）都攸關安全。

### CAM 表溢位（CAM table overflow）

一種針對交換器的 CAM（MAC 位址）表的攻擊：攻擊者以使用大量偽造來源 MAC 位址的訊框淹沒交換器，直到有限的表被填滿。交換器接著會故障開放（fail open），像集線器一樣將後續訊框自每個連接埠氾流而出，讓攻擊者得以竊聽流量。緩解方式是連接埠安全（port security，限制每個連接埠所學習到的 MAC 數量）。
