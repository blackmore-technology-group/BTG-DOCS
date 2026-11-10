# BTG BC Map Core — Shared Navigation and Intelligence Architecture

**Engineering proposal, 10 November 2026.** This is the target architecture; it is not a claim that the currently separate applications already consume a single map library.

## Decision

Maintain **one version-controlled, source-backed BC map foundation** with domain-neutral navigation and a common HUD. Keep Elevation 3D, HUNT3D and Geo3D as separate branded products with independent intelligence engines, permissions, entitlements and distributions. No prediction engine may overwrite the authoritative terrain, waterways, roads, buildings, route graph, GPS positions or navigation camera.

## 1. Components and ownership

| Component | Owns | Forbidden coupling |
|---|---|---|
| `@btg/bc-map-core` | DEM/DSM terrain tiles, vertical datum conversion, PBR materials, building footprints/heights, water/shoreline/bridge geometry, transport and trail references, place name index, 3D rendering, streaming/LOD, offline asset validation | No HUNT3D/NIKI/Geo3D business logic |
| `@btg/bc-navigation` | GPS, compass orientation, camera, pan/zoom, source-backed routing, waypoint and track storage, elevation/distance/ETA estimation, GPX and interchange format | No species, geology or tourism prediction model |
| `@btg/bc-hud` | Responsive branded header, search, name cards, layer visibility, route planning panel, accessible HUD controls, desktop/iPad/phone layouts | No physical map geometry or scientific scoring |
| `@btg/intelligence-contract` | Plugin registration, geographic coordinates, source provenance, prediction overlay metadata, percentage/score semantics, click/selection events, rendering and visibility lifecycle | No unconditional writes to navigation/terrain |
| Elevation 3D application | Tourism, recreation discovery, destination cards and regional distribution | Must use shared map/navigation contracts |
| HUNT3D application | NIKI big-game species, bedding/feeding/funnel suitability, wildlife evidence and access references | Must not change shared map source layers |
| Geo3D application | Geology, mineral occurrences, structural overlays, prospects and geological cross-section intelligence | Must not change shared navigation |
| Desktop planning client | Native Windows/macOS/Linux shell, saved plans, region downloads, route editing, synchronization controls | Must not invent live mobile device heading or GPS |

**Extraction sequence:** The present HUNT3D and Elevation_3D release branches contain duplicated versions of `app.js`, `ground_navigation.js`, `screen_heading.js`, `forest_renderer.js`, map layers and HUD. Convert these modules into independently versioned packages *after* baseline regression snapshots. Do not copy a newer prototype over a working product without comparison and QA. Geo3D remains in its current local engineering worktree until its repository and source tree are confirmed.

## 2. Geographic data and renderer contracts

- Maintain one manifest per map-core version and region: stable tile IDs, WGS84 horizontal coordinates plus declared projected CRS, verified vertical datum and conversion metadata, elevation resolution, checksum, provenance/licensing, coverage extent, LOD, feature and graph index versions.
- Distinguish measured versus inferred building heights, verified versus unverified trails, historical imagery versus current field conditions and map style versus geographic source accuracy.
- Only upgrade approved renderer resources; preserve all existing verified watercourses, reflective water and bank meshes, roads, trails, bridges, buildings, georeferenced vegetation, panning and name-card interactions.
- iPhone and iPad GPU budgets are device-dependent; independent iPad performance/heading QA is mandatory. A higher-resolution display does not imply a larger safe memory budget.
- Per-region signed or otherwise integrity-checked content packs allow one BC map to power several products without independently repackaging content by hand. Respect each source license.

## 3. Intelligence plugin contract

Plugin may implement `id`, `version`, `capabilities`, `availableRegions`, `requiredDatasets`, `load(region,context)`, `getOverlay(visibleArea,appState)`, `getCards(feature)`, `onMapSelection(geopoint)`, `setVisibility(layer,visible)`, `dispose()`.

A plugin receives read-only map contexts (terrain height, feature query, geographic conversion, source route candidates) and returns independently addressable world/draped map objects with source IDs and display metadata. The base map is never destroyed on intelligence toggle. On app switch, GPS, route, names, HUD and map pan remain in the map core.

