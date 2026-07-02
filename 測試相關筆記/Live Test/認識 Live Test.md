標籤：#AI #軟體測試 #LiveTest #索引筆記

## 核心問題

Live Test 是什麼，它和 Unit Test、Integration Test、E2E Test 這類測試分類有什麼不同？

## 相關卡片

- [[Live Test 原始資料]]
- [[Live Test 是在真實運作環境中驗證系統]]
- [[Live environment 是正在真實運作的環境]]
- [[Live Test 描述測試環境而不是測試範圍]]
- [[Live Test 需要控制真實使用者與資料風險]]
- [[A B Test 和 Canary Release 是 live environment 中的驗證手段]]
- [[A B Test 用分組比較不同版本的效果]]
- [[Canary Release 用少量流量驗證新版穩定性]]
- [[Canary Beta 和灰度發布的差異]]
- [[Feature Flag 用開關控制功能是否啟用]]

## 初步理解

Live Test 通常指在已承接真實使用者、真實流量、真實資料或真實外部服務副作用的環境中驗證系統，而不是一個定義非常統一的正式測試分類。最典型的 live environment 是 production，但也可能包含 canary、beta 或灰度發布環境。它關心的是測試發生在哪個環境，因此可以和 E2E、smoke test、A/B test、canary release 等方法交疊。

## 來源

- 與 Codex 對話：2026-06-26
