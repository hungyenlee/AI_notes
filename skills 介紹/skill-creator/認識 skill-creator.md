標籤：#AI #Codex #skill #索引筆記

## 核心問題

`skill-creator` 是什麼？剛開始使用 Agent 時，如何用它建立、安裝與改善自己的 skill？

## 相關卡片

- [[skill-creator 是用來建立與改善 skill 的 skill]]
- [[剛開始使用 Agent 可以先用 skill-creator 建第一個 skill]]
- [[skill-creator 不一定需要下載]]
- [[Codex 應優先使用 OpenAI 版 skill-creator]]
- [[Anthropic 版 skill-creator 可安裝但不宜直接覆蓋 Codex 版]]
- [[安裝 skill 後通常需要重啟 Codex]]
- [[自己寫 skill、請 AI 寫 skill 與用 skill-creator 寫 skill 的差異]]
- [[認識 skill]]

## 初步理解

`skill-creator` 可以理解成「教 Agent 如何建立 skill 的 skill」。使用者不需要先會寫 skill，反而可以在完全沒有個人 skill 的時候，請 Agent 使用 `skill-creator` 訪談需求、設計觸發情境、產生 `SKILL.md`、規劃 references / scripts / assets，並用真實 prompt 測試與迭代。若是在 Codex 裡使用，應優先採用 OpenAI 版 `skill-creator`，Anthropic 版可以參考，但不宜直接覆蓋 Codex 版。

## 來源

- [OpenAI skill-creator](https://github.com/openai/skills/tree/main/skills/.system/skill-creator)
- [OpenAI skill-creator SKILL.md](https://raw.githubusercontent.com/openai/skills/main/skills/.system/skill-creator/SKILL.md)
- [Anthropic skill-creator](https://github.com/anthropics/skills/tree/main/skills/skill-creator)
- [Anthropic skill-creator SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md)
- 對話：2026-06-18 關於 `skill-creator` 的使用、安裝與版本差異
