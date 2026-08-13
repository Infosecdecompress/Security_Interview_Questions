# System Admin

### 作業系統

### Windows

- Windows 登錄檔（registry）與群組原則（group policy）。
- Windows SMB。
- Samba（搭配 SMB）。
- 緩衝區溢位（Buffer Overflow）。
- ROP。

### *nix

- SELinux。
- 核心（kernel）、使用者空間（userspace）、權限。
- MAC vs DAC。
- /proc
- /tmp - 程式碼可以儲存在這裡並被執行。
- /shadow
- LDAP - Lightweight Directory Access Protocol。讓使用者可以用一組密碼存取多項服務。這與 Windows 中的 Active Directory 類似。

### MacOS

- Gotofail 錯誤（SSL）。
- MacSweeper。
- 研究 Mac 的弱點。

#### Linux 相較於 Windows 的優勢與劣勢為何？

**Linux 的優勢：** 開放原始碼且可稽核、具備細緻的權限控制搭配強大的 CLI／自動化能力、輕量、在伺服器領域佔主導地位、修補速度快，且作為桌面惡意程式的攻擊目標較小。**劣勢：** 各發行版（distro）之間的碎片化、學習曲線較陡、商業桌面／應用程式支援較少，以及假設使用者具備更多專業知識的設定方式。

**Windows 的優勢：** 在桌面領域無所不在、強大的企業管理能力（Active Directory、Group Policy）、廣泛的軟體／驅動程式與廠商支援，以及熟悉的圖形化介面（GUI）。**劣勢：** 較大的攻擊面與惡意程式目標、封閉原始碼、授權成本，以及歷來較多與權限／登錄檔相關的暴險。

### 你如何在 Linux/Windows 中變更 DNS 設定？

Windows：網際網路介面卡／

Linux：sudo nano /etc/resolv.conf  加入 nameserver x.x.x.x

### Cyber Crime vs Cyber-enabled crime

Cyber-enabled crime（電腦輔助犯罪）：因使用電腦技術而被放大的傳統犯罪

Cyber Crime（網路犯罪）：涉及網路或電腦、並利用其來犯案的非法行為

### 資訊安全在組織或公司內的主要目標是什麼？

保護 CIA（Confidentiality 機密性、Integrity 完整性、Availability 可用性）

### 網路攻擊會造成哪些後果？

財務損失（詐騙、停機、修復、贖金）、客戶資料／智慧財產（IP）／個人身分資訊（PII）遭外洩、營運中斷、名譽受損與失去客戶信任、法律與法規罰則（例如 GDPR/HIPAA 罰款），以及——在關鍵基礎設施或安全相關系統中——可能造成的實體傷害。

### 基礎設施（Prod / Cloud）虛擬化

- Hypervisor（虛擬機器監視器）。
- Hyperjacking。
- 容器（Container）。
- 逃逸（escaping）與權限提升（privilege escalation）技術。
- 站台隔離（site isolation）。
- 來自 VM／容器的網路連線。
- 側通道攻擊（Side-channel attack）。
- Google 的 Beyondcorp
  - 信任主機，但不信任網路。

### 強化 Linux 伺服器的第一步

稽核（Auditing）：使用名為 Lynis 的工具進行系統掃描以做稽核。每個類別都會被個別掃描，並將強化指數（hardening index）提供給稽核人員以進行後續步驟。

強化（Hardening）：稽核完成後，依系統進一步所需的安全等級進行強化。這是一個依稽核人員決策而定的重要流程。

合規（Compliance）：從安全的角度來看，系統幾乎每天都需要檢查，以獲得更好的結果並減少威脅。

### 如何強化 Web 伺服器的安全

- 防毒軟體與防火牆
- 安全地安裝與設定 Web 伺服器軟體
- 安全地安裝與設定作業系統（O.S）
- 掃描系統弱點
- 停用遠端管理
- 移除未使用與預設的帳號
- 將預設連接埠與設定變更為自訂的連接埠與設定
- 更新／修補 Web 伺服器軟體
- 更新檔案的權限／擁有權
- 刪除預設的資料／指令碼
- 移除或保護隱藏的檔案與目錄
- Web 應用程式與 Web 伺服器安全
- 停用額外模組以最小化伺服器功能
- 提高記錄（logging）的詳細程度
- 設定為顯示通用的錯誤訊息
- 確保程式碼中有落實輸入驗證（Input Validation）：安全 QA 測試
- 實施軟體安全政策

### 權限提升（privilege escalation）技術與防範。

**技術：** 利用核心／服務的弱點、濫用錯誤設定（可寫入的 SUID 執行檔、寬鬆的 `sudo` 規則、全域可寫入的檔案／服務、Windows 上未加引號的服務路徑）、竊取並重複使用憑證（credential）或權杖（token），以及 DLL 劫持（DLL hijacking）。**防範：** 最小權限、及時修補、移除不必要的 SUID／管理員權限、強化服務與檔案權限、應用程式白名單，以及監控異常的權限使用。

### 遠端程式碼執行（Remote Code Execution）／取得 shell。

RCE 是指在目標上執行攻擊者提供的程式碼的能力，通常是衝擊最高的結果。攻擊者常將其轉化為互動式 shell：*bind shell* 會在受害者上開啟一個監聽的連接埠供攻擊者連入，而 *reverse shell* 則讓受害者主動連回攻擊者的監聽端（較受青睞，因為對外連線更常能繞過防火牆／NAT）。

### 本機資料庫

- 有些通訊軟體使用 sqlite 來儲存訊息。
- 對數位鑑識（digital forensics）很有用，尤其是在手機上。

### IaaS？

IaaS，即 Infrastructure as a Service（基礎設施即服務），是雲端服務之一，供應商提供伺服器、儲存與網路，客戶則負責作業系統（OS）及其以上的所有部分

#### 你對 AWS IaaS 了解多少？

我確實有設定並管理 AWS ECS 的經驗，因此我知道如何設定它們以及它們如何運作。

#### 你如何從 AWS IaaS 取得記錄（log）？

AWS 有一項名為 CloudWatch 的服務，可處理來自不同 AWS EC2 及其他服務的記錄與資訊，你可以在其中檢視與管理這些記錄。

如果你想查看單一執行個體的記錄與主控台輸出，可以在 Amazon EC2 主控台中找到

#### 你可以從 AWS IaaS 記錄中取得哪些記錄？

你將能夠取得系統記錄、主控台輸出

#### IaaS vs PaaS vs SaaS 是什麼？

在 IaaS 中，供應商處理網路、虛擬機器、儲存。客戶擁有最大的彈性，但必須管理許多事情

在 PaaS 中，供應商處理 IaaS 所處理的部分，同時也包含作業系統、執行環境（runtime）與部分軟體維護。

在 SaaS 中，供應商處理一切，客戶可以直接使用產品，無須處理或維護任何東西。
