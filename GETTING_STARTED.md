# Getting Started with Riyadh Aletqan

This guide will help you get the Riyadh Aletqan B2B platform up and running on your local machine.

## Prerequisites

Before you begin, ensure you have the following installed:

- **Node.js** 18.17 or later ([Download](https://nodejs.org/))
- **Bun** (recommended) or npm ([Install Bun](https://bun.sh/))
- **Git** ([Download](https://git-scm.com/))
- A code editor (we recommend [VS Code](https://code.visualstudio.com/))

## Step-by-Step Setup

### 1. Clone the Repository

```bash
# Clone the repository
git clone https://github.com/yourusername/riyadh-aletqan.git

# Navigate into the project directory
cd riyadh-aletqan
```

### 2. Install Dependencies

Using Bun (recommended):
```bash
bun install
```

Or using npm:
```bash
npm install
```

This will install all required packages including:
- Next.js 15
- React 19
- TypeScript
- Tailwind CSS v4
- Drizzle ORM
- Better Auth
- And many more...

### 3. Set Up Environment Variables

Copy the example environment file:
```bash
cp .env.example .env
```

Now open `.env` in your code editor and fill in the required values:

#### Database Configuration (Turso)

1. **Sign up for Turso** (free tier available):
   - Go to [turso.tech](https://turso.tech/)
   - Sign up with GitHub or email

2. **Create a database**:
   ```bash
   # Install Turso CLI
   curl -sSfL https://get.tur.so/install.sh | bash
   
   # Login to Turso
   turso auth login
   
   # Create your database
   turso db create riyadh-aletqan-dev
   
   # Get connection URL
   turso db show riyadh-aletqan-dev --url
   
   # Create auth token
   turso db tokens create riyadh-aletqan-dev
   ```

3. **Add to .env**:
   ```env
   TURSO_CONNECTION_URL=libsql://riyadh-aletqan-dev-yourname.turso.io
   TURSO_AUTH_TOKEN=eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9...
   ```

#### Authentication Configuration

Generate a secret key:
```bash
# On macOS/Linux
openssl rand -base64 32

# On Windows (PowerShell)
[Convert]::ToBase64String((1..32 | ForEach-Object { Get-Random -Maximum 256 }))
```

Add to `.env`:
```env
BETTER_AUTH_SECRET=your_generated_secret_here
BETTER_AUTH_URL=http://localhost:3000
```

#### Email Configuration (Resend)

1. **Sign up for Resend** (free tier: 100 emails/day):
   - Go to [resend.com](https://resend.com/)
   - Sign up with GitHub or email

2. **Get API Key**:
   - In Resend dashboard, go to **API Keys**
   - Click **Create API Key**
   - Copy the key

3. **Add to .env**:
   ```env
   RESEND_API_KEY=re_yourkey123456
   RESEND_DOMAIN=resend.dev
   BUSINESS_EMAIL=your-business@email.com
   ```

Your complete `.env` should look like:
```env
# Database Configuration (Turso)
TURSO_CONNECTION_URL=libsql://riyadh-aletqan-dev-yourname.turso.io
TURSO_AUTH_TOKEN=eyJhbGciOiJFZERTQSIsInR5cCI6IkpXVCJ9...

# Authentication (Better Auth)
BETTER_AUTH_SECRET=abc123xyz789...
BETTER_AUTH_URL=http://localhost:3000

# Email Configuration (Resend)
RESEND_API_KEY=re_yourkey123456
RESEND_DOMAIN=resend.dev
BUSINESS_EMAIL=belal.elansary@r-aletqan.com
```

### 4. Initialize the Database

Push the database schema to Turso:
```bash
bun run db:push
```

You should see output like:
```
✓ Pulling schema from database...
✓ Changes applied successfully
```

### 5. Seed Sample Data (Optional)

To populate your database with sample products and data:
```bash
bun run db:seed
```

This will add:
- 1000+ sample products
- Various categories and brands
- Test data for development

### 6. Start the Development Server

```bash
bun dev
```

You should see:
```
▲ Next.js 15.3.5
- Local:        http://localhost:3000
- Network:      http://192.168.1.x:3000

✓ Ready in 2.5s
```

### 7. Open in Browser

Navigate to [http://localhost:3000](http://localhost:3000)

You should see the Riyadh Aletqan homepage! 🎉

## Common Setup Issues

### Issue: "Failed to connect to database"

**Solution**: Verify your Turso credentials
```bash
# Test connection
turso db shell riyadh-aletqan-dev
```

### Issue: "Module not found" errors

**Solution**: Clear cache and reinstall
```bash
rm -rf node_modules .next
bun install
```

### Issue: "Port 3000 already in use"

**Solution**: Kill the process or use a different port
```bash
# Kill process on port 3000
lsof -ti:3000 | xargs kill -9

# Or run on different port
bun dev --port 3001
```

### Issue: Email not sending

**Solution**: 
1. Verify Resend API key is correct
2. Check that `BUSINESS_EMAIL` is a valid email
3. For development, check Resend dashboard for logs

## Next Steps

Now that your development environment is set up:

### 1. Create an Account
- Go to [http://localhost:3000/register](http://localhost:3000/register)
- Create a user account
- Login at [http://localhost:3000/login](http://localhost:3000/login)

### 2. Explore the Admin Dashboard
- Navigate to [http://localhost:3000/admin](http://localhost:3000/admin)
- Manage products and view quote requests
- Note: You may need to manually set admin role in database

### 3. Test Features
- Browse products at `/products`
- Search for specific items
- Submit a quote request
- Check email notifications

### 4. Customize Content
- Update company info in `src/components/layout/footer.tsx`
- Modify service pages in `src/app/services/`
- Adjust brand colors in `src/app/globals.css`

### 5. Add Your Products
- Use the admin dashboard to add products
- Or modify the seed data in `src/db/seeds/products.ts`
- Re-run `bun run db:seed` to update

## Development Workflow

### Making Changes

1. Edit files in `src/` directory
2. Changes auto-reload (hot reload enabled)
3. View changes instantly in browser

### Working with Database

```bash
# View database in browser
bun run db:studio

# Push schema changes
bun run db:push

# Reset and reseed database
bun run db:seed
```

### Code Quality

```bash
# Run linter
bun lint

# Build for production (test)
bun run build
```

## Useful Commands

| Command | Description |
|---------|-------------|
| `bun dev` | Start development server |
| `bun build` | Build for production |
| `bun start` | Start production server |
| `bun lint` | Run ESLint |
| `bun run db:push` | Push schema to database |
| `bun run db:studio` | Open database studio |
| `bun run db:seed` | Seed sample data |

## Project Structure Overview

```
riyadh-aletqan/
├── src/
│   ├── app/           # Pages and routes
│   ├── components/    # React components
│   ├── db/           # Database schema
│   └── lib/          # Utilities
├── public/           # Static files
├── .env              # Environment variables
└── package.json      # Dependencies
```

## Learning Resources

- **Next.js**: [nextjs.org/docs](https://nextjs.org/docs)
- **TypeScript**: [typescriptlang.org/docs](https://www.typescriptlang.org/docs/)
- **Tailwind CSS**: [tailwindcss.com/docs](https://tailwindcss.com/docs)
- **Drizzle ORM**: [orm.drizzle.team/docs](https://orm.drizzle.team/docs/overview)
- **Better Auth**: [better-auth.com/docs](https://better-auth.com/docs)

## Getting Help

- **Documentation**: Check [README.md](./README.md) for detailed info
- **Deployment**: See [DEPLOYMENT.md](./DEPLOYMENT.md)
- **Architecture**: Read [PROJECT_STRUCTURE.md](./PROJECT_STRUCTURE.md)
- **Issues**: Open a GitHub issue
- **Email**: belal.elansary@r-aletqan.com

## What's Next?

Once you're comfortable with the local setup:

1. Read [CONTRIBUTING.md](./CONTRIBUTING.md) to learn about coding standards
2. Check [DEPLOYMENT.md](./DEPLOYMENT.md) to deploy to production
3. Customize the platform for your specific needs
4. Add your own products and content

---

**Happy coding! 🚀**

If you encounter any issues not covered here, please open a GitHub issue or contact support.
