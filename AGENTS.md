# Repository Guidelines

## Project Structure & Module Organization

This repository contains a Tampermonkey userscript for importing and exporting PKU Treehole followed posts.

- `PKU-Hole export tool.js`: main userscript, including metadata, DOM integration, API calls, import/export helpers, and UI behavior.
- `README.md`: user-facing installation and usage notes, with the Greasy Fork link.
- `LICENSE`: MIT license.

There is currently no separate `src/`, `test/`, or asset directory. Keep new code in the userscript unless the project grows enough to justify splitting helper files.

## Build, Test, and Development Commands

There is no package manager, bundler, or automated build step. Development is manual:

- Install the script in Tampermonkey, or paste the contents of `PKU-Hole export tool.js` into a local userscript.
- Visit `https://treehole.pku.edu.cn/web/*` while authenticated.
- Exercise import/export flows from the injected "import/export" UI.

Useful local inspection commands:

```powershell
rg "function|async function" "PKU-Hole export tool.js"
git diff
```

## Coding Style & Naming Conventions

Use plain browser JavaScript compatible with Tampermonkey and the target site. The existing script uses tabs for indentation, semicolons, `camelCase` function names, and async helpers for network and file operations. Keep metadata in the userscript header accurate, especially `@version`, `@match`, and `@description`.

Avoid adding dependencies unless there is a strong reason; this script is designed to run directly in the browser without a build pipeline.

## Testing Guidelines

No automated tests are configured. Validate changes manually in Tampermonkey:

- Export a small followed list and confirm both `.txt` and `.json` outputs are generated when applicable.
- Import a known-good JSON export and verify followed holes are restored as expected.
- Check browser console output for API, permission, or parsing errors.

When changing API calls, test with a real authenticated session because requests depend on cookies, `pku_token`, and `localStorage` values from the site.

## Commit & Pull Request Guidelines

Recent commits use short messages such as `Update README.md` and `update readme`. Prefer concise imperative messages that name the changed area, for example `Update export flow` or `Fix import JSON parsing`.

Pull requests should include a short description, manual test steps, affected browser/userscript manager versions, and screenshots or exported sample notes when UI behavior changes. Do not include private tokens, cookies, user IDs, or exported personal data.

## Security & Configuration Tips

Treat exported files as sensitive user data. Do not log authorization headers, cookies, `pku_token`, or raw private exports in issues, commits, or screenshots.
