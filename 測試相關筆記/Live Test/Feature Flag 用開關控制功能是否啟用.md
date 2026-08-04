#AI #軟體測試 #LiveTest #知識卡

## 一句話

Feature Flag 讓程式碼可以先部署到正式環境，但功能是否開放由開關控制。

## 內容

Feature Flag 實際運作時，程式碼可能已經部署到 production，但使用者是否看到新功能取決於設定。例如 `new_checkout = false` 時，即使新版程式碼存在，使用者仍看到舊版流程；當開關對特定測試帳號、beta 使用者、某個地區或少量百分比使用者打開時，這些人才能看到新版功能。

Feature Flag 常和 A/B Test 或 Canary Release 搭配使用，因為它可以細緻控制誰看到新功能，也能在出問題時快速關閉功能，而不一定要重新部署。它降低了上線風險，但也需要管理旗標生命週期，避免舊旗標長期留在程式碼中造成複雜度。

## 連結

- [[認識 Live Test]]
- [[A B Test 和 Canary Release 是 live environment 中的驗證手段]]
- [[Live Test 需要控制真實使用者與資料風險]]

## 來源

- 與 Codex 對話：2026-06-26
