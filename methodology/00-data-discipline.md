# 00 — 資料紀律（所有分析的前提）

> 來源：每個框架檔開頭的 `Data Verification` 與 `Data & Sources Header`；`result-validator` 的合約檢查。

資料錯，後面全錯。InvestSkill 把資料紀律寫成強制規則。

## 規則

1. **現價一定要即時取得**：不可用模型記憶中的價格。拿不到就明確警告「Live data unavailable」。
2. **每份輸出開頭都要有資料來源區塊**：

```
Data & Sources
  As of:      <數據所代表的日期>
  Source:     <SEC EDGAR 10-K/10-Q、公司 IR、FRED、交易所…>
  Retrieval:  <pasted by user | web/tool retrieval | model memory>
  Confidence: <HIGH | MEDIUM | LOW>
```

3. `Retrieval: model memory` **必須**搭配 `Confidence: LOW`。
4. 多來源不可混在一起，各自標 as-of 日期。
5. 超過 90 天的資料要明確警告。

## 新鮮度

新增或覆蓋 `analysis/` 個股報告時，先重新抓取網路上目前最新的公開資料，再依這次抓取改寫整份內容。來源順序用下方優先表。

完成條件，全部成立才算寫完：

1. 這次抓取包含現價、最新財報、公司有公布時的最新月營收、最新一場法說、若另有召開的最新財報會議，以及截至寫入日已公開且會影響論點的新聞。
2. 報告裡每個數字都來自這次抓取，並帶該次的 as-of 日期與來源；拿不到的標 `未評估`。
3. `Produced` 是這次寫入日期。`As of` 的股價日期是這次現價的日期。法說、財報會議、每則採用的新聞都在 Source 標日期。
4. 法說、財報會議、新聞的敘述都來自這次抓到的最新一場與最新事件。留下的每一句既有文字，這次來源仍然支持它。來源已經不同的句子，改成與這次抓取一致。

## 資料來源優先順序

| 優先 | 來源 | 用途 |
|------|------|------|
| 1 | 10-K / 10-Q / 8-K / DEF 14A（SEC EDGAR） | 財報、風險因子、附註、管理層薪酬 |
| 2 | 公司 IR、法說會逐字稿 | 指引、管理層語氣 |
| 3 | Form 4、13F | 內部人、機構持股 |
| 4 | 資料終端、分析師共識 | 交叉比對 |

## 為什麼重要

`result-validator` 會先檢查三件事是否存在：Data & Sources 區塊、Thesis Invalidation、Investment Signal 區塊。缺 Data & Sources 時，Data Quality 最高只能拿 10/20。
