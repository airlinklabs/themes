# Airlink panel v2 community themes

This branch contains theme packages for the **panel v2** rewrite. The `main`
branch keeps the original panel v1 themes (`pterolink/`).

## Packages

| Theme | Mode | Directory |
| --- | --- | --- |
| Solarized Light | light | [`solarized-light/`](solarized-light/) |
| Midnight | dark | [`midnight/`](midnight/) |

Each directory follows the v2 package format:

```
<theme-id>/
├── theme.json   # id, name, author, version, description, mode, css
└── theme.css    # --theme-* variables + classic Tailwind overrides
```

## Using the store

In panel v2, open **Admin → Settings → Themes** and set the community index
source to the raw `themes.json` on this branch:

```
https://raw.githubusercontent.com/airlinklabs/themes/panel-v2/themes.json
```

The store will list both themes. Installing downloads `theme.json` and
`theme.css` from the URLs in `themes.json` and writes them into
`frontend/public/themes/installed/<id>/`. Select the installed theme for light
or dark mode from the active-themes form.

## Adding a theme

1. Create a directory with a filename-safe `id` (`[a-zA-Z0-9][a-zA-Z0-9._-]{0,63}`).
2. Add `theme.json` with `mode` of `light`, `dark` or `both` and `css` pointing
   at your CSS file.
3. Add `theme.css` using the `--theme-*` variables from panel v1, plus any
   `!important` Tailwind overrides you need.
4. Add an entry to [`themes.json`](themes.json) with `files.theme.json` and
   `files.theme.css` pointing at raw URLs on this branch.
