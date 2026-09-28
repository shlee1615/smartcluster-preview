# 跨網路連線指引

[首頁](../README.zh-TW.md) · [English](WAN.en.md) · [使用手冊](USER_GUIDE.zh-TW.md)

第一預覽版提供 Tailscale 設定指引，沒有代管 VPN。新版 LAN 跨機測試已通過；舊版有 Tailscale 限定試點，但新版 WAN 及長時間運作尚待驗收。

## 帳號與責任

客戶或其 IT 管理自己的 Tailscale 帳號、tailnet、裝置與存取規則。不同客戶不共用供應商個人網路或登入資訊。按實際用途核對現行[官方方案](https://tailscale.com/pricing)及適用條款，不要假設免費個人方案涵蓋客戶部署。本文件不提供產品或第三方商業授權。

企業 VPN、WireGuard 或 NetBird 可能提供需要的路由，但尚未驗證，不承諾本版支援。VPN 提供可達性，SmartCluster 的配對、mTLS 及本機授權仍需完成。

## 設定順序

1. 依 IT 規則安裝[官方 Tailscale](https://tailscale.com/download)，加入客戶核准的 tailnet。
2. 核對 Hub 的穩定位址；Hub 服務啟動前，VPN 介面需就緒。
3. 建立群組時填入該 Hub 的實際 Tailscale IPv4。請先完成單機診斷；沒有現有閘道位址的圖形編輯功能。
4. 啟動 Hub，建立並私下交付成員短效邀請；核對群組、Hub URL 與 CA 指紋。
5. 以邀請 URL 的實際 TCP 埠設定必要來源與目的的網路規則。每群埠不同；不開放本機管理頁或不必要的遠端服務。
6. 成員加入後啟動服務、設為接單群並完成診斷。這不等於 AI、App 或 WAN 全功能已驗收。

逾時時查路由、實際埠、服務與規則；TLS 錯誤查時間、位址與來源，不略過驗證。位址變動或金鑰生命週期需要另外維護，目前沒有完整續期精靈。停止 Hub 會使其成員斷線。SmartCluster 不自動安裝 VPN、不代改防火牆，也不提供公共中繼服務承諾。
