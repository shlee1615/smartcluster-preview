# SmartCluster 使用手冊

[首頁](../README.zh-TW.md) · [English](USER_GUIDE.en.md)

文件版本：2026-10-26；適用 0.14.0.dev5 Windows x64 限邀請試用版。[支援與已知問題](RELEASE_NOTES.zh-TW.md)


## Preview 2 能力範圍

此包為管理／派工端與支援的本機節點功能，不附 AI 客戶端或模型訂閱。Gemini CLI、Gemini App MCP／sidecar 安裝與隔離開發目前需要已配置的開發部署；本次 frozen Node 不執行隔離寫檔／測試。Hub 可向已支援、驗收且授權的執行節點派工，不能把遠端節點的能力當成本包本機能力。CTE-Codex 主程式與設定另行部署，未包含在此 ZIP。

本版是限邀請候選；先核對[驗收狀態](RELEASE_NOTES.zh-TW.md)，不以舊版 smoke 替代乾淨帳號或新版跨機驗收。離線介紹可開啟 `guide/preview2/index.html`；其中互動流程不會提交真實工作。

## 先選擇你的目標

| 目標 | 需要什麼 | 完成標準 |
|---|---|---|
| 在一台 Windows 體驗 | 邀請人提供的試用 ZIP 與 SHA-256；不需 AI 帳號 | 診斷任務 completed，結果相符 |
| 邀請另一台電腦 | 相同版本、可達的 Hub IPv4、短效邀請 | 成員加入後完成跨機診斷 |
| 從對話派工 | 支援本機 stdio MCP 的 AI 客戶端（Codex App／CLI、Claude Desktop／Code） | 看見工具實際呼叫及最終任務結果 |
| 使用遠端 AI | 目標電腦已安裝、登入及啟用所選 provider | 真實 AI 工作完成；不是 diagnostic.echo |
| 派工給指定 App 對話 | 已連接的接收器、來源與專案授權、收件活動 | App 實際收件並回報完成 |

**Hub** 主持群組並保存協作狀態；**Node** 是參與工作的節點；**profile** 是這台電腦保存的群組設定。`profile_id`、`cluster_id` 與 `node_id` 是不同識別碼。

## 1. 取得、核對與安裝

1. 由邀請人取得 `SmartCluster-0.14.0.dev5-windows-x64-preview.zip` 與它的 SHA-256。
2. 核對：

   ```powershell
   Get-FileHash .\SmartCluster-0.14.0.dev5-windows-x64-preview.zip -Algorithm SHA256
   ```

   不相符就不要解壓，向邀請人確認。
