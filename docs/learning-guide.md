# Learning Guide: how each file in this project was built

This guide explains, file type by file type, how the project was created and why. Read it with the files open next to it.

## 0. The big idea: one source of truth
Your executed spreadsheet (`02-test-cases.xlsx`) is the **single source of truth**. Every number in every other document was calculated from it, never typed from memory:

```
test cases (xlsx/csv)  ->  RTM  ->  bug reports  ->  summary report  ->  README
```

If a test result changes, update the spreadsheet first, then the documents after it. This is what makes a QA project trustworthy.

## 1. `.xlsx` -> `.csv` (02-test-cases)
**Why two formats?** GitHub shows `.csv` files as a readable table in the browser and lets people see changes line by line. `.xlsx` is binary and cannot be previewed or compared. Keep both: CSV for viewing, XLSX for editing.

**How it was done:** a short Python script read the workbook with `openpyxl`, found the header row (`TC ID`) and wrote every row with the `csv` module.

```python
import openpyxl, csv
ws = openpyxl.load_workbook("01-test-cases.xlsx", data_only=True).active
rows = [r for r in ws.iter_rows(values_only=True) if r[0]]
csv.writer(open("02-test-cases.csv", "w", newline="", encoding="utf-8")).writerows(rows)
```

**Check afterwards:** the script counted 53 rows, 45 Pass and 8 Fail. Always count after converting.

## 2. Test plan (`01-test-plan.md`), Markdown
**What it is:** the "contract" written before testing: what is in scope, how you test, and when you can stop.

**How it was built:** each section answers one question a reader asks:

| Section | Question it answers |
|---------|---------------------|
| Objectives, Scope | What are we testing, and what not? |
| Approach | Which techniques? |
| Environment | On what? |
| Entry / Exit criteria | When do we start, when are we done? |
| Defect management | What do severity and priority mean? |
| Risks | What could go wrong? |

The exit criteria in the plan are the same four lines evaluated in section 8 of the summary report. Plan and report must match.

**Markdown basics used:** `#` headings, `| a | b |` tables (second row `|---|---|` is required), `**bold**`, backtick `code`, and ``` fences for templates.

## 3. Requirements Traceability Matrix (`03-...md`)
**What it is:** a table linking each requirement to its test cases and bugs.

**How it was calculated** (the logic you can repeat by hand):
1. Group the 53 test cases by their `Req ID` column.
2. A requirement is **Fail** if any of its test cases failed, otherwise **Pass**.
3. Put the failing test cases' Bug IDs in the Bug IDs column.
4. Build the *reverse trace* (bug -> test case -> requirement) from the same data.

Result: 7 requirements failed, 7 passed, 14 covered. Check: 7 + 7 = 14.

## 4. Bug reports (`04-bug-reports.md`)
**Source:** each bug comes from a **Fail** row: the *Actual Result* column becomes the bug's "Actual result", the *Expected Result* becomes "Expected result", the *Test Steps* become "Steps to reproduce".

**What was added by judgment (review these yourself):**
- **Severity:** how bad is the problem? Blocked purchase for a user group = Major; small visual/validation issue with workaround = Minor.
- **Priority:** how soon to fix? Major -> P2, Minor -> P3.
- **Titles** use the pattern `[Component] what is wrong, for whom`.

**Rules followed:** one bug per report, exact steps, compare with the working case (`standard_user`), describe what you saw and do not guess the cause.

## 5. Test summary report (`05-...md`)
**Every number and how to get it:**

| Number | Formula |
|--------|---------|
| Executed | count of rows with a status = 53 |
| Pass rate | Passed / Executed = 45 / 53 = **84.9%** |
| Execution rate | Executed / Total = 53 / 53 = 100% |
| Results by module | count Pass/Fail per group of the `Module` column (Login + Session are combined, Inventory + Sorting are combined) |
| Defects by severity | count bugs per severity from the defect log |

**Release recommendation logic:** no Critical open defects and the main purchase path works -> *Release with known issues*, but list what must be fixed. A recommendation always needs a reason.

## 6. README.md
The README is the front page of the repository. It answers in 30 seconds: what is this, what were the results, where is everything. Order: title -> one-line description -> results table -> file index -> failures -> how it was done -> status.

## 7. `.github/ISSUE_TEMPLATE/bug_report.md`
GitHub reads this special folder and offers the template whenever someone opens a new issue. The block between `---` lines (front matter) sets the template name, default title and label.

## 8. `.gitignore`
Lists files git should never upload (system junk, Excel temp files).

## 9. Placeholders
While building the documents, details only the tester knows (name, dates, OS, browser versions) were left as `{{TOKENS}}` instead of being invented. They were then replaced with the real values in one pass. Lesson: never guess facts you cannot verify; mark the gap, then fill it with real data.

## 10. Publishing on GitHub (step by step)
1. Create an empty repository on github.com named e.g. `saucedemo-manual-testing` (no README, no .gitignore).
2. Add your screenshots to `evidence/` using the names in `evidence/README.md`.
3. In a terminal inside the project folder:
```bash
git init
git add .
git commit -m "Add SauceDemo test documentation and results"
git branch -M main
git remote add origin https://github.com/<your-username>/saucedemo-manual-testing.git
git push -u origin main
```
4. Open the repo page and check that tables render and the README links work.
5. Optional: copy each bug from `04-bug-reports.md` into GitHub Issues (Issues -> New issue -> Bug report) to show a real defect workflow.
6. Optional: on the repo page add Topics (`manual-testing`, `qa`, `test-cases`, `saucedemo`).
