# SmartCluster 使用手冊

[首頁](../README.zh-TW.md) · [English](USER_GUIDE.en.md)

文件版本：2026-09-28；適用 0.11.0.dev3 開發預覽候選版。[支援與已知問題](RELEASE_NOTES.zh-TW.md)

## 先選擇你的目標

| 目標 | 需要什麼 | 完成標準 |
|---|---|---|
| 在一台 Windows 體驗 | 維護者提供的可信候選包；不需 AI 帳號 | 診斷任務 completed，結果相符 |
| 邀請另一台電腦 | 相容版本、可達的 Hub IPv4、短效邀請 | 成員加入後完成跨機診斷 |
| 從對話派工 | 支援本機 stdio MCP 的 AI 客戶端 | 看見工具實際呼叫及最終任務結果 |
| 使用遠端 AI | 目標電腦已安裝、登入及啟用所選 provider | 真實 AI 工作完成；不是 diagnostic.echo |
| 派工給指定 App 對話 | 已連接的接收器、來源與專案授權、收件活動 | App 實際收件並回報完成 |

**Hub** 主持群組並保存協作狀態；**Node** 是參與工作的節點；**profile** 是這台電腦保存的群組設定。`profile_id`、`cluster_id` 與 `node_id` 是不同識別碼。

## 1. 取得與啟動

公開下載尚未開放。若已取得維護者提供的候選包，先核對版本、來源及 SHA256SUMS，再將 SmartCluster.exe 解壓到固定資料夾。執行檔版不需自行安裝產品 Python 環境；乾淨機驗收仍待完成。

```powershell
Get-FileHash .\SmartCluster.exe -Algorithm SHA256
```

雙擊執行檔，瀏覽器開啟「我的群組」。啟動器視窗需保持開啟，關閉管理頁服務可在該視窗按 Ctrl+C。管理頁服務與各群組背景服務分開；關閉瀏覽器分頁不代表群組停止。若遇系統阻擋，核對來源並交由 IT／維護者確認，不要關閉防護。

## 2. 建立第一個群組

1. 在「建立群組」輸入英文名稱，例如 **Work Group**。
2. 只在本機體驗時，LAN／VPN IPv4 留空。要邀請其他電腦時，填入本機實際可達的 IPv4；預覽版沒有事後編輯閘道位址的圖形介面。需不同位址時保留原群，再建立合適的測試群。
3. 按「啟動服務」，再按「設為接單群」。接單標示不代表服務健康或 AI 可用。
4. 按「送出診斷示範」，開啟控制台查看 `SmartCluster connection demo`。
5. 確認狀態為 `completed`，結果為 `Hello from SmartCluster`。這是**不呼叫 AI 的連線診斷**。

網頁介面可切換繁體中文／English。建立其他群可使用 **Personal Group**；不同群組各有資料與埠設定。

## 3. 邀請及加入

群主先啟動已設定 LAN／VPN 位址的 Hub，在控制台的加入精靈建立指定電腦的短效邀請。私下交付 `invitation.json`，由成員核對群名、Hub URL 與 CA 指紋。實際埠以邀請 URL 為準，不照抄其他群的埠。

成員開啟「加入其他群組」，填寫**這台電腦的名稱**，例如 **Windows Test Node**，選取邀請檔並加入。啟動服務、設為接單群，再完成診斷。雙方需支援 0.11 intake 協定；macOS 獨立執行檔目前不在公開交付範圍。

加入不會自動授予專案、檔案、AI 帳號或 App 收件權限。每台電腦的使用者仍決定本機授權。加入中斷時先使用「接續未完成的加入」，避免重複建立身分。

dev3 邀請保留設定的英文群名，已使用重建 EXE 在建置機驗證；舊 dev2 仍可能顯示預設中文群名。詳見[版本紀錄](RELEASE_NOTES.zh-TW.md)。不要只靠名稱判斷信任，仍需核對群主與憑證指紋。

