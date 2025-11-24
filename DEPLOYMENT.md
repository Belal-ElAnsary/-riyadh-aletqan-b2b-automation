# Deployment Guide - Riyadh Aletqan

Complete guide to deploying your Riyadh Aletqan application to production.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Deploy to Vercel](#deploy-to-vercel)
- [Database Setup](#database-setup)
- [Environment Variables](#environment-variables)
- [Custom Domain Setup](#custom-domain-setup)
- [Post-Deployment](#post-deployment)
- [Troubleshooting](#troubleshooting)

## Prerequisites

Before deploying, ensure you have:

✅ GitHub account  
✅ Turso database created  
✅ Resend account with API key  
✅ Domain name (optional: riyadhenergy.net)  

## Deploy to Vercel

Vercel is the recommended platform for Next.js applications.

### Step 1: Push to GitHub

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - Riyadh Aletqan B2B Platform"

# Create GitHub repository at github.com/new
# Then add remote and push
git remote add origin https://github.com/yourusername/riyadh-aletqan.git
git branch -M main
git push -u origin main
```

### Step 2: Import to Vercel

1. Go to [vercel.com](https://vercel.com) and sign in
2. Click **"Add New Project"**
3. Click **"Import Git Repository"**
4. Select your `riyadh-aletqan` repository
5. Vercel will auto-detect Next.js settings

**Build Settings** (auto-configured):
```
Framework Preset: Next.js
Build Command: npm run build
Output Directory: .next
Install Command: npm install
```

### Step 3: Configure Environment Variables

In Vercel dashboard, go to **Settings → Environment Variables** and add:

```env
# Database (Turso)
TURSO_CONNECTION_URL=libsql://your-database.turso.io
TURSO_AUTH_TOKEN=your_turso_token

# Authentication
BETTER_AUTH_SECRET=your_secret_here
BETTER_AUTH_URL=https://your-app.vercel.app

# Email (Resend)
RESEND_API_KEY=re_your_key
RESEND_DOMAIN=resend.dev
BUSINESS_EMAIL=belal.elansary@r-aletqan.com
```

⚠️ **Important**: Update `BETTER_AUTH_URL` to your actual Vercel URL after first deployment.

### Step 4: Deploy

Click **"Deploy"** - Vercel will:
1. Install dependencies
2. Build your application
3. Deploy to production
4. Provide a live URL (e.g., `riyadh-aletqan.vercel.app`)

## Database Setup

### Option 1: Use Existing Turso Database

If you already have a Turso database with data:
1. Use the same `TURSO_CONNECTION_URL` and `TURSO_AUTH_TOKEN`
2. Your production app will use the existing data

### Option 2: Create New Production Database

For a fresh production database:

```bash
# Install Turso CLI
curl -sSfL https://get.tur.so/install.sh | bash

# Login
turso auth login

# Create production database
turso db create riyadh-aletqan-prod

# Get connection URL
turso db show riyadh-aletqan-prod --url

# Create auth token
turso db tokens create riyadh-aletqan-prod

# Push schema
npm run db:push

# Optional: Seed data
npm run db:seed
```

Add the new credentials to Vercel environment variables.

## Environment Variables

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `TURSO_CONNECTION_URL` | Turso database URL | `libsql://your-db.turso.io` |
| `TURSO_AUTH_TOKEN` | Turso authentication token | `eyJ...` |
| `BETTER_AUTH_SECRET` | Auth secret (32+ chars) | Generate with `openssl rand -base64 32` |
| `BETTER_AUTH_URL` | Your production URL | `https://your-app.vercel.app` |
| `RESEND_API_KEY` | Resend API key | `re_...` |
| `BUSINESS_EMAIL` | Business contact email | `contact@example.com` |

### Optional Variables

| Variable | Description |
|----------|-------------|
| `RESEND_DOMAIN` | Custom email domain |
| `STRIPE_SECRET_KEY` | Stripe integration (if needed) |
| `STRIPE_PUBLISHABLE_KEY` | Stripe public key |

### Generating Secrets

```bash
# Generate BETTER_AUTH_SECRET
openssl rand -base64 32
```

## Custom Domain Setup

To use your custom domain `riyadhenergy.net`:

### Step 1: Add Domain in Vercel

1. In Vercel dashboard, go to **Settings → Domains**
2. Click **"Add Domain"**
3. Enter `riyadhenergy.net` and `www.riyadhenergy.net`
4. Click **"Add"**

### Step 2: Configure DNS Records

Vercel will provide DNS instructions. Typically:

**Option A: Using A Records** (Recommended)
```
Type    Name    Value               TTL
A       @       76.76.21.21         3600
CNAME   www     cname.vercel-dns.com 3600
```

**Option B: Using Vercel Nameservers**
```
Nameserver 1: ns1.vercel-dns.com
Nameserver 2: ns2.vercel-dns.com
```

### Step 3: Update DNS at Your Registrar

1. Login to your domain registrar (e.g., GoDaddy, Namecheap)
2. Find DNS settings for `riyadhenergy.net`
3. Add the A record and CNAME record as specified
4. Save changes

### Step 4: Verify & Wait

- DNS propagation takes 5 minutes to 48 hours
- Check status at [dnschecker.org](https://dnschecker.org/)
- Vercel will auto-issue SSL certificate when DNS is ready

### Step 5: Update Environment Variables

Once domain is live, update in Vercel:
```env
BETTER_AUTH_URL=https://riyadhenergy.net
```

Redeploy the application for changes to take effect.

## Post-Deployment

### 1. Test Core Functionality

- ✅ Homepage loads correctly
- ✅ Product catalog displays products
- ✅ Search functionality works
- ✅ User registration and login
- ✅ Request quote form submits
- ✅ Admin dashboard accessible

### 2. Create Admin User

```bash
# Option 1: Through UI
1. Go to https://your-domain.com/register
2. Create an account
3. Manually update database to make user admin

# Option 2: Using Turso CLI
turso db shell riyadh-aletqan-prod
# Then run SQL:
UPDATE users SET role = 'admin' WHERE email = 'admin@example.com';
```

### 3. Populate Products

- Login to admin dashboard: `/admin`
- Add products manually or
- Run seed script with production connection

### 4. Test Email System

- Submit a quote request
- Verify emails are received
- Check Resend dashboard for delivery logs

### 5. Configure Error Monitoring (Optional)

Consider adding:
- [Sentry](https://sentry.io/) for error tracking
- [Vercel Analytics](https://vercel.com/analytics) for performance
- [PostHog](https://posthog.com/) for product analytics

## Alternative Platforms

### Deploy to Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
netlify deploy --prod
```

### Deploy to Railway

1. Go to [railway.app](https://railway.app)
2. Click "New Project" → "Deploy from GitHub"
3. Select repository
4. Add environment variables
5. Deploy

### Deploy to DigitalOcean

1. Create a Droplet or use App Platform
2. Follow [DigitalOcean Next.js guide](https://docs.digitalocean.com/products/app-platform/languages-frameworks/nodejs/)
3. Configure environment variables
4. Deploy

## Troubleshooting

### Build Fails

**Error: Environment variables missing**
```bash
# Solution: Add all required env vars in Vercel dashboard
```

**Error: Database connection failed**
```bash
# Solution: Verify Turso credentials
turso db show your-database --url
```

### Runtime Errors

**500 Internal Server Error**
- Check Vercel function logs: Dashboard → Deployments → [Latest] → Functions
- Verify environment variables are set
- Check database connection

**Email Not Sending**
- Verify Resend API key is valid
- Check Resend dashboard for errors
- Verify `BUSINESS_EMAIL` is correct

**Authentication Issues**
- Ensure `BETTER_AUTH_SECRET` is set
- Verify `BETTER_AUTH_URL` matches your domain
- Check session table in database

### Domain Issues

**Domain Not Resolving**
```bash
# Check DNS propagation
dig riyadhenergy.net
nslookup riyadhenergy.net

# Use online tool
https://dnschecker.org/
```

**SSL Certificate Issues**
- Wait for DNS propagation to complete
- Vercel auto-issues certificates via Let's Encrypt
- Check Vercel domain settings for status

### Performance Issues

**Slow Page Loads**
- Enable Vercel Analytics
- Check database query performance
- Consider adding caching layer (Redis)

**High Memory Usage**
- Review Vercel function logs
- Optimize database queries
- Use `next/image` for images

## Continuous Deployment

Once set up, Vercel automatically:
- Builds and deploys on every push to `main` branch
- Creates preview deployments for pull requests
- Runs checks before deploying

**Workflow:**
```bash
# Make changes locally
git add .
git commit -m "Update product catalog"
git push origin main

# Vercel automatically deploys
# Check deployment at vercel.com/dashboard
```

## Rollback

If deployment fails:
1. Go to Vercel Dashboard → Deployments
2. Find previous working deployment
3. Click **"⋮"** menu → **"Promote to Production"**

## Security Checklist

Before going live:
- ✅ All environment variables secured
- ✅ `.env` files not committed to git
- ✅ Database has proper access controls
- ✅ HTTPS enabled (automatic with Vercel)
- ✅ Admin routes protected
- ✅ CORS configured if using external APIs
- ✅ Rate limiting on API routes (consider adding)

## Monitoring & Maintenance

### Regular Tasks
- Monitor error logs weekly
- Check email delivery rates
- Review database storage usage
- Update dependencies monthly
- Backup database regularly

### Recommended Tools
- **Uptime Monitoring**: [UptimeRobot](https://uptimerobot.com/)
- **Error Tracking**: [Sentry](https://sentry.io/)
- **Analytics**: [Vercel Analytics](https://vercel.com/analytics)

## Support

Need help deploying?
- Vercel Docs: [vercel.com/docs](https://vercel.com/docs)
- Turso Docs: [docs.turso.tech](https://docs.turso.tech)
- Next.js Docs: [nextjs.org/docs](https://nextjs.org/docs)

---

**🎉 Congratulations!** Your Riyadh Aletqan platform is now live!
