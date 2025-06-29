# Technical Design (AI-Optimized)

## DataModel

type Product = {
  id: number
  category: string
  name: string
  price: number
  cpu: string
  ram: string
  rom: string
  battery: string
  weight: string
  display: string
  fetched_at: string
  rank?: number
}

source_data: Google Spreadsheet
output_data: /data/products.json (JSON, Array<Product>)

## BackendLogic

entrypoint: /app/api/score/route.ts (Next.js App Router)
logic_module: /app/api/score/logic.ts

POST /api/score:
  - input: Array<Product> (without rank)
  - process:
      - for each category
      - apply category-specific rule-based scoring
      - sort by score desc
      - assign rank (1-based)
  - output: Array<Product> (with rank)

## Frontend

framework: Next.js (App Router)
page: /app/page.tsx
data_source: /data/products.json (import or getStaticProps)
components:
  - /app/components/CategoryRanking.tsx
  - /app/components/ProductCard.tsx
display_order:
  - rank
  - name
  - price
  - cpu
  - ram
  - rom
  - battery
  - weight
  - display
  - fetched_at

## Testing

framework: Jest
target: /app/api/score/logic.ts
mock_fs: true
mock_input: Array<Product>
assertions:
  - correct score calculation
  - correct rank assignment
  - sorted output

## DirectoryStructure

/data/
  products.json

/scripts/
  fetchSheet.ts
  scoreProducts.ts

/app/
  page.tsx
  /components/
    CategoryRanking.tsx
    ProductCard.tsx
  /api/
    /products/
      route.ts
    /score/
      route.ts
      logic.ts

/types/
  product.ts

/tests/
  scoreProducts.test.ts
