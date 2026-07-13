標籤：#AI #軟體測試 #冒煙測試 #SanityTesting

## 一句話

冒煙測試用來確認新 build 是否穩定到可以繼續測，Sanity Testing 則常用來確認穩定 build 中的特定修正或功能是否合理。

## 內容

Smoke Testing 和 Sanity Testing 都是快速檢查，但它們的焦點不同。冒煙測試通常發生在新 build 或新部署之後，目標是先判斷整體版本是否具備基本穩定性，能不能進入更深入的測試。

Sanity Testing 比較常發生在某個修正、新功能或小範圍變更之後，目標是確認這個特定改動看起來合理，沒有立刻暴露明顯問題。可以把冒煙測試想成「版本能不能測」，把 Sanity Testing 想成「這個改動是不是大致正常」。

## 連結

- [[認識冒煙測試]]
- [[冒煙測試和回歸測試的差別在範圍與深度]]
- [[認識回歸測試]]

## 來源

- [TechTarget：What is Smoke Testing?](https://www.techtarget.com/searchsoftwarequality/definition/smoke-testing)
