# Helixra™ — Official Website

> Sri Lankan Games. Eternal Legacy.  
> © 2025 Yellow House Productions Pvt Ltd. All rights reserved.

---

## Project Structure

```
helixra-site/
├── index.html              ← Main landing page
├── play/
│   └── index.html          ← Olinda Keliya game (Chapter I)
├── assets/
│   ├── img/
│   │   ├── helixra-logo.png        ← Main Helixra logo
│   │   ├── yhp-logo.png            ← ADD THIS: Yellow House Productions logo
│   │   └── yhp-logo-placeholder.svg
│   ├── css/                ← (future: extracted stylesheets)
│   └── js/                 ← (future: extracted scripts)
├── netlify.toml            ← Netlify build config
├── _redirects              ← URL redirect rules
└── README.md               ← This file
```

---

## Deploying to Netlify

### Option A — Drag & Drop (fastest)
1. Go to [app.netlify.com](https://app.netlify.com)
2. Drag the entire `helixra-site/` folder onto the deploy area
3. Done — your site is live

### Option B — Git (recommended for ongoing updates)
1. Create a new repository on GitHub/GitLab
2. Push this folder:
   ```bash
   cd helixra-site
   git init
   git add .
   git commit -m "Initial Helixra site launch"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/helixra-site.git
   git push -u origin main
   ```
3. Go to [app.netlify.com](https://app.netlify.com) → New site from Git
4. Connect your repo — Netlify auto-detects `netlify.toml`
5. Every `git push` auto-deploys

### Custom Domain (helixra.com)
1. In Netlify: Site settings → Domain management → Add custom domain
2. Point your DNS to Netlify's nameservers
3. SSL is automatic (Let's Encrypt)

---

## To Replace Logos

### Helixra Logo
- Replace: `assets/img/helixra-logo.png`
- Keep the same filename, or update the `src` in `index.html`

### Yellow House Productions Logo
- Add file as: `assets/img/yhp-logo.png`
- The placeholder in the YHP section will auto-replace
- Recommended: PNG with transparent background, ~400×150px

---

## Wiring the Subscribe Form

In `index.html`, find the comment `// Wire to: POST /api/subscribe` in the JS.  
Replace the `handleSubscribe()` function with:

```javascript
async function handleSubscribe() {
  const email = document.getElementById('sub-email').value.trim();
  const name = document.getElementById('sub-name').value.trim();
  if (!email || !email.includes('@')) { /* validation */ return; }
  
  await fetch('/.netlify/functions/subscribe', {
    method: 'POST',
    body: JSON.stringify({ email, name, path: selPath })
  });
  
  document.getElementById('sub-form').style.display = 'none';
  document.getElementById('sub-success').classList.add('show');
}
```

Add a `netlify/functions/subscribe.js` file with your Resend/Supabase logic.

---

## Trademark & Legal
- **Helixra™** is a trademark of Yellow House Productions Pvt Ltd
- All game content is © 2025 Yellow House Productions Pvt Ltd
- Heritage data sourced from verified Sri Lankan museum and academic records

---

*Built by Yellow House Productions Pvt Ltd — Colombo, Sri Lanka 🇱🇰*
