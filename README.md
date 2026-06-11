# SmartThings OAuth Callback Page for Stream Deck Plugin

This is a simple static page that handles the OAuth2 redirect callback for the Stream Deck SmartThings plugin.

## Deployment Instructions

### Option 1: Deploy to Vercel (Recommended)

1. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```

2. Deploy:
   ```bash
   cd /tmp/vercel-oauth-deployment
   vercel --prod
   ```

3. Copy the production URL (e.g., `https://your-app.vercel.app`)

4. Update the redirect URI in your plugin code:
   - Edit `src/utils/oauth-client.ts`
   - Replace the `redirectUri` with: `https://your-app.vercel.app/oauth-callback.html`

5. **IMPORTANT**: Add this redirect URI to your SmartThings Developer Workspace:
   - Go to https://smartthings.developer.samsung.com/workspace/projects
   - Select your project
   - Go to "Register App" → "OAuth Client"
   - Add `https://your-app.vercel.app/oauth-callback.html` to the list of Redirect URIs
   - Save changes

### Option 2: GitHub + Vercel Auto-Deploy

1. Create a new GitHub repository
2. Push this folder to the repository
3. Connect the repository to Vercel at https://vercel.com/new
4. Vercel will auto-deploy on every push
5. Follow steps 3-5 from Option 1

### Option 3: Other Static Hosts

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
