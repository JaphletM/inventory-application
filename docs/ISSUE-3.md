# ISSUE-3.md

## Title

Search active products by name or SKU

## User Story

As an Inventory Employee, I want to search active products by name or SKU so that I can quickly find a product without scrolling through rows.

Acceptance criteria:
- Given a search term matches an active product name with different casing, when search is applied, then the product is returned.
- Given a search term matches all or part of an active product SKU, when search is applied, then the product is returned.
- Given a search term matches an inactive product, when search is applied, then the inactive product is not returned.
- Given the search input is empty, when search is applied, then active products are returned without a search restriction.
- Given a stock-status filter is also supplied, when search is applied, then results satisfy both the search term and the stock-status filter.

## Functions

The implementation should expose or use these function contracts:
- `validate_search_input(term)`: accepts text or empty input and rejects invalid input types at the boundary.
- `normalize_search_term(term)`: trims whitespace and normalizes casing as a pure transformation.
- `search_products_by_name_or_sku(products, term)`: searches product name and SKU in active product data.
- `filter_active_products(products)`: shared active-product rule from ISSUE-1.
- `filter_products_by_stock_status(products, status)`: shared stock-status filter from ISSUE-2.
- `run_inventory_search(path, search_term=None, stock_status=None)`: coordinates CSV loading, validation, active filtering, optional status filtering, search, and output formatting.

Search decisions:
- Name search is case-insensitive.
- SKU search is case-insensitive.
- SKU search allows exact or partial matching.
- Empty search input means no search filter.

## Required Skills

- `.skills/SKILLS.md`
- `.skills/skills/app-configuration.md`
- `.skills/skills/file-structure.md`
- `.skills/skills/function-definitions.md`
- `.skills/skills/validation.md`

## Expected Output

- A search input validation contract.
- A search normalization contract.
- A pure search function for product name and SKU matching.
- An application-level search contract that composes CSV loading, validation, active filtering, optional stock-status filtering, search, and readable output.
- Pytest coverage plan or tests for name search, SKU search, empty input, inactive-product exclusion, and combined search plus status filtering.

## Validation

- Test that name search is case-insensitive.
- Test that leading and trailing whitespace are ignored.
- Test that exact SKU search returns matching active products.
- Test that partial SKU search returns matching active products.
- Test that empty search input returns active products.
- Test that inactive products are excluded from search results.
- Test that search can combine with stock-status filtering without changing either rule.
- Test that search logic runs without CSV or CLI access.

## Rules

- Keep this issue small enough for one branch and one pull request.
- Give this issue exactly one main user story.
- Reuse active-product filtering from ISSUE-1.
- Reuse stock-status filtering from ISSUE-2 where combined queries are needed.
- Keep search rules independent from UI and data access.
- Do not silently replace invalid search input with defaults.
- Do not implement product detail lookup in this issue.
- Do not generate implementation code in this issue file.
