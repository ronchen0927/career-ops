# 模式: pipeline -- URL 收件匣（Second Brain）

處理累積在 `data/pipeline.md` 的職缺 URL。候選人隨時可以新增 URL，之後執行 `/career-ops pipeline` 批次處理。

## 工作流程

1. **讀取** `data/pipeline.md` → 找出「待處理」區塊中的 `- [ ]` 項目
2. **對每個待處理 URL：**
   a. 計算下一個 `REPORT_NUM`（讀 `reports/`，最大號碼 + 1）
   b. **擷取 JD**：Playwright（browser_navigate + browser_snapshot）→ WebFetch → WebSearch
   c. 若 URL 無法存取 → 標記為 `- [!]` 並備注，繼續下一個
   d. **執行完整 auto-pipeline**：評估 A-F → 報告 .md → PDF（分數 >= 3.0）→ Tracker
   e. **從「待處理」移到「已處理」**：`- [x] #NNN | URL | 公司名 | 職位名稱 | 分數/5 | PDF ✅/❌`
3. **若有 3 個以上 URL**，用 Agent tool 並行啟動（`run_in_background`）加速。
4. **完成後**，顯示摘要表格：

```
| # | 公司 | 職位 | 分數 | PDF | 建議行動 |
```

## pipeline.md 格式

```markdown
## 待處理
- [ ] https://jobs.example.com/posting/123
- [ ] https://boards.greenhouse.io/company/jobs/456 | 公司名 | 資深 PM
- [!] https://private.url/job — 錯誤: 需要登入

## 已處理
- [x] #143 | https://jobs.example.com/posting/789 | Acme Corp | AI PM | 4.2/5 | PDF ✅
- [x] #144 | https://boards.greenhouse.io/xyz/jobs/012 | BigCo | SA | 2.1/5 | PDF ❌
```

> 注：區塊標題可使用 EN（"Pending"/"Processed"）、ES（"Pendientes"/"Procesadas"）、DE（"Offen"/"Verarbeitet"）、JA（"未処理"/"処理済み"）或 ZH-TW（「待處理」/「已處理」）。讀取時彈性處理，寫入時維持現有格式。

## 從 URL 智慧偵測 JD

1. **Playwright（優先）：** `browser_navigate` + `browser_snapshot`。支援所有 SPA。
2. **WebFetch（備援）：** 靜態頁面，或 Playwright 不可用時。
3. **WebSearch（最後手段）：** 在二手求職平台搜尋 JD。

**特殊情況：**
- **LinkedIn**：可能需要登入 → 標記為 `[!]`，請候選人貼上文字
- **PDF**：URL 指向 PDF，用 Read tool 直接讀取
- **`local:` 前綴**：讀取本機檔案。例：`local:jds/104-pm-ai.md` → 讀取 `jds/104-pm-ai.md`
- **104 人力銀行**：台灣最大求職平台。Playwright 可存取，但需注意防爬蟲機制；若失敗改用 WebFetch
- **CakeResume (Cake.me)**：台灣新創友善平台。Playwright 或 WebFetch 可存取
- **Yourator**：新創職缺平台。通常 WebFetch 可存取
- **Meet.jobs**：國際求職平台，包含台灣職缺。WebFetch 可存取
- **1111 人力銀行**：可能需要登入 → 嘗試 WebFetch，失敗則標記 `[!]`
- **LinkedIn TW**：與全球 LinkedIn 相同限制——可能需要登入

## 自動編號

1. 列出 `reports/` 中所有檔案
2. 從前綴擷取號碼（例：`142-medispend...` → 142）
3. 新號碼 = 找到的最大值 + 1

## 來源同步

處理 URL 前先確認同步：

```bash
node cv-sync-check.mjs
```

若有不同步，在繼續前告知候選人。
