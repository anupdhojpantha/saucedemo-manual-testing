# Bug Reports

Eight defects were found and confirmed during execution of the 53 test cases. Each report follows the same template. Severity and priority are the tester's assessment (see `01-test-plan.md`, section 9).

Environment for all bugs: Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com

## Defect log summary

| Bug ID | Title | Severity | Priority | Status | TC | Req |
|--------|-------|----------|----------|--------|----|-----|
| BUG-001 | [Cart] Checkout can be started with an empty cart | Minor | P3 | New | TC-029 | REQ-07 |
| BUG-002 | [Checkout] Form accepts 256+ characters and special characters without validation | Major | P2 | New | TC-035 | REQ-08 |
| BUG-003 | [UI] visual_user sees wrong image, misaligned titles and different prices | Minor | P3 | New | TC-048 | REQ-13 |
| BUG-004 | [Inventory] problem_user: all product images identical and Add/Remove buttons fail | Major | P2 | New | TC-049 | REQ-04 |
| BUG-005 | [Inventory] problem_user: sorting does not reorder products | Major | P2 | New | TC-050 | REQ-05 |
| BUG-006 | [Checkout] problem_user: Last Name text goes into First Name field | Major | P2 | New | TC-051 | REQ-08 |
| BUG-007 | [Performance] performance_glitch_user: inventory loads in about 5 s (LCP 5.06 s) | Minor | P3 | New | TC-052 | REQ-14 |
| BUG-008 | [Checkout] error_user: Finish button cannot be clicked, order cannot be completed | Major | P2 | New | TC-053 | REQ-10 |

---

## BUG-001

```
Bug ID:        BUG-001
Title:         [Cart] Checkout can be started with an empty cart
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-029              Requirement: REQ-07
Severity:      Minor
Priority:      P3
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: standard_user

Preconditions:
  - Logged in as standard_user / secret_sauce
  - Cart is empty (all items removed)

Steps to reproduce:
  1. Click the cart icon.
  2. Click Checkout.

Expected result:
  The system blocks checkout or shows a warning that the cart is empty.

Actual result:
  The checkout form (step one) opens and no warning is shown.

Reproducibility: Always
Evidence: evidence/BUG-001.png
Notes / workaround: The user can continue through checkout with nothing in the cart.
```

## BUG-002

```
Bug ID:        BUG-002
Title:         [Checkout] Form accepts 256+ characters and special characters without validation
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-035              Requirement: REQ-08
Severity:      Major
Priority:      P2
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: standard_user

Preconditions:
  - Logged in as standard_user with at least one item in the cart
  - On Checkout: Your Information (step one)

Steps to reproduce:
  1. Enter a 256-character string in First Name.
  2. Enter <script>alert(1)</script> in Last Name.
  3. Enter !@#$% in Postal Code.
  4. Click Continue.

Expected result:
  Input is handled or rejected gracefully (length limit and/or validation message); no script execution.

Actual result:
  The form accepted all values and moved to Checkout: Overview (step two). No length limit or validation was applied.

Reproducibility: Always
Evidence: evidence/BUG-002.png
Notes / workaround: Valid input (TC-030) works. Missing input validation is a quality and security-hygiene risk.
```

## BUG-003

```
Bug ID:        BUG-003
Title:         [UI] visual_user sees wrong image, misaligned titles and different prices
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-048              Requirement: REQ-13
Severity:      Minor
Priority:      P3
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: visual_user

Preconditions:
  - Login page open

Steps to reproduce:
  1. Log in as visual_user / secret_sauce.
  2. Compare the Products page with the same page as standard_user.

Expected result:
  No visual differences from standard_user.

Actual result:
  - The image for Sauce Labs Backpack is wrong.
  - Product title text alignment differs from standard_user.
  - Prices differ from those shown to standard_user.

Reproducibility: Always
Evidence: evidence/BUG-003.png (side-by-side with standard_user)
Notes / workaround: Price differences can mislead customers, so the pricing part may deserve a higher severity if confirmed as unintended.
```

## BUG-004

