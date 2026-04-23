# Mock E-Commerce Site — Copilot Instructions

## Project Overview

This is a **mock e-commerce web application** called **"Mock Shop"** for educational purposes. It has a React frontend and an ASP.NET Core backend. The repository name is `mock-e-commerce-site`.

---

## Tech Stack

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| **React** | 19.2.4 | UI library |
| **React DOM** | 19.2.4 | DOM rendering |
| **TypeScript** | ~6.0.2 | Language |
| **Vite** | 8.0.4 | Build tool & dev server |
| **Vitest** | 4.1.4 | Test runner |
| **@testing-library/react** | 16.3.2 | Component testing |
| **@testing-library/jest-dom** | 6.9.1 | DOM matchers |
| **@testing-library/user-event** | 14.6.1 | User interaction simulation |
| **jsdom** | 29.0.2 | DOM environment for tests |
| **ESLint** | 9.39.4 | Linter (flat config) |
| **typescript-eslint** | 8.58.0 | TS linting |
| **@vitest/coverage-v8** | 4.1.4 | Coverage |

### Backend
| Technology | Version | Purpose |
|---|---|---|
| **ASP.NET Core** | .NET 10.0 (`net10.0`) | Web framework |
| **Minimal APIs** | (built-in) | Endpoint routing (MapGroup, MapGet, MapPost, MapDelete) |
| **Microsoft.AspNetCore.OpenApi** | 10.0.5 | OpenAPI/Swagger support |
| **xUnit** | 2.9.3 | Test framework |
| **Microsoft.AspNetCore.Mvc.Testing** | 10.0.* | Integration test support (WebApplicationFactory) |
| **Microsoft.NET.Test.Sdk** | 17.14.1 | Test SDK |
| **coverlet.collector** | 6.0.4 | Code coverage |

---

## Project Structure

