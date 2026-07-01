# Requirement Summary

Build a read-only command-line inventory overview or small report using Python, pandas, a CSV file, and pytest. Inventory employees must be able to view active products, search by product name or SKU, filter by stock status, open one product's details, and see when stock information was last updated.

The CSV-backed product input must include:
- `id`
- `sku`
- `name`
- `description`
- `price`
- `stock_quantity`
- `active`
- `last_updated_at`

Business rules:
- Only active products are shown.
- Stock status is derived from `stock_quantity`.
- `Out of stock` means quantity equals `0`.
- `Low stock` means quantity is `1` through `5`.
- `In stock` means quantity is greater than `5`.
- Products can be searched by name or SKU.
- The first version is read-only; employees do not add products or adjust stock.

Resolved assumptions for open questions:
- Name search is case-insensitive.
- SKU search accepts exact and partial matches.
- Empty search input means no search filter and returns active products.

Proposed implementation boundaries:
- `inventory/domain/`: pure active filtering, stock-status calculation, search matching, and product detail selection.
- `inventory/infrastructure/`: pandas CSV loading.
- `inventory/application/`: orchestration of load, validate, filter, search, detail lookup, and formatting.
- `inventory/cli/`: command-line entry point and readable terminal or report output.
- `tests/`: pytest coverage for every business rule, boundary value, and validation rule.

## User Stories Ordered by Dependency

1. As an Inventory Employee, I want to view active products so that I can see only products currently sold by the retailer.
2. As an Inventory Employee, I want to filter active products by stock status so that I can focus on products needing stock attention.
3. As an Inventory Employee, I want to search active products by name or SKU so that I can quickly find a product without scrolling through rows.
4. As an Inventory Employee, I want to open the details of one active product so that I can review its full read-only product and stock information.

## Functional Breakdown

### 1. View Active Products

Functional scope:
- Define and validate the CSV product schema.
- Load inventory rows from CSV with pandas through an infrastructure boundary.
- Reject invalid raw input before domain processing.
- Filter inactive products through a pure domain function.
- Derive stock status from quantity through one shared pure domain function.
- Format an overview that includes product id, SKU, name, price, stock quantity, stock status, and last-updated timestamp.

Primary rule coverage:
- Only active products are shown.
- Stock status comes from stock quantity.
- Missing SKU is rejected at the input boundary.
- Negative stock quantity is rejected.

### 2. Filter by Stock Status

Functional scope:
- Define accepted stock-status filter values.
- Validate stock-status filter input at the application or CLI boundary.
- Apply stock-status filtering after active-product filtering.
- Reuse the shared stock-status derivation function.

Primary rule coverage:
- Quantity `0` becomes `Out of stock`.
- Quantities `1` and `5` become `Low stock`.
- Quantity `6` becomes `In stock`.
- Invalid stock-status filter values are rejected.

### 3. Search by Name or SKU

Functional scope:
- Validate and normalize employee search input.
- Search active products by normalized product name or SKU.
- Treat empty input as no search filter.
- Combine search with existing active-product and optional stock-status filtering.

Primary rule coverage:
- Products can be searched by name or SKU.
- Name search is case-insensitive.
- SKU search supports partial and exact matching.
- Empty input returns active products instead of failing.

### 4. Open Product Details

Functional scope:
- Validate product identifier input.
- Select one active product by id or SKU.
- Exclude inactive products from detail lookup.
- Format all product fields for read-only detail output.
- Include the derived stock status and last-updated timestamp in details.

Primary rule coverage:
- Only active products are available in detail view.
- Stock status in detail view comes from stock quantity.
- Missing or unknown product identifiers produce clear errors.
- Detail output is read-only and does not expose add or stock-adjustment behavior.