## 4. 管理多群組

| 操作 | 實際作用 |
|---|---|
| 查看 | 改變畫面選取，不改派工目的地或接單群 |
| 設為接單群 | 同一群組登錄目錄一次一群接新工作；切換需等原工作結束或核對 |
| 暫停接單 | 停止接受新工作；Hub 保持運行 |
| 停止服務 | 停止該群本機服務；若此機主持 Hub，其他成員會斷線 |

切換等候時，核對原工作；可以「繼續切換」或取消切換。不要刪日誌或盲目重送可能已執行的工作。此限制以同一 registry 為範圍，既有獨立安裝不會自動納入管理。

## 5. 連接 MCP

先完成基本診斷。在「查看」或 `groups --list` 找到本機 profile_id，在 AI 客戶端新增本機 stdio MCP server。以下為常見 JSON 格式示例，實際外層格式依客戶端而定；必須換成真實路徑及 profile_id。

```json
{
  "mcpServers": {
    "smartcluster-work": {
      "command": "C:\\Apps\\SmartCluster\\SmartCluster.exe",
      "args": ["--profiles-dir", "C:\\SmartClusterData", "--profile", "REPLACE_WITH_PROFILE_UUID", "mcp"]
    }
  }
}
```

`C:\SmartClusterData` 只是範例，必須與建立／加入時使用的資料根目錄一致。預設為使用者家目錄的 `.smartcluster-groups`。重新載入工具後，先要求 AI 使用 `cluster_service_status` 及 `cluster_list_nodes` 查驗連線。

MCP 固定綁定 profile，不會跟隨網頁「查看」或接單群切換。只支援遠端 HTTP MCP 的聊天服務，不能直接使用此本機 stdio 入口。將命令貼到對話中也不等於已設定 MCP。

## 6. 用對話完成工作

| 想做的事 | 可以這樣說 | 核對方式 |
|---|---|---|
| 查節點 | 請列出目前群組的節點與 AI provider 狀態。 | 檢查名稱、在線狀態及目標 ID |
| 連線診斷 | 向 Windows Test Node 送出不使用 AI 的診斷，追蹤到完成。 | diagnostic.echo 的 completed 與相符結果 |
| AI 分析 | 請讓 Demo Mac 上已啟用的 Claude CLI 審閱這段文字。 | agent.analyze、provider、最終結果與任務 ID |
| App 工作 | 列出已連接接收器，再把工作交給我指定的專案對話。 | App 實際收件；用 cluster_app_job 追蹤 |
| 本機啟動 | 檢查本機 SmartCluster 服務；未啟動時啟動既有服務。 | cluster_service_status／cluster_service_start |

`cluster_get_task` 追蹤一般任務；`cluster_cancel_task` 提出取消後仍需核對最後狀態。App 取消使用其對應工具，已發生的修改不會因此回滾。建立／切換群組目前仍使用 UI，MCP 並非任意控制作業系統的入口。

## 7. 資料與日常維護

群組狀態預設存在 `.smartcluster-groups`，不隨刪除 EXE 消失，也不自動匯入舊 `.state`。工作輸入、結果、事件與中繼資料會依功能傳給目標或保存在 Hub／Node；完整 App 對話歷史留在原電腦。使用 AI 分析會將提交內容交給所選節點與 AI 服務。

跨機使用 mTLS 驗證節點身分並加密通訊；這不等於磁碟資料加密或程式防逆向。不要公開邀請、登入連結、私鑰、權杖或整份資料目錄。

備份／換版前，先暫停接單、完成或核對既有工作，再停止相關服務，完整備份資料根目錄及 SQLite 相關檔案。保留舊 EXE 和一致備份；沒有自動更新／回復介面，不保證資料可直接降版使用。若主持 Hub，先安排成員停機時間。[排錯 FAQ](FAQ.zh-TW.md) · [WAN](WAN.zh-TW.md)