```
mock-e-commerce-site/
├── .github/
│   └── CODEOWNERS                          # Owner: @kranoz91
├── package.json                            # Root workspace config (workspaces: ["src/frontend"])
├── package-lock.json
├── tsconfig.json                           # Root TS config for tests (includes test/frontend/**)
├── vitest.config.ts                        # Vitest config (jsdom, globals, setup file)
├── .editorconfig                           # 2-space indent for web files, 4-space for C#
├── .gitignore                              # Ignores node_modules, dist, bin, obj, etc.
├── LICENSE
├── README.md                               # Minimal: "mock-e-commerce-site - educational mock repository"
│
├── src/
│   ├── frontend/                           # React frontend (npm workspace)
│   │   ├── package.json                    # Frontend package (name: "frontend", version: 0.0.0)
│   │   ├── index.html                      # HTML entry point (title: "Mock Shop")
│   │   ├── vite.config.ts                  # Vite config with proxy: /api → http://localhost:5063
│   │   ├── eslint.config.js                # ESLint flat config
│   │   ├── tsconfig.json                   # References tsconfig.app.json & tsconfig.node.json
│   │   ├── tsconfig.app.json               # App TS config (target: ES2023, jsx: react-jsx)
│   │   ├── tsconfig.node.json              # Node TS config for vite.config.ts
│   │   ├── public/                         # Static assets (favicon.svg)
│   │   └── src/
│   │       ├── main.tsx                    # React entry point (StrictMode + createRoot)
│   │       ├── App.tsx                     # Root component (products, cart, loading/error states)
│   │       ├── App.css                     # All component styles (header, hero, product card/list)
│   │       ├── index.css                   # Global CSS variables, light/dark theme, reset
│   │       ├── test-setup.ts               # Imports @testing-library/jest-dom
│   │       ├── api/
│   │       │   └── index.ts                # API client: fetchProducts, fetchProductById, addToCart
│   │       ├── types/
│   │       │   └── index.ts                # TypeScript interfaces: Product, AddToCartRequest
│   │       ├── hooks/
│   │       │   └── useProducts.ts          # Custom hook: fetches products on mount
│   │       ├── components/
│   │       │   ├── Header/
│   │       │   │   └── Header.tsx          # Sticky header with logo, nav, cart button
│   │       │   ├── HeroBanner/
│   │       │   │   └── HeroBanner.tsx      # Yellow promotional banner with CTA
│   │       │   ├── ProductCard/
│   │       │   │   └── ProductCard.tsx     # Individual product card with add-to-cart
│   │       │   └── ProductList/
│   │       │       └── ProductList.tsx     # Grid list of ProductCard components
│   │       └── assets/                     # Static assets folder
│   │
│   └── backend/
│       ├── MockEcommerce.slnx              # .NET solution file (references API + Tests projects)
│       └── MockEcommerce.Api/
│           ├── MockEcommerce.Api.csproj    # .NET 10.0 project, OpenApi package
│           ├── Program.cs                  # Entry point: DI, CORS, middleware, endpoint mapping
│           ├── appsettings.json            # Default logging config
│           ├── appsettings.Development.json # Dev logging config
│           ├── Properties/
│           │   └── launchSettings.json     # HTTP: localhost:5063, HTTPS: localhost:7296
│           ├── Models/
│           │   ├── Product.cs              # Product model (Id, Name, Description, Price, Category, Stock, ImageUrl)
│           │   └── CartItem.cs             # CartItem model (ProductId, ProductName, UnitPrice, Quantity, TotalPrice computed)
│           ├── Services/
│           │   ├── IProductService.cs      # Interface: GetAll(), GetById(int id)
│           │   ├── MockProductService.cs   # Implementation with 5 hardcoded products
│           │   ├── ICartService.cs         # Interface: GetAll(), Add(), GetByProductId(), Remove(), Clear()
│           │   └── InMemoryCartService.cs  # ⚠️ STUBBED — all methods throw NotImplementedException
│           └── Endpoints/
│               ├── ProductEndpoints.cs     # ✅ Implemented: GET /api/products, GET /api/products/{id}
│               └── CartEndpoints.cs        # ⚠️ STUBBED — all 4 endpoints throw NotImplementedException
│
├── test/
│   ├── frontend/
│   │   ├── App.test.tsx                    # 8 tests for App component
│   │   ├── components/
│   │   │   ├── Header/
│   │   │   │   └── Header.test.tsx         # 6 tests for Header
│   │   │   ├── HeroBanner/
│   │   │   │   └── HeroBanner.test.tsx     # 4 tests for HeroBanner
│   │   │   ├── ProductCard/
│   │   │   │   └── ProductCard.test.tsx    # 7 tests for ProductCard
│   │   │   └── ProductList/
│   │   │       └── ProductList.test.tsx    # 3 tests for ProductList
│   │   └── hooks/
│   │       └── useProducts.test.ts         # 4 tests for useProducts hook
│   │
│   └── backend/
│       └── MockEcommerce.Api.Tests/
│           ├── MockEcommerce.Api.Tests.csproj  # xUnit 2.9.3, Mvc.Testing, coverlet
│           ├── Endpoints/
│           │   └── ProductEndpointTests.cs     # 3 integration tests (WebApplicationFactory)
│           └── Services/
│               └── MockProductServiceTests.cs  # 4 unit tests
```

---

## How to Run Tests

### Frontend Tests (Vitest)
```bash
# From the repository root:
npm test
# or equivalently:
npm run test:frontend
# or:
npx vitest run

# These all run: vitest run
# Environment: jsdom
# Setup file: src/frontend/src/test-setup.ts
# Test pattern: test/frontend/**/*.{test,spec}.{ts,tsx}
```

There are **32 frontend tests** across 6 test files:
- `test/frontend/App.test.tsx` — 8 tests (App component rendering, loading, error, cart)
- `test/frontend/components/Header/Header.test.tsx` — 6 tests
- `test/frontend/components/HeroBanner/HeroBanner.test.tsx` — 4 tests
- `test/frontend/components/ProductCard/ProductCard.test.tsx` — 7 tests
- `test/frontend/components/ProductList/ProductList.test.tsx` — 3 tests
- `test/frontend/hooks/useProducts.test.ts` — 4 tests

