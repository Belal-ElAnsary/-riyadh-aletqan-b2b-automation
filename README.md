# Riyadh Aletqan - Industrial Automation B2B Platform

A professional B2B e-commerce platform for industrial automation and electrical solutions, built with Next.js 15, TypeScript, and Tailwind CSS.

![Next.js](https://img.shields.io/badge/Next.js-15-black)
![TypeScript](https://img.shields.io/badge/TypeScript-5-blue)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-38bdf8)
![License](https://img.shields.io/badge/license-MIT-green)

## 🚀 Features

### Core Functionality
- **Product Catalog** - Browse 1000+ industrial automation products with advanced filtering
- **Smart Search** - Search by product name, code, brand, or category
- **Product Details** - Comprehensive specifications, datasheets, and warranty information
- **Dual Action System** - "Add to Cart" for fixed-price items, "Request Quote" for custom solutions
- **Request for Quote (RFQ)** - Complete quote management system with file uploads

### Business Services
- **Turnkey Projects** - End-to-end industrial project delivery
- **Maintenance Contracts** - Annual Maintenance Contracts (AMC)
- **Installation Services** - Professional installation by certified engineers
- **Calibration & Testing** - Precision calibration and commissioning services
- **Partner Program** - Supplier and distributor onboarding portal

### Technical Features
- **Bilingual Support** - Full Arabic/English interface (ready for i18n)
- **Authentication** - Secure user authentication with Better Auth
- **Email Notifications** - Automated email system via Resend
- **Responsive Design** - Mobile-first, fully responsive UI
- **Admin Dashboard** - Product management and quote handling
- **Database Integration** - Turso (LibSQL) with Drizzle ORM

### Brands & Categories
**Featured Brands**: ABB, Siemens, Schneider Electric, Allen-Bradley, Delta, Omron, Phoenix Contact

**Product Categories**: Power Supply, PLCs, HMIs, VFDs, Sensors, Safety Systems, Industrial Communication, Circuit Protection

## 🛠️ Tech Stack

- **Framework**: [Next.js 15](https://nextjs.org/) (App Router)
- **Language**: [TypeScript](https://www.typescriptlang.org/)
- **Styling**: [Tailwind CSS v4](https://tailwindcss.com/)
- **UI Components**: [Radix UI](https://www.radix-ui.com/) + [shadcn/ui](https://ui.shadcn.com/)
- **Database**: [Turso](https://turso.tech/) (LibSQL) + [Drizzle ORM](https://orm.drizzle.team/)
- **Authentication**: [Better Auth](https://better-auth.com/)
- **Email**: [Resend](https://resend.com/) + [React Email](https://react.email/)
- **Forms**: [React Hook Form](https://react-hook-form.com/) + [Zod](https://zod.dev/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Animations**: [Framer Motion](https://www.framer.com/motion/)

## 📋 Prerequisites

- **Node.js** 18.17 or later
- **Bun** (recommended) or npm/yarn/pnpm
- **Turso Account** for database ([sign up free](https://turso.tech/))
- **Resend Account** for email ([sign up free](https://resend.com/))

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/riyadh-aletqan.git
cd riyadh-aletqan
```

### 2. Install Dependencies

```bash
# Using Bun (recommended)
bun install

# Or using npm
npm install
```

### 3. Configure Environment Variables

Copy `.env.example` to `.env` and fill in your credentials:

```bash
cp .env.example .env
```

**Required variables:**
```env
# Database
TURSO_CONNECTION_URL=libsql://your-db.turso.io
TURSO_AUTH_TOKEN=your_token

# Auth (generate with: openssl rand -base64 32)
BETTER_AUTH_SECRET=your_secret_key
BETTER_AUTH_URL=http://localhost:3000

# Email
RESEND_API_KEY=re_your_key
BUSINESS_EMAIL=your@email.com
```

### 4. Set Up Database

```bash
# Push schema to database
bun run db:push

# Or using npm
npm run db:push

# Seed sample data (optional)
bun run db:seed
```

### 5. Run Development Server

```bash
# Using Bun
bun dev

# Or using npm
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## 📁 Project Structure

```
riyadh-aletqan/
├── src/
│   ├── app/                    # Next.js App Router pages
│   │   ├── (routes)/          # Route groups
│   │   ├── api/               # API routes
│   │   ├── admin/             # Admin dashboard
│   │   └── layout.tsx         # Root layout
│   ├── components/            # React components
│   │   ├── ui/               # shadcn/ui components
│   │   └── email/            # Email templates
│   ├── db/                    # Database configuration
│   │   ├── schema.ts         # Drizzle schema
│   │   └── seeds/            # Database seeders
│   ├── lib/                   # Utility functions
│   │   ├── auth.ts           # Auth configuration
│   │   └── email/            # Email utilities
│   └── hooks/                 # Custom React hooks
├── public/                    # Static assets
├── drizzle/                   # Database migrations
├── .env.example              # Environment template
├── drizzle.config.ts         # Drizzle configuration
├── middleware.ts             # Next.js middleware
├── next.config.ts            # Next.js configuration
└── package.json              # Dependencies
```

## 🗄️ Database Schema

The application uses the following main tables:

- **users** - User accounts and authentication
- **products** - Product catalog (1000+ items)
- **quotes** - Quote requests and RFQ management
- **quote_items** - Individual items in quotes
- **session** - User sessions

See `src/db/schema.ts` for complete schema definitions.

## 📧 Email Configuration

The app sends automated emails for:
- Quote request confirmations (customer)
- Quote notifications (business)
- Admin notifications

Configure email settings in `.env`:
```env
RESEND_API_KEY=your_key
BUSINESS_EMAIL=business@example.com
```

## 🔐 Authentication

The application uses Better Auth for secure authentication:

- Email/password registration
- Secure session management
- Password hashing with bcrypt
- Protected routes via middleware

**Admin Access**: Create an admin user through the registration flow and manually update the database.

## 🌐 Deployment

### Deploy to Vercel (Recommended)

1. **Push to GitHub**:
   ```bash
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

2. **Import to Vercel**:
   - Go to [vercel.com](https://vercel.com)
   - Click "Add New Project"
   - Import your GitHub repository
   - Vercel auto-detects Next.js

3. **Add Environment Variables**:
   - In Vercel dashboard, go to Settings → Environment Variables
   - Add all variables from `.env`
   - Update `BETTER_AUTH_URL` to your production domain

4. **Deploy**:
   - Vercel automatically deploys on every push
   - Your app will be live at `your-project.vercel.app`

5. **Custom Domain** (Optional):
   - Go to Settings → Domains
   - Add `riyadhenergy.net`
   - Configure DNS records as instructed

See [DEPLOYMENT.md](./DEPLOYMENT.md) for detailed deployment instructions.

### Other Platforms

The app can also be deployed to:
- **Netlify**
- **AWS Amplify**
- **Railway**
- **DigitalOcean App Platform**

## 🛠️ Available Scripts

```bash
# Development
bun dev              # Start dev server
bun build            # Build for production
bun start            # Start production server

# Database
bun run db:push      # Push schema changes
bun run db:studio    # Open Drizzle Studio
bun run db:seed      # Seed sample data

# Code Quality
bun lint             # Run ESLint
```

## 📱 Pages & Routes

### Public Pages
- `/` - Homepage with featured products and categories
- `/products` - Product catalog with filtering
- `/products/[id]` - Individual product details
- `/request-quote` - Request for Quote form
- `/turnkey-projects` - Turnkey project information
- `/services/*` - Service pages (AMC, Installation, etc.)
- `/partner` - Become a Partner form

### User Pages
- `/login` - User login
- `/register` - User registration
- `/payments` - Payment processing (Stripe ready)

### Admin Pages
- `/admin` - Admin dashboard (product & quote management)

### Legal Pages
- `/terms` - Terms & Conditions
- `/privacy` - Privacy Policy
- `/shipping` - Shipping & Delivery
- `/returns` - Returns & Refunds

## 🎨 Customization

### Brand Colors

Update brand colors in `src/app/globals.css`:

```css
:root {
  --primary: oklch(0.25 0.12 250);      /* Dark Blue */
  --secondary: oklch(0.62 0.19 35);     /* Orange */
  /* ... other colors */
}
```

### Content

- **Company Info**: Update in `src/components/layout/footer.tsx`
- **Product Data**: Managed through admin dashboard or database seeds
- **Service Pages**: Edit content in `src/app/services/*`

## 🌍 Internationalization

The app is designed with bilingual support in mind (Arabic/English). To enable:

1. Install `next-intl` or `next-i18next`
2. Add translation files
3. Update components with translation keys

## 🐛 Troubleshooting

### Database Connection Issues
```bash
# Verify Turso connection
bun run db:studio
```

### Email Not Sending
- Verify Resend API key is valid
- Check email templates in `src/components/email/`
- Test in Resend dashboard

### Build Errors
```bash
# Clear Next.js cache
rm -rf .next
bun run build
```

## 📝 License

This project is proprietary software. All rights reserved.

## 🤝 Support

For technical support or business inquiries:
- **Email**: belal.elansary@r-aletqan.com
- **Website**: [riyadhenergy.net](https://riyadhenergy.net)

## 🙏 Acknowledgments

- Built with [Next.js](https://nextjs.org/)
- UI components from [shadcn/ui](https://ui.shadcn.com/)
- Icons from [Lucide](https://lucide.dev/)
- Design inspiration from [WI Automation](https://sa.wiautomation.com/)

---

**Built with ❤️ for Riyadh Aletqan Company**