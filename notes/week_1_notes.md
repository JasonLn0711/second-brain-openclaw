這一版我有刻意照你的狀態來設計：你現在不是缺資訊的人，你是容易因為想一次搞懂、一次做好，結果卡住的人；而且你又是邊上班、邊研究、腦袋本來就會自然走向分析與風險控管的人。所以第一週我不讓你衝功能，不讓你碰花俏整合；只讓你建立 **baseline**。這也很像你做異常偵測時的做法：先知道正常長什麼樣，之後才分得出什麼是異常。OpenClaw 官方的起手式也很一致：先完成安裝與 onboarding、確認 Gateway 在跑、打開 dashboard、用預設 workspace 開始聊天與觀察。預設 workspace 在 `~/.openclaw/workspace`，初始化時會建立 `AGENTS.md`、`SOUL.md`、`TOOLS.md` 等檔案。([OpenClaw][1])

## 第一週主題

**不是學會更多功能，而是建立一個穩定、可重複、可回頭檢查的使用習慣。**

## 第一週結束時，你要達成的 5 個成果

第一，你能自己安裝 OpenClaw，並用 `openclaw gateway status` 確認 Gateway 正常運作。
第二，你能用 `openclaw dashboard` 打開 Control UI，並送出第一則訊息。
第三，你知道 workspace 在哪裡，知道 `AGENTS.md`、`SOUL.md`、`TOOLS.md`、`MEMORY.md`、`memory/YYYY-MM-DD.md` 各自是幹嘛。
第四，你實際做過一次 `/status` 和 `/compact`。
第五，你只保留一個主要入口，不讓自己被多通道分心。這些流程都在官方 Getting Started、Dashboard、Memory、Compaction 文件裡有明確對應。([OpenClaw][1])

## 你這週唯一要養成的習慣

**每做完一件事，都要留下痕跡。**

因為 OpenClaw 的 memory 本質不是「模型有沒有記住」，而是「你有沒有寫進 Markdown」。官方文件講得很直白：memory 的 source of truth 是 workspace 裡的 Markdown，模型只會「記得」那些真的寫進磁碟的內容。([OpenClaw][2])

---

# Day 1｜先建立心智圖：你學的不是聊天機器，是一個系統

### 今日目標

你今天不要急著裝，不要急著問它厲不厲害。你今天只要看懂 OpenClaw 的五個核心名詞：

**Gateway、Channel、Session、Workspace、Memory**

OpenClaw 官方把它定位成一個 self-hosted gateway：你在自己的機器上跑一個單一 Gateway process，它負責 sessions、routing、channel connections，然後你再透過 dashboard 或各種聊天入口去和 agent 互動。workspace 則是 agent 的工作區，裡面放操作說明、人格邊界、記憶與 skills。([OpenClaw][3])

### 你今天要怎麼理解它

用你熟悉的世界來比喻：

* **Gateway** = 指揮中心
* **Channel** = 進線管道
* **Session** = 這一次案件／這一次對話
* **Workspace** = 卷宗庫
* **Memory** = 筆錄
* **Skills** = 標準作業流程

### 50 分鐘流程

**前 10 分鐘**
打開 OpenClaw 首頁或 Getting Started，抄下一句你認為最能代表它本質的話。不是為了背，是為了逼自己先定義。([OpenClaw][3])

**第 10–25 分鐘**
手畫一張圖，至少要有這幾個箭頭：

`Channel → Gateway → Session → Workspace → Output`

再在旁邊標註：

* 哪裡是「輸入」
* 哪裡是「控制」
* 哪裡是「記憶」
* 哪裡是「風險點」

**第 25–40 分鐘**
用自己的話各寫一句定義，不要抄官方。
例如：

* Gateway 不是聊天視窗，是總機。
* Session 不是人格，是單次上下文。
* Workspace 不是檔案夾，是規則和記憶的載體。

