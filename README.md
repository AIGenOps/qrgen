# Mini QR

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

An app to create beautiful QR codes and scan various QR code types.

## Features

- ✅ Accessible: minimally WCAG A compliant
- 🎨 Customizable colors and styles
- 🖼️ Export to PNG, JPG & SVG\*
- 📋 Copy to clipboard
- 🌓 Light/dark/system-preference mode toggle
- 🎲 Randomize style button
- 🌐 Available in 30+ languages
- 💾 Save & Load QR Code config
- 🖼️ Upload custom image for logo
- 🎭 Presets: Pre-crafted QR code styles
- 🖌️ Frame customization: Add text labels and style the frame around your QR code
- 🛡️ Error correction level: affects the size of the QR code and logo within
- 📱 QR Code Scanner: Scan QR codes using your camera or by uploading images
- 📦 Batch data export: Import a CSV file with multiple data strings and export QR codes for them all at once
- 📲 PWA Support: Install MiniQR as a desktop or mobile app
- 📝 Data templates: Support for various data types including text, URLs, emails, phone numbers, SMS, WiFi credentials, vCards, locations, and calendar events

\*SVG export has limited support and may not display correctly in all software.

## Self-hosting

### Self-hosting with Docker 🐋

Mini-QR can easily be self-hosted using Docker. We provide a [docker-compose.yml](docker-compose.yml) file and a production-ready multi-stage [Dockerfile](Dockerfile).

Quick Start (using prebuilt image)

```bash
wget https://github.com/AIGenOps/qr-gen/raw/main/docker-compose.yml

docker compose up -d
```

This will pull the latest production image from GitHub Container Registry and start the app at [http://localhost:8081](http://localhost:8081).

To build and run locally (for development or custom builds)

```bash
docker compose up -d --build
```

Or build and run manually:

```bash
docker build -t mini-qr .
docker run -d -p 8081:8080 mini-qr
```

### Self-hosting without Docker 🌐

You can also simply compile the application directly using NPM and Vite like follows:

```bash
git clone https://github.com/AIGenOps/qr-gen.git
cd mini-qr
npm install
npm run build
```

From there, the application will be built into `dist` folder and this folder can simply be hosted from any kind of web server.

### Environment Variables

| Variable                      | Description                                                                        | Default   |
| ----------------------------- | ---------------------------------------------------------------------------------- | --------- |
| `BASE_PATH`                   | Base path for deployment                                                           | `/`       |
| `VITE_HIDE_CREDITS`           | Set to `"true"` to hide credits in the footer                                      | `"false"` |
| `VITE_DEFAULT_PRESET`         | Name of the default QR code preset to load                                         | `""`      |
| `VITE_DEFAULT_DATA_TO_ENCODE` | Default data to encode when the app first loads                                    | `""`      |
| `VITE_QR_CODE_PRESETS`        | JSON string defining custom QR code presets                                        | `"[]"`    |
| `VITE_FRAME_PRESET`           | Name of the default frame preset to load                                           | `""`      |
| `VITE_FRAME_PRESETS`          | JSON string defining custom frame presets                                          | `"[]"`    |
| `VITE_DISABLE_LOCAL_STORAGE`  | Set to `"true"` to disable loading saved settings from local storage on startup    | `"false"` |

## Development

```bash
# Install dependencies
pnpm install

# Start dev server
pnpm dev

# Run unit tests
pnpm vitest

# Run E2E tests
pnpm test:e2e

# Lint & format
pnpm lint
pnpm format

# Build for production
pnpm build
```

## License

[GPL-3.0](LICENSE)

---

Made by **AIGenOps**