3. 解壓**整個 ZIP** 到固定資料夾，例如 `C:\Apps\SmartCluster-0.14.0.dev5`。解壓後應有 `SmartCluster\SmartCluster.exe`、`SmartCluster\SmartCluster-background.exe`、`SmartCluster\_internal\`、`README.md`、`guide\`、`notices\`、`SHA256SUMS.txt`。`SHA256SUMS.txt` 列出包內每個檔案的雜湊，可用它核對解壓是否完整。
4. **不要**把 `SmartCluster.exe` 單獨複製到別處：它需要同一層的 `_internal`。之後若要搬動，請搬整個 `SmartCluster` 資料夾，並重新設定自動啟動與 MCP（見第 8、9 節）。

此版**未簽署**。第一次執行 Windows 可能顯示 SmartScreen 提示；請只在雜湊核對相符後才繼續。公司管理的裝置請交由 IT 決定；不要關閉防毒或 SmartScreen。詳見[常見問題](FAQ.zh-TW.md)。

## 2. 啟動

雙擊 `SmartCluster\SmartCluster.exe`，會出現一個主控台視窗，瀏覽器開啟「我的群組」。**這個視窗要保持開啟**；它是群組管理頁的服務，關閉管理頁服務在該視窗按 Ctrl+C。各群組的背景服務與它分開：關閉瀏覽器分頁或管理頁，不會停止已啟動的群組。

`SmartCluster-background.exe` 是同一個程式的無視窗版本，只供「登入後自動啟動」使用；雙擊它不會有任何動作。

網頁介面可切換繁體中文／English。

## 3. 建立第一個群組

1. 在「建立群組」輸入英文名稱，例如 **Work Group**。
2. 只在本機體驗時，LAN／VPN IPv4 留空。要邀請其他電腦時，填入本機實際可達的 IPv4；目前沒有事後編輯閘道位址的圖形介面，需不同位址時保留原群，再建立合適的群組。
3. 按「啟動服務」，再按「設為接單群」。接單標示不代表服務健康或 AI 可用。
4. 按「送出診斷示範」，開啟主控台查看 `SmartCluster connection demo`。
5. 確認狀態為 `completed`，結果為 `Hello from SmartCluster`。這是**不呼叫 AI 的連線診斷**。

不同群組各有資料與埠設定；建立其他群可用 **Personal Group**。

## 4. 邀請及加入

群主先啟動已設定 LAN／VPN 位址的 Hub，在主控台的加入精靈建立指定電腦的短效邀請，產生的壓縮檔內含 `invitation.json` 與 `READ-ME.txt`。私下交付給成員，由成員核對群名、Hub URL 與 CA 指紋。實際埠以邀請 URL 為準。

成員開啟「加入其他群組」，填寫**這台電腦的名稱**，例如 **Windows Test Node**，選取 `invitation.json` 並加入。啟動服務、設為接單群，再完成診斷。雙方應使用**相同版本**；macOS 電腦無法用此執行檔版加入（macOS 目前以原始碼方式部署，請向邀請人索取步驟）。

加入不會自動授予專案、檔案、AI 帳號或 App 收件權限。每台電腦的使用者仍決定本機授權。加入中斷時先使用「接續未完成的加入」，避免重複建立身分。不要只靠名稱判斷信任，仍需核對群主與憑證指紋。

## 5. 管理多群組

| 操作 | 實際作用 |
|---|---|
| 查看 | 改變畫面選取，不改派工目的地或接單群 |
| 設為接單群 | 同一群組登錄目錄一次一群接新工作；切換需等原工作結束或核對 |
| 暫停接單 | 停止接受新工作；Hub 保持運行 |
| 停止服務 | 停止該群本機服務；若此機主持 Hub，其他成員會斷線 |

切換等候時，核對原工作；可以「繼續切換」或取消切換。不要刪日誌或盲目重送可能已執行的工作。此限制以同一 registry 為範圍，既有獨立安裝不會自動納入管理。

## 6. 連接 MCP

先完成基本診斷。在「查看」或 `SmartCluster.exe groups --list` 找到本機 `profile_id`。MCP 指令永遠是 **EXE 的完整路徑**，參數依序為 `--profiles-dir`、資料根目錄、`--profile`、profile_id、`mcp`。預設資料根目錄是 `%USERPROFILE%\.smartcluster-groups`；下面以 `C:\Users\you\.smartcluster-groups` 為例，請換成真實路徑與 ID。

**Codex（App 或 CLI）**：在專案的 `.codex\config.toml`（或 `%USERPROFILE%\.codex\config.toml`）加入：

```toml
[mcp_servers.smartcluster]
command = "C:\\Apps\\SmartCluster-0.14.0.dev5\\SmartCluster\\SmartCluster.exe"
args = ["--profiles-dir", "C:\\Users\\you\\.smartcluster-groups", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
```

加入精靈在「加入其他群組」完成時，可代你寫入該專案的 Codex 設定。

**Claude Desktop**：在 `%APPDATA%\Claude\claude_desktop_config.json` 的 `mcpServers` 加入：

```json
{
  "mcpServers": {
    "smartcluster-work": {
      "command": "C:\\Apps\\SmartCluster-0.14.0.dev5\\SmartCluster\\SmartCluster.exe",
      "args": ["--profiles-dir", "C:\\Users\\you\\.smartcluster-groups", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
    }
  }
}
```

改完設定要**完全結束並重新開啟** App（只開新對話不會載入新工具）。重新載入後，先要求 AI 使用 `cluster_service_status` 及 `cluster_list_nodes` 查驗連線。

MCP 固定綁定 profile，不會跟隨網頁「查看」或接單群切換。只支援遠端 HTTP MCP 的聊天服務不能直接使用此本機 stdio 入口。把命令貼到對話中不等於已設定 MCP。

## 7. 用對話完成工作

| 想做的事 | 可以這樣說 | 核對方式 |
|---|---|---|
| 查節點 | 請列出目前群組的節點與 AI provider 狀態。 | 檢查名稱、在線狀態及目標 ID |
| 連線診斷 | 向 Windows Test Node 送出不使用 AI 的診斷，追蹤到完成。 | diagnostic.echo 的 completed 與相符結果 |
| AI 分析 | 請讓 Demo Mac 上已啟用的 Codex CLI 審閱這段文字。 | agent.analyze、provider、最終結果與任務 ID |
| App 工作 | 列出已連接接收器，再把工作交給我指定的專案對話。 | App 實際收件；用 cluster_app_job 追蹤 |
| 本機啟動 | 檢查本機 SmartCluster 服務；未啟動時啟動既有服務。 | cluster_service_status／cluster_service_start |

`cluster_get_task` 追蹤一般任務；`cluster_cancel_task` 提出取消後仍需核對最後狀態。App 取消使用其對應工具，已發生的修改不會因此回滾。建立／切換群組目前仍使用 UI，MCP 並非任意控制作業系統的入口。

## 8. 登入後自動啟動

在群組的設定頁開啟「登入後自動啟動」，或執行：

```powershell
C:\Apps\SmartCluster-0.14.0.dev5\SmartCluster\SmartCluster.exe --profiles-dir "C:\Users\you\.smartcluster-groups" --profile REPLACE_WITH_PROFILE_UUID service autostart enable
```

它會在目前使用者的登入啟動項寫入 `SmartCluster-background.exe` 的**絕對路徑**，登入後在背景啟動該群組，不會出現視窗。搬動或換版程式資料夾後，要在新位置重新開啟一次。改成 `disable` 即可關閉。

## 9. 手動更新（此版沒有自動更新）

Hub 的「設定 › 版本與更新」會把執行檔安裝的節點顯示為「執行檔安裝：手動更新」，不會推送給它。更新步驟：

1. 在主控台把這台的群組「暫停接單」，等進行中的工作結束。
2. 結束會用到 SmartCluster MCP 的 AI App，停止這台所有群組的服務，關閉 `SmartCluster.exe` 的視窗。
3. 備份 `%USERPROFILE%\.smartcluster-groups`（整個資料夾，含 SQLite 檔）。
4. 把新版 ZIP 核對雜湊後解壓到**新的**資料夾，例如 `C:\Apps\SmartCluster-0.14.0.dev5`。
5. 若希望 MCP 設定與自動啟動不用改路徑：把舊的程式資料夾改名（例如加 `-old`），再把新版資料夾改成原本的名稱。否則請更新 MCP 設定中的路徑，並重新開啟自動啟動。
6. 從新版啟動，確認「我的群組」顯示的版本、群組與節點身分都還在，再恢復接單。
7. 確認正常後再刪除舊程式資料夾。退回舊版：停止服務，把資料夾改名回去，再啟動；**新版可能已更新資料庫格式，退回前請先還原第 3 步的備份**。

Hub 與成員請使用相同版本；混合版本未經驗證。

## 10. 移除

1. 暫停接單並等工作結束；停止這台所有群組的服務；關閉 `SmartCluster.exe` 視窗。
2. 關閉自動啟動（`service autostart disable`，或在設定頁關閉）。
3. 從 AI App 的 MCP 設定移除 SmartCluster 項目。
4. 若這台是成員，請群主在 Hub 主控台撤銷這個節點。
5. 刪除程式資料夾。群組資料 `%USERPROFILE%\.smartcluster-groups` 會保留；確定不再需要時再手動刪除。

## 11. 資料與日常維護

群組狀態預設存在 `.smartcluster-groups`，不隨刪除 EXE 消失，也不自動匯入舊 `.state` 或其他安裝的資料。工作輸入、結果、事件與中繼資料會依功能傳給目標或保存在 Hub／Node；完整 App 對話歷史留在原電腦。使用 AI 分析會將提交內容交給所選節點與 AI 服務。

跨機使用 mTLS 驗證節點身分並加密通訊；這不等於磁碟資料加密或程式防逆向。不要公開邀請、登入連結、私鑰、權杖或整份資料目錄。[排錯 FAQ](FAQ.zh-TW.md) · [WAN](WAN.zh-TW.md)
