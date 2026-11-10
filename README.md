# DarkVault

A private, offline vault for Android phones. Store documents and reminders behind a 6-digit security code — everything stays on your phone.

## Features
- 6-digit security code setup and unlock, with lockout after 5 wrong tries
- Optional fingerprint unlock (on supported phones)
- Documents: folders, upload, open, rename, move, delete — file contents are encrypted
- Reminders: categories, multiple alerts, calendar, upcoming and history views
- Settings: profile, security, appearance (dark/light, binary rain), notifications, storage
- Encrypted backup and restore
- Installs on Android from Chrome ("Install app" / "Add to Home screen")

## Security
- The security code is never stored — only a salted PBKDF2-SHA-256 hash.
- Files are encrypted with AES-GCM using a key that cannot be exported from the device.
- All data lives in the browser's IndexedDB. No server, no account, no internet needed.

## Run in VS Code
Requires Node.js 20 or newer (https://nodejs.org).

```sh
npm install
npm run dev
```
Open the address shown (e.g. http://localhost:8080). Use your browser's phone view for the intended layout.

| Command | What it does |
| --- | --- |
| `npm run dev` | Start the app locally |
| `npm run build` | Create the production build in `dist/` |
| `npm run preview` | Preview the production build |
| `npm test` | Run the tests |
| `npm run lint` | Check code style |

Bun also works: `bun install` then `bun run dev`.

## Project layout
```
public/             App icons and install manifest
src/assets/         Logo and splash artwork
src/components/vault/  DarkVault screens' building blocks
src/components/ui/  Shared UI toolkit
src/lib/            Storage, encryption, vault session, rules, backup
src/routes/         Screens (setup, unlock, home, documents, reminders, settings)
src/test/           Tests
```

## Notes
- No environment variables, database or service worker are needed.
- `node_modules/` and `dist/` are created on your computer by the commands above.
- Clearing browser data deletes the vault — make an encrypted backup first.
