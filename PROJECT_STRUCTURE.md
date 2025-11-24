# Project Structure - Riyadh Aletqan

Complete overview of the project's file organization and architecture.

## Directory Tree

```
riyadh-aletqan/
├── src/                          # Source code
│   ├── app/                      # Next.js App Router
│   │   ├── page.tsx             # Homepage
│   │   ├── layout.tsx           # Root layout
│   │   ├── globals.css          # Global styles
│   │   │
│   │   ├── actions/             # Server actions
│   │   │   └── quotes.ts        # Quote form actions
│   │   │
│   │   ├── admin/               # Admin dashboard
│   │   │   └── page.tsx         # Admin panel
│   │   │
│   │   ├── api/                 # API routes
│   │   │   ├── auth/[...all]/   # Authentication endpoints
│   │   │   ├── products/        # Product CRUD
│   │   │   │   ├── route.ts     # List/create products
│   │   │   │   └── [id]/route.ts # Get/update/delete product
│   │   │   └── quote/
│   │   │       └── route.ts     # Quote submission
│   │   │
│   │   ├── login/               # Authentication pages
│   │   │   └── page.tsx
│   │   ├── register/
│   │   │   └── page.tsx
│   │   │
│   │   ├── products/            # Product pages
│   │   │   ├── page.tsx         # Product catalog
│   │   │   └── [id]/
│   │   │       └── page.tsx     # Product detail
│   │   │
│   │   ├── request-quote/       # RFQ form
│   │   │   └── page.tsx
│   │   │
│   │   ├── services/            # Service pages
│   │   │   ├── amc/
│   │   │   ├── installation/
│   │   │   ├── calibration/
│   │   │   └── commissioning/
│   │   │
│   │   ├── turnkey-projects/    # Turnkey projects page
│   │   ├── partner/             # Partner onboarding
│   │   ├── payments/            # Payment handling
│   │   │
│   │   └── (legal)/             # Legal pages
│   │       ├── terms/
│   │       ├── privacy/
│   │       ├── shipping/
│   │       └── returns/
│   │
│   ├── components/              # React components
│   │   ├── ui/                  # shadcn/ui components
│   │   │   ├── button.tsx
│   │   │   ├── card.tsx
│   │   │   ├── dialog.tsx
│   │   │   ├── input.tsx
│   │   │   └── ... (40+ components)
│   │   │
│   │   ├── email/               # Email templates
│   │   │   ├── quote-confirmation.tsx
│   │   │   └── quote-notification.tsx
│   │   │
│   │   └── layout/              # Layout components
│   │       ├── header.tsx
│   │       ├── footer.tsx
│   │       └── navigation.tsx
│   │
│   ├── db/                      # Database
│   │   ├── index.ts             # Database connection
│   │   ├── schema.ts            # Drizzle schema
│   │   └── seeds/               # Database seeders
│   │       └── products.ts      # Product seed data
│   │
│   ├── lib/                     # Utility functions
│   │   ├── auth.ts              # Better Auth config
│   │   ├── auth-client.ts       # Auth client (frontend)
│   │   ├── utils.ts             # Helper functions
│   │   └── email/               # Email utilities
│   │       ├── send.ts          # Email sender
│   │       └── templates.tsx    # Email templates
│   │
│   └── hooks/                   # Custom React hooks
│       └── use-toast.ts         # Toast notifications
│
├── public/                      # Static assets
│   ├── images/                  # Product images, logos
│   └── ...
│
├── drizzle/                     # Database migrations
│   └── migrations/              # SQL migration files
│
├── .env                         # Environment variables (gitignored)
├── .env.example                 # Environment template
├── .gitignore                   # Git ignore rules
├── drizzle.config.ts            # Drizzle ORM config
├── middleware.ts                # Next.js middleware
├── next.config.ts               # Next.js configuration
├── package.json                 # Dependencies
├── tsconfig.json                # TypeScript config
├── tailwind.config.ts           # Tailwind configuration
├── postcss.config.mjs           # PostCSS config
├── README.md                    # Project documentation
├── DEPLOYMENT.md                # Deployment guide
└── PROJECT_STRUCTURE.md         # This file
```

## Key Directories

### `/src/app` - Application Routes

Next.js 15 App Router structure. Each folder represents a route.

