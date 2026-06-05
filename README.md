# package-icons

Curated software icons/logos, keyed by package-manager ID (winget / Chocolatey), served via
[jsDelivr](https://www.jsdelivr.com/). A single controlled source of icon bytes, instead of
hotlinking dozens of uncontrolled third-party hosts.

## What this is for

For use in the following projects:

- **Winhance** → <https://github.com/memstechtips/Winhance>
- **Winhance website** → <https://winhance.net> (<https://github.com/memstechtips/winhance-website>)

The repo is public so the icons can be fetched at runtime via jsDelivr (and/or bundled at build
time). It is not a general-purpose icon CDN — it exists to serve those projects — but the layout
is deliberately app-agnostic so it can be reused.

## Naming convention

Icons live under `icons/` and are named by their **package-manager ID, lowercased**:

```
icons/<winget-or-choco-id>.png
```

- Lowercase always — GitHub and jsDelivr paths are case-sensitive, so normalizing avoids
  `Notepad++` vs `notepad++` mismatches.
- Use the **full** winget Package ID (e.g. `notepad++.notepad++.png`); fall back to the
  Chocolatey ID when there's no winget package.
- **PNG**, with a transparent background where the source provides one. Resolution is whatever
  the best available vendor asset ships — it is **not** normalized to a fixed size, so icons
  range from small (a vendor's only asset may be ~32px) up to a few thousand pixels.

## How to consume

Always **commit-pin** in shipped code — never `@main`/`@dev`/`@latest`. Pinned URLs are immutable
and cached, which is what guarantees the bytes can't change under users:

```
https://cdn.jsdelivr.net/gh/memstechtips/package-icons@<commit-sha>/icons/<id>.png
```

## Manifest

`manifest.json` lists every icon with its `sha256` and the app's package-manager identities, so
a consumer can map an app to its icon and detect when an icon's bytes change. Entry shape:

```json
{
  "icons": {
    "notepad++.notepad++.png": {
      "sha256": "…",
      "name": "Notepad++",
      "winget": ["Notepad++.Notepad++"],
      "choco": "notepadplusplus"
    }
  }
}
```

`msstore` and `downloadUrl` are included when the app defines them. Pin a commit and download
only the icons whose `sha256` differs from your last sync.

## Trademarks & removal requests

All product names, logos, and brands are the property of their respective owners. Icons are
included solely to identify the corresponding software (nominative fair use); no affiliation or
endorsement is implied. See [`THIRD-PARTY-NOTICES`](./THIRD-PARTY-NOTICES) for the full notice.

**If you are an individual or company that owns rights to a logo here and you want it removed,
please [open an issue](https://github.com/memstechtips/package-icons/issues) and it will be taken
down.** No need to escalate elsewhere first — an issue is the fastest way to reach me.

Microsoft's **Windows component** icons (built-in Store apps, capabilities, and optional
features) are intentionally **not** hosted here — those are resolved from the user's machine or
Microsoft-served sources. Microsoft's downloadable **applications** (e.g. Visual Studio Code,
PowerShell, PowerToys, Microsoft 365), however, are included like any other vendor's: they're
installed the same way via a package manager and identified under the same nominative fair use.
