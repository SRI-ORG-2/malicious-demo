# Malicious Package Detection Demo

Demo repository for testing Aqua's **Malicious Package Detection & Blocking** feature.

> ⚠️ **WARNING**: This repository contains known malicious packages for demonstration purposes only. Do NOT install these packages.

## Quick Start

1. **Fork/clone** this repo to your GitHub
2. **GitHub Secrets** (`AQUA_KEY` / `AQUA_SECRET`):
   - If you already have org-level secrets configured, skip this step
   - Otherwise, add them in repo Settings → Secrets → Actions
3. **Update URLs** in `.github/workflows/aqua.yml` for your region
4. **Connect** the repo in Aqua UI (Supply Chain Security → Integrations)
5. **Create PR** from `test/add-malicious-packages` → `main`

## Regional URLs

Update `.github/workflows/aqua.yml` with your region:

| Region | AQUA_URL | CSPM_URL |
|--------|----------|----------|
| US | `https://api.supply-chain.cloud.aquasec.com` | `https://api.cloudsploit.com` |
| EU | `https://api.eu-1.supply-chain.cloud.aquasec.com` | `https://eu-1.api.cloudsploit.com` |
| Asia | `https://api.asia-1.supply-chain.cloud.aquasec.com` | `https://asia-1.api.cloudsploit.com` |

## What's In This Demo

**Main branch** (baseline): 
- `express@4.18.2` - clean package (2 MEDIUM CVEs)
- `payu-ui-v2@1.0.0` - malicious package (already in codebase)
- `react@18.2.0` - clean package

**PR branch** (`test/add-malicious-packages`): Adds NEW malicious packages:
- `mstate-cli@0.4.7` - backend
- `lemaaa@1.0.0` - backend (dev)
- `discord-selfbot-v14@1.0.0` - frontend
- `noblox.js-vps@1.0.0` - frontend

## Expected Result

PR will be blocked with the NEW malicious packages detected:
```
The PR has been blocked due to the following known malicious packages:
lemaaa@1.0.0 (MAL-2022-4280) [dev]
mstate-cli@0.4.7 (MAL-2025-47329)
discord-selfbot-v14@1.0.0 (MAL-2022-2490)
noblox.js-vps@1.0.0 (MAL-2023-1044)
```

Note: The baseline malicious package (`payu-ui-v2`) is already in main, so only newly introduced malicious packages trigger the block.

## Troubleshooting

- **Not detecting malicious?** Contact Aqua to enable Malicious Package Detection
- **Scanner not running?** Check `AQUA_KEY`/`AQUA_SECRET` secrets are set