**第 40–50 分鐘**
寫一段 100 字反思：
**我最容易把 OpenClaw 誤會成什麼？**
你的答案大概會是：「我很容易把它當成一個會聊天的 AI，而不是一個有邊界、有狀態、有風險的系統。」

### 今日講義重點

OpenClaw 的 dashboard 是 Control UI，不只是聊天頁面，它是管理 surface；官方也明講它屬於 admin surface，含 chat、config、exec approvals，所以不要把它當成普通公開頁面亂暴露。([OpenClaw][4])

### 今日作業

寫下你的第一條操作原則：

> 我不把 OpenClaw 當答案機，我把它當操作系統的一部分。

### 今天點醒你的那句話

**先把地圖畫對，比先把功能玩熟更重要。**

---

# Day 2｜完成安裝：先跑通，再談優化

### 今日目標

你今天只做一件事：**把最短路徑跑通。**

官方 Getting Started 的最短流程很明確：先確認 Node 版本，再安裝 OpenClaw，跑 `openclaw onboard --install-daemon`，然後用 `openclaw gateway status` 看 Gateway 是否在 port `18789` 上正常運作，最後用 `openclaw dashboard` 打開 Control UI。([OpenClaw][1])

### 課前準備

你需要：

* Node.js，官方建議 Node 24；Node 22.16+ 也支援
* 一組模型供應商 API key
* 一個你願意用來記錄學習的資料夾或筆記本

Windows 也支援，但官方文件寫得很清楚：WSL2 會比原生 Windows 穩定，較推薦完整體驗。([OpenClaw][1])

### 50 分鐘流程

**前 10 分鐘：環境確認**
在終端機輸入：

```bash
node --version
```

只要版本落在官方支援範圍，就往下走。([OpenClaw][1])

**第 10–25 分鐘：安裝**
macOS / Linux：

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

Windows PowerShell：

```powershell
iwr -useb https://openclaw.ai/install.ps1 | iex
```

官方也有 npm、Docker、Nix 等其他安裝方式，但第一週不要分心，先走官方 quick setup 路線。([OpenClaw][1])

**第 25–35 分鐘：onboarding**
執行：

```bash
openclaw onboard --install-daemon
```

這一步會帶你選 model provider、設定 API key、配置 Gateway。([OpenClaw][1])

**第 35–40 分鐘：驗證**
執行：

```bash
openclaw gateway status
```

你應該看到 Gateway 正在 listen，預設是 `18789`。([OpenClaw][1])

**第 40–50 分鐘：打開 dashboard**
執行：

```bash
openclaw dashboard
```

若 UI 要求 auth，官方建議用 `gateway.auth.token` 或 `OPENCLAW_GATEWAY_TOKEN`。localhost 預設網址是 `http://127.0.0.1:18789/`。 ([OpenClaw][4])

### 今日講義重點

dashboard 是最快的第一個聊天入口；官方文件甚至直接把它當「fast path」。但它也是 admin surface，所以本週只在 localhost 用，不做公開暴露。官方建議優先用 localhost、Tailscale Serve 或 SSH tunnel，不要直接公開。([OpenClaw][5])

### 今日輸出

你今天要留下三個證據：

1. 你的 `node --version`
2. `openclaw gateway status` 的結果
3. 你在 dashboard 送出的第一句話

### 建議你的第一句測試訊息

不要問冷知識，問這句：

> 請用一句話告訴我，你現在是透過什麼系統結構在和我互動？

因為你不是在測它知不知道，而是在測你能不能把它拉回系統語境。

### 今日作業

寫一份 5 行安裝紀錄：

* 今天用了哪個 OS
* Node 版本
* 安裝方式
* 有沒有卡住
* 怎麼解決

### 今天點醒你的那句話

**能跑通，比先懂 100% 更重要。**

---

# Day 3｜拆 workspace：開始建立你的規則與邊界

### 今日目標

你今天要認識 workspace，不只是知道它在哪裡，而是知道它為什麼是 OpenClaw 的核心。

