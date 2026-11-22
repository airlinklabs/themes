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

In panel v2, open **Admin → Settings → Themes** and set the community index
source to the raw `themes.json` on this branch:

```
https://cdn.jsdelivr.net/gh/airlinklabs/themes@panel-v2/themes.json
```

jsDelivr is recommended because `raw.githubusercontent.com` can serve a cached
index for a while after a branch is updated.

The store lists both themes as image tiles. Clicking a tile opens a popup with
the preview gallery, full description and an **Install** button plus a
**GitHub** link to the source. Installing downloads every file listed in the
index `files` map — `theme.json`, CSS, `info.json` and all preview images — and
writes them into `frontend/public/themes/installed/<id>/`. Select the installed
theme for light or dark mode from the active-themes form; the selected tile gets
a green border and check mark.

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
