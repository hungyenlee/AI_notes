#AI #README #AI-agent #知識卡

## 一句話

`README.md` 不是 AI agent 進專案時固定自動載入的規則檔，而是 agent 在需要理解專案內容、使用方式或驗證流程時，常會主動讀取的專案地圖。

## 內容

對 Codex 來說，`AGENTS.md` 和 `README.md` 的角色不同。`AGENTS.md` 是開始工作前會自動載入的工作規則，告訴 agent 在這個 repo 或資料夾中應該怎麼行動；`README.md` 則不是同一種自動規則來源，而是任務中需要專案脈絡時，agent 可能主動選擇閱讀的說明文件。

當 agent 面對陌生專案，或任務需要回答「這個專案做什麼」「怎麼安裝」「怎麼啟動」「怎麼測試」時，README 就會變得很有用。agent 可能先看檔案列表，再依任務讀 `README.md`、`package.json`、`docs/`、測試檔或相關原始碼。這不是固定順序，而是根據任務需求選擇上下文。

所以更精準的說法是：`AGENTS.md` 提供工作規則，`README.md` 提供專案理解。前者偏向「agent 應該怎麼做」，後者偏向「這個專案是什麼，以及該怎麼使用」。

## 連結

- [[認識 README.md]]
- [[README.md 是專案的入口說明文件]]
- [[好的 README.md 會回答如何開始使用]]
- [[認識 AGENTS.md]]

## 來源

- 對話整理，2026-06-12
- [Custom instructions with AGENTS.md - Codex | OpenAI Developers](https://developers.openai.com/codex/guides/agents-md)
