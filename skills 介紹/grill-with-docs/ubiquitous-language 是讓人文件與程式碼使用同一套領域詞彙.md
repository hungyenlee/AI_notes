#AI #Codex #skill #DDD #知識卡

## 一句話

`ubiquitous-language` 是讓開發者、領域專家、文件與程式碼都使用同一套領域詞彙。

## 內容

`ubiquitous-language` 是 Domain-Driven Design 裡的概念，重點不是翻譯名詞，而是建立一套團隊共同使用的語言。當 PM、使用者、開發者、測試、文件和程式碼都用不同詞描述同一個概念時，系統很容易長出誤解。

例如同一個概念有時叫 `Customer`，有時叫 `User`，資料表又叫 `Account`，就需要釐清它們是同一件事，還是三個不同概念。`ubiquitous-language` 會選出標準詞，說明定義、關係和不要混用的別名。

在 Matt Pocock 的 skill 演化裡，`ubiquitous-language` 曾經是獨立 skill，用來輸出 `UBIQUITOUS_LANGUAGE.md`。後來它被併入 `grill-with-docs`，再逐步演化成由 `domain-modeling` 維護 `CONTEXT.md` 與 ADR 的能力。

## 連結

- [[認識 grill-with-docs]]
- [[domain-modeling 負責維護專案共同語言與架構決策]]
- [[grill-me 到 domain-modeling 的演化是追問流程與文件化能力拆分]]

## 來源

- [Skills Changelog: Ubiquitous Language -> /grill-with-docs](https://www.aihero.dev/skills-changelog-ubiquitous-language-grill-with-docs.md)
- [ubiquitous-language SKILL.md](https://github.com/mattpocock/skills/blob/main/skills/deprecated/ubiquitous-language/SKILL.md)
- [grill-with-docs: Align Before You Build](https://www.aihero.dev/grill-with-docs.md)
