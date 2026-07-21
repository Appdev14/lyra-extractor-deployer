# Lyra Extractor Deployer

Auto-deploys the latest [alexeichhorn/YouTubeKit-Server](https://github.com/alexeichhorn/YouTubeKit-Server)
to your own Cloudflare Workers account, nightly. Serves as Lyra's second
audio-extraction fallback: `[.local, this worker, Alex's public server]`.

## Setup (one time)
1. Cloudflare: free account → register a `*.workers.dev` subdomain
   (Workers & Pages page prompts you) → copy your **Account ID** (sidebar)
   → My Profile → API Tokens → Create Token → template
   **"Edit Cloudflare Workers"** → copy the token.
2. This repo: Settings → Secrets and variables → Actions → add
   `CLOUDFLARE_API_TOKEN` and `CLOUDFLARE_ACCOUNT_ID`.
3. Actions tab → "Deploy latest YouTubeKit-Server" → **Run workflow**.
4. When green: your Worker lives at
   `https://youtubekit-server.<your-subdomain>.workers.dev`
   → paste that URL into `Secrets.ownRemoteExtractorURL` in Lyra.

Uses SQLite-backed Durable Objects (works on Cloudflare's FREE plan).
Built-in per-app rate limit: 5,000 requests/day — far above Lyra's needs.
