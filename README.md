# SmartThings OAuth Callback Page for Stream Deck Plugin

This is a simple static page that handles the OAuth2 redirect callback for the Stream Deck SmartThings plugin.

**Repository**: https://github.mpi-internal.com/thibaut-sabot/streamdeck-smartthings-oauth  
**Live Demo**: https://streamdeck-smartthings-oauth.vercel.app

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.mpi-internal.com/thibaut-sabot/streamdeck-smartthings-oauth)

## Deployment Instructions

### Option 1: One-Click Deploy (Easiest)

1. Click the "Deploy with Vercel" button above
2. Sign in to Vercel (or create a free account)
3. Click "Deploy"
4. Wait for deployment to complete
5. Copy your production URL (e.g., `https://your-app.vercel.app`)
6. Follow the "After Deployment" steps below

### Option 2: Deploy via Vercel CLI (Recommended)

1. Clone or navigate to this repository:
   ```bash
   cd ~/Projects/streamdeck-smartthings-oauth
   ```

2. Install Vercel CLI (if not already installed):
   ```bash
   npm install -g vercel
   ```

3. Deploy:
   ```bash
   vercel --prod
   ```

4. Copy the production URL and follow "After Deployment" steps below

### Option 3: GitHub + Vercel Auto-Deploy (Best for CI/CD)

1. Go to [vercel.com/new](https://vercel.com/new)
2. Import the GitHub repository: `thibaut-sabot/streamdeck-smartthings-oauth`
3. Click "Deploy"
4. Vercel will auto-deploy on every push to main branch
5. Follow "After Deployment" steps below

### After Deployment

**Update plugin code** (if you deployed to a different URL than the default):
```bash
cd ~/Projects/streamdeck-plugin-smartthings
# Edit src/utils/oauth-client.ts and update the redirectUri
npm run build
```

**⚠️ CRITICAL - Add redirect URI to SmartThings Developer Workspace**:
1. Go to https://smartthings.developer.samsung.com/workspace/projects
2. Select your project
3. Go to "Register App" → "OAuth Client"
4. Add your callback URL to "Redirect URIs":
   - Default: `https://streamdeck-smartthings-oauth.vercel.app/oauth-callback.html`
   - Or your custom URL: `https://your-app.vercel.app/oauth-callback.html`
5. Click "Save"

### Option 4: Other Static Hosts

You can also host this on:
- Netlify
- GitHub Pages
- Cloudflare Pages
- Any static file hosting service

Just make sure to:
1. Host the `oauth-callback.html` file
2. Use HTTPS (required for OAuth2)
3. Update the redirect URI in both your plugin code AND SmartThings Developer Workspace

## How It Works

1. User clicks "Open Authorization Page" in Stream Deck
2. Browser opens SmartThings OAuth page
3. User logs in and authorizes
4. SmartThings redirects to your Vercel page with `?code=xxx` in the URL
5. The page extracts the code and displays it to the user
6. User copies the code and pastes it back into Stream Deck
7. Plugin exchanges the code for access tokens

## Testing

After deployment, test the page by visiting:
```
https://your-app.vercel.app/oauth-callback.html?code=test123
```

You should see the test code displayed with a copy button.

## Security Notes

- The authorization code is displayed client-side only
- No server-side code runs
- The code is never stored or logged
- Uses PKCE for additional security
- HTTPS is required for OAuth2 security
