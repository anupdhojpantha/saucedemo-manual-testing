# Test Plan: SauceDemo Web Application

| Field | Value |
|-------|-------|
| Test plan ID | TP-WEB-001 |
| Version | 1.0 |
| Author | Anup Pantha |
| Date | 2026-10-14 |
| Application under test | https://www.saucedemo.com (public practice site by Sauce Labs) |

## 1. Introduction
This plan describes how the SauceDemo e-commerce web application is tested manually. The goal is to confirm that the main shopping journey (login, browse, cart, checkout) works correctly and to find defects in the special user profiles the site provides.

## 2. Objectives
- Verify the core user journey works end to end: login -> browse -> add to cart -> checkout -> order confirmation.
- Verify validation and error messages on the login and checkout forms.
- Verify the behavior of all six test user profiles.
- Check basic UI, responsive layout and cross-browser consistency.
- Provide traceability from requirements to test cases to defects.

## 3. Scope

### In scope
| Area | Requirement IDs |
|------|-----------------|
| Login and error messages, locked-out user | REQ-01, REQ-02, REQ-03 |
| Product inventory display and sorting | REQ-04, REQ-05 |
| Add / remove items, cart management | REQ-06, REQ-07 |
| Checkout form validation, order overview, order completion | REQ-08, REQ-09, REQ-10 |
| Session handling | REQ-11 |
| Product detail page | REQ-12 |
| UI, menu, responsive layout (375px), cross-browser | REQ-13 |
| Basic performance (page load of inventory) | REQ-14 |

### Out of scope
- Load, stress and penetration testing.
- Formal accessibility audit (WCAG).
- Backend, API and database testing.
- Real payment processing (the site has none).

## 4. Test approach
| Technique | How it is used |
|-----------|----------------|
| Functional testing | Positive flows for every feature |
| Negative testing | Invalid, empty and wrong input on forms |
| Boundary / error guessing | 256-character input, special characters, spaces, empty cart |
| User-profile testing | Same journey with each of the six profiles, compared against `standard_user` |
| UI and compatibility | 375px width, Chrome, Firefox and Edge |
| Performance (basic) | Chrome DevTools Lighthouse / Performance panel for `performance_glitch_user` |

Test design techniques used: equivalence partitioning, boundary value analysis, error guessing, state-based checks (cart persistence).

## 5. Test environment
| Item | Value |
|------|-------|
| Operating system | Windows 11 |
| Browsers | Chrome 156.0.8078.48, Firefox 158.0 (64-bit), Edge 155.0.4283.45 (64-bit) |
| Tools | Chrome DevTools, Excel / Google Sheets, GitHub Issues, screen recorder |
| Test accounts | `standard_user`, `locked_out_user`, `problem_user`, `performance_glitch_user`, `error_user`, `visual_user` (password for all: `secret_sauce`) |

## 6. Test deliverables
| File | Purpose |
|------|---------|
| `01-test-plan.md` | This document |
| `02-test-cases.csv` / `02-test-cases.xlsx` | 53 executed test cases |
| `03-requirements-traceability-matrix.md` | Requirement -> test case -> bug mapping |
| `04-bug-reports.md` | Eight confirmed defect reports |
| `05-test-summary-report.md` | Results, metrics, release recommendation |

## 7. Entry criteria
- Application is reachable at the URL above.
- All six test accounts can be used.
- Test cases are written and reviewed.
- Supported browsers are installed.

## 8. Exit criteria
- 100% of High priority test cases executed.
- At least 95% of all test cases executed.
- No open Critical defects.
- All defects logged with evidence.

## 9. Defect management
**Severity**
| Level | Meaning |
|-------|---------|
| Critical | Core function broken for all users, no workaround, or data/security loss |
| Major | Important function broken or blocked for a user group |
| Minor | Small functional or visual problem with an easy workaround |
| Trivial | Cosmetic issue with no effect on use |

**Priority:** P1 (fix immediately), P2 (fix before release), P3 (fix when possible), P4 (backlog).

**Lifecycle:** New -> Open -> In Progress -> Fixed -> Retest -> Closed (or Reopened / Rejected).

## 10. Risks and mitigations
| Risk | Mitigation |
|------|------------|
| No formal requirements document | Requirements derived by exploring the application |
| Public site may change without notice | Record date and browser versions; keep evidence |
| Special profiles behave unpredictably | Compare each profile against `standard_user` |
| Browser differences | Run smoke tests in three browsers |

## 11. Roles
| Role | Person |
|------|--------|
| Test designer, executor, reporter | Anup Pantha |

## 12. Schedule
| Activity | Date |
|----------|------|
| Exploration and planning | 2026-10-14 |
| Test case execution | 2026-10-14 to 2026-10-14 |
| Reporting | 2026-10-14 |
