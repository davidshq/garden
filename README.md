# Dave's Digital Garden

An Obsidian vault published with Quartz 5.1.0 at https://garden.davemackey.net/.

## Local development

Use Node.js 24 and npm 10.9.2 or newer:

```sh
npm ci
npx quartz plugin install
npx quartz plugin doctor
npx quartz build --serve
```

Site settings, plugin options, and layout are in `quartz.config.yaml`.
The `quartz.ts` entry point loads that configuration. Plugin packages are
pinned by `package-lock.json`; npm plugins do not require `quartz.lock.json`.

Obsidian Bases (`.base` files, embedded Bases, and inline `base` blocks) render
through BasesPage. Their results update when the site rebuilds. Dataview query
blocks are not evaluated by this configuration.

The vault is in `content/`. `.obsidian`, `.smart-env`, `private`, and `templates`
are excluded from publication. Smart Environment files remain local and are
ignored by Git. Only assets referenced by published pages are copied.

## Validation

```sh
npx tsc --noEmit
npm test
npx quartz plugin doctor
npx quartz build
```

The garden check workflow runs these checks for pull requests. The deployment
workflow publishes pushes to `v5` to GitHub Pages. The previous `v4` branch is
retained for rollback. Existing aliases and redirects for mixed-case v4 URLs
are handled by AliasRedirects.

## Updating Quartz

This migration uses the stable `v5.1.0` release. On v5, `npx quartz upgrade`
pulls the upstream v5 branch, restores plugins, and runs compatibility checks;
that branch may contain changes beyond the latest release. Review the
upstream changes before upgrading. Commit intentional note edits first and
review plugin or dependency changes before publishing.

[Quartz documentation](https://quartz.jzhao.xyz/)
