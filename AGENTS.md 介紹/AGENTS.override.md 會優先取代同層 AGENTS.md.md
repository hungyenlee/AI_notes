標籤：#AI #Codex #AGENTS #永久筆記

## 一句話

在同一個資料夾中，Codex 會優先讀取 `AGENTS.override.md`，只有沒有 override 時才讀取 `AGENTS.md`。

## 內容

`AGENTS.md` 和 `AGENTS.override.md` 都是 Codex 的指令檔，差別在同一層目錄的優先順序。Codex 讀取指令時，會先看 Codex home 裡的全域規則，再從專案 root 一路走到目前工作目錄；在每一層資料夾中，它會先找 `AGENTS.override.md`，找不到才找 `AGENTS.md`。

因此，同一個資料夾如果同時存在 `AGENTS.override.md` 和 `AGENTS.md`，這一層實際生效的是 override，原本的 `AGENTS.md` 會被略過。再加上越靠近目前工作目錄的指令越晚被放進 prompt，較深層的 override 通常也更容易覆蓋上層或全域規則。

可以把 `AGENTS.md` 理解成穩定預設，把 `AGENTS.override.md` 理解成高優先權替代。它不是另一份補充說明，而是同層規則的取代入口。

## 連結

- [[認識 AGENTS.md]]
- [[AGENTS.override.md 適合暫時或局部覆蓋規則]]
- [[AGENTS.md 會先組成指令鏈而 skill 會按需讀取]]

## 來源

- [Custom instructions with AGENTS.md - Codex | OpenAI Developers](https://developers.openai.com/codex/guides/agents-md)
