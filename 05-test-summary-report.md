# Test Summary Report: SauceDemo Web Application

| Field | Value |
|-------|-------|
| Project | SauceDemo Web Testing |
| Report date | 2026-10-14 |
| Tester | Anup Pantha |
| Test period | 2026-10-14 to 2026-10-14 |
| Environment | Windows 11; Chrome 156.0.8078.48, Firefox 158.0 (64-bit), Edge 155.0.4283.45 (64-bit) |
| Test plan | TP-WEB-001 v1.0 |

## 1. Executive summary
Testing covered 14 requirements through 53 test cases. All 53 were executed: 45 passed and 8 failed (84.9% pass rate). The main purchase flow for `standard_user` works (all four smoke tests passed), but 8 defects were found: 2 affecting `standard_user` (checkout allowed with an empty cart; no input validation on checkout fields) and 6 in the special profiles (`problem_user`, `error_user`, `visual_user`, `performance_glitch_user`). There are no Critical defects, but 5 are Major.

**Recommendation: Release with known issues.** The standard purchase path is stable, but the Major defects (BUG-002, 004, 005, 006, 008) should be fixed before the affected users or inputs are exposed in production.

## 2. Test execution metrics

| Metric | Count |
|--------|-------|
| Total test cases | 53 |
| Executed | 53 |
| Passed | 45 |
| Failed | 8 |
| Blocked | 0 |
| Not run | 0 |
| **Pass rate** (Passed / Executed) | 84.9% |
| **Execution rate** (Executed / Total) | 100% |

## 3. Results by module

| Module | Total | Pass | Fail | Blocked |
|--------|-------|------|------|---------|
| Login / Session | 14 | 14 | 0 | 0 |
| Inventory / Sorting | 8 | 6 | 2 | 0 |
| Cart | 9 | 8 | 1 | 0 |
| Checkout | 15 | 12 | 3 | 0 |
| Product detail | 2 | 2 | 0 | 0 |
| UI / Compatibility | 4 | 3 | 1 | 0 |
| Performance | 1 | 0 | 1 | 0 |
| **Total** | **53** | **45** | **8** | **0** |

Module grouping: Login / Session = TC-001 to 014; Inventory / Sorting = TC-015 to 020, 049, 050; Cart = TC-021 to 029; Checkout = TC-030 to 042, 051, 053; Product detail = TC-043, 044; UI = TC-045 to 048; Performance = TC-052.

## 4. Defect summary

| Severity | Open | Fixed/Closed | Total |
|----------|------|--------------|-------|
| Critical | 0 | 0 | 0 |
| Major | 5 | 0 | 5 |
| Minor | 3 | 0 | 3 |
| Trivial | 0 | 0 | 0 |
| **Total** | **8** | **0** | **8** |

Top defects:
1. BUG-008: [Checkout] error_user cannot click Finish, so the order cannot be completed.
2. BUG-006: [Checkout] problem_user: Last Name text goes into the First Name field, blocking checkout.
3. BUG-004: [Inventory] problem_user: all images identical and Add/Remove buttons fail.

Full details: `04-bug-reports.md`.

## 5. Requirement coverage
14 of 14 requirements covered by at least one test case (see `03-requirements-traceability-matrix.md`). Requirements with failures (7): REQ-04, REQ-05, REQ-07, REQ-08, REQ-10, REQ-13, REQ-14. Requirements fully passed (7): REQ-01, REQ-02, REQ-03, REQ-06, REQ-09, REQ-11, REQ-12.

## 6. Browser compatibility
| Browser | Result | Notes |
|---------|--------|-------|
| Chrome | Pass | Primary browser for all test cases |
| Firefox | Pass | Login, add to cart and checkout behaved the same (TC-046) |
| Edge | Pass | Login, add to cart and checkout behaved the same (TC-046) |

## 7. Exit criteria evaluation
| Criterion | Met? |
|-----------|------|
| 100% High priority cases executed | Yes (all 53 cases executed) |
| At least 95% of all cases executed | Yes (100%) |
| No open Critical defects | Yes (0 Critical) |
| All defects logged with evidence | Yes, once the screenshots in `evidence/` are added (8 reports written) |

## 8. Risks, limitations, assumptions
- Requirements derived by exploration (no formal spec).
- Public demo site; behavior may change without notice.
- Accessibility, security and load testing out of scope.
- Exploratory testing was not part of this test cycle; all results come from the 53 scripted test cases.
- Severity and priority are the tester's own judgment, not agreed with a product owner.
- Responsive testing covered 375px width only.

## 9. Recommendations
- Fix the Major defects first: BUG-008 and BUG-006 (checkout cannot be completed), BUG-004 and BUG-005 (inventory), BUG-002 (input validation).
- Block checkout when the cart is empty (BUG-001).
- Investigate the price and layout differences seen by `visual_user` (BUG-003); price differences could mislead customers.
- Reduce inventory load time for `performance_glitch_user` below 3 seconds (BUG-007).
- Next steps: automate smoke + regression with Playwright/Selenium; add accessibility checks.

## 10. Lessons learned
- Comparing every special profile against `standard_user` made defects easy to isolate.
- Writing expected results before execution (with exact error text) made pass/fail decisions fast and objective.
- Several defects were found only by trying unusual input (256 characters, empty cart), which shows the value of error guessing within scripted cases.
- A requirement traceability matrix shows at a glance which features are affected by each defect.
