# Overleaf (Community Edition) on Umbrel

Collaborative self-hosted LaTeX editor for writing, editing, and publishing scientific documents.

## First-time Setup
1. Open the app from your Umbrel dashboard or navigate to `http://<umbrel-ip>:8185/launchpad`.
2. Follow the prompt on `/launchpad` to create your initial admin user.

## Installing TeX Live Packages (Fix Missing Packages)
The official Overleaf image comes with a minimal installation of TeX Live. If you encounter missing packages (like `babel-spanish`, `titlesec`, etc.):

1. Open the Overleaf terminal:
   * Go to `http://<umbrel-ip>/settings/terminal/app/makrron-overleaf` in your browser.
   * Or via SSH: `docker exec -it makrron-overleaf_server_1 bash`

2. Run inside the container:
   * Update manager:
     ```bash
     tlmgr update --self
     ```
   * Install missing packages (e.g. Spanish & titlesec):
     ```bash
     tlmgr install babel-spanish titlesec
     tlmgr path add
     ```
   * Or install popular collections:
     ```bash
     tlmgr install collection-latexextra collection-langspanish
     tlmgr path add
     ```
   * Or install the full TeX Live distribution (scheme-full):
     ```bash
     tlmgr install scheme-full
     tlmgr path add
     ```

## Persisting Packages Across Recreations
To permanently freeze the installed packages into your local Docker image:
```bash
docker commit makrron-overleaf_server_1 sharelatex/sharelatex:6.3.0
```
