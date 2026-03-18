# Mini QR — Project Summary

> **Version:** 0.13.1 · **License:** GPL-3.0 · **Package Manager:** pnpm 8.14.0

## Overview

**Mini QR** is an open-source, feature-rich Progressive Web App (PWA) for **creating** and **scanning** QR codes. It is built with **Vue 3**, **Vite**, and **TailwindCSS**, and supports 50+ languages via **vue-i18n**. The project is maintained by **AIGenOps**.

**Live Demo:** [mini-qr-code-generator.vercel.app](https://mini-qr-code-generator.vercel.app/)

---

## Tech Stack

| Layer         | Technology                                                      |
| ------------- | --------------------------------------------------------------- |
| Framework     | Vue 3 (Composition API, `<script setup>`, TypeScript)           |
| Build Tool    | Vite 5                                                          |
| Styling       | TailwindCSS 3 + PostCSS + tailwindcss-animate                   |
| UI Primitives | Radix Vue / Reka UI (Accordion, Button, Combobox, Dialog, etc.) |
| QR Engine     | `qr-code-styling` (generation), `html5-qrcode` / `qr-scanner` (scanning) |
| i18n          | vue-i18n (50 locale files in `/locales`)                        |
| PWA           | vite-plugin-pwa + Workbox runtime caching                       |
| Icons         | Lucide (via `lucide-vue-next`) + inline SVGs                    |
| Image Export  | `dom-to-image`, `dom-to-svg`, `file-saver`, `jszip`            |
| Linting       | ESLint 9 + Prettier + lint-staged + Husky                       |
| Testing       | Vitest (unit) + Playwright (e2e)                                |
| Containerisation | Docker (multi-stage) + Nginx + docker-compose                |

---

## Key Features

- ✅ **WCAG-A Accessible** — keyboard navigable, ARIA labels, focus-visible styles
- 🎨 **Customisable QR Codes** — colors, dot/corner styles, error correction levels
- 🖼️ **Export** — PNG, JPG, SVG; copy-to-clipboard support
- 🎭 **Presets** — pre-crafted brand-themed QR styles (Supabase, Vercel, Padlet, etc.)
- 🖌️ **Frame Customisation** — text labels and styled frames around QR codes
- 🌐 **30+ Languages** — community-translated via Crowdin
- 🌓 **Dark / Light / System Mode** — toggle with persistence
- 🎲 **Randomise Style** — one-click style randomiser
- 💾 **Save & Load Configs** — persist QR settings to local storage
- 🖼️ **Custom Logo Upload** — embed images inside QR codes
- 📱 **QR Scanner** — camera-based and image-upload scanning with smart detection (URL, email, phone, WiFi, vCard, etc.)
- 📦 **Batch Export** — import CSV → bulk-generate QR codes as a ZIP
- 📝 **Data Templates** — URL, email, phone, SMS, WiFi, vCard, location, calendar event
- 📲 **PWA** — installable on desktop & mobile with offline support

---

## Project Structure

```
mini-qr-main/
├── .github/
│   ├── FUNDING.yml              # GitHub Sponsors config
│   └── workflows/
│       ├── docker.yml           # CI: build & push Docker image
│       └── test.yml             # CI: run tests
├── locales/                     # 50 i18n JSON files (en, fr, ja, zh, …)
├── public/
│   ├── presets/                 # Pre-built QR SVG presets
│   ├── app_icons/               # PWA icons & splash screens
│   ├── CHANGELOG.md             # Release notes
│   └── *.csv                    # Sample batch-export CSVs
├── scripts/
│   ├── generate-pwa-icons.js    # Sharp-based icon generator
│   ├── generate-splash-screens.js
│   ├── generate-version.sh      # Changelog auto-generation
│   └── sync-i18n.mjs           # Locale key synchronisation
├── src/
│   ├── main.js                  # App entry point (Vue + i18n + PWA registration)
│   ├── App.vue                  # Root component (header, mode toggle, routing)
│   ├── index.css / style.css    # Global styles
│   ├── assets/                  # Static assets
│   ├── components/
│   │   ├── QRCodeCreate.vue     # Main creation UI (71 KB, largest component)
│   │   ├── QRCodeScan.vue       # Scanner UI (camera + upload)
│   │   ├── QRCodeCameraScanner.vue
│   │   ├── QRCodeFrame.vue      # Frame renderer
│   │   ├── StyledQRCode.vue     # QR rendering wrapper
│   │   ├── DataTemplatesModal.vue # Data template picker
│   │   ├── BatchExportFieldsGuide.vue
│   │   ├── CopyImageModal.vue
│   │   ├── VCardPreview.vue
│   │   ├── LanguageSelector.vue
│   │   ├── MobileMenu.vue       # Hamburger menu for mobile
│   │   ├── AppFooter.vue
│   │   └── ui/                  # Reusable UI primitives (Radix/Reka wrappers)
│   │       ├── accordion/
│   │       ├── button/
│   │       ├── Combobox/
│   │       ├── command/
│   │       ├── dialog/
│   │       ├── drawer/
│   │       └── popover/
│   ├── lib/
│   │   └── utils.ts             # clsx + tailwind-merge helper
│   └── utils/
│       ├── basePath.ts          # Dynamic base-path resolution
│       ├── clipboard.ts         # Clipboard API wrapper
│       ├── color.ts             # Colour utilities
│       ├── convertToImage.ts    # DOM → PNG/JPG/SVG export logic
│       ├── css.ts / css.test.ts
│       ├── csv.ts / csv.test.ts # CSV parsing for batch import
│       ├── csvBatchProcessing.ts / .test.ts
│       ├── dataEncoding.ts / .test.ts  # Encode various data types for QR
│       ├── formatting.ts
│       ├── framePresets.ts / .test.ts
│       ├── i18n.ts              # vue-i18n setup & locale loading
│       ├── language.ts          # Language detection
│       ├── qrCodePresets.ts / .test.ts # Built-in QR style presets
│       ├── useDarkModePreference.ts    # Composable for dark mode
│       └── useQRCodeStorage.ts / .test.ts  # localStorage persistence
├── tests/
│   └── e2e/
│       ├── create.spec.ts       # Playwright E2E tests for QR creation
│       └── scan.spec.ts         # Playwright E2E tests for scanning
├── Dockerfile                   # Multi-stage build (Node → serve)
├── docker-compose.yml           # Docker Compose config
├── nginx.conf / nginx-proxy.conf
├── vite.config.js               # Vite config with PWA plugin
├── tailwind.config.js           # TailwindCSS config with custom theme
├── tsconfig.json / tsconfig.node.json
├── vitest.config.ts / vitest.workspace.ts
├── eslint.config.js
├── playwright.config.ts
├── package.json
├── .env.example                 # Env var documentation
└── README.md / CONTRIBUTING.md / CODE_OF_CONDUCT.md / LICENSE
```

---

## Application Architecture

### Entry & Root

- **`main.js`** — bootstraps Vue 3, installs `vue-i18n`, registers the Service Worker.
- **`App.vue`** — root component with two modes: **Create** and **Scan**, toggled via a segmented control in both desktop and mobile headers. Includes scroll-aware header collapse, dark mode toggle, language selector, and GitHub link.

### Core Components

| Component                   | Purpose                                                        |
| --------------------------- | -------------------------------------------------------------- |
| `QRCodeCreate.vue`          | Full creation interface — data input, style options, presets, export, frames, batch export. The largest component (~71 KB). |
| `QRCodeScan.vue`            | Scanning interface — camera or image upload, smart detection of data types. |
| `QRCodeCameraScanner.vue`   | Camera-based live QR scanning via `html5-qrcode`.              |
| `StyledQRCode.vue`          | Renders a styled QR code using `qr-code-styling`.              |
| `QRCodeFrame.vue`           | Renders the decorative frame around a QR code.                 |
| `DataTemplatesModal.vue`    | Modal for picking data templates (URL, vCard, WiFi, etc.).     |
| `BatchExportFieldsGuide.vue`| Guide for CSV batch import fields.                             |
| `VCardPreview.vue`          | Preview for vCard contact data.                                |
| `CopyImageModal.vue`        | "Copied to clipboard" feedback modal.                          |

### Utility Modules

| Module                     | Purpose                                           |
| -------------------------- | ------------------------------------------------- |
| `dataEncoding.ts`          | Encodes text, URL, email, phone, SMS, WiFi, vCard, location, and calendar data into QR-scannable strings. |
| `qrCodePresets.ts`         | Defines 15+ built-in style presets with colours, dot types, and logos. |
| `framePresets.ts`          | Defines frame style presets (border, text, colours). |
| `convertToImage.ts`        | Exports QR codes to PNG, JPG, and SVG using `dom-to-image`. |
| `csv.ts` / `csvBatchProcessing.ts` | Parses CSV files and generates batch QR code exports as ZIP. |
| `clipboard.ts`             | Wraps the Clipboard API for copy-to-clipboard functionality. |
| `useDarkModePreference.ts` | Vue composable — detects system preference, toggles, and persists dark mode. |
| `useQRCodeStorage.ts`      | Vue composable — saves/loads QR configs from localStorage. |
| `i18n.ts`                  | Sets up vue-i18n, lazy-loads locale files based on browser language. |

---

## Environment Variables

| Variable                      | Description                              | Default   |
| ----------------------------- | ---------------------------------------- | --------- |
| `BASE_PATH`                   | Base path for deployment                 | `/`       |
| `VITE_HIDE_CREDITS`           | Hide footer credits                      | `"false"` |
| `VITE_DEFAULT_PRESET`         | Default QR style preset name             | `""`      |
| `VITE_DEFAULT_DATA_TO_ENCODE` | Default data for the QR                  | `""`      |
| `VITE_QR_CODE_PRESETS`        | Custom preset definitions (JSON)         | `"[]"`    |
| `VITE_FRAME_PRESET`           | Default frame preset name                | `""`      |
| `VITE_FRAME_PRESETS`          | Custom frame preset definitions (JSON)   | `"[]"`    |
| `VITE_DISABLE_LOCAL_STORAGE`  | Disable loading saved settings           | `"false"` |

---

## Development

```bash
# Install dependencies
pnpm install

# Start dev server (http://localhost:5173)
pnpm dev

# Run unit tests
pnpm vitest

# Run E2E tests (Playwright)
pnpm test:e2e

# Lint & format
pnpm lint
pnpm format

# Build for production
pnpm build
```

---

## Deployment

### Vercel (Primary)
The live demo is hosted on Vercel at [mini-qr-code-generator.vercel.app](https://mini-qr-code-generator.vercel.app/).

### Docker
```bash
# Quick start with prebuilt image
docker compose up -d
# → http://localhost:8081

# Build locally
docker compose up -d --build

# Deploy at a subdirectory
BASE_PATH=/mini-qr docker compose up -d
```

The Docker setup uses a multi-stage build (Node LTS Alpine → `serve` for static hosting) with optional Nginx reverse proxy support.

---

## CI/CD

| Workflow       | File                         | Trigger              | Actions                      |
| -------------- | ---------------------------- | -------------------- | ---------------------------- |
| **Test**       | `.github/workflows/test.yml` | Push / PR            | Runs linting and test suite  |
| **Docker**     | `.github/workflows/docker.yml` | Push to main / tags | Builds & pushes Docker image to GHCR |

---

## Testing

- **Unit Tests** — Vitest with browser mode (`@vitest/browser`), covering: CSV parsing, data encoding, CSS utilities, QR/frame presets, localStorage storage.
- **E2E Tests** — Playwright specs for QR creation flow (`create.spec.ts`) and scanning flow (`scan.spec.ts`), with visual regression snapshot support.

---

## Internationalisation

- **50 locale files** in `/locales` (e.g., `en.json`, `ja.json`, `zh.json`, `fr.json`, `ar.json`, …)
- Translation management via **Crowdin** ([crowdin.com/project/miniqr](https://crowdin.com/project/miniqr))
- Locale synchronisation script: `scripts/sync-i18n.mjs`
- Auto-detects browser language on first load

---

## Contributors

The project follows the [All Contributors](https://allcontributors.org/) specification, with 20+ contributors providing code, translations, design, documentation, and reviews. Community contributions (translations & bug fixes) are welcomed.
