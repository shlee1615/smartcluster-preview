# Preview 2：版本狀態與驗證範圍

[首頁](../README.zh-TW.md) · [English](RELEASE_NOTES.en.md)

更新：2026-10-26。**Preview 2 介紹網站已公開；0.14.0.dev5 Windows x64 程式仍是限邀請候選版，尚未公開發布新版執行檔。** 建置與實測結果必須對應同一版本、commit 與套件雜湊。

## 公開網站更新 · 2026-10-26

- [繁體中文網站](https://smartcluster.pages.dev/preview2/?lang=zh-TW) · [English](https://smartcluster.pages.dev/preview2/?lang=en)。
- 新增 120 秒英文原生 App 案例，提供中英文旁白及字幕、36 秒 Hub 截圖畫面與可放大的 Hub 圖庫；另外保留 60 秒概念動畫。
- 公開儲存庫僅提供介紹頁、文件與剪輯媒體。本次不發布新版程式執行檔、產品原始碼、憑證或對話紀錄；既有歷史 Release 附件保持原狀。

## dev5 本輪更新

- 新增三種目標的快速開始導覽：本機試用、加入群組、配置 Gemini／CTE；純指引，不修改連線或授權。
- 首頁任務傳遞動態可暫停，並遵循系統減少動態偏好；影片新增六章定位，選章不自動出聲。
- 中英文影片重製較輕快的分鏡、自然旁白與原創低音量配樂；旁白時自動降低音樂，字幕同步。
- 移除控制台側欄過期的 0.11 版號；實際版本以頂列 0.14.0.dev5 為準。核心 Agent 功能與部署能力範圍沿用 dev4。

## 本次重點

- 以同一個 Hub 管理已授權的 Codex、Claude、Gemini 與自有 Agent bridge，查詢、派工及讀取結果。
- Gemini 在支援的開發部署已有分析、持續對話、受限再分工、模型切換與桌面 App 自動收件驗收。
- CTE-Codex bridge 在支援的開發部署已有隔離寫檔、測試與回報驗收；成果供檢閱，不自動合併。
- 新增可離線開啟的雙語介紹頁與影片。互動流程與動畫為示意，實機證據另列。
- 沿用 Windows onedir 包裝、無視窗登入啟動、多群組與手動更新；不交付產品原始碼。

## 執行檔與執行節點的差異

| 能力 | 本次 Windows 執行檔 | 既有已配置的開發部署 |
|---|---|---|
| 群組、Hub 管理、MCP、診斷、支援的任務派工 | 包含；候選套件驗收另列 | 已有驗收紀錄 |
| Codex／Claude CLI | 另需安裝、登入與本機授權；不附 AI 客戶端 | 已有驗收紀錄；逐節點能力不同 |
| Gemini CLI 與 Gemini App MCP／sidecar 安裝 | 本次 frozen Node 不支援 | Primary 已驗收；需原生 App 開啟及專案授權 |
| 隔離工作樹寫檔／測試 | 本次 frozen Node 不執行 | 支援的 Node 可接收 Hub 派工，需當下驗收與本機授權 |
| CTE-Codex bridge | 不隨包附 CTE 主程式、帳戶或設定 | 已驗收固定 bridge；無再分工、Hub 模型覆寫及完整用量 |

Hub 可以向符合條件的執行節點派工，不代表 Hub 所在的執行檔 Node 自動獲得該能力。已配置節點的來源安裝不在本試用包內；設定由部署者管理。不同安裝形式可有不同能力，混合**版本**相容性仍須逐案驗證。

## 驗收紀錄

| 範圍 | 狀態與界線 |
|---|---|
| Preview 2 候選完整回歸 | 2026-10-26 完整重跑成功：Python 691 項（8 項略過）、JavaScript 74 項通過；紀錄 `outputs/preview2-refresh-full-tests.log` |
| Preview 2 套件完整性與無原始碼稽核 | 建置成功；115 個程式檔案、160 個受稽核封裝項目，路徑／連結／文字內容稽核通過。最終 commit 與 ZIP SHA-256 見隨包外層 `SHA256SUMS.txt` 及建置紀錄 |
| Preview 2 同機隔離多群組／mTLS smoke | 本次執行檔 9 項通過：暫停接單、雙群組隔離、瀏覽不切接單群、drain 切換、前一 Hub 保持在線、固定群組 MCP、英文邀請名稱、mTLS 加入／重試身分、成員診斷往返；不同於乾淨帳號或兩台實體機驗收 |
| Preview 2 GUI、無 Python 標準帳號及跨實體機 | 未完成；取得各項真實結果後另行更新 |
| Primary 開發部署（2026-10-26） | Gemini 模型 `gemini-4-argon-medium` 三輪新建／續接驗收；Gemini 桌面收件、寫檔、5 項 unittest 與回報；CTE bridge 隔離寫檔、unittest exit 0、Hub completed，原始專案不變 |
| SmartCluster 先前來源回歸 | HEAD `517ecf9` 對應紀錄：Python 677 項（8 項略過）、JavaScript 74 項通過；不是此候選的新回歸 |
| CTE 重新打包（2026-10-26） | `0.9.9l-bridge-20261026` 完整 `npm run check` 成功；舊兩項測試失敗已修正。設定、既有專案與對話保留；這是獨立 CTE 套件驗收 |
| 0.13.0.dev7 歷史執行檔 | 曾通過建置稽核與同機隔離 smoke；GUI／乾淨帳號當時未完成，不能轉列為 Preview 2 通過 |
| 2026-10-05 原始碼安裝叢集 | MSI 一鍵 dev5→dev6；兩台 Mac 手動升級；不等於執行檔更新能力 |

不同批次、子集與不同產品的測試數不可相加為一套回歸。服務在線、provider 已設定、App 自動收件及真實工作完成是不同狀態。

## 已知限制

- 未簽署；核對 ZIP 雜湊，不關閉 SmartScreen 或防毒。
- 執行檔更新與回復為手動。舊資料升級與退版需備份及對應版本驗收。
- 沒有 macOS 執行檔；既有 macOS 部署與 Windows 本包分別驗收。
- 不保證喚醒任意閒置 App。Gemini 自動通知只對已配置的原生 App／sidecar 成立；其他接收器依實際收件方式運作。
- Gemini App 的模型使用原生選擇器；Hub 的 CLI 模型設定不覆寫 App 模型。
- Windows 原生 Computer Use 的瀏覽器網址辨識仍有工具限制；Chrome 擴充 Browser Use 的通過不等於該路徑已修復。
- 完整 WAN 開發交付、長時間穩定性、其他 VPN、新版跨機部署仍需驗收。
- 沒有完整人員角色管理、群主移轉、正式離群／解散或自動遮敏匯出。

## 包裝與試用條款

內容為 `SmartCluster/`、`README.md`、`guide/`（含 `preview2/index.html` 與媒體）、`notices/`、`SHA256SUMS.txt`。不附產品 Python／TypeScript 原始碼、開發工具、邀請、憑證或私人資料庫。正常 HTML／CSS／JavaScript 與 Python 位元組碼可讀取或分析，不保證防逆向。

僅供邀請人指定的測試者評估，不得轉散佈。軟體依現狀提供，請勿用於生產資料或無備份環境。期限及其他條款由邀請人告知；第三方授權文字見 `notices/`。
