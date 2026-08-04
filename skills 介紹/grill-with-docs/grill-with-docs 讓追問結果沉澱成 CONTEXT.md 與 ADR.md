#AI #Codex #skill #知識卡

## 一句話

`grill-with-docs` 的核心改進，是把追問中形成的共識寫進 `CONTEXT.md` 和 ADR，避免每次都重新解釋。

## 內容

`grill-me` 可以讓使用者和 AI 透過追問形成共同理解，但這些理解如果只留在對話裡，很容易在下一次 session 消失。`grill-with-docs` 補上的就是這一層薄文件：用 `CONTEXT.md` 保存專案共同語言，用 ADR 保存重要且不容易反轉的架構決策。

`CONTEXT.md` 比較像 glossary，記錄 domain terms、概念邊界和關係。ADR 則只在決策難以反轉、沒有背景會令人意外、且確實存在取捨時才建立。這讓文件不是流水帳，而是保留未來最容易遺忘、也最需要對齊的知識。

## 連結

- [[認識 grill-with-docs]]
- [[domain-modeling 負責維護專案共同語言與架構決策]]
- [[grill-me 適合通用計畫盤問而 grill-with-docs 適合 codebase]]

## 來源

- [grill-with-docs: Align Before You Build](https://www.aihero.dev/grill-with-docs.md)
- [domain-modeling SKILL.md](https://github.com/mattpocock/skills/blob/main/skills/engineering/domain-modeling/SKILL.md)
