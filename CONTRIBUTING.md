# Contributing to Riyadh Aletqan

Thank you for your interest in contributing to the Riyadh Aletqan project! This document provides guidelines and instructions for contributors.

## Table of Contents
- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Guidelines](#testing-guidelines)

## Code of Conduct

### Our Standards
- Be respectful and inclusive
- Focus on constructive feedback
- Prioritize project goals over personal preferences
- Maintain professionalism in all interactions

## Getting Started

### Prerequisites
- Node.js 18.17 or later
- Bun (recommended) or npm/yarn
- Git
- Basic knowledge of Next.js, React, and TypeScript

### Initial Setup

1. **Fork the Repository**
   ```bash
   # Visit GitHub and click "Fork"
   # Then clone your fork
   git clone https://github.com/YOUR_USERNAME/riyadh-aletqan.git
   cd riyadh-aletqan
   ```

2. **Install Dependencies**
   ```bash
   bun install
   ```

3. **Set Up Environment**
   ```bash
   cp .env.example .env
   # Fill in your development credentials
   ```

4. **Run Database Migrations**
   ```bash
   bun run db:push
   bun run db:seed
   ```

5. **Start Development Server**
   ```bash
   bun dev
   ```

## Development Workflow

### Branch Naming Convention

Use descriptive branch names:
```
feature/add-product-comparison
fix/cart-calculation-error
docs/update-readme
refactor/optimize-product-query
```

### Workflow Steps

1. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   ```

2. **Make Changes**
   - Write code following our coding standards
   - Test your changes thoroughly
   - Write/update tests if applicable

3. **Commit Changes**
   ```bash
   git add .
   git commit -m "feat: add product comparison feature"
   ```

4. **Push to Your Fork**
   ```bash
   git push origin feature/your-feature-name
   ```

5. **Create Pull Request**
   - Go to GitHub
   - Click "New Pull Request"
   - Provide clear description of changes

## Coding Standards

### TypeScript

**Use TypeScript for all new files**
```typescript
// ✅ Good - Explicit types
interface Product {
  id: number;
  name: string;
  price: number;
}

function getProduct(id: number): Promise<Product> {
  // ...
}

// ❌ Bad - Implicit any
function getProduct(id) {
  // ...
}
```

### React Components

**Use functional components with TypeScript**
```typescript
// ✅ Good
interface ButtonProps {
  label: string;
  onClick: () => void;
  variant?: 'primary' | 'secondary';
}

export function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  return (
    <button onClick={onClick} className={cn('btn', `btn-${variant}`)}>
      {label}
    </button>
  );
}

// ❌ Bad - No types, class component
export class Button extends React.Component {
  render() {
    return <button>{this.props.label}</button>
  }
}
```

### File Organization

**Follow Next.js conventions**
```
src/
├── app/
│   └── products/
│       ├── page.tsx          # Page component
│       ├── loading.tsx       # Loading state
│       └── error.tsx         # Error boundary
├── components/
│   └── product-card.tsx      # Reusable component
└── lib/
    └── utils.ts              # Utility functions
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `ProductCard.tsx` |
| Functions | camelCase | `fetchProducts()` |
| Constants | UPPER_SNAKE_CASE | `API_BASE_URL` |
| Files | kebab-case | `product-card.tsx` |
| Interfaces | PascalCase + I prefix (optional) | `IProductProps` or `ProductProps` |

### Styling

**Use Tailwind CSS utility classes**
```tsx
// ✅ Good
<div className="flex items-center gap-4 p-6 rounded-lg bg-primary text-primary-foreground">
  <h2 className="text-xl font-bold">Title</h2>
</div>

// ❌ Bad - Inline styles
<div style={{ display: 'flex', padding: '24px' }}>
  <h2 style={{ fontSize: '20px' }}>Title</h2>
</div>
```

### API Routes

**Follow RESTful conventions**
```typescript
// src/app/api/products/route.ts
export async function GET(request: Request) {
  // List products
}

export async function POST(request: Request) {
  // Create product
}

// src/app/api/products/[id]/route.ts
export async function GET(request: Request, { params }: { params: { id: string } }) {
  // Get single product
}

export async function PUT(request: Request, { params }: { params: { id: string } }) {
  // Update product
}

export async function DELETE(request: Request, { params }: { params: { id: string } }) {
  // Delete product
}
```

