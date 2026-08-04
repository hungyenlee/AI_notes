#AI #QA #自動化測試 #品質判斷 #原始資料卡

## 來源

- ChatGPT 每日關注：2026-07-13

## 摘要

這份原始資料保存 AI 對 QA 工作影響的整理，核心是 QA 的重心正在從執行測試轉向品質判斷。它把 AI automation、bounded delegation、risk analysis、exploratory testing 與 release strategy 連在一起。

## 可沉澱的知識卡

- [[探索式測試用來發現未知風險]]
- [[風險分析用來決定測試優先順序]]
- [[發布策略用來降低上線風險]]

## 核心觀點

AI 正在把 QA 的重心推向「品質判斷」。

Microsoft 一項近期研究調查了 860 位工程師，發現開發者希望 AI 不只是協助寫程式，而是協助：

- 找出品質風險
- 提前提供品質訊號
- 協助 Review
- 發現 Regression
- 提供可信度（Provenance）
- 明確標示不確定性（Uncertainty）

## Bounded Delegation：有限授權

研究提出一個重要概念：Bounded Delegation（有限授權）。

意思是：

> AI 可以負責大量執行工作，但最後的判斷仍應由人負責。

## 不同觀點

### 支持 AI Automation

AI 能讓 QA 更專注於高價值工作，例如：

- Exploratory Testing
- Risk Analysis
- Release Strategy

### 保守派

AI 可以生成測試，但目前仍無法真正理解：

- 商業需求
- 品質定義
- 使用者體驗

## 對工作的實際做法

最近研究的測試主題：

- Test Pyramid
- Contract Test
- Integration Test
- Testability

都可以開始加入一個新的問題：

> 這個工作，AI 可以做到哪一步？

例如：

| 工作 | AI 適合？ |
| --- | --- |
| Generate Unit Test | ✅ |
| Generate Test Data | ✅ |
| Root Cause Analysis | ✅（協助） |
| Release Decision | ❌ |
| Quality Strategy | ❌ |

## 小結

AI 在測試工作中適合承擔大量產生、分析、檢查與輔助判斷任務，但不適合完全接管品質策略或發布決策。

QA 的價值會更靠近：

- 品質風險判斷
- 測試策略設計
- 發布風險評估
- 對 AI 輸出的驗證與取捨

## 相關連結

- [[QA 品質風險判斷原始資料]]
