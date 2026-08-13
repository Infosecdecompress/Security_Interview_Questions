# 密碼學

### 非對稱與對稱的比較

非對稱加密速度較慢，但適合用來建立受信任的連線。

對稱加密使用共享金鑰，速度較快。協定通常會使用非對稱加密來傳輸對稱金鑰。

前向保密（Perfect Forward Secrecy）—例如 Signal 就採用這種機制。

#### 加密標準與實作

對稱式

* DES
* RCx
* Blowfish
* Rijndael（[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)）
* [Chacha/Salsa](https://en.wikipedia.org/wiki/Salsa20#ChaCha_variant)

非對稱式

- [RSA（非對稱）](https://en.wikipedia.org/wiki/RSA_(cryptosystem))。
- [ECC（也就是 ed25519）（非對稱）](https://en.wikipedia.org/wiki/EdDSA)
- Diffie Hellman
- El Gamal
- DSA

### SSL 與 TLS

#### SSL、TLS 與 HTTPS 之間的差異

SSL：用來確保網際網路連線安全、並保護在兩個系統之間傳送的任何敏感資料的標準技術，可防止犯罪者讀取或修改任何被傳輸的資訊，包括可能的個人詳細資料。

TLS：一種在網際網路上提供安全通訊的密碼學協定。TLS 協定的主要目標是在兩個正在通訊的電腦應用程式之間提供隱私與資料完整性。

HTTPS：HTTP 的安全版本，也就是在你的瀏覽器與你所連線的網站之間傳送資料所使用的協定。TLS 與 SSL 是最廣為人知、用來為網頁瀏覽器與網頁伺服器之間的網際網路交易提供安全 HTTP（HTTPS）的協定。

HTTPS 在傳輸層使用 TCP。SSL 則用於資料加密。

#### TLS 使用對稱還是非對稱加密？

兩者皆有，最初的交換是使用非對稱加密完成的，而大量資料的加密需要速度，因此使用對稱演算法。

#### 什麼是 HTTP 嚴格傳輸安全（HSTS）？

HSTS 是一個標頭，讓網站能夠在用戶端網頁瀏覽器中指定並強制執行安全政策。這種政策強制執行可保護安全網站免於遭受降級攻擊、SSL stripping 以及 cookie 劫持。它讓網頁伺服器能夠宣告一項政策，要求瀏覽器只能使用安全的 HTTPS 連線來連線，並確保終端使用者無法「點擊略過」重要的安全警告。HSTS 對於高安全性網站而言是一項重要的安全機制。HSTS 標頭只有在透過 HTTPS 連線提供時才會被遵循，透過 HTTP 提供時則不會。

HSTS 在使用者網頁瀏覽器中通常有以下行為：

- 不安全的 HTTP 連結會變成安全的 HTTPS 連結
- SSL 憑證警告或其他錯誤會顯示錯誤訊息，且使用者無法略過

更多細節：[Cloudflare Understanding HSTS (HTTP Strict Transport Security)](https://support.cloudflare.com/hc/en-us/articles/204183088-Understanding-HSTS-HTTP-Strict-Transport-Security-)

#### 如果有人竊取了伺服器的私鑰，他們能夠解密先前傳送到該伺服器的所有內容嗎？

這取決於金鑰交換方式。若採用靜態 RSA 金鑰交換（沒有前向保密），答案是可以——任何錄下過去流量的人都能使用被竊取的私鑰來回復每一個工作階段金鑰並回溯性地解密。若採用臨時 Diffie-Hellman（DHE/ECDHE，也就是前向保密），答案是不行——工作階段金鑰是臨時的且從不傳輸，因此被竊取的長期金鑰無法解密先前擷取的工作階段（不過它確實能讓攻擊者在往後偽冒伺服器或進行主動式 MITM）。

#### TLS 常見的攻擊方式有哪些，以及／或它過去曾遭受過哪些攻擊方式？

弱加密演算法、像是 Heartbleed、BEAST 這類的弱點，

#### 什麼是前向保密（Forward Secrecy）？

一種使用臨時工作階段金鑰來實際加密 TLS 資料的系統，如此一來，即使伺服器的私鑰遭到入侵，攻擊者也無法用它來解密過去傳送到該伺服器、已被擷取的資料。

### 公開金鑰基礎架構（Public Key Infrastructure）

#### 就密碼學而言，在公開媒介上建立共享秘密的主要方法是什麼？

Diffie-Hellman

#### Diffie-Hellman 與 RSA 之間有什麼差異？

Diffie-Hellman 是一種金鑰交換協定，而 RSA 是一種加密／簽章協定。RSA 需要事先取得金鑰材料，Diffie-Hellman 則不需要。

#### 標準的 Diffie-Hellman 交換容易遭受哪一種攻擊？

MITM

### 編碼、加密、雜湊、混淆與簽章之間有什麼差異？

[各種攻擊模型（例如選擇明文攻擊）](https://en.wikipedia.org/wiki/Attack_model)。

### 加密中 IV 的用途是什麼？

初始化向量（Initialization Vector）是一個非機密但隨機／唯一的值，會被輸入到密碼演算法中，使得在相同金鑰下加密相同的明文每次都會產生不同的密文，藉此防止模式外洩。在 CBC 中，它會與第一個明文區塊進行 XOR 運算，且必須是不可預測的；在 CTR/GCM 中，它構成 nonce/計數器，且對於同一個金鑰絕不能重複使用（在 GCM 中重複使用 nonce 是災難性的，可能會外洩驗證金鑰）。IV 通常會與密文一起以明文形式傳送。

### 加密模式（Cipher Modes）

#### 什麼是區塊密碼與串流密碼？它們之間有什麼差異，你會在什麼情況下使用其中一種而不是另一種？

以區塊為基礎的加密演算法一次處理一個明文區塊，最適合用於你已知訊息大小的情境，例如檔案。串流密碼則處理單一單位的明文，例如一個位元或一個位元組，最適合用於你不確定訊息會有多長的情況。

- [區塊密碼與串流密碼的比較](https://en.wikipedia.org/wiki/Cipher)。
- [區塊密碼運作模式](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation)。
- [AES-GCM](https://en.wikipedia.org/wiki/Galois/Counter_Mode)。

#### 常見的區塊密碼模式有哪些？

ECB（Electronic Code Book）與 CBC（Cipher Block Chaining）。

#### ECB 與 CBC 在安全性上的主要差異是什麼？

ECB（Electronic Code Book）獨立加密每一個區塊，不使用 IV，因此相同的明文區塊永遠會產生相同的密文區塊。這會外洩資料中的模式（經典的「ECB 企鵝」圖片），並使其相當容易遭受攻擊。

CBC（Cipher Block Chaining）對第一個區塊使用 IV，然後將前一個區塊的 XOR 結果傳遞到後續區塊上。其結果的差異可能非常顯著。

### 完整性與真實性基元（Integrity and authenticity primitives）

- [雜湊函式，例如 MD5、Sha-1、BLAKE](https://en.wikipedia.org/wiki/Cryptographic_hash_function)。用於識別符，對於為惡意軟體樣本建立指紋非常有用。
- [訊息驗證碼（MACs）](https://en.wikipedia.org/wiki/Message_authentication_code)。
- [金鑰雜湊訊息驗證碼（HMAC）](https://en.wikipedia.org/wiki/HMAC)。

### 熵（Entropy）

- PRNG（虛擬亂數產生器）。
- 熵緩衝區耗盡。
- 填充熵緩衝區的方法。

### 進行個人身分驗證有哪些不同的方式

1. 密碼：使用者所知道的東西
2. 權杖（Token）：使用者所擁有的東西
3. 生物特徵：使用者本身是誰
4. OTP：一次性密碼

### 安全模組（Security Modules）

#### 什麼是 HSM 硬體安全模組（Hardware Security Module）？

一種你可以加入系統中的安全裝置，用來管理、產生並安全地儲存密碼金鑰。

#### 什麼是 TPM 信任平台模組（Trusted Platform Modules）？

一顆位於電腦主機板上的硬體晶片，用來儲存用於加密的密碼金鑰。許多筆記型電腦都內建 TPM，但如果系統未內建，事後要加裝並不可行。

在裝置／主機本機上為憑證與驗證資料提供受信任的儲存空間。

#### HSM 與 TPM 的比較

HSM 是可移除或外接的裝置。相較之下，TPM 是嵌入主機板的晶片。你可以輕鬆地將 HSM 加入系統或網路中，但如果系統出廠時未內建 TPM，事後要加裝並不可行。兩者都透過儲存與使用 RSA 金鑰來提供安全的加密能力。
