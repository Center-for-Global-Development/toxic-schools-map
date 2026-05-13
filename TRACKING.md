# Event Tracking: Toxic Schools Map

`interactive_name`: `toxic-schools-map`

Tracking implemented per the CGD Interactive Analytics Tracking Standard. Events are sent from the embedded iframe to the cgdev.org parent via `window.parent.postMessage(...)` and forwarded to GA4 via GTM.

## Tracked Events

### `interactive_view`

Fired once when `index.html` executes. No additional parameters beyond `interactive_name`.

### `interactive_engagement`

| `action_type` | `action_label` | `action_value` | Trigger |
|---|---|---|---|
| `filter` | `layer_sites` | `on` / `off` | Toggle "Polluted sites (TSIP)" checkbox |
| `filter` | `layer_schools_1km` | `on` / `off` | Toggle "Schools within 1 km" checkbox |
| `filter` | `layer_schools_5km` | `on` / `off` | Toggle "Schools 1–5 km" checkbox (also triggers lazy load on first `on`) |
| `filter` | `layer_buffers` | `on` / `off` | Toggle "5km buffer circles" checkbox |
| `filter` | `country_filter` | country name (e.g. `India`, `Indonesia`) — omitted when reset to "All countries" | Country dropdown change |
| `filter` | `industry_filter` | one of: `Battery (ULAB)`, `Manufacturing`, `Mining & smelting`, `Other`, `Recycling & waste` — omitted when reset to "All industries" | Industry dropdown change |
| `detail_open` | `site_popup` | industry name (5 values, bounded) | Click on a polluted-site marker |
| `detail_open` | `school_1km_popup` | country name (~19 values, bounded) | Click on a school marker inside 1 km cluster |
| `detail_open` | `school_5km_popup` | country name (~19 values, bounded) | Click on a school marker inside 1–5 km cluster |
| `external_link` | `about_page` | — | Click "About & paper" link in the side panel |
| `external_link` | `source_pure_earth` | — | Click Pure Earth / contaminatedsites.org link in attribution |
| `external_link` | `source_overture` | — | Click Overture Maps link in attribution |

## Cardinality Notes

- Site and school popups use **bounded category values** (industry for sites; country for schools) instead of per-record IDs/names. With 2,971 sites and ~171,000 schools in the data, passing the underlying identifiers would blow past GA4's 500-unique-value bucketing.
- All other `action_value`s come from fixed enumerations (4 layer keys, 5 industries, ~19 countries, `on`/`off`).

## Implementation Notes (project-specific, not part of the CGD standard)

These are local conventions chosen for this codebase. They're compliant with the standard but worth knowing if you maintain this map.

- **`_cgdAction` marker property.** Each Leaflet marker gets an `_cgdAction = [action_type, action_label, action_value]` tuple set when it's created. A single map-level `popupopen` listener reads `e.layer._cgdAction` and forwards to `CGDTracking.trackEngagement(...)`. This avoids attaching ~174k per-marker `popupopen` listeners (one per site + 1km school + 5km school). The `_` prefix follows Leaflet's own private-property convention; `cgd` namespaces it to this project. The property is read in `index.html` in the popup-open tracking block — search for `_cgdAction` if renaming.
- **Layer toggles classified as `filter`** (not `view_control`). The standard defines `filter` as "any control that changes which data is shown," which fits toggling a marker layer on/off. `action_label` is per layer (`layer_sites`, `layer_schools_1km`, `layer_schools_5km`, `layer_buffers`); `action_value` is `on` or `off`.
- **Attribution-link tracking** uses a single delegated click listener on the Leaflet attribution control element (`map.attributionControl.getContainer()`), routed by `href` substring to the right semantic label. This means a new attribution link added later won't be auto-tracked — it needs to be added to the routing block in `index.html`.
- **`trackView()` fires at script start**, before the JSON data finishes loading. Interpretation of "fires once when the interactive loads" — a user who navigates away during the data fetch still counts as a view. If you want view-on-ready instead, move the call into the `Promise.all([...]).then` block at the bottom of the script.
- **No `detail_close` events.** Leaflet popups close implicitly on the next map click or cluster zoom; emitting `detail_close` from those would be noisy and the `detail_open` already captures intent.
- **Popup tracking only fires for in-cluster markers that are actually rendered.** Clicking a cluster icon zooms in (no event); clicking the resulting individual marker fires the popup and the event. This is Leaflet/markercluster behaviour, not something we control.

## Not Tracked

- **Map pan and zoom.** Continuous gestures, not discrete events (per standard).
- **Marker cluster clicks.** A cluster click only zooms the map into the cluster — same category as pan/zoom, no underlying data semantic.
- **OSM / CARTO basemap attribution clicks.** Basemap provider links rather than data sources of interest.
- **`detail_close` for popups.** Leaflet popups close on click-outside / cluster zoom; close events would be noisy and the open events already capture intent.
- **Popup-internal "school list" rendering.** The list of nearby schools shown inside a site popup is static content, not a separate interaction.
