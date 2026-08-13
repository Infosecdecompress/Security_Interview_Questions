# 基礎加密與驗證

### 什麼是三向交握（three-way handshake）？

這是 TCP 連線建立的交換過程：用戶端送出 `SYN`，伺服器回覆 `SYN-ACK`，用戶端再回應 `ACK`。這個過程會同步序號，並在任何資料傳輸之前確認雙方都能收送資料。

![3wayhandshake](assets/images/3wayhandshake.png)

### Cookie 如何運作？

由瀏覽器儲存並在每次請求時送給伺服器的資料。屬於用戶端。

### Session 如何運作？

儲存在伺服器上、並與特定使用者關聯的一組資料（通常透過一個含有 id 代碼的 cookie 來關聯）。

### 什麼是 SSL 交握（handshake）？

這是建立 TLS session 的協商過程：用戶端與伺服器就協定版本與加密套件（cipher suite）達成共識，伺服器出示其憑證（證明身分），雙方建立共用的對稱式 session 金鑰（透過 RSA 金鑰傳輸，或更理想的是使用暫時性的 Diffie-Hellman 以達成前向保密），接著切換到快速的對稱式加密來傳輸實際資料。

![SSLhandshake](assets/images/SSLhandshake.jpg)

### HMAC 如何運作？

HMAC（Hash-based Message Authentication Code）利用共用的秘密金鑰 K 與雜湊函式 H，同時證明訊息的完整性與真實性。其定義為 `HMAC(K, m) = H((K XOR opad) || H((K XOR ipad) || m))`，其中 K 會被填補（pad）至雜湊的區塊大小，而 `ipad`/`opad` 分別是重複的常數 `0x36` 與 `0x5c`。傳送方與接收方共用 K；接收方會針對收到的訊息重新計算 HMAC，並以固定時間（constant time）方式與送來的標籤（tag）比對。

### 為什麼 HMAC 要這樣設計？

這種巢狀的兩階段（two-pass）結構（先用內層金鑰雜湊，再用外層金鑰對結果雜湊）能抵禦長度延展攻擊（length-extension attack），這類攻擊會影響 Merkle-Damgard 型的雜湊，例如 MD5、SHA-1 與 SHA-256。單純的 `H(key || message)` 這種 MAC 是可偽造的，因為攻擊者不需知道金鑰就能延展訊息；把內層摘要包在外層帶金鑰的雜湊裡即可防止此問題。此外，只要底層的壓縮函式（compression function）表現得像一個 PRF，HMAC 作為 MAC/PRF 就具有可證明的安全性，這也是為什麼即使搭配抗碰撞性已被攻破的雜湊（如 SHA-1），HMAC 仍能保持安全。

### Diffie-Hellman 與 RSA 有什麼差別？

RSA 是一種用於簽章或加密的協定，差別在於你事先就握有所有的金鑰材料。

Diffie-Hellman 是一種用於交換金鑰的協定。

### Kerberos 如何運作？

這是一種以票證（ticket）為基礎的驗證協定，圍繞著一個受信任的金鑰發放中心（Key Distribution Center，KDC）建構。用戶端先向驗證伺服器（Authentication Server）驗證一次，取得一張票證授權票證（Ticket-Granting Ticket，TGT）；要存取某個服務時，它會把 TGT 出示給票證授權伺服器（Ticket-Granting Server），取得一張服務票證（service ticket），再交給目標服務。密碼永遠不會在網路上傳送，而且票證會加上時間戳記以限制重放（replay）攻擊，這也是為什麼 Kerberos 對主機之間的時鐘偏差（clock skew）很敏感。

![Kerberos](assets/images/kerberos.png)

### 如果你要壓縮並加密一個檔案，會先做哪一個？為什麼？

先壓縮資料。

這是因為對資料加密後，我們會得到一串隨機的位元流。這些隨機位元變得無法壓縮，換句話說，它們是不可壓縮的。

這些隨機位元之所以不可壓縮，是因為缺乏任何具規律的結構。

壓縮資料一定需要某種特定的規律才能進行，而隨機位元正好缺乏這種規律。

### 驗證相關

#### 驗證系統

SAML 2.0。

OpenID。

#### 生物辨識（biometrics）

不像密碼可以更換（rotate）。

#### 密碼管理

輪換密碼（以及為什麼這樣做並不好）。

各種不同的密碼保管工具（password locker）。

#### U2F / FIDO

例如 Yubikey。

有助於防止憑證被成功釣魚（phishing）。

#### 比較與對照多因素驗證（MFA）方法

MFA 結合來自不同類別的因素，包括你所知道的（something you know，如密碼/PIN）、你所擁有的（something you have，如手機、硬體權杖），或你本身的特徵（something you are，如生物辨識）。
- **SMS/email OTP：** 容易使用，但可被釣魚，且容易遭受 SIM 卡側錄（SIM-swapping）與攔截。
- **TOTP 應用程式（Google Authenticator/Authy）：** 可離線產生驗證碼，比 SMS 好，但若使用者把驗證碼輸入到偽造網站上，仍然會被釣魚。
- **推播核准（Push approval）：** 方便，但容易遭受「MFA 疲勞」式的連續轟炸（prompt-bombing）。
- **硬體安全金鑰（U2F/FIDO2，例如 YubiKey）：** 最強——採用與來源網域綁定（origin-bound）的公鑰驗證，能抵抗釣魚，因為金鑰不會為外觀相似的假網域進行簽章。
- **生物辨識：** 方便且難以猜測，但一旦外洩就無法更換，因此最適合用作本機解鎖，而非共用的秘密。
