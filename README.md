# OAuth Token Viewer

A simple, client-side web page to display and manage OAuth 2.0 access tokens that are passed via the URL fragment.

## Features

*   **Displays Access Token:** Shows the `access_token` found in the URL hash.
*   **Token Expiry Information:**
    *   Calculates and displays the token's expiry time.
    *   Indicates if the token is currently valid or has expired.
    *   Correctly calculates expiry across page reloads or if the token is opened in multiple tabs by storing the token's first seen time in `localStorage`.
*   **Copy to Clipboard:** Allows the user to easily copy the access token by clicking on it.
*   **Notifications:** Uses toast notifications to confirm if the token copy was successful.

## How to Use

1.  Ensure your OAuth 2.0 authorization flow redirects to this `index.html` page.
2.  The access token and its expiry duration (in seconds) must be included in the URL fragment (the part after `#`).
    *   Example: `https://your-domain.com/index.html#access_token=YOUR_ACTUAL_TOKEN&expires_in=3600`
    *   The `access_token` parameter will contain the token itself.
    *   The `expires_in` parameter should be the lifetime of the token in seconds (e.g., 3600 for 1 hour).
3.  Open the `index.html` page (or the URL you've been redirected to) in your web browser.
4.  The token will be displayed. Click on the token text to copy it to your clipboard.
5.  The page will also show when the token is valid until or if it has expired.

## Technical Details

*   The page is a single HTML file with embedded JavaScript and CSS.
*   It uses `URLSearchParams` to parse the `access_token` and `expires_in` values from `window.location.hash`.
*   To accurately track the token's validity period, especially if the page is reloaded or the token is used across multiple instances, the timestamp of when a token is first seen is stored in the browser's `localStorage`. A simple hash of the token is used as the key.
*   User notifications (e.g., "Access token copied") are handled by [Toastify.js](https://github.com/apvarun/toastify-js).

## Setup / Deployment

*   **No special build process is required.**
*   Simply deploy `index.html` as a static file on any web server (e.g., GitHub Pages, Netlify, Vercel, or a traditional web server like Nginx or Apache).
*   It can also be opened directly in a web browser from your local filesystem (`file:///path/to/index.html`), but be aware that some browser security features related to `localStorage` might behave differently with `file:///` URLs compared to `http://` or `https://` URLs, though it should generally work for this use case.