### Error Handling

**Always handle errors gracefully**
```typescript
// ✅ Good
try {
  const product = await fetchProduct(id);
  return Response.json(product);
} catch (error) {
  console.error('Failed to fetch product:', error);
  return Response.json(
    { error: 'Failed to fetch product' },
    { status: 500 }
  );
}

// ❌ Bad - No error handling
const product = await fetchProduct(id);
return Response.json(product);
```

## Commit Guidelines

### Commit Message Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding/updating tests
- `chore`: Maintenance tasks

### Examples

```bash
# Feature
git commit -m "feat(products): add product comparison feature"

# Bug fix
git commit -m "fix(cart): resolve calculation error for discounted items"

# Documentation
git commit -m "docs(readme): update installation instructions"

# Refactor
git commit -m "refactor(api): optimize product query performance"
```

### Commit Best Practices
- Keep commits atomic (one logical change per commit)
- Write clear, descriptive messages
- Reference issue numbers when applicable: `fix(cart): resolve #123`

## Pull Request Process

### PR Checklist

Before submitting a PR, ensure:

- [ ] Code follows project coding standards
- [ ] All tests pass
- [ ] New features have corresponding tests
- [ ] Documentation is updated
- [ ] Commit messages follow guidelines
- [ ] Branch is up-to-date with main

### PR Template

When creating a PR, include:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
Describe how you tested your changes

## Screenshots (if applicable)
Add screenshots for UI changes

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Tests added/updated
- [ ] Documentation updated
```

### Review Process

1. **Automated Checks**
   - Linting passes
   - Build succeeds
   - Tests pass

2. **Code Review**
   - At least one approval required
   - Address all comments
   - Make requested changes

3. **Merge**
   - Squash commits if necessary
   - Merge into main branch

## Testing Guidelines

### Unit Tests (Recommended)

```typescript
// tests/components/product-card.test.tsx
import { render, screen } from '@testing-library/react';
import { ProductCard } from '@/components/product-card';

describe('ProductCard', () => {
  it('renders product name', () => {
    const product = { id: 1, name: 'Test Product', price: 100 };
    render(<ProductCard product={product} />);
    expect(screen.getByText('Test Product')).toBeInTheDocument();
  });
});
```

### Integration Tests

```typescript
// tests/api/products.test.ts
import { GET } from '@/app/api/products/route';

describe('GET /api/products', () => {
  it('returns list of products', async () => {
    const request = new Request('http://localhost/api/products');
    const response = await GET(request);
    const data = await response.json();
    expect(Array.isArray(data)).toBe(true);
  });
});
```

### E2E Tests (Recommended)

```typescript
// tests/e2e/product-flow.spec.ts
import { test, expect } from '@playwright/test';

test('user can search and view product', async ({ page }) => {
  await page.goto('/');
  await page.fill('input[placeholder*="Search"]', 'Siemens PLC');
  await page.press('input[placeholder*="Search"]', 'Enter');
  await expect(page).toHaveURL(/products\?search=/);
  await page.click('text=Siemens');
  await expect(page).toHaveURL(/products\/\d+/);
});
```

## Common Tasks

### Adding a New Page

1. Create page file: `src/app/new-page/page.tsx`
2. Add to navigation: `src/components/layout/header.tsx`
3. Update documentation: `PROJECT_STRUCTURE.md`

### Adding a New API Endpoint

1. Create route file: `src/app/api/endpoint/route.ts`
2. Implement HTTP methods (GET, POST, etc.)
3. Add authentication if needed
4. Document in API section

### Adding a New Component

1. Create component: `src/components/my-component.tsx`
2. Add to shadcn if reusable UI: `src/components/ui/`
3. Export from index if needed
4. Document props with TypeScript

### Updating Database Schema

1. Modify: `src/db/schema.ts`
2. Generate migration: `bun run db:push`
3. Update seed data if needed: `src/db/seeds/`
4. Update documentation

## Need Help?

- **Questions**: Open a GitHub Discussion
- **Bugs**: Open a GitHub Issue
- **Features**: Open a GitHub Issue with [Feature Request] tag
- **Security**: Email directly (don't post publicly)

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

**Thank you for contributing to Riyadh Aletqan! 🙏**
