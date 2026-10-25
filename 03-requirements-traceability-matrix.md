# Requirements Traceability Matrix (RTM)

Purpose: prove every requirement has test coverage and trace every defect back to a requirement.

| Req ID | Requirement | Test Case IDs | # Cases | Bug IDs | Status |
|--------|-------------|---------------|---------|---------|--------|
| REQ-01 | Login with valid credentials | TC-001 | 1 | | Pass |
| REQ-02 | Login validation and error messages | TC-002, 003, 004, 005, 006, 007, 008, 009, 010 | 9 | | Pass |
| REQ-03 | Locked-out user handling | TC-011 | 1 | | Pass |
| REQ-04 | Product inventory display | TC-015, 016, 049 | 3 | BUG-004 | Fail |
| REQ-05 | Product sorting | TC-017, 018, 019, 020, 050 | 5 | BUG-005 | Fail |
| REQ-06 | Add / remove items (inventory page) | TC-021, 022, 023, 024 | 4 | | Pass |
| REQ-07 | Shopping cart management | TC-025, 026, 027, 028, 029 | 5 | BUG-001 | Fail |
| REQ-08 | Checkout form validation | TC-030, 031, 032, 033, 034, 035, 036, 051 | 8 | BUG-002, BUG-006 | Fail |
| REQ-09 | Order overview calculations | TC-037, 038, 039, 040 | 4 | | Pass |
| REQ-10 | Order completion | TC-041, 042, 053 | 3 | BUG-008 | Fail |
| REQ-11 | Session handling | TC-012, 013, 014 | 3 | | Pass |
| REQ-12 | Product detail page | TC-043, 044 | 2 | | Pass |
| REQ-13 | UI, menu, responsive, cross-browser | TC-045, 046, 047, 048 | 4 | BUG-003 | Fail |
| REQ-14 | Basic performance | TC-052 | 1 | BUG-007 | Fail |

**Total:** 14 requirements, 53 test cases, 100% requirement coverage by design.

Status rule: a requirement is **Pass** only if every linked test case passed; one failed case makes it **Fail**.

## Coverage check
- Requirements with at least one test case: 14 / 14
- Requirements with a failed case: 7 (REQ-04, 05, 07, 08, 10, 13, 14)
- Requirements fully passed: 7 (REQ-01, 02, 03, 06, 09, 11, 12)

## Reverse trace (defect -> test case -> requirement)
| Bug ID | Found in Test Case | Requirement |
|--------|--------------------|-------------|
| BUG-001 | TC-029 | REQ-07 |
| BUG-002 | TC-035 | REQ-08 |
| BUG-003 | TC-048 | REQ-13 |
| BUG-004 | TC-049 | REQ-04 |
| BUG-005 | TC-050 | REQ-05 |
| BUG-006 | TC-051 | REQ-08 |
| BUG-007 | TC-052 | REQ-14 |
| BUG-008 | TC-053 | REQ-10 |
