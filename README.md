# SmartThings OAuth Callback Page for Stream Deck Plugin

This is a simple static page that handles the OAuth2 redirect callback for the Stream Deck SmartThings plugin.

**Live Demo**: https://streamdeck-smartthings-oauth.vercel.app

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/thibautsabot/streamdeck-smartthings-oauth)


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