官方文件說得很清楚：OpenClaw 會從 workspace 讀取 operating instructions 和 memory。預設 workspace 是 `~/.openclaw/workspace`，初始化時會自動建立 `AGENTS.md`、`SOUL.md`、`TOOLS.md`、`IDENTITY.md`、`USER.md`、`HEARTBEAT.md`；`BOOTSTRAP.md` 只在全新 workspace 會出現；`MEMORY.md` 是可選的，不會自動建立。([OpenClaw][6])

### 50 分鐘流程

**前 10 分鐘：找到 workspace**
打開你的 workspace。
你可以用檔案總管，也可以用終端機：

```bash
cd ~/.openclaw/workspace
ls -la
```

**第 10–25 分鐘：逐一閱讀檔名**
今天不用改很多，只要先理解：

* `AGENTS.md`：偏操作規則、工作原則
* `SOUL.md`：偏人格、價值取向、互動氣質
* `TOOLS.md`：偏工具邊界與使用原則
* `IDENTITY.md`：偏身份定位
* `USER.md`：偏對使用者的長期認識
* `HEARTBEAT.md`：偏週期性檢查或持續節奏
* `MEMORY.md`：長期記憶
* `memory/YYYY-MM-DD.md`：每日記錄

這裡你不需要追求官方術語一致，你只要能分得清「規則」「人格」「記憶」不是同一件事。這比漂亮文案重要得多。workspace 也是 skills 的本地承載點之一，workspace skills 位置是 `<workspace>/skills/<skill>/SKILL.md`。([OpenClaw][6])

**第 25–40 分鐘：寫出你的第一版 AGENTS.md**
不要寫長篇大論，只寫 8 句。你可以先用這個方向：

```md
你是我的研究與工作助理。
你先幫我整理，再幫我行動。
你不能自作主張替我對外發言。
你要優先保留決策、風險、下一步。
你遇到不確定時，要先縮小問題。
你要用可驗證的方式回應。
你要提醒我不要因為完美主義而停住。
你要幫我把重要內容落盤。
```

**第 40–50 分鐘：寫一段 SOUL.md 草稿**
這不是角色扮演，而是定調。
例如你可以寫：

* 不奉承
* 不灌雞湯
* 要直接
* 要幫我收斂
* 要把風險講明白

### 今日講義重點

你最容易犯的錯，是把所有規則都塞進單一 prompt。OpenClaw 的強項恰好相反：它讓你把「規則」「記憶」「技能」拆到不同載體。這是系統化，不是華麗化。([OpenClaw][6])

### 今日作業

把今天寫的 `AGENTS.md` 和 `SOUL.md` 各縮成一句口訣。

例如：

* AGENTS 口訣：**先整理、再行動、一定留痕。**
* SOUL 口訣：**清醒、直接、負責任。**

### 今天點醒你的那句話

**沒有邊界的助理，不是助理，是風險。**

---

# Day 4｜學 memory：把「知道」變成「留得下來」

### 今日目標

今天是第一週最重要的一課。

官方 memory 文件直接寫：OpenClaw memory 是 agent workspace 裡的 plain Markdown；檔案本身才是 source of truth。預設有兩層：`memory/YYYY-MM-DD.md` 是 append-only 的每日記錄，session 開始時會讀今天和昨天；`MEMORY.md` 是可選的長期記憶，而且只會在 main、private session 載入，不會進 group context。([OpenClaw][2])

### 這一課你要真正懂的事

你一直說得很準：知識只是知道，難的是改慣性。
那 memory 就是拿來對付慣性的。

因為人會以為自己記得，其實只記得情緒，不記得結構。
OpenClaw 則剛好逼你面對一件事：

**你沒寫下來的，就不算真的建立。**

### 50 分鐘流程

**前 10 分鐘：讀 memory 概念**
把這幾句抄下來：