```
Bug ID:        BUG-004
Title:         [Inventory] problem_user: all product images identical and Add/Remove buttons fail
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-049              Requirement: REQ-04
Severity:      Major
Priority:      P2
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: problem_user

Preconditions:
  - Login page open

Steps to reproduce:
  1. Log in as problem_user / secret_sauce.
  2. Look at the product images.
  3. Click Add to cart on each product, then try Remove.

Expected result:
  Each product shows its own image; every Add to cart and Remove button works.

Actual result:
  - All products show the same image.
  - Add to cart does not work for more than two products.
  - The Remove button cannot be clicked.

Reproducibility: Always
Evidence: evidence/BUG-004.png
Notes / workaround: standard_user behaves correctly (TC-015, TC-016, TC-021 to TC-024 passed). This report covers two symptoms found in one test case; they can be split into two issues if the developers prefer one bug per report.
```

## BUG-005

```
Bug ID:        BUG-005
Title:         [Inventory] problem_user: sorting does not reorder products
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-050              Requirement: REQ-05
Severity:      Major
Priority:      P2
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: problem_user

Preconditions:
  - Logged in as problem_user / secret_sauce

Steps to reproduce:
  1. On the Products page open the sort dropdown (top right).
  2. Select each option in turn (Name A-Z, Name Z-A, Price low-high, Price high-low).

Expected result:
  Products are reordered according to the selected option.

Actual result:
  The product order does not change for any option.

Reproducibility: Always
Evidence: evidence/BUG-005.png
Notes / workaround: standard_user sorts correctly (TC-017 to TC-020 passed).
```

## BUG-006

```
Bug ID:        BUG-006
Title:         [Checkout] problem_user: Last Name text goes into First Name field
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-051              Requirement: REQ-08
Severity:      Major
Priority:      P2
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: problem_user

Preconditions:
  - Logged in as problem_user with one item in the cart

Steps to reproduce:
  1. Click the cart icon, then Checkout.
  2. Type Jane in First Name, Doe in Last Name, 27701 in Postal Code.
  3. Click Continue.

Expected result:
  All values are accepted as typed and checkout continues.

Actual result:
  The Last Name text is entered into the First Name field, leaving Last Name empty. Clicking Continue shows "Error: Last Name is required".

Reproducibility: Always
Evidence: evidence/BUG-006.png
Notes / workaround: With standard_user the same steps succeed (TC-030 passed). The problem_user cannot place an order.
```

## BUG-007

```
Bug ID:        BUG-007
Title:         [Performance] performance_glitch_user: inventory loads in about 5 s (LCP 5.06 s)
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-052              Requirement: REQ-14
Severity:      Minor
Priority:      P3
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: performance_glitch_user

Preconditions:
  - Login page open

Steps to reproduce:
  1. Log in as performance_glitch_user / secret_sauce.
  2. Measure the time until the inventory page loads (Chrome DevTools).

Expected result:
  Inventory page loads within 3 seconds.

Actual result:
  Largest Contentful Paint (LCP) was 5.06 s and Interaction to Next Paint (INP) was 5,040 ms, both above the 3-second expectation.

Reproducibility: Always
Evidence: evidence/BUG-007.png (DevTools performance results)
Notes / workaround: The page works, only slowly.
```

## BUG-008

```
Bug ID:        BUG-008
Title:         [Checkout] error_user: Finish button cannot be clicked, order cannot be completed
Reported by:   Anup Pantha          Date: 2026-10-14
Related TC:    TC-053              Requirement: REQ-10
Severity:      Major
Priority:      P2
Status:        New
Environment:   Windows 11, Chrome 156.0.8078.48, https://www.saucedemo.com, user: error_user

Preconditions:
  - Login page open

Steps to reproduce:
  1. Log in as error_user / secret_sauce.
  2. Add an item to the cart and open the cart.
  3. Click Checkout.
  4. Enter First Name, Last Name and Postal Code, then click Continue.
  5. On the overview page click Finish.

Expected result:
  Checkout completes and the confirmation page appears.

Actual result:
  The Finish button cannot be clicked, so the order cannot be completed.

Reproducibility: Always
Evidence: evidence/BUG-008.png
Notes / workaround: standard_user completes checkout (TC-041 passed). Severity is Major because the purchase is blocked, but only for this profile.
```
