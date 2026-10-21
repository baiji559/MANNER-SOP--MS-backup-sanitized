# Sanitized backup

This repository is a fresh backup without the original Git histories.

Removed from the backup:

- dependency directories and downloaded Android SDK/build tools
- build caches, APKs, ZIP deployment packages, and signing keystores
- local Wrangler state and environment files

Replaced with placeholders:

- the owner email (`owner@example.invalid`)
- the Supabase project reference and publishable key
- OpenAI Hosting project IDs

Before deploying, replace the placeholders using values from the intended environment. Keep service-role keys, Cloudflare tokens, emergency access codes, signing keys, and other credentials in the relevant platform secret store rather than in Git.
