標籤：#AI #Codex #AGENTS #索引筆記

## 核心問題

`AGENTS.md` 如何讓 Codex 取得長期工作規則，而 `AGENTS.override.md` 又在什麼情況下應該介入？

## 相關卡片

- [[AGENTS.override.md 會優先取代同層 AGENTS.md]]
- [[AGENTS.override.md 適合暫時或局部覆蓋規則]]
- [[AGENTS.md 會先組成指令鏈而 skill 會按需讀取]]

## 初步理解

`AGENTS.md` 是 Codex 的長期工作規則入口，適合放穩定、會反覆使用的 repo 或資料夾規範。`AGENTS.override.md` 則是更高優先權的同層替代檔，適合用來暫時、局部或強制覆蓋原本規則。理解兩者差異的重點不是檔名，而是「長期預設」與「高優先權覆蓋」的分工。

## 來源

- [Custom instructions with AGENTS.md - Codex | OpenAI Developers](https://developers.openai.com/codex/guides/agents-md)
