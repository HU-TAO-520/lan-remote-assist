# LAN Remote Assist

[English](#english) | [繁體中文](#traditional-chinese) | [简体中文](#simplified-chinese)

<a id="english"></a>
## English

LAN Remote Assist is a Windows remote-assistance MVP being designed for one-to-one, attended sessions on a local network. Its initial tasks are editing Microsoft Office documents and using Bing in a browser.

### Project status

The MVP requirements and development plan are documented. Application implementation, technical validation, and acceptance testing have not started. There is no runnable application or installer yet. Features and performance figures below are planned requirements, not verified capabilities.

### Planned MVP

| Area | Initial scope |
| --- | --- |
| Platform | Windows 10 22H2 x64 |
| Network | Reachable devices on the same IPv4 subnet; Ethernet, Wi-Fi, and mixed connections |
| Session | One controller and one assisted user; explicit local approval for every connection |
| Connection | LAN discovery and manual numeric IPv4 address entry |
| Authentication | Compare a fresh connection verification code on both devices before local acceptance |
| Display | Primary monitor; 1280×720 and 1920×1080; 100%, 125%, and 150% scaling |
| Input | Mouse, keyboard, editing shortcuts, and committed Chinese text from the controller's IME |
| Permissions | Logged-in administrator's UAC Yes/No prompts and elevated applications; local termination remains available |
| Technology | C# / WPF targeting .NET Framework 4.8 for the UI; Rust for the remote-control core |

The assisted user must enter the waiting state and approve each session. Screen transmission and remote input must remain disabled before acceptance. Either participant can end the session; a new session requires fresh verification and approval.

### Network requirement

The remote-assistance software and its dependencies must make **zero public-network connection attempts**. Discovery, authentication, screen data, and input must stay on the approved LAN; diagnostics stay local. Cloud signaling, relays, telemetry uploads, online updates, and runtime dependency downloads are excluded. Offline installation is required.

Independent browser, Office, and Windows traffic is managed separately. The Bing acceptance task intentionally uses the browser's own Internet connection. Development tools and this GitHub repository are outside the shipped application's runtime network boundary. Zero public-network egress still requires implementation and verification.

### Acceptance targets

- Actual 1920×1080 dynamic content displayed at an average of at least 30 FPS.
- Input-to-visible-remote-response latency: P95 at or below 150 ms on the registered test configurations.
- One continuous 60-minute session alternating Word editing, Bing search/results browsing, and idle periods.
- Twenty complete connection, verification, approval, task, and termination cycles.
- Display, permission, installation, failure-recovery, and network-egress tests defined in the development plan.

The second test computer's configuration is **to be confirmed**. These targets do not establish general minimum hardware requirements.

### Outside the first release

WAN access, NAT traversal, unattended access, login/lock-screen control, credential-entry prompts, multiple monitors, file transfer, shared clipboard, audio, recording, and cloud accounts are outside the initial scope. Copy and paste within the assisted computer is included.

### Development sequence

1. Validate UAC, local emergency termination, authentication design, and the capture pipeline.
2. Build the application structure, LAN connection, authorization, video, and input paths.
3. Integrate permissions and failure handling, then optimize measured two-device performance.
4. Complete offline packaging, network-egress auditing, acceptance tests, and a small controlled pilot.

See the [MVP requirements and development plan](<Version/Minimun Viable Product/plan/MVP需求文档与开发计划.md>) for stages M0–M8, requirements, and acceptance cases. The detailed plan is currently written in Simplified Chinese.

### License

Original project code and documentation are licensed under **GNU GPL version 3 only** (`GPL-3.0-only`). See [LICENSE](LICENSE). Third-party components retain their respective licenses; dependency and distribution obligations will be recorded when components are integrated.

<a id="traditional-chinese"></a>
## 繁體中文

LAN Remote Assist 是一個規劃中的 Windows 區域網路遠端協助 MVP，提供一對一、每次均經現場同意的協助。首輪使用任務為編輯 Microsoft Office 文件，以及透過瀏覽器使用 Bing。

### 專案狀態

MVP 需求與開發計畫已完成整理。應用程式實作、技術驗證及驗收測試尚未開始，目前沒有可執行的應用程式或安裝包。下列功能與效能數值均為規劃需求，仍待實作與實測。

### 首版規劃

| 項目 | 首輪範圍 |
| --- | --- |
| 平台 | Windows 10 22H2 x64 |
| 網路 | 同一 IPv4 子網且可互通；涵蓋有線、Wi-Fi 與混合連線 |
| 工作階段 | 一名協助方與一名被協助方；每次連線均須在被控電腦上明確同意 |
| 連線 | 區域網路自動探索，以及手動輸入數字 IPv4 位址 |
| 身分核對 | 雙方核對當次連線的新校驗碼，再由被協助方接受 |
| 顯示 | 主螢幕；1280×720、1920×1080；100%、125%、150% 縮放 |
| 輸入 | 滑鼠、鍵盤、編輯快捷鍵，以及協助方輸入法選字後確定的中文文字 |
| 權限 | 已登入管理員帳號的 UAC「是／否」提示及系統管理員應用程式；保留本機終止能力 |
| 技術 | C# / WPF 與 .NET Framework 4.8 介面；Rust 遠端控制核心 |

被協助方必須主動進入等待狀態，並逐次同意協助。接受前禁止傳送畫面或注入遠端輸入。任一方均可結束；再次連線須重新核對及授權。

### 網路要求

遠端協助軟體及其依賴必須達到**零公網連線嘗試**。裝置探索、身分驗證、畫面及輸入只在允許的區域網路內傳輸，診斷資料保留於本機。不使用雲端訊號服務、中繼、遙測上傳、線上更新或執行時下載依賴，並須支援完整離線安裝。

瀏覽器、Office 與 Windows 的獨立連網另行管理。Bing 驗收任務使用瀏覽器本身的網際網路連線。開發工具與此 GitHub 倉庫不屬於交付應用程式的執行時網路範圍。零公網外連要求仍待實作與驗證。

### 驗收目標

- 真實 1920×1080 動態內容的實際呈現平均至少 30 FPS。
- 登記測試組態中的操作至遠端畫面回應延遲 P95 不超過 150 毫秒。
- 連續執行 60 分鐘，交替進行 Word 編輯、Bing 搜尋及結果瀏覽、閒置等待。
- 完成 20 輪連線、核對、接受、操作與結束流程。
- 通過開發計畫中的顯示、權限、安裝、異常恢復及網路外連測試。

第二台測試電腦的資料維持**待查**。上述目標尚不能用來推定通用最低硬體需求。

### 首輪範圍以外

公網連線、NAT 穿透、無人值守、登入或鎖定畫面控制、輸入管理員憑證的提示、多螢幕、檔案傳輸、共用剪貼簿、音訊、錄影及雲端帳號均不納入首輪。被控電腦內部的複製貼上則在範圍內。

### 開發順序

1. 驗證 UAC、本機緊急終止、認證設計及畫面擷取管線。
2. 建立工程骨架、區域網路連線、授權、畫面及輸入功能。
3. 整合權限與異常處理，再依雙機實測結果優化效能。
4. 完成離線安裝、網路外連稽核、驗收測試及小範圍試用。

完整 M0–M8 階段、需求及驗收案例請見 [MVP 需求文件與開發計畫](<Version/Minimun Viable Product/plan/MVP需求文档与开发计划.md>)。詳細計畫目前以簡體中文撰寫。

### 授權條款

專案原創程式碼與文件採用 **GNU GPL 第 3 版，僅限此版本**（`GPL-3.0-only`），詳見 [LICENSE](LICENSE)。第三方元件保留各自的授權條款；整合時將登記依賴及分發義務。

<a id="simplified-chinese"></a>
## 简体中文

LAN Remote Assist 是一个规划中的 Windows 局域网远程协助 MVP，提供一对一、每次均经现场同意的协助。首轮使用任务为编辑 Microsoft Office 文档，以及通过浏览器使用 Bing。

### 项目状态

MVP 需求与开发计划已完成整理。应用实现、技术验证及验收测试尚未开始，目前没有可运行的应用或安装包。以下功能与性能数值均为规划需求，仍待实现与实测。

### 首版规划

| 项目 | 首轮范围 |
| --- | --- |
| 平台 | Windows 10 22H2 x64 |
| 网络 | 同一 IPv4 子网且可互通；覆盖有线、Wi-Fi 与混合连接 |
| 会话 | 一名协助方与一名被协助方；每次连接均须在被控电脑上明确同意 |
| 连接 | 局域网自动发现，以及手动输入数字 IPv4 地址 |
| 身份核对 | 双方核对当次连接的新校验码，再由被协助方接受 |
| 显示 | 主显示器；1280×720、1920×1080；100%、125%、150% 缩放 |
| 输入 | 鼠标、键盘、编辑快捷键，以及协助方输入法选字后确定的中文文字 |
| 权限 | 已登录管理员账号的 UAC“是／否”提示及管理员应用；保留本机终止能力 |
| 技术 | C# / WPF 与 .NET Framework 4.8 界面；Rust 远控核心 |

被协助方必须主动进入等待状态，并逐次同意协助。接受前禁止传输画面或注入远程输入。任一方均可结束；再次连接须重新核对及授权。

### 网络要求

远程协助软件及其依赖必须达到**零公网连接尝试**。设备发现、身份验证、画面及输入只在允许的局域网内传输，诊断数据保留在本机。不使用云端信令、中继、遥测上传、在线更新或运行时下载依赖，并须支持完整离线安装。

浏览器、Office 与 Windows 的独立联网另行管理。Bing 验收任务使用浏览器自身的互联网连接。开发工具与此 GitHub 仓库不属于交付应用的运行时网络范围。零公网外联要求仍待实现与验证。

### 验收目标

- 真实 1920×1080 动态内容的实际呈现平均至少 30 FPS。
- 登记测试配置中的操作至远端画面响应延迟 P95 不超过 150 毫秒。
- 连续运行 60 分钟，交替进行 Word 编辑、Bing 搜索及结果浏览、空闲等待。
- 完成 20 轮连接、核对、接受、操作与结束流程。
- 通过开发计划中的显示、权限、安装、异常恢复及网络外联测试。

第二台测试电脑的信息保持**待查**。上述目标尚不能用来推定通用最低硬件要求。

### 首轮范围以外

公网连接、NAT 穿透、无人值守、登录或锁屏控制、输入管理员凭据的提示、多显示器、文件传输、共享剪贴板、音频、录像及云端账号均不纳入首轮。被控电脑内部的复制粘贴则在范围内。

### 开发顺序

1. 验证 UAC、本机紧急终止、认证设计及画面采集管线。
2. 建立工程骨架、局域网连接、授权、画面及输入功能。
3. 整合权限与异常处理，再依据双机实测结果优化性能。
4. 完成离线安装、网络外联审计、验收测试及小范围试用。

完整 M0–M8 阶段、需求及验收用例请见 [MVP 需求文档与开发计划](<Version/Minimun Viable Product/plan/MVP需求文档与开发计划.md>)。详细计划目前以简体中文编写。

### 许可证

项目原创代码与文档采用 **GNU GPL 第 3 版，仅限此版本**（`GPL-3.0-only`），详见 [LICENSE](LICENSE)。第三方组件保留各自的许可证；集成时将登记依赖及分发义务。
