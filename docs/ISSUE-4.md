# ISSUE-4.md

## Title

Open read-only details for one active product

## User Story

As an Inventory Employee, I want to open the details of one active product so that I can review its full read-only product and stock information.

Acceptance criteria:
- Given an active product id is provided, when details are opened, then the product detail output shows all product fields.
- Given an active SKU is provided, when details are opened, then the matching product detail output is shown.
- Given the product is inactive, when details are requested, then the product is not shown.
- Given no product matches the provided id or SKU, when details are requested, then the application reports that no active product was found.
- Given product details are shown, then stock status is derived from stock quantity and last-updated timestamp is visible.

## Functions

The implementation should expose or use these function contracts:
- `validate_product_lookup_input(identifier)`: accepts product id or SKU input and rejects missing or invalid lookup values.
- `normalize_product_identifier(identifier)`: trims and normalizes lookup input for matching.
- `find_active_product_by_id_or_sku(products, identifier)`: returns one active product matching id or SKU.
- `filter_active_products(products)`: shared active-product rule from ISSUE-1.
- `determine_stock_status(stock_quantity)`: shared stock-status rule from ISSUE-1.
- `format_product_detail(product)`: prepares readable read-only detail output for one product.
- `run_product_detail_query(path, identifier)`: coordinates CSV loading, validation, active filtering, product lookup, stock-status derivation, and detail formatting.

Detail output fields:
- `id`
- `sku`
- `name`
- `description`
- `price`
- `stock_quantity`
- derived stock status
- `active`
- `last_updated_at`

## Required Skills

- `.skills/SKILLS.md`
- `.skills/skills/app-configuration.md`
- `.skills/skills/file-structure.md`
- `.skills/skills/function-definitions.md`
- `.skills/skills/validation.md`

## Expected Output

- A product lookup validation contract.
- A pure active product lookup function by id or SKU.
- A read-only product detail output design showing every product field plus derived stock status.
- An application-level detail query contract that composes CSV loading, validation, active filtering, lookup, stock-status derivation, and readable output.
- Pytest coverage plan or tests for active lookup, inactive exclusion, unknown identifier behavior, and read-only detail output fields.

## Validation

- Test that active product lookup by id returns one matching product.
- Test that active product lookup by SKU returns one matching product.
- Test that inactive products are excluded from detail lookup.
- Test that unknown identifiers produce a clear not-found result or error.
- Test that missing lookup input is rejected.
- Test that detail output includes description, price, stock quantity, derived stock status, active status, and last-updated timestamp.
- Test that detail lookup logic runs without CSV or CLI access.

## Rules

- Keep this issue small enough for one branch and one pull request.
- Give this issue exactly one main user story.
- Reuse active-product filtering from ISSUE-1.
- Reuse stock-status derivation from ISSUE-1.
- Keep product detail lookup independent from UI and data access.
- Do not add product creation, product editing, or stock adjustment behavior.
- Do not generate implementation code in this issue file.