### Backend Tests (xUnit)
```bash
# From the repository root:
dotnet test src/backend/MockEcommerce.slnx

# or from the test project directory:
cd test/backend/MockEcommerce.Api.Tests
dotnet test
```

There are **7 backend tests** across 2 test files:
- `test/backend/MockEcommerce.Api.Tests/Endpoints/ProductEndpointTests.cs` — 3 integration tests
- `test/backend/MockEcommerce.Api.Tests/Services/MockProductServiceTests.cs` — 4 unit tests

### Frontend Linting
```bash
cd src/frontend
npm run lint
# Runs: eslint .
```

---

## How to Run the Application

### Backend
```bash
cd src/backend/MockEcommerce.Api
dotnet run
# Runs on http://localhost:5063 (HTTP) or https://localhost:7296 (HTTPS)
```

### Frontend
```bash
cd src/frontend
npm run dev
# Runs Vite dev server (default http://localhost:5173)
# Proxies /api requests to http://localhost:5063 (the backend)
```

### Frontend Build
```bash
cd src/frontend
npm run build
# Runs: tsc -b && vite build
```

---

## Product Catalog (Hardcoded Mock Data)

The product data is hardcoded in `src/backend/MockEcommerce.Api/Services/MockProductService.cs`. There is **no database** — data is stored in a static in-memory list.

| ID | Name | Category | Price | Stock | Description |
|----|------|----------|-------|-------|-------------|
| 1 | Wireless Headphones | Electronics | $79.99 | 25 | Over-ear noise-cancelling wireless headphones with 30-hour battery life. |
| 2 | Running Shoes | Footwear | $59.99 | 40 | Lightweight breathable running shoes for all-terrain use. |
| 3 | Stainless Steel Water Bottle | Accessories | $24.99 | 100 | Insulated 32 oz water bottle that keeps drinks cold for 24 hours. |
| 4 | Mechanical Keyboard | Electronics | $109.99 | 15 | Compact tenkeyless mechanical keyboard with Cherry MX Blue switches. |
| 5 | Yoga Mat | Sports | $34.99 | 60 | Non-slip 6mm thick yoga mat with carrying strap. |

Product categories: **Electronics** (2 products), **Footwear** (1), **Accessories** (1), **Sports** (1).

All product images use placeholder URLs from `placehold.co` (e.g., `https://placehold.co/300x300?text=Headphones`).

---

## API Endpoints

All endpoints are defined using ASP.NET Core **Minimal APIs** with `MapGroup`.

### Product Endpoints — ✅ Fully Implemented
Defined in `src/backend/MockEcommerce.Api/Endpoints/ProductEndpoints.cs`:

| Method | Path | Status | Description |
|--------|------|--------|-------------|
| GET | `/api/products` | ✅ Implemented | Returns all 5 products (200 OK) |
| GET | `/api/products/{id}` | ✅ Implemented | Returns single product (200 OK) or 404 Not Found |

### Cart Endpoints — ⚠️ ALL STUBBED (Not Implemented)
Defined in `src/backend/MockEcommerce.Api/Endpoints/CartEndpoints.cs`:

| Method | Path | Status | Description |
|--------|------|--------|-------------|
| GET | `/api/cart` | ❌ Stubbed | Throws `NotImplementedException` |
| POST | `/api/cart` | ❌ Stubbed | Throws `NotImplementedException`. Accepts `AddToCartRequest(ProductId, Quantity)` |
| DELETE | `/api/cart/{productId}` | ❌ Stubbed | Throws `NotImplementedException` |
| DELETE | `/api/cart` | ❌ Stubbed | Throws `NotImplementedException` (clear all) |

---

## Implementation Status

### ✅ Fully Implemented
- **Product listing** — Backend serves 5 hardcoded products, frontend fetches and displays them in a responsive CSS Grid
- **Product detail** — Backend serves individual product by ID
- **Product display** — Frontend renders ProductCard components with name, price, category, description, image
- **Loading state** — "Loading products…" shown while fetching
- **Error state** — Error message displayed on fetch failure
- **Cart item count UI** — Header shows cart badge with count (increments on add-to-cart click)
- **Add-to-cart notification** — Success/error notification appears for 3 seconds after clicking add-to-cart button
- **Responsive design** — CSS Grid layout adapts to mobile, hero banner reflows, nav hidden on mobile
- **Dark mode** — CSS custom properties with `prefers-color-scheme: dark` media query
- **Accessibility** — Semantic HTML, aria-labels on buttons/regions, keyboard navigation
- **OpenAPI** — Swagger/OpenAPI documentation endpoint mapped
- **CORS** — Configured to allow frontend at `http://localhost:5173`

