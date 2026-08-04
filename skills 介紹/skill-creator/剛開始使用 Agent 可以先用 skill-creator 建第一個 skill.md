#AI #Codex #skill #知識卡

## 一句話

剛開始使用 Agent 且沒有任何個人 skill 時，可以直接請 Agent 使用 `skill-creator`，從一個重複任務開始建立第一個 skill。

## 內容

新手不需要先學完整 skill 規格，最好的起點是找一個最近重複做過、而且希望 Agent 下次更穩定執行的任務。接著直接要求：「請使用 `skill-creator` 幫我建立一個 skill，但先訪談我，不要直接寫檔。」

訪談通常會釐清這個 skill 要做什麼、哪些使用者說法應該觸發、輸出格式是什麼、有沒有固定範本，以及需要哪些測試 prompt。第一版可以先只有 `SKILL.md`，等流程穩定後，再補 `references/`、`scripts/` 或 `assets/`。真正的重點不是一次寫完，而是用真實任務測試後，把失敗案例補回 skill。

## 連結

- [[認識 skill-creator]]
- [[skill-creator 是用來建立與改善 skill 的 skill]]
- [[建立 skill 需要先定義觸發情境]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]

## 來源

- [OpenAI skill-creator SKILL.md](https://raw.githubusercontent.com/openai/skills/main/skills/.system/skill-creator/SKILL.md)
- 對話：2026-06-18 關於剛開始使用 Agent 時如何使用 `skill-creator`
