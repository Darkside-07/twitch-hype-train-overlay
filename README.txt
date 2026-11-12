TWITCH HYPE TRAIN OVERLAY — OBS-ONLY VERSION

This version runs entirely inside OBS Browser Source. It does NOT need Node.js,
Streamer.bot, npm, or a separate background app.

IMPORTANT: Twitch browser OAuth requires an HTTPS redirect URL. Host these static
files on GitHub Pages (free) or another HTTPS static host. Do not open index.html
as a local file; OAuth will not work from file://.

GITHUB PAGES SETUP
1. Create a GitHub repository, e.g. twitch-hype-train-overlay.
2. Upload index.html (and optionally overlay.html) from this folder to the repo.
3. In the repository, open Settings > Pages.
4. Set Build and deployment to Deploy from a branch; choose main and /(root).
5. Wait for GitHub Pages to publish the site. Its address will look like:
   https://YOUR-GITHUB-USERNAME.github.io/twitch-hype-train-overlay/

TWITCH DEVELOPER APP
1. Open https://dev.twitch.tv/console/apps and edit/create your application.
2. Set OAuth Redirect URL to the exact GitHub Pages address above, including the
   repository path and trailing slash. Example:
   https://YOUR-GITHUB-USERNAME.github.io/twitch-hype-train-overlay/
3. Set Client Type to Public and save.
4. Copy the Client ID.

OBS SETUP
1. Add a Browser Source.
2. Set its URL to the GitHub Pages address (same as the redirect URL).
3. Set width/height to your canvas (e.g. 1920 x 1080), and enable Shutdown source
   when not visible only if you are happy to reconnect when it becomes visible.
4. Right-click the Browser Source > Interact.
5. Paste your Twitch Client ID and click Save Client ID, then Login with Twitch.
6. Approve the permissions. The page returns to the overlay and connects.
7. The Client ID and access token are stored in this OBS Browser Source's local
   browser storage. The token is not sent to a third-party server by this page.

PERMISSIONS
- channel:read:hype_train (required)
- user:read:chat (optional, used for the overlay's !emote command)

NOTES / LIMITATIONS
- This uses Twitch's Implicit Grant because Twitch documents it for client-side
  apps that do not use a server. Implicit tokens do not include refresh tokens;
  when Twitch expires/revokes the token, use Interact > Login with Twitch again.
- OBS must be able to reach GitHub Pages, Twitch OAuth, Twitch Helix and the
  EventSub WebSocket endpoint.
- Test animation is available by adding ?test=1 to the page URL.
- Add ?debug=1 to show the event log.
- Hype Train top contributor windows come from Twitch's top_contributions field;
  Twitch does not provide a complete contribution history in each event.

SECURITY
The Client ID is public by design. The access token is a bearer credential and is
stored in OBS's local browser storage. Do not share your OBS profile or browser
storage folder with anyone you do not trust. Disconnecting removes the token.