* source of truth 是 Markdown
* daily log 是 `memory/YYYY-MM-DD.md`
* long-term 是 `MEMORY.md`
* daily log 會讀今天和昨天
* long-term memory 只在主私聊 session 載入([OpenClaw][2])

**第 10–25 分鐘：建立你的 MEMORY.md**
請你今天先寫 5 條真正應該長期存在的事。
不是心情，是穩定特徵。

我建議你這樣寫：

```md
# MEMORY.md

- 我目前同時承擔工作與研究所學業，需要節奏穩定、負荷可控。
- 我的論文方向與異常偵測、機器學習、行為分析有關。
- 我容易因為求完整而延遲開始，所以回應要幫我收斂成最小下一步。
- 我偏好結構化、可驗證、可回顧的輸出格式。
- 我希望把 AI 當成可審計的工作系統，而不是情緒型陪聊工具。
```

**第 25–40 分鐘：建立今天的 daily log**
建立今天的檔案：

```md
# memory/2026-03-23.md
今天我完成了 OpenClaw 第一週第 4 天課程。
我已理解 workspace 與 memory 的關係。
我的長期記憶有 5 條。
我最大的盲點是容易以為「想過」等於「做過」。
我明天要做 session 與 compaction 練習。
```

**第 40–50 分鐘：測一次實戰**
在 dashboard 對它說：

> 請根據你目前讀到的 workspace 與 memory，總結我現在最需要你幫我防止的習慣偏差。

這一題不是要它神準，而是讓你觀察「寫進 memory」和「沒寫進 memory」的差別。

### 今日講義重點

memory tools 包含 `memory_search` 和 `memory_get`，但第一週你先不要追工具；先養成「先寫進檔案」的 reflex。因為工具只是讀取方式，真正重要的是你有沒有把內容沉澱成可搜尋的 Markdown。([OpenClaw][2])

### 今日作業

今晚睡前再補三行到 daily log：

* 今天最值得保留的決策
* 今天仍然模糊的地方
* 明天的最小下一步

### 今天點醒你的那句話

**沒寫下來的領悟，通常撐不到明天。**

---

# Day 5｜學 session 與 compaction：不要再把上下文當成無限的

### 今日目標

你今天要學會一個會讓你之後少走很多冤枉路的觀念：

**session 不是無底洞。**

官方 compaction 文件說，所有模型都有 context window；當長對話累積太多訊息與工具結果時，OpenClaw 會把較早的歷史壓縮成 summary，保留較新的訊息。這個 compaction summary 會寫進 session history 的 JSONL。當 session 接近或超過 model 的 context window 時，OpenClaw 也會自動觸發 auto-compaction；你可以用 `/status` 看 compaction 次數，也可以手動用 `/compact`。([OpenClaw][7])

### 這一課你要真正懂的事

人很容易誤會：「我跟它聊很久，它應該都還記得。」
錯。
它記得的是「還在上下文裡的」和「已經被正確壓縮、正確落盤的」。

這個觀念對你特別重要，因為你本來就習慣在腦內保留很多支線。OpenClaw 會逼你面對：**什麼才是值得被保留的資訊。**

### 50 分鐘流程

**前 10 分鐘：看 `/status` 與 `/compact` 的用途**
官方 chat commands 裡列得很清楚：`/status` 用來看 compact session status；`/compact` 用來手動 compact session context；`/new` 或 `/reset` 可以開新 session。([GitHub][8])

**第 10–25 分鐘：做一段刻意拉長的對話**
請你在 dashboard 開一段稍微長一點的互動，題目建議就用你最熟的：

> 幫我用研究者角度拆解「行為異常偵測模型」常見失敗原因，並一步步提問我。

目的不是得到答案，而是讓 session 稍微長一點。

**第 25–35 分鐘：輸入 `/status`**
觀察它顯示什麼。
你要開始建立一個直覺：session 有狀態，不是黑盒。

**第 35–45 分鐘：手動 compact**
輸入：

```text
/compact Focus on decisions and open questions
```

