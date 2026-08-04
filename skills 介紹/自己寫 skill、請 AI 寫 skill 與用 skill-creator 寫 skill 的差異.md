#AI #Codex #skill #筆記 #知識卡

## 一句話

自己寫 skill、請 AI 寫 skill、用 `skill-creator` 寫 skill 的差異，在於流程正式程度與品質保障不同。

## 連結

- [[認識 skill]]
- [[skill 是 AI agent 的可重複任務能力]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[建立 skill 需要先定義觸發情境]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
- [[認識 skill-creator]]
- [[認識 MCP 與 skill 的分工]]

## 內容

自己寫 skill、請 AI 寫 skill、請 AI 透過 `skill-creator` skill 來寫 skill，可以理解成三個不同層次：

| 做法 | 本質 | 最適合 |
|---|---|---|
| 自己寫 skill | 你直接把工作流程寫成 `SKILL.md` | 你很清楚流程，且 skill 很簡單 |
| 請 AI 寫 skill | 讓 AI 幫你草擬一份 skill | 快速起草、把模糊想法變成初稿 |
| 請 AI 透過 `skill-creator` 寫 skill | 讓 AI 使用「寫 skill 的專門流程」來設計、驗證、改善 skill | 想做可重複使用、觸發穩定、品質較高的 skill |

一句話差異：

自己寫 skill，是你在寫作業手冊。  
請 AI 寫 skill，是請 AI 幫你代筆。  
請 AI 透過 `skill-creator` 寫 skill，是請 AI 按照一套「如何設計好 skill」的 SOP 來訪談、拆解、撰寫、測試與優化。

## 自己寫 skill

優點是最貼近你的真實意圖。你知道自己的工作流程、偏好、踩過的坑，也知道哪些事情對你來說很重要。這種情況下，自己寫出的 skill 往往比較有「現場感」。

缺點是容易漏掉 skill 的工程細節，例如：

- `description` 寫得太弱，導致 AI 不知道何時該觸發
- `SKILL.md` 太長，把大量知識一次塞進 context
- 沒有區分 `scripts/`、`references/`、`assets/`
- 沒有測試 prompt，不知道 skill 實際用起來如何
- 寫得像給人看的文件，而不是給 agent 用的操作指令

所以自己寫適合小型、明確、個人用的 skill。例如：「每次整理我的 Obsidian 筆記時，請遵守這些格式」。

## 請 AI 寫 skill

這比較像快速產生初稿。你描述需求，AI 幫你整理成 `SKILL.md`。

優點是快，而且 AI 很擅長把雜亂的想法整理成結構化文件。你可以說：「幫我把這段工作流程變成 skill」，AI 通常能產出一個能看的版本。

缺點是 AI 可能寫得「像 skill」，但不一定是好 skill。常見問題是：

- 寫太多模型本來就知道的常識
- `description` 不夠精準，觸發不穩
- 指令太泛，沒有真正提高 agent 表現
- 缺少測試案例
- 沒有判斷哪些內容該放 `SKILL.md`，哪些該拆成 reference 或 script
- 可能過度迎合你的描述，而沒有反問關鍵邊界條件

所以請 AI 寫 skill 很適合做第一版，但通常需要你再 review。

## 請 AI 透過 skill-creator 寫 skill

這是最完整、最正式的做法。`skill-creator` 本身就是一個「教 AI 如何建立 skill」的 skill。它會提醒 AI 不只是寫一份 Markdown，而是要思考：

- 這個 skill 要讓 agent 做什麼？
- 什麼情境下應該觸發？
- `description` 是否足夠明確？
- 哪些資訊應該放在 `SKILL.md`？
- 哪些應該拆到 `references/`？
- 有沒有重複、脆弱、需要確定性的步驟應該做成 `scripts/`？
- 要不要設計測試 prompt？
- 實際跑起來有沒有比不用 skill 更好？
- 是否需要優化觸發描述？

它的優點是品質比較穩，因為 AI 不是憑感覺寫，而是按一套設計流程走。缺點是比較重，需要更多時間，也可能會問你更多問題。

## 怎麼選

| 情境 | 建議 |
|---|---|
| 只是自己用的小流程 | 自己寫，或請 AI 幫你整理 |
| 已經有明確流程，但想省時間 | 請 AI 寫第一版 |
| 這個 skill 會常用、會分享、會影響重要工作 | 用 `skill-creator` |
| skill 需要 scripts、references、assets | 用 `skill-creator` |
| 你在意觸發準確度與可測試性 | 用 `skill-creator` |
| 只是想記錄偏好或格式規則 | 不一定需要 `skill-creator` |

## 建議流程

最實用的做法其實是混合：

1. 你先用自然語言寫下「我希望這個 skill 做什麼」
2. 請 AI 草擬 skill
3. 再請 AI 用 `skill-creator` 的標準檢查與重寫
4. 實際用幾次後，把失敗案例補回 skill

所以不是「自己寫 vs AI 寫 vs skill-creator」三選一。比較好的理解是：

> 自己提供真實需求，AI 負責結構化，`skill-creator` 負責把它變成比較可靠的 skill。

## 來源

- 對話：2026-06-18 關於自己寫 skill、請 AI 寫 skill、用 `skill-creator` 寫 skill 的差異
