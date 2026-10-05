# 個股分析報告

用固定漏斗判斷一家公司值不值得買，並把結果寫成可逐節對照的報告。一家公司一份檔，放在 `analysis/`。同一次寫入也產出一張價量疊圖，放在 `analysis/img/`。

僅供學習用途，非投資建議。

## 產出一份報告

在這個專案的對話裡直接說：

| 你說 | 結果 | 大約時間 |
|------|------|----------|
| `分析 2330` | 深入研究，寫入 `analysis/2330_TSMC.md`，並畫價量疊圖 | 一次完整報告 |
| `更新 2330 報告` | 重抓公開資料，覆蓋同一檔、換掉舊圖 | 重跑估值與決策 |
| `快篩 2308、2454` | 每檔留下或淘汰，不寫報告、不畫圖 | 每檔約 15 分鐘的判斷 |

檔名固定為：

- 報告：`analysis/{股票代號}_{英文簡稱}.md`（股價日期寫在報告開頭，不寫進檔名）
- 圖：`analysis/img/{股票代號}_price_volume_overlay_{YYYY-MM-DD}.png`（日期 = 開頭 `As of` 的股價日期）

重跑覆蓋同一份報告；新圖產生後刪除舊圖，一家公司只留一張。執行順序在 [`.cursor/skills/equity-analysis/SKILL.md`](.cursor/skills/equity-analysis/SKILL.md)。寫入前會重抓最新公開資料（含日 K、成交量、分價量）；寫完會依 [`methodology/09-report-format.md`](methodology/09-report-format.md) §6 自查，分數或缺圖就不算完成。

## 報告裡有什麼

開頭先給結論，後面章節編號固定。不適用的章節保留標題，內文寫「不適用：原因」。

1. **結論先講**：好公司？好價格？綜合分數、建議動作、最大風險
2. **關鍵數據**：股價、市值、倍數、營收結構；其下固定小節「價量疊圖」（不佔編號）
3. **快篩**：五條硬門檻，任一條觸發就淘汰
4. **深入研究**：護城河、財務體質、盈餘品質、管理層
5. **估值與反方**：DCF、三情境、安全邊際、bear case
6. **決策**：綜合分數、進場價、3–5 個 KPI、論點失效條件
7. **同業比較**與**本次未驗證 / 待補**

價量疊圖畫：日 K、成交量、72 日分價量（POC / VA20）、SMA20、SMA60。不畫收盤線、SMA120、SMA240。K 線與成交量標【官方】，分價量（富邦 DJ 等同源頁）標【二手】。圖不產生買賣價位，結論不寫進「結論先講」。規格在 [`methodology/09-report-format.md`](methodology/09-report-format.md) §7。

來源分四級：【一手】公司文件、【官方】交易所、【二手】券商與資料商、【缺件】取不到。見 [`methodology/00-data-discipline.md`](methodology/00-data-discipline.md) 規則 6。

金額用 NT$億，日期用 `YYYY-MM-DD`。範本見 [`analysis/2330_TSMC.md`](analysis/2330_TSMC.md)（含價量疊圖與富邦 DJ 二手補件）。

## 怎麼下決定

好公司 = 有護城河 + 財務健康 + 盈餘是真的 + 管理層會分配資本。
好投資 = 好公司 + 價格低於內在價值 + 風險可承受。

| 綜合分數 | 動作 |
|----------|------|
| ≥ 6.5，且安全邊際達標 | 買進 |
| 5.0–6.4 | 觀察名單 |
| < 5.0 | 放棄 |

安全邊際門檻：價值型 25–35%、GARP 10–20%、成長型 0–10%。Bear case 強度要 ≤ 4.0，風險報酬比要 ≥ 3:1，才算價格過關。

完整漏斗在 [`methodology/workflow.md`](methodology/workflow.md)。一頁門檻在 [`methodology/checklist.md`](methodology/checklist.md)。

## 目錄

| 路徑 | 用途 |
|------|------|
| [`methodology/workflow.md`](methodology/workflow.md) | 五階段流程：找候選 → 快篩 → 深入研究 → 估值 → 決策 |
| [`methodology/00-data-discipline.md`](methodology/00-data-discipline.md) | 資料來源、四級標示、新鮮度 |
| [`methodology/01-business-moat.md`](methodology/01-business-moat.md) … [`08-theme-analysis.md`](methodology/08-theme-analysis.md) | 各關的算法與分數 |
| [`methodology/09-report-format.md`](methodology/09-report-format.md) | 報告骨架、必填分數、價量疊圖規格、交付自查 |
| [`methodology/README.md`](methodology/README.md) | 方法論索引與評分一覽 |
| [`analysis/`](analysis/) | 已產出的個股報告 |
| [`analysis/img/`](analysis/img/) | 報告引用的價量疊圖 |

已有報告：

| 代號 | 公司 | 檔案 | 價量疊圖 |
|------|------|------|----------|
| 2330 | 台積電 | [`analysis/2330_TSMC.md`](analysis/2330_TSMC.md) | 有（As of 2026-10-02） |
| 2308 | 台達電 | [`analysis/2308_Delta.md`](analysis/2308_Delta.md) | 下次重跑補上 |
| 2449 | 京元電子 | [`analysis/2449_KYEC.md`](analysis/2449_KYEC.md) | 下次重跑補上 |
| 2454 | 聯發科 | [`analysis/2454_MediaTek.md`](analysis/2454_MediaTek.md) | 有（As of 2026-10-02） |
| 3037 | 欣興電子 | [`analysis/3037_Unimicron.md`](analysis/3037_Unimicron.md) | 下次重跑補上 |
| 3711 | 日月光投控 | [`analysis/3711_ASE.md`](analysis/3711_ASE.md) | 下次重跑補上 |

2026-10-04 以前寫成、還沒有價量疊圖的報告，下次 `更新 … 報告` 時補上。

## 改規則時改哪裡

| 要改的事 | 改這個檔 |
|----------|----------|
| 報告章節、單位、必填分數 | `methodology/09-report-format.md` |
| 圖上畫什麼、圖檔名、缺件寫法 | `methodology/09-report-format.md` §7 |
| 來源分級與寫入前要重抓什麼 | `methodology/00-data-discipline.md` |
| 漏斗階段或淘汰條件 | `methodology/workflow.md`、`methodology/checklist.md` |
| 某一關怎麼打分 | `methodology/01` 到 `08` 對應檔 |

## 美股與其他框架

`.investskill/prompts/` 另有 34 個美股框架（估值、財報、技術面、ETF、投組等）。對話點名其中一種分析時，會讀對應框架來寫。這個專案的主產出仍是上面的台股個股報告。
