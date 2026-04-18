# career-ops -- 繁體中文模式 (`modes/zh-TW/`)

此資料夾包含 career-ops 主要模式的繁體中文翻譯，並針對台灣職場文化、勞動法規和求職生態系統進行在地化，適合在台灣求職或應徵台灣公司的候選人使用。

## 什麼時候使用這些模式？

符合以下任一條件，請使用 `modes/zh-TW/`：

- 主要應徵**繁體中文職缺**（104人力銀行、CakeResume、Yourator、Meet.jobs、1111 人力銀行、LinkedIn Taiwan 等）
- 需要符合**台灣勞動法規**的評估：勞基法、責任制核備、加班費計算、競業禁止條款
- 需要了解**台灣薪酬結構**：月薪×月數制、年終獎金、績效獎金、三節獎金、勞退提撥
- 需要**自然的台灣科技業繁體中文**，而非機器翻譯
- 求職目標包含**外商台灣分公司、本土大企業、台灣新創**等不同類型公司的評估

若大多數職缺為英文，請使用預設的 `modes/`。英文模式也能處理中文職缺，但不具備同等程度的台灣市場專業知識。

## 如何啟用？

career-ops 沒有程式碼層面的「語言切換」旗標，有兩種方法：

### 方法 1 -- 單次 session 指示

在 session 開頭告訴 Claude：

> 「使用 `modes/zh-TW/` 的繁體中文模式。」

或

> 「評估和應徵用繁體中文，讀取 `modes/zh-TW/_shared.md` 和 `modes/zh-TW/ping-gu.md`。」

Claude 會讀取此資料夾的檔案，而非 `modes/` 的預設版本。

### 方法 2 -- profile 永久設定

在 `config/profile.yml` 新增語言設定：

```yaml
language:
  primary: zh-TW
  modes_dir: modes/zh-TW
```

第一次 session 告訴 Claude 尊重此設定（「看一下 `profile.yml`，我設了 `language.modes_dir`」）。之後 Claude 會自動使用繁體中文模式。

> 注：`language.modes_dir` 是慣例，不是嚴格的 schema。

## 包含哪些翻譯？

第一個版本涵蓋影響最大的 4 個模式：

| 檔案 | 翻譯自 | 用途 |
|-----|-------|------|
| `_shared.md` | `modes/_shared.md` (EN) | 共用情境、職缺類型、全局規則、台灣市場特有注意事項 |
| `ping-gu.md` | `modes/oferta.md` (ES) | 職缺完整評估（A-F 區塊）+ 台灣勞動法合規性檢查（G 區塊）|
| `ying-zheng.md` | `modes/apply.md` (EN) | 應徵表單填寫線上助手 |
| `pipeline.md` | `modes/pipeline.md` (EN) | URL 收件匣 / 職缺 Second Brain |

其餘模式（`scan`、`batch`、`pdf`、`tracker`、`auto-pipeline`、`deep`、`contacto`、`ofertas`、`project`、`training`）暫不包含——這些主要為工具配管、路徑和設定指令，應保持語言無關。

社群採用此繁體中文模式後，後續 PR 會翻譯更多模式。

## 保留英文的項目

以下為意圖保留英文的標準科技術語：

- `cv.md`、`pipeline`、`tracker`、`report`、`score`、`archetype`、`proof point`
- 工具名稱（`Playwright`、`WebSearch`、`WebFetch`、`Read`、`Write`、`Edit`、`Bash`）
- Tracker 狀態值（`Evaluated`、`Applied`、`Interview`、`Offer`、`Rejected`）
- 程式碼片段、檔案路徑、指令
- 常見技術詞彙（`stack`、`pipeline`、`deployment`、`embedding`、`LLM`、`API`）

模式使用台北、新竹、台中科技業實際使用的自然繁體中文：行文用繁體中文，已普及的科技術語維持英文原文。

## 台灣市場特有功能

`ping-gu.md` 的 G 區塊（合法性）包含台灣特有的紅旗偵測：

| 紅旗 | 嚴重程度 |
|-----|---------|
| 責任制無勞動部核備 | 🔴 違法 |
| 薪資面議無範圍（104/1111 已強制揭露）| ⚠️ 不透明 |
| 底薪低 + 高抽成無保障 | ⚠️ 風險 |
| 競業禁止無合理補償 | ⚠️ 不具強制力 |
| 勞健保投保薪資低於實際薪資 | 🔴 違法 |
| 試用期超過 3 個月且降薪 | ⚠️ 異常 |

## 參考術語表

| 英文 | 繁體中文（此 codebase）|
|-----|----------------------|
| Job posting | 職缺 / 職位 |
| Application | 應徵 |
| Cover letter | 求職信 / 自傳 |
| Resume / CV | 履歷 / 履歷表 |
| Salary | 薪資 / 薪酬 |
| Compensation | 薪酬 / 待遇 |
| Skills | 技能 |
| Interview | 面試 |
| Hiring manager | 用人主管 / Hiring manager |
| Recruiter | 招募人員 / 人資 |
| Requirements | 必要條件 / 加分條件 |
| Career history | 工作經歷 |
| Notice period | 離職預告期 |
| Probation | 試用期 |
| Vacation | 特休假 |
| Bonus | 獎金 / 年終獎金 |
| Full-time employment | 正職員工 |
| Contractor | 約聘 / 外包 |
| Annual salary | 年薪制 |
| Health insurance | 健康保險（健保）|
| Overtime pay | 加班費 |
| Commuting allowance | 交通補助 |
| Housing allowance | 住宅補貼 |
| Stock options | 選擇權 / 認股選擇權 |
| Severance | 資遣費 |
| Labor insurance | 勞工保險（勞保）|
| Retirement fund | 退休金 / 勞退 |
| Year-end bonus | 年終獎金 |
| Performance bonus | 績效獎金 |

## 如何貢獻

1. 依 `CONTRIBUTING.md` 開 issue 提案
2. 遵循上方術語表以保持語氣一致
3. 自然慣用的翻譯——不要逐字直譯
4. 結構元素（A-F 區塊、表格、程式碼區塊、工具指示）與原文完全一致
5. 送 PR 前先用台灣的真實職缺（104、CakeResume、Yourator 等）測試
