#AI #context #AI-agent #知識卡

## 一句話

AI 看起來「忘記」舊內容，通常不是因為單一 prompt 被刪掉，而是因為 context 太長時被壓縮，某些細節在摘要過程中流失。

## 內容

一個 thread 裡的資訊必須放進模型的 context window。當對話、工具輸出、檔案內容和工作紀錄越來越多時，系統不可能無限制保留完整原文，因此可能會做 compaction，也就是把舊內容壓縮成較短摘要。

壓縮會盡量保留主幹，例如目前目標、已完成事項、重要決策、關鍵檔案、待辦事項和限制。但摘要不是原文，早期對話中的某句原話、小例外、工具輸出細節或使用者隨口補充的要求，可能在壓縮後沒有被保留下來。

所以「忘記」比較像是：原始對話太長，系統把舊內容摘要成較短版本，後面的模型只能看到摘要後的 context。模型不是故意忽略你，而是它已經看不到那些沒有進入摘要的細節。

## 連結

- [[認識 prompt、context、memory]]
- [[context 是 AI 當下能參考的資料包]]
- [[prompt 是使用者這次給 AI 的任務指令]]
- [[memory 是跨對話保存的長期資訊]]

## 來源

- 對話整理，2026-06-12
- [Prompting - Codex | OpenAI Developers](https://developers.openai.com/codex/prompting)
