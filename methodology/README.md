# 公司好壞評估方法論（InvestSkill 歸納）

> 來源：`.investskill/prompts/` 下 34 個框架檔。本資料夾只抽出「判斷一家公司好不好、值不值得買」的方法論，技術面、選擇權、稅務、ETF 等非公司品質框架不納入。
> 僅供學習用途，非投資建議。

---

## 一句話總結

**好公司 = 有護城河 + 財務健康 + 盈餘是真的 + 管理層會分配資本；好投資 = 好公司 + 價格低於內在價值（安全邊際）+ 風險可承受。**

---

## 評估流程（依序執行）

| 步驟 | 問題 | 對應檔案 | 主要來源框架 |
|------|------|----------|--------------|
| 0 | 資料可信嗎？ | [00-data-discipline.md](00-data-discipline.md) | 所有框架共用的 Data & Sources 規則 |
| 1 | 生意好不好？有沒有護城河？ | [01-business-moat.md](01-business-moat.md) | `competitor-analysis`、`stock-eval` |
| 2 | 財務體質健不健康？ | [02-financial-health.md](02-financial-health.md) | `stock-eval`、`fundamental-analysis` |
| 3 | 賺的錢是真的嗎？ | [03-earnings-quality.md](03-earnings-quality.md) | `stock-eval`、`financial-report-analyst` |
| 4 | 管理層可信、會用錢嗎？ | [04-management.md](04-management.md) | `stock-eval`、`dividend-analysis`、`earnings-call-analysis`、`insider-trading` |
| 5 | 現在價格貴不貴？ | [05-valuation.md](05-valuation.md) | `stock-valuation`、`dcf-valuation` |
| 6 | 最壞會怎樣？什麼情況我會錯？ | [06-risk-and-bear-case.md](06-risk-and-bear-case.md) | `bear-case`、`stock-eval` 風險矩陣 |
| 7 | 綜合起來給幾分？買/持有/賣？ | [07-scoring-and-decision.md](07-scoring-and-decision.md) | `full-report`、`stock-screener`、`result-validator` |
| 題材 | 熱門題材的錢會流到誰？現在擠不擠？ | [08-theme-analysis.md](08-theme-analysis.md) | `industry-map`、`sector-analysis`、`thesis-tracker`（含非原生補充） |
| 輸出 | 報告要寫成什麼格式？ | [09-report-format.md](09-report-format.md) | `full-report`、`report-generator`（本專案統一格式） |

**從哪裡開始**：先讀 [workflow.md](workflow.md)（從找候選到追蹤的五階段完整流程）。
快速版：直接看 [checklist.md](checklist.md)（一頁式門檻速查表）。

---

## 方法論的四個核心原則

1. **先品質、後估值**：`full-report` 的流程規定 Phase 1（商業品質）必須先於 Phase 2（估值），因為護城河決定 WACC 與終值成長率的假設。
2. **現金流是真相**：損益表可以被調整，現金流量表最難造假。所有品質判斷最後都回到 CFO、FCF 與淨利的比較。
3. **ROIC vs. WACC 是價值創造的唯一標準**：ROIC > WACC 才是在創造價值；成長但 ROIC < WACC 是在毀滅價值。
4. **每個結論都要有「我錯了的條件」**：每個框架結尾都必須寫 Thesis Invalidation（論點失效條件），並搭配 `bear-case` 做反方壓力測試。

---

## 評分體系一覽

| 評分 | 範圍 | 用途 | 所在檔案 |
|------|------|------|----------|
| Piotroski F-Score | 0–9 | 財務體質改善程度 | 03 |
| Accounting Quality Score | 0–21 | 會計品質 | 03 |
| Composite Moat Score | 0–10 | 護城河強度 | 01 |
| Five Forces 產業吸引力 | 1–5 | 產業結構 | 01 |
| Capital Allocation Quality Score | 0–10 | 管理層資本配置 | 04 |
| Dividend Safety Score | 0–100 | 股利安全性 | 04 |
| Margin of Safety | % | 價格 vs. 內在價值 | 05 |
| Bear Case Strength | 0–10 | 反方論點強度（越高越糟） | 06 |
| Full Report Composite | 0–10 | 最終綜合分數 | 07 |
| Confidence Score | 0–100 | 分析本身可信度 | 07 |
| Bottleneck Score | 0–10 | 供應鏈某層的瓶頸力量 | 08 |
| Sector Composite Rank | 1–11 | 產業動能排名 | 08 |
| Thesis Health Score | 0–10 | 題材 / 個股論點是否仍成立 | 08 |
