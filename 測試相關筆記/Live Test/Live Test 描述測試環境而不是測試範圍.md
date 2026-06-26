標籤：#AI #軟體測試 #LiveTest

## 一句話

Live Test 和 E2E Test 是不同維度：Live Test 描述測試在哪裡執行，E2E Test 描述測試範圍有多完整。

## 內容

Unit Test、Integration Test、E2E Test 通常是在描述測試涵蓋的範圍。Unit Test 著重單一函式、類別或模組；Integration Test 關心多個元件能不能一起工作；E2E Test 則從使用者角度走完整流程。

Live Test 描述的是另一個維度：測試是否在真實運作中的 live environment 執行。因此兩者可以組合，而不是互斥。你可以在 staging 跑 E2E Test，也可以在 production 跑簡短的 production smoke test；如果在 production、canary 或 beta 這類承接真實使用情境的環境跑完整使用者流程，它也可以被稱為 E2E Live Test。

要注意的是，production-like environment 只是「像 production」，不一定是 live environment。若它只是複製正式環境、使用測試資料或脫敏資料，且不承接真實使用者與營運風險，通常更適合稱為 staging testing 或 production-like testing。

這也是為什麼 Live Test 不是像 unit、integration、E2E 那樣穩定的測試分類。它比較像對測試環境與風險層級的描述。

## 連結

- [[認識 Live Test]]
- [[Live Test 是在真實運作環境中驗證系統]]
- [[Live environment 是正在真實運作的環境]]
- [[測試分層讓回饋速度與真實性平衡]]

## 來源

- 與 Codex 對話：2026-06-26
