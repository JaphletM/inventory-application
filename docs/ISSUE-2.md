# ISSUE-2.md

## Title

Filter active products by stock status

## User Story

As an Inventory Employee, I want to filter active products by stock status so that I can focus on products needing stock attention.

Acceptance criteria:
- Given active products have different stock quantities, when the employee filters by stock status, then only active products with that derived status are shown.
- Given inactive products have the requested stock status, when filtering is applied, then inactive products are still excluded.
- Given an invalid stock-status filter is provided, when the query is validated, then the application reports the invalid filter clearly.

## Functions

The implementation should expose or use these function contracts:
- `validate_stock_status_filter(status)`: accepts only supported stock-status filter values at the boundary.
- `determine_stock_status(stock_quantity)`: shared pure domain function from ISSUE-1.
- `attach_stock_status(products)`: shared transformation from ISSUE-1.
- `filter_active_products(products)`: shared active-product rule from ISSUE-1.
- `filter_products_by_stock_status(products, status)`: returns active products matching the requested derived status.
- `format_stock_status_results(products, status)`: prepares readable terminal or report output for filtered products.

Supported status filters:
- `Out of stock`
- `Low stock`
- `In stock`

## Required Skills

- `.skills/SKILLS.md`
- `.skills/skills/app-configuration.md`
- `.skills/skills/file-structure.md`
- `.skills/skills/function-definitions.md`
- `.skills/skills/validation.md`

## Expected Output

- A stock-status filter contract that reuses the shared stock-status derivation rule.
- A validation contract for accepted stock-status filter values.
- A filtered overview output design that shows only matching active products.
- Pytest coverage plan or tests for valid statuses, invalid statuses, and active-product enforcement.

## Validation

- Test that filtering by `Out of stock` returns only active products with quantity `0`.
- Test that filtering by `Low stock` returns only active products with quantities `1` through `5`.
- Test that filtering by `In stock` returns only active products with quantities greater than `5`.
- Test that inactive products are excluded even when their derived status matches.
- Test that unsupported status values produce a clear validation error.
- Test that stock-status filtering runs without CSV or CLI access.

## Rules

- Keep this issue small enough for one branch and one pull request.
- Give this issue exactly one main user story.
- Reuse active-product filtering from ISSUE-1.
- Derive stock status from quantity in one shared domain function.
- Keep status filter validation at the input boundary.
- Do not implement product search in this issue.
- Do not implement product detail lookup in this issue.
- Do not generate implementation code in this issue file.
