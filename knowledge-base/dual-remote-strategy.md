# Dual-Remote Strategy & Workflow

This document describes how we maintain a custom version of OpenClaw while remaining compatible with the official upstream updates.

## Remote Configuration

We use two remotes:

1. **upstream**: The official OpenClaw repository (`https://github.com/openclaw/openclaw`).
2. **origin**: Your private repository for backups and collaboration (`git@github.com:robig/openclaw.git`).

## Branching Strategy

- **main**: Tracks `upstream/main`. Keep this clean.
- **local-main**: Our production branch. It contains `main` plus our local features.
- **feature/\***: Short-lived branches for specific logic (e.g., `feature/chat-history-up-arrow`).

## The Update Workflow

To pull official updates and keep our local features active:

1. **Update local main from official source:**

   ```bash
   git checkout main
   git pull upstream main
   git push origin main
   ```

2. **Rebase/Merge into local-main:**

   ```bash
   git checkout local-main
   git merge main
   ```

3. **Deploy & Build:**

   ```bash
   # Rebuild the UI if UI files were changed
   cd ui && npm install && npm run build
   # Restart the service
   openclaw gateway restart
   ```

4. **Backup:**
   ```bash
   git push origin local-main
   ```

## Active Local Features

- **Arrow Up History**: Recall last user message in the Web UI when input is empty.
- **Dedicated API Plugin**: Session-isolated API endpoints for external integration.

---

_Maintained by NeoBot & Robert._
