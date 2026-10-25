# SauceDemo Web Application Testing

Manual functional, UI and compatibility testing of an e-commerce web app, with a complete QA document set: test plan, test cases, traceability matrix, bug reports and test summary report.

- **Application under test:** https://www.saucedemo.com (public practice site by Sauce Labs)
- **Test accounts:** `standard_user`, `locked_out_user`, `problem_user`, `performance_glitch_user`, `error_user`, `visual_user` (password for all: `secret_sauce`)
- **Tools:** Chrome DevTools, Excel/Google Sheets, GitHub Issues, screen recorder
- **Browsers:** Chrome, Firefox, Edge

## Results at a glance

| Metric | Result |
|--------|--------|
| Requirements covered | 14 / 14 |
| Test cases executed | 53 / 53 (100%) |
| Passed / Failed / Blocked | 45 / 8 / 0 |
| Pass rate | 84.9% |
| Defects logged | 8 (0 Critical, 5 Major, 3 Minor) |
| Recommendation | Release with known issues |

**Most interesting defect:** BUG-008, `error_user` cannot click Finish, so the order cannot be completed.

## Deliverables

| File | Purpose |
|------|---------|
| [01-test-plan.md](./01-test-plan.md) | Scope, strategy, risks, environment, entry/exit criteria |
| [02-test-cases.csv](./02-test-cases.csv) | 53 executed test cases with actual results (also as [02-test-cases.xlsx](./02-test-cases.xlsx)) |
| [03-requirements-traceability-matrix.md](./03-requirements-traceability-matrix.md) | Requirements mapped to test cases and bugs |
| [04-bug-reports.md](./04-bug-reports.md) | 8 confirmed bug reports |
| [05-test-summary-report.md](./05-test-summary-report.md) | Results, metrics, release recommendation |
| [evidence/](./evidence) | Screenshots and videos for each bug |
| [docs/learning-guide.md](./docs/learning-guide.md) | How each document type was built and how to publish on GitHub |

## Failed test cases

| Bug | Test case | User | Summary | Severity |
|-----|-----------|------|---------|----------|
| BUG-001 | TC-029 | standard_user | Checkout opens with an empty cart | Minor |
| BUG-002 | TC-035 | standard_user | Checkout accepts 256+ chars and special characters | Major |
| BUG-003 | TC-048 | visual_user | Wrong image, misaligned titles, different prices | Minor |
| BUG-004 | TC-049 | problem_user | Identical images, Add/Remove buttons fail | Major |
| BUG-005 | TC-050 | problem_user | Sorting does nothing | Major |
| BUG-006 | TC-051 | problem_user | Last Name goes into First Name | Major |
| BUG-007 | TC-052 | performance_glitch_user | Inventory LCP 5.06 s (expected under 3 s) | Minor |
| BUG-008 | TC-053 | error_user | Finish button cannot be clicked | Major |

## How the testing was done

1. Explored the app as a normal user.
2. Wrote 53 test cases across 14 requirements, then executed them in this order: smoke (TC-001, 021, 030, 041), functional, negative, UI, user-profile cases (TC-049 to 053).
3. Captured evidence for every failure and wrote a bug report.
4. Traced every defect back to a requirement in the RTM.
5. Compiled metrics and a release recommendation in the summary report.

## Status

- [x] Test cases executed
- [x] Bugs logged
- [ ] Evidence screenshots added to `evidence/`
- [x] Summary report completed

## Evidence

Screenshots are stored in [`evidence/`](./evidence) named after the bug ID (for example `BUG-004.png`).
