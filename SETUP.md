# Loop

Plain HTML, CSS and JavaScript short-video app. Supabase stores videos, accounts, likes and comments. GitHub Pages hosts the frontend.

## Finish deployment

1. Open https://github.com/tuffrealy/123ilo4/settings/pages and set **Source → GitHub Actions**.
2. Open Actions → Publish Loop to GitHub Pages → Run workflow.
3. The site address will be https://tuffrealy.github.io/123ilo4/ . Use the deployment URL reported by GitHub as the authoritative address.

## Enable Google registration / login

Google authentication is not yet configured. The frontend includes the complete OAuth flow; first sign-in registers the user.

1. In Google Cloud Console, configure the Google Auth Platform consent screen and create a Web application OAuth client.
2. Add this authorized redirect URI: `https://hgvvnfzevklbanudjaff.supabase.co/auth/v1/callback`.
3. In Supabase project hgvvnfzevklbanudjaff → Authentication → Sign In / Providers → Google, enable Google and enter the client ID and secret. Keep the secret only in Supabase, never in this repository.
4. Under Authentication → URL Configuration, set Site URL and an allowed redirect URL to `https://tuffrealy.github.io/123ilo4/`.
5. If your Google app is in testing mode, add test users or publish the OAuth consent configuration for general access.
6. Sign in on the deployed site and upload your first video.

## Implemented

- Vertical scroll-snap feed with touch swiping, arrow keys and spacebar play/pause.
- Only the visible video plays; hidden tabs and open dialogs pause playback.
- Sound toggle, playback progress / seeking, looping.
- Title, drag/drop or file selection, local preview, upload status, 50 MB limit.
- Persistent likes, comments and creator-owned deletion.
- Google OAuth sign-in and sign-out, personal video feed.
- Mobile and desktop layouts, reduced motion and keyboard focus styles.
- Public Supabase Storage bucket with authenticated owner-folder upload/delete policies.
- RLS on all app tables. Public reads; authenticated users can write/delete only their own rows.

The feed starts empty. No fake creators, engagement or sample posts are inserted. Visitors can privately preview a device video without publishing it.

The bundled Supabase JS client is pinned to 2.57.4. Only the public publishable key is present. Source: https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2.57.4/dist/umd/supabase.js . Supabase JS is MIT licensed: https://github.com/supabase/supabase-js/blob/v2.57.4/LICENSE .

## Verification and limits

JavaScript syntax, live REST reads, row-level security configuration and Supabase security advisor checks passed. Browser UI verification could not run because the environment had no browser installed and the browser download failed. Full OAuth and authenticated publishing require the Google provider configuration above. This is a working starter social app, not TikTok's recommendation or moderation infrastructure. The feed is newest-first; uploads are public and served as original files, without transcoding. MP4 H.264 provides broad compatibility. Comments show the newest 100 entries; the feed loads 12 videos at a time. For a larger public launch, add moderation, abuse throttling and video transcoding. Configure Supabase quotas to match your expected usage.

Run locally with `python3 -m http.server 8080`, then open http://localhost:8080. Add the local URL to Supabase redirect URLs if testing OAuth locally.
