---
name: equity-analysis
description: >-
  Runs the methodology stock-analysis funnel and writes an analysis/ report.
  Use when the user asks to 分析個股 or write a single-stock report, to 更新報告,
  or to 快篩 a name before a deep dive.
---

# Equity analysis

The funnel, the scores, and the report skeleton already live in `methodology/`. This skill picks the branch and sequences the reads. Apply each file in place.

A required score is **做完** when it is a number from this fetch. `未評估` is 做完 only under `methodology/09-report-format.md` §1.2: the primary document is not public as of `As of`. Valuation is 做完 when every method in `05-valuation.md` §5 that has a public source has a low, a mid, a high, and a weight.

A request that names a framework listed in `.cursor/rules/investskill.mdc` follows that rule.

## 1. Pick the branch

| Signal | Branch |
|--------|--------|
| One named company, and the user wants a report | Deep dive |
| User says 更新報告 | Update |
| User says 快篩 or 找候選, or has not named one company | Screen |

Done when exactly one branch is selected.

## 2. Deep dive

1. Read `methodology/00-data-discipline.md`. Re-fetch the latest public data in **新鮮度** bullet 1. Done when that fetch is in hand.
2. Read `01-business-moat.md`, `02-financial-health.md`, `03-earnings-quality.md`, `04-management.md`, in that order. Done when each file's required scores are 做完.
3. Read `05-valuation.md` and `06-risk-and-bear-case.md`. Done when margin of safety, risk/reward, bear-case strength, and the §5 methods are 做完.
4. Read `07-scoring-and-decision.md`. Read `08-theme-analysis.md` only when the thesis is a theme. Done when the composite score and the decision (買進 / 觀察 / 放棄) are set.
5. Read `methodology/09-report-format.md`. Copy the §5 skeleton into the §2 path. Set `Produced` to the date the file is written. The price as-of date goes in `As of`. Done when every numbered section in that skeleton is present.
6. Build the price-volume chart from this fetch's daily K and volume, following `methodology/09-report-format.md` §7. Save it at the §2 image path and fill the `### 關鍵數據補充：價量疊圖` subsection. Done when the image path in the report opens, the image date equals `As of`, and every plotted number sits in the subsection table with its source tag.

## 3. Update

`更新報告` reruns workflow stages 0, 3, 4, and 5 for that company. That is the deep-dive read above, including 新鮮度. Stages 1–2 stay on the screen branch. `workflow.md` calls this 重跑.

One company has one file, the §2 path in `methodology/09-report-format.md`.

1. Run the deep-dive reads, including the chart step.
2. Overwrite that same path, and delete the previous chart image so the company keeps one image.

Done when every 新鮮度 bullet holds on that path, every required score is 做完, and the chart subsection matches the new `As of`.

## 4. Screen

1. Read stages 1–2 of `methodology/workflow.md` and sections B and C of `methodology/checklist.md`.
2. State each name as kept, or name the one kill condition from the checklist.

Done when every name is kept or killed. A screen does not write a 09 report.

## 5. Deliver

Run §6 in `methodology/09-report-format.md` on the file just written. Done when every §6 box passes. Fix the file until it does.
