# Ordendum — Warehouse & Office Order Tracking

Ordendum is a desktop app that replaces a shared spreadsheet for warehouse and office operations. It provides separate role-based views, simple status rules, and a cleaner workflow so orders move from received to ready to shipped without breaking dependencies.

## Features

- Separate role views
  - Office view: full data access and editing
  - Warehouse view: focused fields with required step order
- Order lifecycle with dependencies
  - Done must be checked before Ready
  - Done and Ready must both be checked before Shipped Picked
  - Warehouse must check RCVD before any of: Weight WH, Ship Today, Ready, Shipped Picked
- Optional fields: Clean, Stic, Comments, Ship Today
- Weight WH is ignored in logic/metrics
- Search and filter for quick order lookup
- Local persistence so work is saved between sessions
- Build artifacts are excluded from Git

## Role behavior and rules

- Office
  - Full table, can edit all fields, can correct mistakes
  - May perform bulk updates and exports (if enabled)
- Warehouse
  - Minimal table with required step order
  - Must set RCVD first before any other action
- Status dependencies
  - Done → Ready → Shipped Picked (in that order)
  - Weight WH is not used for logic

## Tech stack

- Electron (desktop shell)
- HTML, CSS, JavaScript (UI)
- Local persistence (for example JSON or a lightweight store; implementation detail)

## Project structure

Ordendum/
├─ app/                  # UI: HTML/CSS/JS
│  ├─ index.html
│  ├─ styles.css
│  └─ renderer.js
├─ main/                 # Electron main process
│  └─ main.js
├─ data/                 # local JSON/DB (ignored if sensitive)
├─ package.json
├─ .gitignore
└─ README.md

## Getting started

### Prerequisites
- Node.js 18 or newer
- npm

### Install
```bash
git clone https://github.com/UmrAsf/Ordendum.git
cd Ordendum
npm install
````

### Run (development)

```bash
npm start
```

### Build (production)

Update your package.json build scripts as needed (for example, electron-builder). Then:

```bash
npm run build
```

Build outputs such as out/ or dist/ should be ignored by Git and shared through Releases if needed.

## Data and safety

* Do not commit secrets or local databases.
* Large binaries (.app, .zip, .asar) should not be committed.
* Use GitHub Releases to share installers or archives.

## Roadmap

* Role-based authentication (separate sign-ins)
* CSV/PDF export of filtered orders
* GitHub Actions workflow to build and upload release artifacts
* Audit log for status changes
* Optional cloud sync for multi-machine use

## Contributing

* Open an issue first with a short proposal.
* Keep pull requests focused.
* Do not include build artifacts in commits.
