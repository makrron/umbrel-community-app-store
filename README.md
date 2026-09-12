# Makrron Umbrel Community App Store

Community App Store for umbrelOS featuring custom and updated self-hosted applications.

## Apps Available

* **Overleaf (Community Edition)**: Collaborative cloud-based LaTeX editor for writing, editing, and publishing scientific documents.
* **SimpleTorrent (v1.4.0)**: Modernized fork of SimpleTorrent with updated scrapers, multi-arch support, and direct integration with Umbrel's shared Downloads folder.

## How to Install in Umbrel

1. Open your Umbrel dashboard.
2. Go to the **App Store**.
3. Click the settings icon in the top-right corner -> **Community App Stores**.
4. Add the repository URL:
   ```text
   https://github.com/makrron/umbrel-community-app-store
   ```
5. Click **Add**. You will now see the **Makrron App Store** in your App Store catalog!

## Overleaf (Community Edition) Guide

### 1. First-time Setup
After installing Overleaf:
1. Open the app from your Umbrel dashboard or navigate to `http://<umbrel-ip>:8185/launchpad`.
2. Follow the prompt on `/launchpad` to create your initial admin user.
3. Start creating and compiling your LaTeX documents!

### 2. Installing TeX Live Packages (Fix Missing Packages)
By default, the official Overleaf Docker image includes a minimal TeX Live installation. If your documents require extra packages (such as `babel-spanish`, `titlesec`, etc.), you can install them using the terminal:

1. Access the Overleaf container terminal from the Umbrel web UI:
   * Navigate in your browser to:
     ```text
     http://<umbrel-ip>/settings/terminal/app/makrron-overleaf
     ```
   * Or if you connect via SSH to your Umbrel host, open a shell in the container with:
     ```bash
     docker exec -it makrron-overleaf_server_1 bash
     ```

2. Inside the container, run the package manager:
   * **Update TeX Live package manager:**
     ```bash
     tlmgr update --self
     ```
   * **Option A: Install specific packages (e.g. Spanish language & titlesec):**
     ```bash
     tlmgr install babel-spanish titlesec
     tlmgr path add
     ```
   * **Option B: Install recommended collections (popular packages & languages):**
     ```bash
     tlmgr install collection-latexextra collection-langspanish
     tlmgr path add
     ```
   * **Option C: Install the complete TeX Live distribution (scheme-full, ~4–5 GB):**
     ```bash
     tlmgr install scheme-full
     tlmgr path add
     ```

### 3. Persist Installed Packages Across Container Recreations
In Docker, container filesystem changes are lost if the container is recreated or updated. To permanently preserve the installed packages across restarts or app reinstalls, run on your host server terminal:
```bash
docker commit makrron-overleaf_server_1 sharelatex/sharelatex:6.3.0
```
This updates your local Docker image with the installed packages, ensuring they persist permanently.
