# Functional Design (AI-Optimized)

## PageStructure

- route: /
- type: use-case-based ranked PC list
- displayed_fields_order:
  - rank
  - product_name
  - price_yen
  - cpu
  - ram
  - storage
  - battery_life
  - weight
  - display_size
  - data_fetched_at

## FunctionalSpecification

### product_list_retrieval

- source: Google Spreadsheet (manual input)
- convert_script: Node.js script to output JSON to /data/products.json
- scoring_logic: use-case-based scoring written in Node.js
- min_items_per_category: 5
- pagination: not implemented (future)

### data_rendering

- frontend: static or dynamic rendering via Next.js
- rendering_fields:
  - rank
  - product_name
  - price_yen
  - cpu
  - ram
  - storage
  - battery_life
  - weight
  - display_size
  - data_fetched_at
- ui_principles:
  - simple
  - non-technical-user-friendly

## InternalArchitecture

### technologies

- frontend:
  - framework: Next.js (React + TypeScript)
  - features: SSG, App Router
- backend_logic:
  - language: Node.js
  - purpose: JSON generation, scoring
- data_source: Google Spreadsheet
- static_data_file: /data/products.json

### modules

- scoring_logic: Node.js
- json_generator: Node.js
- categories: statically defined (basic, office, media)
- display: rendered by Next.js frontend

## NonFunctionalSpecification

### test_policy

- unit_test_targets:
  - scoring logic (Node.js)
  - JSON generation logic
- tools:
  - Jest (Node.js)
  - React Testing Library
- manual_e2e: for initial verification
- future_tooling: Cypress (optional)

### constraints

- max_display_time: ≤ 2 seconds for 20 items
- responsive_ui: required (PC / tablet / mobile)
- no_technical_terms: enforce plain language
- code_standard: must follow internal coding guidelines

## FutureExtensions

- filters: by CPU type, price range
- detail_pages: per product
- affiliate: Amazon tag integration
- admin_ui: spreadsheet sync, upload form
