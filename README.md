# InnerLoop Landing Pages

Geo-targeted landing pages for InnerLoop — AI-powered personalized intelligence briefs.

## Structure

```
/index.html     → India version (default)
/in/index.html  → India version (explicit)
/us/index.html  → US version
```

## URLs after deploy

- `yoursite.vercel.app` → India page
- `yoursite.vercel.app/in` → India page
- `yoursite.vercel.app/us` → US page

## Deploy to Vercel

### Option 1: GitHub + Vercel (recommended)

1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com) → "Add New Project"
3. Import your GitHub repo
4. Framework preset: **Other**
5. Click Deploy — done

### Option 2: Vercel CLI

```bash
npm i -g vercel
cd innerloop-landing
vercel
```

## Instagram Ad Setup

Point your ad campaigns to:
- **India campaign** → `yourdomain.com/in`
- **US campaign** → `yourdomain.com/us`

## Adding Google Sheets webhook

In each `index.html`, find the commented-out `fetch()` call in the `submitWaitlist()` function. Replace `YOUR_GOOGLE_SHEETS_WEBHOOK_URL` with your Google Apps Script web app URL.

### Setting up Google Sheets collection:

1. Create a new Google Sheet
2. Go to Extensions → Apps Script
3. Paste this code:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    new Date(),
    data.name,
    data.email,
    data.loc,
    data.seniority,
    data.func,
    data.stage,
    data.alumni,
    data.industries,
    data.signals,
    data.actions,
    data.position,
    data.source
  ]);
  return ContentService.createTextOutput(
    JSON.stringify({ status: 'ok' })
  ).setMimeType(ContentService.MimeType.JSON);
}
```

4. Deploy → New deployment → Web app → Anyone can access
5. Copy the URL and paste it in both `index.html` files

## Adding Meta Pixel

Add this in the `<head>` of each page (replace `YOUR_PIXEL_ID`):

```html
<script>
!function(f,b,e,v,n,t,s)
{if(f.fbq)return;n=f.fbq=function(){n.callMethod?
n.callMethod.apply(n,arguments):n.queue.push(arguments)};
if(!f._fbq)f._fbq=n;n.push=n;n.loaded=!0;n.version='2.0';
n.queue=[];t=b.createElement(e);t.async=!0;
t.src=v;s=b.getElementsByTagName(e)[0];
s.parentNode.insertBefore(t,s)}(window, document,'script',
'https://connect.facebook.net/en_US/fbevents.js');
fbq('init', 'YOUR_PIXEL_ID');
fbq('track', 'PageView');
</script>
```

Then add these events in the JavaScript:
- On CTA click: `fbq('track', 'ViewContent');`
- On profile complete: `fbq('track', 'Lead');`
- On signup complete: `fbq('track', 'CompleteRegistration');`
