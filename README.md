# insight

A TypeScript analytics platform with a type-safe semantic layer for querying large datasets. Provides a query builder, data modeling abstractions, and dashboard components for building analytics applications.

## Overview

Analytics dashboards require a layer between raw data and the UI that handles query construction, caching, access control, and type safety. Insight provides this semantic layer so you can build dashboards without writing raw SQL or dealing with untyped query results.

## Structure

```
packages/          - Core packages: query builder, semantic layer, SDK
python/            - Python utilities for data ingestion
scripts/           - Build and deployment scripts
testing/           - Test utilities and fixtures
specs/             - Project specifications and RFCs
website-next/      - Documentation website
```

## Features

- **Type-safe query builder** — compile-time validation of queries
- **Semantic data modeling** — define metrics and dimensions declaratively
- **Multi-datasource** — connect to ClickHouse, Postgres, and more
- **Caching layer** — automatic query result caching with TTL
- **Dashboard components** — React components for charts and tables
- **Access control** — row-level and column-level permissions

## Getting Started

```bash
# Install dependencies
pnpm install

# Start development
pnpm dev

# Run tests
pnpm test

# Build all packages
pnpm build
```

## Defining a Model

```typescript
import { defineModel } from '@insight/semantic'

const salesModel = defineModel({
  name: 'sales',
  table: 'events.sales',
  dimensions: {
    region: { column: 'geo.region', type: 'string' },
    date: { column: 'timestamp', type: 'date' },
  },
  metrics: {
    revenue: { column: 'amount', aggregation: 'sum' },
    orders: { column: 'id', aggregation: 'count' },
  },
})
```

## Querying

```typescript
const result = await insight.query(salesModel)
  .select(['region', 'revenue'])
  .filter({ date: { gte: '2024-01-01' } })
  .groupBy('region')
  .execute()
```

## Workspace

This is a pnpm monorepo managed with Turborepo. See `turbo.json` for task configuration.

## License

MIT