**File Conventions:**
- `page.tsx` - Page component (rendered at route)
- `layout.tsx` - Layout wrapper (persistent across routes)
- `loading.tsx` - Loading UI (Suspense fallback)
- `error.tsx` - Error boundary
- `not-found.tsx` - 404 page
- `route.ts` - API endpoint

**Route Groups:**
- `(auth)` - Authentication routes (login, register)
- `(legal)` - Legal pages (terms, privacy)
- `api/` - API routes

### `/src/components` - React Components

Reusable UI components organized by type.

**Component Categories:**
- `ui/` - Base UI components from shadcn/ui
- `email/` - Email templates (React Email)
- `layout/` - Layout components (header, footer)
- `forms/` - Form components (if needed)

### `/src/db` - Database Layer

Database schema, connection, and seed data.

**Files:**
- `index.ts` - Drizzle client initialization
- `schema.ts` - Table definitions (Drizzle ORM)
- `seeds/` - Sample data for development

### `/src/lib` - Utilities & Configuration

Helper functions and third-party service configs.

**Files:**
- `auth.ts` - Better Auth server configuration
- `auth-client.ts` - Better Auth client (React hooks)
- `utils.ts` - General utilities (cn, formatters)
- `email/` - Email service (Resend integration)

## Important Files

### Configuration Files

| File | Purpose |
|------|---------|
| `next.config.ts` | Next.js configuration (image domains, etc.) |
| `drizzle.config.ts` | Database connection for Drizzle Kit |
| `middleware.ts` | Request middleware (auth, redirects) |
| `tailwind.config.ts` | Tailwind CSS customization |
| `tsconfig.json` | TypeScript compiler options |
| `package.json` | Dependencies and scripts |

### Environment Files

| File | Purpose |
|------|---------|
| `.env` | Environment variables (NEVER commit) |
| `.env.example` | Template for environment setup |

### Documentation

| File | Purpose |
|------|---------|
| `README.md` | Project overview and quick start |
| `DEPLOYMENT.md` | Deployment instructions |
| `PROJECT_STRUCTURE.md` | This file |

## Data Flow

### 1. User Request Flow
```
User Browser
    ↓
Next.js Middleware (auth check)
    ↓
App Router Page (src/app/*/page.tsx)
    ↓
React Components (src/components/)
    ↓
API Routes (src/app/api/*/route.ts)
    ↓
Database (Turso via Drizzle)
```

### 2. Authentication Flow
```
Login Form (src/app/login/page.tsx)
    ↓
Better Auth Client (src/lib/auth-client.ts)
    ↓
Better Auth API (src/app/api/auth/[...all]/route.ts)
    ↓
Better Auth Server (src/lib/auth.ts)
    ↓
Database Session Table
    ↓
Middleware (middleware.ts) - validates on each request
```

### 3. Product Catalog Flow
```
Products Page (src/app/products/page.tsx)
    ↓
Fetch from API (GET /api/products)
    ↓
API Route (src/app/api/products/route.ts)
    ↓
Drizzle Query (src/db/schema.ts)
    ↓
Turso Database
    ↓
JSON Response
    ↓
React State
    ↓
Render Product Cards
```

### 4. Quote Request Flow
```
Quote Form (src/app/request-quote/page.tsx)
    ↓
Form Submission (React Hook Form + Zod)
    ↓
Server Action or API (src/app/actions/quotes.ts)
    ↓
Database Insert (quotes table)
    ↓
Email Notification (src/lib/email/send.ts)
    ↓
Resend API
    ↓
Confirmation Email Sent
```

## Database Schema

### Main Tables

**users**
- id, email, name, password_hash, created_at

**session**
- id, user_id, token, expires_at, ip_address, user_agent

**products**
- id, name, code, category, brand, price, image, description, stock_count, voltage_level

**quotes**
- id, user_id, company_name, contact_name, email, phone, notes, status, created_at

**quote_items**
- id, quote_id, product_id, product_name, quantity, notes

See `src/db/schema.ts` for complete schema.

## API Endpoints

### Authentication
- `POST /api/auth/sign-up` - User registration
- `POST /api/auth/sign-in` - User login
- `POST /api/auth/sign-out` - User logout
- `GET /api/auth/session` - Get current session

### Products
- `GET /api/products` - List products (with filters)
- `POST /api/products` - Create product (admin)
- `GET /api/products/[id]` - Get single product
- `PUT /api/products/[id]` - Update product (admin)
- `DELETE /api/products/[id]` - Delete product (admin)

