# Laratta Labs public repo standards

Every public repo under `github.com/larattalabs` follows this checklist. It builds on Noah's personal standard ([nlaratta/nlaratta STANDARDS.md](https://github.com/nlaratta/nlaratta/blob/main/STANDARDS.md)). Where they differ, this file wins for org repos. Forks of other people's projects are exempt, apart from keeping their license notices.

Decided by Noah on 2026-10-10.

## Checklist

- [ ] **License:** MIT, `Copyright (c) <year> Laratta Labs`. For code derived from someone else's MIT project, **keep their notice** and add ours below it ([see Licensing](#licensing)).
- [ ] **README** follows the [template](#readme-template), and its Quick start works verbatim from a fresh clone.
- [ ] **Hero:** lead with a real image (a screenshot, render or demo GIF) when the project has one. Otherwise use the generated studio banner at `.github/banner.png` ([see Branding](#branding)).
- [ ] **Social preview:** the generated studio-theme `social.png`, set under Settings → General → Social preview (browser only; no API).
- [ ] **CI:** `.github/workflows/ci.yml` named `CI`, runs on push and PR to `main`, and proves the project builds and its tests pass.
- [ ] **About sidebar:**
  - a one-sentence description;
  - 3–8 topics;
  - a homepage pointing to the project's page on noahlaratta.com (`https://noahlaratta.com/projects/<slug>`) once one exists.
- [ ] **Org profile:**
  - a row in the "Open source" table in [`profile/README.md`](profile/README.md);
  - an entry in `brand/profile.json` → `labs.openSource` in nlaratta/nlaratta (that list appears on Noah's profile);
  - consider pinning it on the org page (6 pins max; current: architect-mc, local-lab, blender-hunyuan3d-mac, lab-ui).
- [ ] **Keep profiles current:** when a repo is published, renamed, archived or made private, or a product changes, update both profiles and noahlaratta.com. The event-by-event table is in [Profile READMEs](https://github.com/nlaratta/nlaratta/blob/main/STANDARDS.md#profile-readmes).
- [ ] **Hygiene:** a full-history secret scan (`gitleaks git .`) before the repo goes public. No generated or local-only files committed.
- [ ] **New repos start private.** They go public only when Noah says so.

## Licensing

- **Original work:** use the standard MIT text with `Copyright (c) <year> Laratta Labs`.
- **Derived work:** MIT requires keeping the original copyright notice, so put both lines in the LICENSE. Follow [agentcraft-worlds](https://github.com/larattalabs/agentcraft-worlds/blob/main/LICENSE):

  ```
  Copyright (c) 2026 AgentCraft contributors
  Copyright (c) 2026 Laratta Labs (<project> changes)
  ```

  This covers **lab-ui**: its code moved out of AgentCraft Worlds, a fork of `blendi-remade/agentcraft` (MIT, "AgentCraft contributors"). Keep the upstream line and add the Laratta Labs line.
- **README footer:** `[MIT](LICENSE) © Laratta Labs`. For derived repos, add "Based on [upstream](link)."

## Branding

The studio palette and type come from [larattalabs.com](https://larattalabs.com):

| Token | Hex | Use |
|---|---|---|
| Rust | `#B7410E` | accent, license badge |
| Rust deep | `#8A2F06` | hover and pressed states |
| Iron | `#6B7280` | secondary text and rules on cream |
| Iron light | `#A3A9B3` | secondary text on ink (iron on ink is only 3.8:1; this is 7.8:1) |
| Ink | `#0F1419` | dark backgrounds |
| Cream | `#F8F7F4` | light backgrounds, text on ink |

Type: Inter for text, JetBrains Mono for labels and code. The mark (rust and iron brackets with a terminal chevron) is in [`profile/avatar.png`](profile/avatar.png). The vector is `public/mark.svg` in the private `larattalabs/website` repo.

**Generated banners and social previews** come from `brand/` in [nlaratta/nlaratta](https://github.com/nlaratta/nlaratta/tree/main/brand). Each `brand/repos.json` entry takes an `owner` field (default `nlaratta`). With `"owner": "larattalabs"`, the generator should:

- use the studio theme (ink or cream background, rust accent, the studio mark in place of Noah's avatar);
- label the eyebrow `larattalabs / <repo>`;
- link to `github.com/larattalabs/<repo>` in the generated profile README.

Run `pnpm build <repo>` for `out/<repo>/banner.png` and `social.png`, then `pnpm readme` for Noah's profile.

## README template

```markdown
<p align="center">
  <img src="<hero image or .github/banner.png>" alt="<what the image shows>" width="100%">
</p>

<p align="center">
  <a href="https://github.com/larattalabs/<repo>/actions/workflows/ci.yml"><img src="https://github.com/larattalabs/<repo>/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-B7410E" alt="MIT license"></a>
  <!-- project badges (Minecraft version, loader, platform…) use iron 6B7280 or rust B7410E -->
</p>

<One or two sentences: what it is and who it's for.>

## Quick start
## How it works          <!-- or "What it does" -->
## Project structure     <!-- optional -->

## License

[MIT](LICENSE) © Laratta Labs · Built by [Laratta Labs](https://larattalabs.com)
```

Keep it honest and brief. Skip sections you'd only fill with padding. Mark planned features as planned (Steward: "Early planning stage").

## CI and releases

- **CI:** follow the nlaratta conventions for action versions (`actions/checkout@v7`, `actions/setup-java@v6`, `actions/setup-node@v7`, and so on).
- **Fabric / Minecraft mods** (architect-mc, lab-ui, steward-mc, agentcraft-worlds):
  - a `v*` tag runs `.github/workflows/publish.yml`, which publishes `dev.larattalabs:<artifact>` to **GitHub Packages (Maven)**;
  - consumers such as Architect read `dev.larattalabs:lab_ui` from there;
  - versions are semver, documented in each README's "Versioning" section.
- **Other projects:** publish to the ecosystem's registry (npm, PyPI) only when Noah asks.

## Web pages

Org open-source projects get pages on Noah's portfolio, not on larattalabs.com, which stays focused on clients and products. Each one is an entry in `lib/projects.ts` in [nlaratta/noahlaratta](https://github.com/nlaratta/noahlaratta) with `context: 'Laratta Labs'`. The page URL then goes in the repo's homepage field. Merging to that repo deploys noahlaratta.com, so it needs Noah's OK.