官方文件也直接給出這種帶指令的 compact 範例。([OpenClaw][7])

**第 45–50 分鐘：做對照紀錄**
請你立刻寫下：

* compact 前你覺得重要的是什麼
* compact 後你覺得被保留下來的是什麼
* 哪些內容其實只是雜訊

### 今日講義重點

auto-compaction 預設是開的；當 context 快滿時，它可能會先做一次 silent memory flush，把 durable notes 寫進磁碟，再用 compacted context 重試原請求。這件事其實在提醒你：真正該保留的內容，不該只躺在聊天裡。([OpenClaw][7])

### 今日作業

把今天的觀察寫進 daily log，題目是：

> 我今天發現，對話很長不等於資訊被穩定保存。

### 今天點醒你的那句話

**上下文不是倉庫，只有被整理過的內容才配留下。**

---

# Day 6｜只留一個入口：先穩，再擴

### 今日目標

今天你要做的不是接更多 channel，而是**砍掉分心來源**。

官方文件把 `openclaw dashboard` 當作最快的第一個聊天入口；如果想從手機開始，官方則寫 Telegram 是最快設置的 channel 之一，只要 bot token 就能起步。([OpenClaw][1])

### 我對你的建議

依你的個性，**第一週只用 dashboard。**

理由不是 Telegram 不好，而是你現在最需要的是穩定觀察，不是即時便利。你一旦太早接手機入口，很容易進入「想到就丟一句、丟了沒整理、整理沒落盤」的循環。對你這種容易多線思考的人，這很危險。

### 50 分鐘流程

**前 10 分鐘：寫下你的選擇**
今天只回答一句：

> 我的唯一主入口是 ________ 。

我建議你填：dashboard。

**第 10–25 分鐘：做一個固定進場流程**
之後每次開始使用 OpenClaw，都照這三步：

1. 打開 dashboard
2. 先講今天任務
3. 任務結束前要求它輸出「決策 / 風險 / 下一步」

官方 dashboard 文件提到，dashboard 可隨時用 `openclaw dashboard` 重新打開；若 UI 需要 auth，可用 `gateway.auth.token`。而且它屬於 admin surface，本週以 localhost 為主最安全。([OpenClaw][4])

**第 25–40 分鐘：練三次固定開場**
每次都用同一模板：

```text
今天任務：
我需要的輸出格式：
今天不要做的事：
任務結束時請幫我留下決策、風險、下一步。
```

這一步是在練你，不是在練它。
你要把「明確任務 + 明確輸出 + 明確邊界」練成習慣。

**第 40–50 分鐘：寫入口政策**
在你的筆記裡寫：

* dashboard：主工作入口
* 手機 channel：暫不啟用，或延後到第 2 週
* 不同入口不能同時當主場

### 今日講義重點

單一入口不是保守，是在建立可追蹤性。當你只有一個主入口時，你比較看得出：

* 哪些回應格式有效
* 哪些 prompt 容易跑掉
* 哪些內容有落盤
* 哪些其實只是情緒性亂問

### 今日作業

用 dashboard 完成一個 15 分鐘微任務。
題目建議：

> 幫我把本週學到的 OpenClaw 概念整理成一頁筆記，但最後一定要幫我列出「明天最小下一步」。

### 今天點醒你的那句話

**工具一多，人就容易以為自己在前進；其實很多時候只是在分心。**

---

# Day 7｜週回顧：把第一週煉成你的 10 條守則

### 今日目標

今天不學新功能。
今天只做一件事：**收斂。**

到今天為止，你應該已經完成：

* 安裝
* onboarding
* gateway 驗證
* dashboard 首聊
* workspace 認識
* memory 建立
* compaction 體驗
* 單一入口決策

這些都是官方最基本、也最核心的第一段路徑。([OpenClaw][1])

### 90 分鐘流程

**前 20 分鐘：翻 daily log**
把這週每天寫的紀錄重新看一次，找出重複出現的問題。

