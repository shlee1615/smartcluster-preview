# SmartCluster · Preview 2

### 把分散的 AI，帶進同一個開發流程。

**繁體中文** · [English](README.md) · [開啟線上介紹網站](https://smartcluster.pages.dev/preview2/?lang=zh-TW)

**Preview 2 介紹網站已上線：**[繁體中文](https://smartcluster.pages.dev/preview2/?lang=zh-TW) · [English](https://smartcluster.pages.dev/preview2/?lang=en)。實際案例使用英文畫面，可選中文說明或英文旁白。

從 AI 對話指定已授權的電腦與執行者，讓工作經過派工、執行與回報，最後帶回可查驗的結果。SmartCluster 保存同一項工作的狀態，幫你分清楚「已提交」與「已完成」。

- **選擇適合工作的執行者。** 連接已配置的 Codex、Claude、Gemini，或透過 bridge 接入自有 Agent。
- **讓不同電腦一起工作。** Hub 管理任務，Node 依本機授權執行；加入群組不會共享 AI 帳號或開放整台電腦。
- **以結果完成交付。** 在支援的開發通道中核對檔案差異、測試退出碼與回報，保留原生 App 的核准流程。

## 先看介紹

[觀看 120 秒原生 App 實例](https://smartcluster.pages.dev/preview2/?lang=zh-TW#native-film) · [中文說明影片](preview2/media/smartcluster-native-demo.zh-TW.mp4) · [English video](preview2/media/smartcluster-native-demo.en.mp4) · [展示說明](docs/DEMO.zh-TW.md)

英文結帳案例呈現 Gemini 在 Antigravity 修正一處公式、通過五項測試，再由官方 Claude CLI 審查並回傳結果。影片結合原生 App 畫面、使用者提供的 Hub 截圖及明確標示的編輯摘要；不是連續錄製全程，也不是 Claude 桌面 App 錄影。兩種語言共用同一個英文案例，證據及範圍詳見[展示說明](docs/DEMO.zh-TW.md)。

另外保留 [60 秒概念動畫](https://smartcluster.pages.dev/preview2/?lang=zh-TW#film)，使用動態圖形解說，並非產品操作錄屏。頁面互動流程不會提交真實工作；較早的[跨機實錄](media/SmartCluster-MSI-demo-v3.zh-TW.mp4)另保留作歷史示範。離線觀看可開啟[本機介紹頁](preview2/index.html?lang=zh-TW)。

## 這個試用包提供什麼？

**Preview 2 候選版本為 0.14.0.dev5，Windows x64，限邀請評估；尚未公開發布。** 提供免另裝 Python 的 Hub／節點管理、群組、MCP、診斷及既有派工入口；AI 客戶端與 CLI 需另行安裝、登入及授權。

| 使用方式 | 範圍 |
|---|---|
| 使用本包管理與派工 | 管理群組、查節點、提交支援的任務與查結果；執行檔更新為手動 |
| 使用已配置的執行節點 | Gemini CLI／桌面自動收件及隔離開發需支援該功能、通過驗收且已授權的節點 |
| 在本包的 Node 直接隔離寫檔／測試 | 本版不支援；不因 Hub 可派工就宣稱本機 Node 可執行 |

Gemini 與 CTE-Codex 完整開發流程已在 Primary 的開發部署驗收，這不等於每台新安裝執行檔都具備相同能力。Gemini 的 App 模型與 CLI 模型分別設定；CTE bridge 尚不支援再分工、Hub 模型覆寫或完整用量回報。

## 開始試用

1. 由邀請人取得 ZIP 與 SHA-256，依[使用手冊](docs/USER_GUIDE.zh-TW.md)核對並解壓整包。
2. 建立測試群組，先完成不使用 AI 的連線診斷。
3. 接上本機 MCP，再對已配置的目標派工，核對最終狀態與任務 ID。

[版本與驗收狀態](docs/RELEASE_NOTES.zh-TW.md) · [常見問題](docs/FAQ.zh-TW.md) · [WAN 指引](docs/WAN.zh-TW.md) · [下一階段](docs/ROADMAP.zh-TW.md)

試用包不附產品 Python／TypeScript 原始碼、開發儲存庫或私人狀態。正常網頁資產與 Python 位元組碼仍可讀取或分析，封裝不保證防止逆向。此版未簽署；乾淨帳號與跨實體機新版驗收須依版本紀錄確認。
