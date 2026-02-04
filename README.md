# Windex

Windex is a single‑page, local‑first home dashboard that lets you arrange small widgets on a snap‑to‑grid layout. Everything runs in the browser with no build step.

## What we built
- A 4x4 grid dashboard with draggable, resizable widgets.
- View/Edit modes (view mode locks layout and hides editing controls).
- Widget management: add, edit, remove, and version widgets when they change.
- Safe widget content handling: widget HTML is sanitized to prevent inline script tag injection, while optional widget scripts are supported in a dedicated field.
- Local persistence in `localStorage` for layout and page metadata (title/subtitle, grid size, themes, and custom head HTML).
- Configuration panel with a live table of current widgets and a theme selector.
- Theme system powered by `meta.themes` and `meta.theme` (lightish default + dark/dusk/custom themes).
- Import/Export:
  - Export a JSON backup of the current layout and page metadata.
  - Import a JSON config and merge with local data by widget ID/version.
- Sample widgets and default metadata.
- View mode hides the grid lines.
- Meta editor supports custom `<head>` HTML with validation, plus a "Save anyway" option to persist raw tags.

## Files
- `index.html`: The full UI, styles, and logic (drag/resize, edit overlays, storage, import/export, themes).
- `widgets.json`: Example configuration (title/subtitle, grid size, themes + starter widgets).

## How to use
1. Open `index.html` in your browser.
2. Click `View mode` to switch to edit mode.
3. Drag widgets by the header, resize from the bottom‑right corner, and use `Add widget` to create new ones.
4. Click the page title to edit the dashboard title/subtitle and optional head HTML.
5. Use `Configuration` to export a backup or import a JSON config (such as `widgets.json`).
6. Use the Theme dropdown in Configuration to switch between themes.

## Notes
- All data is stored locally in your browser (`localStorage`).
- Import merges widgets by ID and keeps the newer version when there is a conflict.
- The grid size is the larger of the configured `gridCols`/`gridRows` and the space required by the widgets, so layouts are never clipped.

## Theme JSON Example
```json
{
  "meta": {
    "theme": "lightish",
    "headHtml": "<link rel=\"stylesheet\" href=\"https://cdn.example.com/app.css\">",
    "headHtmlUnsafe": false,
    "themes": {
      "lightish": {
        "bg-1": "#eef3f8",
        "bg-2": "#e2ebf3",
        "ink": "#1b2633",
        "accent": "#6d9bcf",
        "grid-line": "rgba(27, 38, 51, 0.12)",
        "grid-wrap": "linear-gradient(145deg, #f6f9fc, #dde7f1)",
        "card": "#f8fbff",
        "shadow": "rgba(27, 38, 51, 0.18)",
        "border": "rgba(27, 38, 51, 0.16)",
        "border-soft": "rgba(27, 38, 51, 0.08)"
      },
      "light": {
        "bg-1": "#f6f1e7",
        "bg-2": "#f1e9d9",
        "ink": "#1f1d1a",
        "accent": "#d38b5d",
        "grid-line": "rgba(31, 29, 26, 0.12)",
        "grid-wrap": "linear-gradient(145deg, #fff9f0, #f2e7d7)",
        "card": "#fff8ef",
        "shadow": "rgba(31, 29, 26, 0.2)",
        "border": "rgba(31, 29, 26, 0.18)",
        "border-soft": "rgba(31, 29, 26, 0.08)"
      },
      "dusk": {
        "bg-1": "#1b2331",
        "bg-2": "#243048",
        "ink": "#f6f2ea",
        "accent": "#f3b25d",
        "grid-line": "rgba(246, 242, 234, 0.14)",
        "grid-wrap": "linear-gradient(145deg, #2a344c, #1f2938)",
        "card": "#2b3446",
        "shadow": "rgba(0, 0, 0, 0.4)",
        "border": "rgba(246, 242, 234, 0.2)",
        "border-soft": "rgba(246, 242, 234, 0.08)"
      }
    }
  }
}
```

## Theme Tokens
- `bg-1`: Primary page background (used in the radial gradient).
- `bg-2`: Secondary page background (used in the radial gradient).
- `ink`: Primary text color.
- `accent`: Primary button color.
- `grid-line`: The faint grid overlay lines.
- `grid-wrap`: The background for the grid container area.
- `card`: Widget and panel background color.
- `shadow`: Main shadow color for widgets and panels.
- `border`: Standard border color for tables/inputs/handles.
- `border-soft`: Softer border or header background accents.

## Head HTML Validation
- Allowed tags: `script`, `link`, `style`, `meta`.
- Inline event handlers (e.g. `onclick`) and `javascript:` URLs are removed.
- "Save anyway" persists raw head HTML and sets `meta.headHtmlUnsafe` to true.

## Theme Checklist
Use this list to verify nothing is hardcoded when adding a new theme:
1. Page background gradient uses `bg-1` and `bg-2`.
2. Text uses `ink` across headers, body, and panels.
3. Primary buttons use `accent`.
4. Grid overlay lines use `grid-line`.
5. Grid container uses `grid-wrap`.
6. Widget and panel surfaces use `card`.
7. Shadows use `shadow`.
8. Borders (tables/inputs/handles) use `border` and `border-soft`.
