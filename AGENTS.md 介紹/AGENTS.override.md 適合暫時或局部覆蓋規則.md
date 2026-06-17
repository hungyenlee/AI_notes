標籤：#AI #Codex #AGENTS #永久筆記

## 一句話

`AGENTS.override.md` 適合用在需要暫時、局部或強制覆蓋既有 `AGENTS.md`，但又不想改動長期規則的時候。

## 內容

`AGENTS.md` 應該放穩定、長期、團隊或專案共同遵守的規則，例如測試指令、程式風格、筆記格式或資料夾慣例。`AGENTS.override.md` 則適合放短期或特殊情境的規則，讓原本的長期規範先保留下來。

常見用法包括：臨時要求 Codex 只閱讀不修改、在個人本機覆蓋團隊預設、讓某個子資料夾使用不同測試指令、試跑一套新的工作流程，或在敏感區域加入「不要執行 migration」「不要修改 schema」之類的緊急限制。

不適合的用法，是長期把所有正式規則都放進 `AGENTS.override.md`。這會讓 override 失去「暫時覆蓋」的語意，也容易讓人忘記真正生效的不是平常看的 `AGENTS.md`。

## 連結

- [[認識 AGENTS.md]]
- [[AGENTS.override.md 會優先取代同層 AGENTS.md]]
- [[AGENTS.md 會先組成指令鏈而 skill 會按需讀取]]

## 來源

- [Custom instructions with AGENTS.md - Codex | OpenAI Developers](https://developers.openai.com/codex/guides/agents-md)
