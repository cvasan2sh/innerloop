# InnerLoop Landing Pages

Geo-targeted landing pages for InnerLoop — AI-powered weekly intelligence briefs.

## Structure

```
/
├── index.html        # Auto-redirects to /in/ or /us/ based on timezone
├── in/index.html     # India landing page
├── us/index.html     # US landing page
├── vercel.json       # Vercel routing config
└── README.md
```

## URLs

- `yoursite.com` → auto-redirects based on visitor timezone
- `yoursite.com/in` → India page (use for India Instagram ads)
- `yoursite.com/us` → US page (use for US Instagram ads)

## Deploy to Vercel

### Option 1: GitHub + Vercel (recommended)

1. Create a new GitHub repo:
   ```
   gh repo create innerloop-landing --public
   git init
   git add .
   git commit -m "Initial landing pages"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/innerloop-landing.git
   git push -u origin main
   ```

2. Go to [vercel.com](https://vercel.com), sign in with GitHub
3. Click "New Project" → Import your `innerloop-landing` repo
4. Deploy (zero config needed, vercel.json handles routing)
5. You'll get: `innerloop-landing.vercel.app`

### Option 2: Vercel CLI

```
npm i -g vercel
cd innerloop-landing
vercel
```

## Instagram Ad URLs

- **India campaign**: `https://your-domain.com/in`
- **US campaign**: `https://your-domain.com/us`

Use separate UTM params for tracking:
- India: `?utm_source=instagram&utm_campaign=india_launch`
- US: `?utm_source=instagram&utm_campaign=us_launch`

## Custom Domain

1. In Vercel dashboard → Settings → Domains
2. Add your domain (e.g., `getinnerloop.com`)
3. Update DNS as instructed

## Next Steps

- [ ] Add Meta Pixel for Instagram ad tracking
- [ ] Wire up Google Sheets webhook for signup data capture
- [ ] Add UTM parameter tracking
