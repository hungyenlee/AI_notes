標籤：#AI #軟體測試 #LiveTest

## 一句話

Live Test 是在已承接真實使用者、真實流量、真實資料或真實外部服務副作用的環境中驗證系統。

## 內容

Live Test 的核心不是「測試寫得多完整」，而是「測試是否發生在真實運作中的環境」。最常見的 live environment 是 production，例如正式網站、正式 API、正式資料庫、正式寄信服務或第三方服務都已經接上，測試人員用專用帳號確認登入、下訂單、付款流程、Email 寄送或外部服務連線是否正常。

不過 live environment 不一定只限於承接 100% 使用者的主 production。若 **canary、beta 或灰度環境**已經接上真實使用者、真實流量、真實資料或真實外部服務副作用，也可以被視為 live environment。相對地，若只是複製 production 的設定、架構或資料，但沒有承接真實使用與營運風險，通常比較適合稱為 staging、pre-production 或 production-like environment。

## 連結

- [[認識 Live Test]]
- [[Live environment 是正在真實運作的環境]]
- [[Live Test 描述測試環境而不是測試範圍]]
- [[Live Test 需要控制真實使用者與資料風險]]
- [[Canary Beta 和灰度發布的差異]]

## 來源

- 與 Codex 對話：2026-06-26
