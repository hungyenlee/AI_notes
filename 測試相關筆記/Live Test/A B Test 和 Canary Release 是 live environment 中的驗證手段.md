#AI #軟體測試 #LiveTest #知識卡

## 一句話

A/B Test、Canary Release 和 Feature Flag 若發生在 live environment 中，可以作為驗證新版本的手段，但它們本身更像實驗與漸進式發布手段。

## 內容

在承接真實使用者、真實流量、真實資料或真實外部服務副作用的環境裡驗證功能時，團隊不一定會一次把新版本開給所有使用者。A/B Test 可以比較不同版本的使用者行為；Canary Release 可以先讓少量流量使用新版；Feature Flag 則可以控制哪些使用者或條件能看到新功能。這些做法都能降低 Live Test 的風險，因為影響範圍被限制住，異常時也比較容易關閉或回滾。

但這些名詞不應直接等同於 Live Test。A/B Test 比較偏向產品實驗，Canary Release 和 Feature Flag 則偏向 release strategy 或 progressive delivery。它們和 Live Test 的關係是：當這些驗證發生在已承接真實使用情境與營運風險的環境中時，可以被視為 live testing 的一種實務手段；如果只是在 staging 或 production-like environment 裡使用這些技術，通常仍是 staging testing 或 production-like testing。

## 連結

- [[認識 Live Test]]
- [[Live Test 需要控制真實使用者與資料風險]]
- [[Live Test 描述測試環境而不是測試範圍]]
- [[A B Test 用分組比較不同版本的效果]]
- [[Canary Release 用少量流量驗證新版穩定性]]
- [[Feature Flag 用開關控制功能是否啟用]]

## 來源

- 與 Codex 對話：2026-06-26
