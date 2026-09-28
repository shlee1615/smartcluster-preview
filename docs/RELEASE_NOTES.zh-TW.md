# 版本狀態與驗證範圍

[首頁](../README.zh-TW.md) · [English](RELEASE_NOTES.en.md)

更新：2026-09-28。**0.11.0.dev3 是開發預覽候選版，已提供公開實驗試用。** 本文件描述已知狀態，不是上線公告。

## dev3 新增驗證

Windows 候選版已重建，實際 EXE 邀請保留 `Work Group` 英文群名。同機隔離程序的九個 smoke 情境通過，涵蓋固定 profile MCP、TLS 加入／重試、診斷、群組隔離、接單切換及英文名稱；Hub 回報版本為 dev3。這不等於獨立乾淨機驗收或混合版本互通驗證。已收集第三方授權文字與實際封裝清單，完整相依審查及產品條款仍待完成。隨附影片為較早的開發環境錄影。

## 已提供的能力

Windows x64 單一 EXE、多群建立／加入／查看／啟停、同一 registry 排空式切換接單群、明確綁定 profile 的 stdio MCP、內建診斷，以及既有協作任務與 App 接收器功能。跨機通訊使用已實作的 mTLS。

## 已完成的驗證

| 範圍 | 證據與界線 |
|---|---|
| dev3 原始碼回歸 | 本輪 Python 248 項、JavaScript 33 項通過；不是乾淨機執行檔驗收 |
| dev3 Windows 執行檔 | 同機九個程序情境通過，包含英文邀請群名；ZIP 解壓後移除專案 Python 環境變數仍可啟動 |
| 同 Windows 隔離程序 | dev2 群組／發佈檢查 20 項；EXE 多程序 smoke 通過 |
| Mac mini M4 + Windows LAN | 新 Mac 測試 Hub、Windows dev2 EXE 加入；mTLS、診斷往返、去重、停止及重啟佇列恢復通過 |
| Mac 測試執行方式 | 私有原始碼測試部署，接收器回報 17 項 profile 測試通過；不是 macOS 執行檔驗收 |
| 既有 WAN 試點 | 舊版 Tailscale 限定試點；不當作 dev2 WAN 驗收 |

不同批次與子集的測試數不能相加當作全套新回歸。此處不提供含私人狀態的內部測試檔。

## 已知問題

- 歷史 dev2 問題：邀請可能帶固定中文群名。dev3 已納入並驗證修正，舊 dev2 檔案不變。先前 Mac／Windows LAN 證據仍屬 dev2，不是 dev3 新跨機測試。
- 尚未簽署或完成乾淨機驗收；未交付 macOS 獨立執行檔。
- 尚未完成新版跨機 WAN、長時間穩定性與完整更新／回復驗收。
- 沒有群主移轉、人員層群組角色、完整正式離群／解散、全機跨 registry 接單協調、自動更新或遮敏匯出介面。
- 閒置 App 自動喚醒不保證可用。服務就緒、provider 設定、App 收件必須分別確認。

## 公開試用下載

[Windows x64 ZIP 與校驗碼](https://github.com/shlee1615/smartcluster-preview/releases/tag/v0.11.0.dev3)。完整解壓後執行 SmartCluster.exe。擁有者已決定在揭露限制的前提下公開試用。此版尚未簽署，也未通過獨立乾淨機驗收，不是正式生產版本；相依套件聲明為初步收集，完整審查與商業條款仍未完成。

EXE 內含 29 個可讀網頁資產及產品 Python 位元組碼，封裝不防止抽取或逆向。不另附 Python 原始檔、邀請、私鑰或私人狀態。GitHub 自動產生的 source archives 僅含此文件／媒體庫，不是私有產品專案。
