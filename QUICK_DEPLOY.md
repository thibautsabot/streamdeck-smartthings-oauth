# 🚀 Quick Deployment Guide

## Your OAuth Callback Repository is Ready!

**Repository**: https://github.mpi-internal.com/thibaut-sabot/streamdeck-smartthings-oauth  
**Location**: `/Users/thibaut.sabot/Projects/streamdeck-smartthings-oauth`

## Deploy to Vercel (3 Steps)

### Option 1: CLI Deployment (Fastest)

```bash
cd ~/Projects/streamdeck-smartthings-oauth
vercel --prod
```

That's it! Copy the URL you get (e.g., `https://streamdeck-smartthings-oauth.vercel.app`)

### Option 2: One-Click Deploy

1. Visit: https://vercel.com/new/clone?repository-url=https://github.mpi-internal.com/thibaut-sabot/streamdeck-smartthings-oauth
2. Click "Deploy"
3. Done!

### Option 3: Connect GitHub to Vercel (Auto-deploy on push)

1. Go to https://vercel.com/new
2. Import `thibaut-sabot/streamdeck-smartthings-oauth`
3. Click "Deploy"

## After Deployment

### Step 1: Add Redirect URI to SmartThings

⚠️ **This is required or OAuth won't work!**

1. Go to: https://smartthings.developer.samsung.com/workspace/projects
2. Select your project
3. Navigate to: **Register App** → **OAuth Client**
4. Add to Redirect URIs:
   ```
   https://streamdeck-smartthings-oauth.vercel.app/oauth-callback.html
   ```
   (or your custom Vercel URL)
5. Click **Save**

### Step 2: Test It

Visit: `https://your-vercel-url.vercel.app/oauth-callback.html?code=test123`

You should see:
- ✅ Success message
- The test code "test123"
- A copy button
- Instructions

### Step 3: Try the OAuth Flow

1. Open Stream Deck
2. Add a SmartThings button
3. Enter your Client ID and Secret
4. Click "Open Authorization Page"
5. Authorize in the browser
6. You'll see your code on the Vercel page
7. Copy and paste it back into Stream Deck

## Files in Repository

```
streamdeck-smartthings-oauth/
├── index.html           # Landing page with info
├── oauth-callback.html  # The actual OAuth callback handler
├── vercel.json         # Vercel configuration
├── package.json        # Project metadata
├── .gitignore          # Git ignore rules
└── README.md          # Full documentation
```

## Current Plugin Configuration

The plugin is already configured to use:
```
https://streamdeck-smartthings-oauth.vercel.app/oauth-callback.html
```

If you deploy to a different URL, update:
- File: `~/Projects/streamdeck-plugin-smartthings/src/utils/oauth-client.ts`
- Line: 52
- Then run: `npm run build` in the plugin directory

## That's It!

Your OAuth callback is ready to deploy. Just run `vercel --prod` and add the URL to SmartThings!
