#AI #AI-agent #索引卡

## 核心問題

`prompt`、`context`、`memory` 分別是什麼？它們在 AI 回答問題時扮演什麼不同角色？

## 相關卡片

- [[prompt 是使用者這次給 AI 的任務指令]]
- [[context 是 AI 當下能參考的資料包]]
- [[context 太長時會因壓縮而流失細節]]
- [[memory 是跨對話保存的長期資訊]]
- [[Codex memory 預設不會自動永久記錄]]
- [[RAG 找回來的資料會成為 context 的一部分]]
- [[prompt、context、memory 相關原始資料]]

## 初步理解

`prompt` 是使用者當下給 AI 的指令或問題，屬於這一次任務的起點。`context` 是 AI 在回答當下能看到的所有資訊，範圍比 prompt 大，可能包含前文、文件、工具結果、系統規則和 RAG 找回來的資料。`memory` 則是跨對話保存的長期資訊，是否存在與如何使用，取決於產品或應用層設計。

## 來源

- [[prompt、context、memory 相關原始資料]]
