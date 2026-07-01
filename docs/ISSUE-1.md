# ISSUE-1.md

## Title

Create read-only active product overview from CSV

## User Story

As an Inventory Employee, I want to view active products so that I can see only products currently sold by the retailer.

Acceptance criteria:
- Given the CSV contains active and inactive products, when the overview is generated, then inactive products are not shown.
- Given an active product is shown, then the overview includes id, SKU, name, price, stock quantity, derived stock status, and last-updated timestamp.
- Given a product has quantity `0`, then its stock status is `Out of stock`.
- Given a product has quantity `1` through `5`, then its stock status is `Low stock`.
- Given a product has quantity greater than `5`, then its stock status is `In stock`.
- Given required CSV fields are missing or invalid, then validation reports the invalid field clearly.

## Functions

The implementation should expose or use these function contracts:
- `load_products_csv(path)`: reads product rows from CSV with pandas in the infrastructure boundary.
- `validate_product_schema(products)`: validates required columns and raw field formats before domain processing.
- `reject_invalid_product_values(products)`: rejects invalid product values such as missing SKU or negative stock quantity.
- `filter_active_products(products)`: returns only active products as a pure domain transformation.
- `determine_stock_status(stock_quantity)`: derives stock status from stock quantity as a pure domain rule.
- `attach_stock_status(products)`: adds derived stock status for overview output without treating stored status as authoritative.
- `format_product_overview(products)`: prepares readable terminal or report output for active products.

Required CSV fields:
- `id`
- `sku`
- `name`
- `description`
- `price`
- `stock_quantity`
- `active`
- `last_updated_at`

## Required Skills

- `.skills/SKILLS.md`
- `.skills/skills/app-configuration.md`
- `.skills/skills/file-structure.md`
- `.skills/skills/function-definitions.md`
- `.skills/skills/validation.md`

## Expected Output

- A documented proposed Python file tree for domain, infrastructure, application, CLI, and tests.
- A documented CSV schema for product inventory input.
- Function contracts for CSV loading, schema validation, active filtering, stock-status derivation, and overview formatting.
- A readable overview output design showing active product rows only.
- Pytest coverage plan or tests for every business rule in this issue.

## Validation

- Test that inactive products are excluded.
- Test that missing SKU is rejected at the input boundary.
- Test that missing required columns are rejected.
- Test that negative stock quantity is rejected.
- Test that quantity `0` becomes `Out of stock`.
- Test that quantities `1` and `5` become `Low stock`.
- Test that quantity `6` becomes `In stock`.
- Test that active filtering and stock-status calculation run without CSV or CLI access.

## Rules

- Keep this issue small enough for one branch and one pull request.
- Give this issue exactly one main user story.
- Keep business rules independent from UI and data access.
- Keep CSV access in the infrastructure boundary.
- Do not implement stock-status filter selection in this issue.
- Do not implement product search in this issue.
- Do not implement product detail lookup in this issue.
- Do not generate implementation code in this issue file.