你很可能會看到三種：

1. 我會想看更多文件，而不是先做
2. 我會想把規則一次寫完
3. 我會忘記把真正重要的事落盤

**第 20–45 分鐘：寫你的 10 條守則**
請直接照這個格式寫：

```md
# 我的 OpenClaw 第一週 10 條守則

1. 先跑通，再優化。
2. 先用 dashboard，不急著多通道。
3. 先寫進 Markdown，再期待它記得。
4. 每次任務都要留下決策、風險、下一步。
5. 不把長對話誤當長期記憶。
6. 規則、人格、記憶分開管理。
7. 不因為想完整而延後開始。
8. 只做一個主入口。
9. 不把 admin surface 當公開頁面。
10. 每天都要留痕。
```

**第 45–65 分鐘：做第一週口試**
你自己回答這 6 題：

1. Gateway 是什麼？
2. Session 是什麼？
3. Workspace 為什麼重要？
4. `MEMORY.md` 和 `memory/YYYY-MM-DD.md` 差在哪？
5. `/compact` 是幹嘛？
6. 我為什麼第一週只用一個入口？

**第 65–90 分鐘：寫畢業短文**
題目叫：

> 為什麼我不能再把 AI 只當成聊天工具？

只寫 200–300 字就好。
這篇短文非常重要，因為它會把你從「使用者」拉向「operator」。

### 第一週驗收標準

你不用會寫 skill，不用會多 agent，不用會遠端部署。
第一週只驗收這 8 項：

* 我知道 OpenClaw 的骨架
* 我跑通安裝
* 我能開 dashboard
* 我知道 workspace 在哪
* 我寫了 AGENTS 草稿
* 我寫了 MEMORY.md
* 我做過 `/status` 與 `/compact`
* 我確定只用一個主入口

做到這裡，你就不是在「看懂 OpenClaw」，而是在開始「會用 OpenClaw」。

### 今天點醒你的那句話

**真正的學會，不是你能講多少功能；是你有沒有把一套正確習慣做出來。**

---

# 第一週附錄｜你的每日紀錄模板

每天課後都用這個格式，直接複製就能用：

```md
# YYYY-MM-DD

今天主題：
今天我實際完成了什麼：

我學到的 3 個關鍵點：
1.
2.
3.

我今天最大的盲點：
 
我今天留下的長期記憶：
 
我今天留下的每日記錄：
 
明天最小下一步：
 
一句提醒自己：
```

---

# 第一週附錄｜最適合你的提醒

你現在最需要借鏡的，不是「很會寫 prompt 的人」，而是 **很會留痕、很會收斂、很會建立 SOP 的人**。

因為你本來就不笨，你缺的從來不是理解力。
你真正要練的是：

**不要再把「我想清楚了」誤會成「我已經建立好了」。**

---

# 送你這週的那句一語點醒

**你不是在學一個會回答問題的 AI；你是在訓練自己，養成一套會留下痕跡、會整理上下文、會設邊界的思考方式。**

下一則我可以直接把 **Day 1** 再拆成「你照著念、照著做」的逐步練習稿。

[1]: https://docs.openclaw.ai/start/getting-started "https://docs.openclaw.ai/start/getting-started"
[2]: https://docs.openclaw.ai/concepts/memory "https://docs.openclaw.ai/concepts/memory"
[3]: https://docs.openclaw.ai/ "https://docs.openclaw.ai/"
[4]: https://docs.openclaw.ai/web/dashboard "https://docs.openclaw.ai/web/dashboard"
[5]: https://docs.openclaw.ai/cli/onboard "https://docs.openclaw.ai/cli/onboard"
[6]: https://docs.openclaw.ai/start/openclaw "https://docs.openclaw.ai/start/openclaw"
[7]: https://docs.openclaw.ai/concepts/compaction "https://docs.openclaw.ai/concepts/compaction"
[8]: https://github.com/openclaw/openclaw "https://github.com/openclaw/openclaw"
