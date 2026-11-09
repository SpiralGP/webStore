# webStore setup log

Scaffolded 9 November 2026 by Devin, per `../../course-setup-prompt.md`.
First entry of the course-notes record suggested in `docs/spiralshop-course-mapping.md`.

## Working locations

- Course app: `/home/SpiralGP/projects/courses/webStore` (this repo)
- Reusable package/module: `/home/SpiralGP/projects/modules/spiralShop` (empty; built later)
- Existing product (do not modify): `C:\Users\Legend\Projects\SpiralShop` on the Windows host
- Course briefs/registers: `/home/SpiralGP/projects/courses/*.md` (copies in `docs/`)
- Port registry: `/home/SpiralGP/projects/PORT-MAP.md` — this app = **8001**

## Version matrix

| Component | Version |
|---|---|
| Laravel | 13.40.0 |
| PHP | 8.5.12 NTS (deb.sury.org, Debian 13 WSL) |
| Jetstream | 5.5 (Livewire stack) |
| Livewire | 3.8.11 |
| Sanctum | 4.3.3 |
| Pest | 5.x + pest-plugin-laravel |
| Tailwind CSS | 4.3.5 (CSS-first config, no tailwind.config.js) |
| Vite | 8.3.7 |
| Node / npm | 26.13.0 / 11.20.0 via nvm |
| Composer | 2.11.1 |
| Laravel Boost | 2.10 (dev; guidelines + skills + MCP) |

## Decisions and deviations from the 2024 course

- No starter kit at scaffold (`--no-authentication`); Jetstream installed the Livewire stack on top.
- **Tailwind upgraded 3→4** via `@tailwindcss/upgrade` on day one: config is CSS-first in
  `resources/css/app.css` (`@import`, `@plugin`, `@source`, `@theme`); 20 Jetstream blade files were
  auto-migrated (e.g. `shadow-sm`→`shadow-xs`, `outline-none`→`outline-hidden`). The course videos
  show Tailwind v3 config — expected divergence, minor class-name differences.
- **Laravel Boost installed as a dev tool** (user override of the original brief; the brief has
  since been corrected). Guidelines now live in `AGENTS.md`/`CLAUDE.md`; `boost` MCP config added.
- No git repo, no remote, no commits — ask before initialising jj/Git.
- No commerce models/migrations yet — they are created per-lesson (episode 3+), not upfront.

## Environment notes (WSL)

- PHP 8.5.12 lives in WSL (`/usr/bin/php8.5`, deb.sury.org). Windows Herd PHP also exists but is unused.
- Node is via nvm — **new terminals get it from `~/.bashrc`; scripts/cron must source `~/.nvm/nvm.sh`.**
- Windows `/mnt/c` npm/composer binaries exist on PATH — never use them against this tree
  (they already broke one build via UNC paths; node_modules was rebuilt with WSL Node).
- `php8.5-opcache` does not exist on deb.sury.org for trixie — not needed for `artisan serve`.
- `libatomic1` was apt-installed for nvm Node.
- Shells without nvm (non-interactive, or opened before `~/.bashrc` was updated) have no `node` —
  WSL interop then silently substitutes Windows `node.exe`, which fails on UNC paths inside npm
  scripts (seen as: `CMD.EXE ... 'multiplex' is not recognized`). Fix applied: nvm's node/npm/npx
  symlinked into `/usr/local/bin`. If `nvm install` changes the Node version, re-point the symlinks.
- `composer run dev` (`artisan dev` / multiplex) ignores `APP_URL`'s port and defaults `serve`
  to 8000. Fixed by re-registering the `server` dev command as `serve --port=8001` in
  `AppServiceProvider::boot()` — everything now runs on **8001**.

## Verification state at scaffold

- `php artisan test`: 25 passed / 7 skipped (46 assertions). Skips are feature-gated Jetstream
  tests (password resets, account deletion, email verification, 2FA, API tokens) — expected.
- `composer validate --strict`, `check-platform-reqs`, `composer audit`: clean.
- `npm audit`: 2 moderate — `postcss-selector-parser` via `@tailwindcss/typography`; fix requires
  `audit fix --force` (breaking) — deliberately not applied.
- Routes: 38 endpoints; `/`, `/login`, `/register` → 200 on `serve --port=8001`.

## Commands

```bash
cd /home/SpiralGP/projects/courses/webStore
composer run dev          # serve + queue + logs + vite via concurrently
php artisan serve --port=8001
php artisan test
npm run dev | npm run build
```

`composer run dev` must run from `webStore/` (there is no composer.json in `courses/`).

- Commit style (user preference): short, single-purpose messages, no footers,
  no co-author trailers, no "Generated with Devin" lines.

## For the next agent

- Read `docs/course-episode-register.md` and `docs/spiralshop-course-mapping.md` first.
- Setup is complete through episode 2 scope; begin coursework at episode 3 (model scaffolding).
- Never reuse SpiralShop's APP_KEY/DB/credentials; test-mode payments only (Stripe keys go in
  `.env` later, episode 19/20 — never commit them).
- Boost skills (`livewire-development`, `tailwindcss-development`, `testing-best-practices`,
  `fortify-development`) are installed — use them when working in those areas.
