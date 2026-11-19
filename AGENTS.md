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

- The game lives as original static HTML/JS pages in `public/gornitsa/`; `/` redirects there. Why: preserves the migrated vanilla-JS game exactly, with relative links between pages intact.
- Scene pictures are Lovable CDN assets; `public/gornitsa/gornitsa-assets.js` maps picture names to URLs and pages read it before their original filename fallback. Why: keeps large images out of the repo.
- Game progress stays in each visitor's browser storage (localStorage/sessionStorage/IndexedDB). Why: the source app had no server or accounts.
- The Baba Yaga chat calls Gemini only through the server route `/api/public/yaga-chat`, gated by the `yaga_ai` row in `app_settings`. Why: keeps the AI key off the browser and lets the shared AI be paused without code changes.