### Quotes
- `POST /api/quote` - Submit quote request

## Component Architecture

### UI Component Pattern (shadcn/ui)

```tsx
// Base component (src/components/ui/button.tsx)
import { cva, type VariantProps } from "class-variance-authority";

const buttonVariants = cva("base-classes", {
  variants: {
    variant: { default: "", destructive: "" },
    size: { default: "", sm: "", lg: "" }
  }
});

export const Button = ({ variant, size, ...props }) => {
  return <button className={cn(buttonVariants({ variant, size }))} {...props} />
}
```

### Page Component Pattern

```tsx
// src/app/products/page.tsx
import { Suspense } from 'react';

export default function ProductsPage() {
  return (
    <Suspense fallback={<LoadingSkeleton />}>
      <ProductCatalog />
    </Suspense>
  );
}
```

### API Route Pattern

```tsx
// src/app/api/products/route.ts
import { db } from '@/db';
import { products } from '@/db/schema';

export async function GET(request: Request) {
  const { searchParams } = new URL(request.url);
  const category = searchParams.get('category');
  
  const results = await db.select().from(products).where(...);
  return Response.json(results);
}
```

## Styling Architecture

### Tailwind CSS v4

Custom design tokens in `src/app/globals.css`:

```css
@theme inline {
  --color-primary: oklch(0.25 0.12 250);
  --color-secondary: oklch(0.62 0.19 35);
  --radius-lg: var(--radius);
}
```

### Component Styling

```tsx
<Card className="hover:shadow-lg transition-shadow">
  <CardHeader className="bg-primary text-primary-foreground">
    <CardTitle>Product Name</CardTitle>
  </CardHeader>
</Card>
```

## Testing Strategy (Recommended)

While not currently implemented, recommended testing setup:

```
tests/
├── unit/                # Component tests (Vitest)
├── integration/         # API tests
└── e2e/                 # End-to-end tests (Playwright)
```

## Build Process

### Development
```bash
bun dev
# 1. Next.js starts dev server
# 2. Turbopack compiles TypeScript
# 3. Hot reload on file changes
# 4. Available at http://localhost:3000
```

### Production
```bash
bun run build
# 1. TypeScript compilation
# 2. Next.js optimization
# 3. Static generation
# 4. Image optimization
# Output: .next/ directory
```

## Dependencies Overview

### Core Dependencies
- **next** (15.3.5) - React framework
- **react** (19.0.0) - UI library
- **typescript** (5.x) - Type safety

### UI & Styling
- **tailwindcss** (4.x) - Utility-first CSS
- **@radix-ui/*** - Headless UI components
- **lucide-react** - Icons
- **framer-motion** - Animations

### Database
- **drizzle-orm** - TypeScript ORM
- **@libsql/client** - Turso client

### Authentication
- **better-auth** - Authentication framework
- **bcrypt** - Password hashing

### Forms & Validation
- **react-hook-form** - Form handling
- **zod** - Schema validation

### Email
- **resend** - Email API
- **@react-email/components** - Email templates

### Development
- **eslint** - Code linting
- **typescript** - Static typing

## Performance Considerations

### Optimization Strategies
- ✅ Server Components by default (faster initial load)
- ✅ Image optimization via `next/image`
- ✅ Dynamic imports for large components
- ✅ Database indexing on frequently queried fields
- ✅ API route caching (consider adding)

### Bundle Size
- Base bundle: ~200KB (gzipped)
- Use `next/dynamic` for code splitting
- Lazy load admin dashboard components

## Security Features

- ✅ Authentication via Better Auth
- ✅ Password hashing with bcrypt
- ✅ CSRF protection (built into Next.js)
- ✅ SQL injection prevention (Drizzle parameterized queries)
- ✅ XSS protection (React escapes by default)
- ✅ Environment variable security (.env gitignored)
- ✅ Middleware route protection

## Future Enhancements

Potential additions:
- [ ] Internationalization (i18n) for Arabic/English
- [ ] Shopping cart persistence
- [ ] Product comparison feature
- [ ] Advanced search with Algolia
- [ ] Customer dashboard
- [ ] Order tracking
- [ ] Inventory management
- [ ] Analytics dashboard
- [ ] Mobile app (React Native)

---

**Last Updated**: November 2024  
**Maintainer**: Riyadh Aletqan Development Team
