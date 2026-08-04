#AI #Codex #skill #知識卡

## 一句話

`skill-creator` 不是普通範例 skill，而是用來幫 Agent 設計、撰寫、測試與改善其他 skill 的 meta-skill。

## 內容

`skill-creator` 的用途不是直接幫使用者完成某個業務任務，而是幫使用者把可重複的工作流程變成 skill。它會提醒 Agent 先釐清目標、觸發情境、輸出格式、成功標準與失敗案例，再決定 `SKILL.md` 該寫什麼，以及是否需要額外的 `references/`、`scripts/` 或 `assets/`。

它和單純「請 AI 幫我寫 skill」的差異在於，`skill-creator` 會提供一套設計流程。這讓 Agent 不只是產生一份看起來像 skill 的 Markdown，而是更有機會做出能被正確觸發、能被測試、也能持續改善的 skill。

## 連結

- [[認識 skill-creator]]
- [[自己寫 skill、請 AI 寫 skill 與用 skill-creator 寫 skill 的差異]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[建立 skill 需要先定義觸發情境]]

## 來源

- [OpenAI skill-creator SKILL.md](https://raw.githubusercontent.com/openai/skills/main/skills/.system/skill-creator/SKILL.md)
- [Anthropic skill-creator SKILL.md](https://github.com/anthropics/skills/blob/main/skills/skill-creator/SKILL.md)
