<h1 align="center">Makrron App Store</h1>

<p align="center">
  A curated collection of community-packaged, self-hosted applications for <b>umbrelOS</b>.
</p>

<p align="center">
  <a href="https://umbrel.com"><img src="https://img.shields.io/badge/umbrelOS-Compatible-5351FB?style=flat-square&logo=linux" alt="umbrelOS Compatible" /></a>
  <a href="https://github.com/makrron/umbrel-community-app-store"><img src="https://img.shields.io/badge/Apps-2%20Available-brightgreen?style=flat-square" alt="Available Apps" /></a>
  <a href="https://github.com/makrron/umbrel-community-app-store/blob/master/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License" /></a>
</p>

---

## 📦 Available Applications

| App | Description | Category | Port | Architecture |
| :--- | :--- | :--- | :--- | :--- |
| <img src="https://raw.githubusercontent.com/makrron/umbrel-community-app-store/master/makrron-overleaf/icon.svg" width="32" height="32" valign="middle" /> **Overleaf** | Collaborative real-time LaTeX editor with instant PDF preview | `Developer` | `8185` | ![x86_64](https://img.shields.io/badge/arch-x86__64-informational?style=flat-square) |
| <img src="https://raw.githubusercontent.com/makrron/umbrel-community-app-store/master/makrron-simple-torrent/icon.svg" width="32" height="32" valign="middle" /> **SimpleTorrent** | Fast torrent client with modernized scrapers & shared downloads | `Networking` | `8086` | ![multi-arch](https://img.shields.io/badge/arch-multi--arch-success?style=flat-square) |

---

## 🚀 How to Install in Umbrel

Adding this Community App Store to your Umbrel server takes just a few seconds:

1. Open your Umbrel dashboard in your browser (`http://umbrel.local` or your server IP).
2. Open the **App Store**.
3. Click on the **Settings** icon in the top-right corner $\rightarrow$ select **Community App Stores**.
4. Paste the repository URL:
   ```text
   https://github.com/makrron/umbrel-community-app-store
   ```
5. Click **Add**.

The **Makrron App Store** will now appear in your App Store catalog, and its apps will be available to install with a single click.

---

## 📚 Application Guides

### 📄 Overleaf (Community Edition)

Overleaf Community Edition is a self-hosted, web-based collaborative LaTeX editor tailored for writing, editing, and compiling scientific documents.

#### 🔑 First-Time Administrator Setup
1. Launch Overleaf after installation or navigate to:
   ```text
   http://<umbrel-ip>:8185/launchpad
   ```
2. Follow the prompt to create your primary administrator account.

#### 🧩 Installing Additional TeX Live Packages
To keep the initial container size lightweight, Overleaf ships with a minimal TeX Live installation. When compiling documents that rely on packages like `babel-spanish`, `titlesec`, or extra fonts, install them using `tlmgr`:

1. **Access the container terminal:**
   * Via the Umbrel UI: `http://<umbrel-ip>/settings/terminal/app/makrron-overleaf`
   * Or via SSH on your host:
     ```bash
     docker exec -it makrron-overleaf_server_1 bash
     ```

2. **Run `tlmgr` inside the container:**
   ```bash
   # Update package manager
   tlmgr update --self

   # Option A: Install specific packages (e.g. Spanish language & titlesec)
   tlmgr install babel-spanish titlesec
   tlmgr path add

   # Option B: Install recommended collections (common math, fonts & language packs)
   tlmgr install collection-latexextra collection-langspanish
   tlmgr path add

   # Option C: Install full TeX Live distribution (~4-5 GB, includes all packages)
   tlmgr install scheme-full
   tlmgr path add
   ```

3. **Persist installed packages across container restarts:**
   Run the following on your host machine terminal to freeze the packages into your local Docker image:
   ```bash
   docker commit makrron-overleaf_server_1 sharelatex/sharelatex:6.3.0
   ```

---

### ⚡ SimpleTorrent (v1.4.0)

A lightweight remote torrent client with a web interface, built on a modernized Go engine.

* **Shared Storage**: Integrated directly with Umbrel's shared Downloads folder (`${UMBREL_ROOT}/data/storage/downloads`), enabling instant access from media servers like Jellyfin, Plex, and File Browser.
* **Overhauled Search**: Enhanced torrent search engine with modular scrapers and automated mirror failovers (1337x, The Pirate Bay, LimeTorrents, YTS, Nyaa, TorrentGalaxy).
* **Multi-Arch Native**: Prebuilt native support for `amd64` (x86_64) and `arm64` (Raspberry Pi 4/5, Umbrel Home).

---

## 🛠️ Requirements & Compatibility

* **umbrelOS**: 1.0 or newer (tested on 1.3+)
* **Architecture**:
  * **Overleaf**: Intel/AMD (`x86_64`)
  * **SimpleTorrent**: Intel/AMD (`x86_64`) and ARM64 (`aarch64`)

---

## 🤝 Contributing

Issues, feature requests, and pull requests are welcome! If you'd like to suggest an app to be packaged or report a bug, please [open an issue](https://github.com/makrron/umbrel-community-app-store/issues).

---

<p align="center">
  <sub>Maintained by <a href="https://github.com/makrron">@makrron</a> • Built for the Umbrel community</sub>
</p>
