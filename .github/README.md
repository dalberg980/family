# Family Calendar

A password-protected family calendar page powered by the Google Calendar API.

---

## Setup (5 steps)

### 1. Enable the Google Calendar API

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or use an existing one)
3. Go to **APIs & Services → Library** and enable **Google Calendar API**
4. Go to **APIs & Services → Credentials → Create Credentials → API Key**
5. Copy the API key

**Restrict your API key** (important!):
- Under "API restrictions" → select **Google Calendar API**
- Under "Application restrictions" → select **HTTP referrers** → add your GitHub Pages URL (e.g. `https://yourusername.github.io/family-calendar/*`)

### 2. Make your Google Calendar public (read-only)

For each calendar you want to show:
1. Open [Google Calendar](https://calendar.google.com/)
2. Hover over the calendar name → click the three dots → **Settings and sharing**
3. Scroll to **Access permissions** → check **Make available to public** (view-only)

> This lets the API read events using just an API key, without OAuth login.

### 3. Generate your password hash

1. Go to [SHA-256 online tool](https://emn178.github.io/online-tools/sha256.html)
2. Type your chosen password
3. Copy the resulting hash (64 characters)

### 4. Edit `index.html`

Open `index.html` and find the `CONFIG` block near the top of the `<script>`:

```js
const CONFIG = {
  API_KEY: 'YOUR_GOOGLE_API_KEY',       // ← paste your API key here
  PASSWORD_HASH: 'a1b2c3d4...',         // ← paste your SHA-256 hash here
};
```

Replace both values and save.

### 5. Push to GitHub Pages

```bash
# If this is a new repo
git init
git add .
git commit -m "Add family calendar"
git remote add origin https://github.com/YOURUSERNAME/YOURREPO.git
git push -u origin main

# Then in GitHub: Settings → Pages → Source: main branch / root
```

Your calendar will be live at:
`https://YOURUSERNAME.github.io/YOURREPO/`

---

## Password security notes

- The password is **never stored in plaintext** — only its SHA-256 hash lives in the HTML
- Authentication is session-only (clears when you close the browser tab)
- The API key is visible in the HTML source — restrict it to your domain and to the Calendar API only
- For stronger security, consider adding a backend (Cloudflare Workers, Netlify Functions) to proxy API calls

---

## Customisation

| What | Where in `index.html` |
|---|---|
| Page title | `<title>` tag + `<h1>` in header |
| Default view | Change `setView('week')` initial call |
| First day of week | Edit `startOfWeek()` function (currently Sunday) |
| Accent color | `--accent` CSS variable |