NIKI score labels must identify *relative habitat suitability* versus actual empirical probabilities, and distinguish bedding/feeding/travel. Geo3D MINFILE markers must have source-name cards and documented confidence, not only squares. A tourism plugin may have verified trails, destinations and events only when sourced.

## 4. Screenshot-driven shared HUD

The supplied four illustrations set **visual targets**, not production screenshots or verified place data. Implement shared responsive frame with:
- official per-app wordmark, region selector and genuine indexed name search;
- fluorescent route graphics correctly draped on source terrain and a map-card panel showing real geographic/route attributes;
- optional toggles for terrain, imagery, trails, roads, waterways, names and destinations;
- one navigation panel for route, waypoint, saved plans, current GPS and walking/elevation estimates;
- per-app intelligence access (NIKI hub; Geo3D geology/prospecting panels) explicitly separated from base navigation and independently hideable;
- true iPhone/iPad/desktop sizing; retain legacy HUD and a reversible feature flag until device acceptance.

An opt-in non-destructive HUD shell has initially been staged in the two iOS repositories at `?btgHudPreview=1`. It proxies existing controls and reads real map values; the final screenshots still require iterative work and physical device tests.

## 5. Cross-platform desktop applications

Prefer reusing the browser-based renderer and UI with a native desktop wrapper such as Tauri 2 (Windows, macOS, Linux). This is a candidate, not a completed desktop build. Confirm graphics hardware requirements, offline asset storage, security signing/notarization, platform-specific installers, WebGL performance and packaging before selecting the framework.

Desktop has full keyboard/mouse map pan/zoom, region cache management, high-detail rendering where hardware allows, route planning, waypoint and field observation review. Mobile retains native GPS/compass and field execution. The same versioned data contract powers both.

## 6. QR pairing and synchronization

**Proposed flow** (not yet implemented):

1. Desktop generates a cryptographically random, short-lived one-time pairing request; QR contains only a pairing URL/code and public session info. **Never put raw routes, GPS trail histories, field observations, credentials or long-term bearer tokens directly into the QR image.**
2. User scans QR with BTG mobile app; both screens show the same short confirmation code and the user explicitly approves the pairing.
3. After secure device authorization, mobile and desktop exchange encrypted requests via an authenticated relay or a separately permissioned local-network channel; tokens expire and are single use. Support revocation and device removal.
4. Transfer opt-in *selected* route drafts, named waypoints, track logs, personal notes and permitted intelligence records; use versioned JSON/GeoJSON/GPX interoperability. Provide offline GPX/GeoJSON file exchange when no pairing connection is available.
5. Resolve conflicts with item IDs, modification times and user choice. Never overwrite an accepted route or local field evidence silently. Validate geographic coordinate ranges, source version and data length; never assume a transferred route has certified safe access.

If Bonjour or local-network discovery is implemented on Apple devices, configure and request local network permission appropriately. If an internet relay is chosen, design retention, consent, privacy declaration and account-linking before deployment.

## 7. Release acceptance gates

- Same visual design across apps, but distinct app branding and visible intelligence module separation.
- Existing Boundary data, waterways, trails, source names and offline route functions not lost.
- First-person compass alignment and real GPS position verified independently on iPhone and iPad in both landscape orientations; include permission-denied and sensor-unavailable states.
- iPad map remains stable under extended pan/zoom/region switches; memory caps, texture lifecycle and WebGL context loss monitored.
- Baseline iPhone performance preserved; no new unverified safety label.
- Native Windows, macOS and Linux packages tested separately.
- Route interchange round-trip equivalence and pairing expiration/revocation/security tested before public sync enablement.
- CodeMagic and App Store builds require signed artifacts and device QA; a PR or source commit alone does not mean a build was installed.

## 8. Phased delivery

**Phase A:** Shared HUD and navigation widgets on isolated feature branches using existing verified data. This can proceed while the BC terrain photorealism effort continues.

**Phase B:** Extract and version single source map core, restore map parity, and migrate applications individually behind a feature gate. Reject regression in water, roads, buildings, trails, zoom, overlays or offline content.

**Phase C:** Desktop planner for Windows, then macOS/Linux; integrate typed route bundle import/export.

**Phase D:** Secure opt-in QR pairing and selective two-way sync after privacy and authorization design, tested in staging.

**Phase E:** Integrate completed terrain/photo-realistic renderer as one versioned BC release, with separate mobile device performance qualification.
