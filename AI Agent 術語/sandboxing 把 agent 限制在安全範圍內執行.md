標籤：#AI #AI-agent #sandboxing

## 一句話

Sandboxing 是把 AI agent 或程式限制在安全範圍內執行，讓它能做事但不能任意碰觸外部資源。

## 內容

Sandboxing 可以理解成一個隔離工作區。Agent 可以在允許的範圍內讀檔、寫檔、執行指令或呼叫工具，但如果動作會碰到更敏感的資源，例如 workspace 外的檔案、網路、系統設定、Git 寫入或高風險操作，就可能需要使用者批准。

它的目的不是讓 agent 什麼都不能做，而是把能力放進可控邊界中。這樣既能讓 agent 幫忙完成實際任務，也能降低誤改檔案、洩漏資料或執行未預期動作的風險。對 coding agent 來說，sandboxing 常會和 permissions、approval policy、allowed tools 一起構成安全控制。

## 連結

- [[從 Claude Code 術語認識 AI agent 概念]]
- [[AI agent 工具概念]]
- [[認識 MCP]]

## 來源

- Codex 對話，2026-07-07
