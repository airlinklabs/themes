# Airlink panel v2 community themes

This branch contains theme packages for the **panel v2** rewrite. The `main`
branch keeps the original panel v1 themes (`pterolink/`).

## Packages

| Theme | Mode | Package | CSS source |
| --- | --- | --- | --- |
| Pterolink Light | light | [`pterolink-light/`](pterolink-light/) | [`pterolink/light.css`](pterolink/light.css) |
| Midnight | dark | [`midnight/`](midnight/) | [`midnight/theme.css`](midnight/theme.css) |

`Pterolink Light` reuses the existing v1 stylesheet from `pterolink/light.css`
through the index `files` map, so no CSS is duplicated. When installed it is
written to `installed/pterolink-light/theme.css`.

Each directory follows the v2 package format:

```
<theme-id>/
├── theme.json   # id, name, author, version, description, mode, css
├── theme.css    # --theme-* variables + classic Tailwind overrides
├── info.json    # store name, long description, updatedAt, preview images
└── images/      # cover + gallery screenshots (first image is the cover)
```

## Using the store

In panel v2, open **Admin → Settings → Themes** and browse **Community themes**.
The panel ships a local seed index; to use this branch directly, set
`COMMUNITY_THEMES_INDEX` (or `frontend/data/theme-sources.json`) to:

```
https://cdn.jsdelivr.net/gh/airlinklabs/themes@c2a922c/themes.json
```

The URL is pinned to a commit so the index and its file URLs always match.
Branch URLs can be cached by CDNs; after publishing changes, update the SHA in
this URL. The admin page no longer has a store-source field.

The store lists both themes as full-bleed cover cards with the details at the
bottom and a check mark over the image when active. Clicking a card opens a
centered popup with a hero preview, arrows, dots and small thumbnails for
browsing images, and the description at the bottom, plus an **Install** button
and a **GitHub** link to the source. Installing downloads every file listed in
the index `files` map — `theme.json`, CSS, `info.json` and all preview images —
and writes them into `frontend/public/themes/installed/<id>/`. Open the
installed card and use **Use for light** or **Use for dark**; the active card
gets a green border and a `✓ Active` label.

## Adding a theme

1. Create a directory with a filename-safe `id` (`[a-zA-Z0-9][a-zA-Z0-9._-]{0,63}`).
2. Add `theme.json` with `mode` of `light`, `dark` or `both` and `css` pointing
   at your CSS file.
3. Add `theme.css` using the `--theme-*` variables from panel v1, plus any
   `!important` Tailwind overrides you need.
4. Add `info.json` with `name`, `description`, `longDescription`, `updatedAt`
   and an `images` array. The first image is used as the tile cover.
5. Add the referenced screenshots to `images/` (`png`, `jpg`, `webp`, `gif` or
   `svg`).
6. Add an entry to [`themes.json`](themes.json). Its `files` map must include
   `theme.json`, the CSS file, `info.json`, and every image path from
   `info.json`, pointing at jsDelivr URLs on this branch:

   ```text
   https://cdn.jsdelivr.net/gh/airlinklabs/themes@panel-v2/<theme-id>/<file>
   ```