### ⚠️ Stubbed / Not Implemented
- **All cart backend logic** — `InMemoryCartService` has `_cart` list and `_lock` (Lock) declared but every method (`GetAll`, `Add`, `GetByProductId`, `Remove`, `Clear`) throws `NotImplementedException`
- **All cart endpoints** — `CartEndpoints.cs` defines routes but every handler throws `NotImplementedException`
- **Cart page/view** — No dedicated cart page exists; only a cart button with item count in the header
- **Checkout flow** — No checkout or payment functionality
- **Authentication** — No user auth; cart is registered as `Singleton` (shared across all users)
- **Database** — No database; all data is hardcoded in-memory

---

## Architecture & Patterns

### Frontend Architecture
- **Component-based**: Functional React components with TypeScript
- **Custom hooks**: `useProducts` hook encapsulates data fetching with `useState` + `useEffect`
- **API layer**: Centralized in `src/frontend/src/api/index.ts` using `fetch()` with `BASE_URL = '/api'`
- **Type definitions**: Shared interfaces in `src/frontend/src/types/index.ts`
- **Styling**: Single CSS file (`App.css`) with CSS custom properties from `index.css`; no CSS-in-JS or CSS modules
- **State management**: Local component state only (no Redux, Context, or other state management library)
- **Component organization**: Each component in its own folder (`Header/Header.tsx`, etc.)

### Backend Architecture
- **Minimal APIs**: Extension methods on `WebApplication` for endpoint grouping (`MapProductEndpoints`, `MapCartEndpoints`)
- **Service pattern**: Interfaces (`IProductService`, `ICartService`) with concrete implementations
- **Dependency injection**: Services registered as `Singleton` via `builder.Services.AddSingleton<>()`
- **Models**: `Product` (7 properties) and `CartItem` (5 properties, `TotalPrice` is computed)
- **No database**: `MockProductService` uses a `static readonly List<Product>` with hardcoded data
- **Thread safety**: `InMemoryCartService` declares a `Lock` for thread-safe cart access (not yet implemented)

### Frontend TypeScript Types
```typescript
interface Product {
  id: number
  name: string
  description: string
  price: number
  category: string
  stock: number
  imageUrl: string
}

interface AddToCartRequest {
  productId: number
  quantity: number
}
```

### Backend C# Models
```csharp
// Product.cs
class Product { Id, Name, Description, Price, Category, Stock, ImageUrl }

// CartItem.cs
class CartItem { ProductId, ProductName, UnitPrice, Quantity, TotalPrice (computed: UnitPrice * Quantity) }

// CartEndpoints.cs
record AddToCartRequest(int ProductId, int Quantity);
```

---

## Configuration Details

### Ports & Proxy
- Backend HTTP: `http://localhost:5063`
- Backend HTTPS: `https://localhost:7296`
- Frontend dev server: `http://localhost:5173` (Vite default)
- Vite proxy: `/api` → `http://localhost:5063`
- CORS allows origin: `http://localhost:5173`

### Workspace Structure
- Root `package.json` uses npm workspaces: `["src/frontend"]`
- Root scripts `test` and `test:frontend` both run `vitest run`
- Frontend has its own `package.json` with `dev`, `build`, `lint`, `preview` scripts

### Editor Config
- Web files (ts, tsx, js, jsx, json, css, html, md, yaml): **2-space indent**
- C# files: **4-space indent**, file-scoped namespaces, primary constructors
- Line endings: LF
- Charset: UTF-8

---

## Code Ownership

The `CODEOWNERS` file (`.github/CODEOWNERS`) assigns **@kranoz91** as the owner for all files (`*`).
