#AI #軟體測試 #LiveTest #知識卡

## 一句話

Live environment 是已經承接真實使用情境與營運風險的環境，而不只是長得像 production 的環境。

## 內容

判斷一個環境是否是 live environment，重點不是它的設定、架構或資料是否接近 production，而是它是否正在承接真實使用者、真實流量、真實資料，或真實外部服務副作用。例如正式付款、寄信、通知、第三方 API 呼叫或會影響實際營運的資料寫入，都會讓測試風險變高。

Production 通常是最典型的 live environment，但 live environment 不一定只限於主 production。若 **canary、beta 或灰度環境**已經承接部分真實流量或真實客戶，也可以被視為 live environment。相對地，若只是複製 production 的設定、架構或資料，但沒有真實使用情境與營運風險，通常更適合稱為 staging、pre-production 或 production-like environment。

## 連結

- [[認識 Live Test]]
- [[Live Test 是在真實運作環境中驗證系統]]
- [[Live Test 描述測試環境而不是測試範圍]]
- [[Canary Beta 和灰度發布的差異]]

## 來源

- 與 Codex 對話：2026-06-26
