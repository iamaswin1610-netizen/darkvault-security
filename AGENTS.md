<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.

## What Lovable manages

Rules outside this block are the project's own. Change the pieces below in
Lovable, not by hand. With the [Lovable MCP](https://mcp.lovable.dev)
connected, `send_message` asks Lovable to do it; otherwise ask the user to
use the editor.

- **Database.** Do not add or edit `supabase/migrations/` or `drizzle/`.
  Ask Lovable to change the schema.
- **Generated files.** Do not edit a file whose header says it is automatically
  generated.
- **AI gateway.** Keep model calls on Lovable's gateway, and keep
  `LOVABLE_API_KEY` out of browser code.
- **Connectors.** Lovable provides native connectors. `list_connectors` shows
  which are enabled; `add_connector` only returns the dashboard link. When a
  connector is enabled, calls go through the connector gateway and need
  `LOVABLE_API_KEY`. When Lovable does not provide one, users can bring their
  own key and store it in Secrets.
- **Secrets.** Lovable manages them. Do not put secret values in the repo.
<!-- LOVABLE:END -->

## Project rules

- All vault data is local-only in IndexedDB (`src/lib/db.ts`); no backend. Why: the design requires files and reminders to never leave the phone.
- Security code is stored only as a salted PBKDF2 hash; file bytes are AES-GCM encrypted with a non-extractable device key (`src/lib/crypto.ts`). Why: protection must be real, not only visual.
- Unlocked state lives only in memory in `VaultProvider` (`src/lib/vault.tsx`); every screen behind the lock sits under the `_vault` pathless layout. Why: a reload or auto-lock must always return to the security check.
- Pure business rules (lockout, folder names, alert timing) live in `src/lib/lockout.ts` and `src/lib/rules.ts` with tests in `src/test/vault-rules.test.ts`. Why: keeps them testable without browser APIs.
- Folder/category colours use `--tone-*` tokens set via `toneVar()` plus `tone-*` utilities in `src/styles.css`. Why: dynamic colours without hardcoded classes.
- Installable on Android via `public/manifest.webmanifest` only (no service worker). Why: home-screen app without preview caching problems.
