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

## 資料來源優先順序

| 優先 | 來源 | 用途 |
|------|------|------|
| 1 | 10-K / 10-Q / 8-K / DEF 14A（SEC EDGAR） | 財報、風險因子、附註、管理層薪酬 |
| 2 | 公司 IR、法說會逐字稿 | 指引、管理層語氣 |
| 3 | Form 4、13F | 內部人、機構持股 |
| 4 | 資料終端、分析師共識 | 交叉比對 |

## 為什麼重要

`result-validator` 會先檢查三件事是否存在：Data & Sources 區塊、Thesis Invalidation、Investment Signal 區塊。缺 Data & Sources 時，Data Quality 最高只能拿 10/20。
