# EVE Fit Procurement release-1.4

> **Purpose.** EVE Fit Procurement is a self-contained browser utility that turns EVE Online EFT fits into procurement lists. It helps prepare one or more ship packages, build a minimal refit set, calculate top-ups, compare trade hubs, and find cheaper alternatives for selected modules. No installation or server layer is required: open the local HTML file in a modern browser.
>
> Four modes are available. **“Fit merge”** adds quantities from all populated fits. **“Refit”** takes the largest quantity of every shared item to produce a non-duplicated package sufficient for any fit. **“Top-up”** treats fit 1 as existing equipment and fits 2 and 3 as alternative targets, then returns the largest shared shortage. **“Make it cheaper”** uses fit 1 and, on request, finds cheaper replacements for a selected fitted module while tracking CPU, Powergrid, and the current fitting budget.
>
> On explicit request, the utility obtains minimum sell prices through **Fuzzwork** and compares Jita, Amarr, Dodixie, Rens, and Hek. Public **EVE ESI** endpoints are used to resolve items, groups, slots, and fitting attributes. Complete fit text, fit headers, quantities, purchase checks, and saved states are never transmitted.
>
> **When network traffic occurs.** The page makes no outgoing requests until the user performs a price or analysis action. Loading prices sends individual item names to ESI to resolve type IDs, then requests ESI metadata by numeric ID and sends only item and station IDs to Fuzzwork. In “Make it cheaper,” capturing the original fit requests CPU/PG and slot data for fitted modules from ESI; “Find cheaper” additionally requests types in the relevant ESI market group and their selected-hub prices from Fuzzwork. These requests are used only for classification, price estimates, fitting-budget checks, and alternative discovery.

## 1. Version history

- **release-1.4**
  - Audited and sanitized the implementation without changing its architecture.
  - Separated total and fitted quantities for identical modules. For example, six guns in high slots plus one in cargo produce seven shopping units while CPU/PG is calculated for only six fitted guns.
  - CPU/PG projections and savings in “Make it cheaper” now use only fitted instances; cargo copies remain unchanged by replacement.
  - Replaced substring-based mass replacement with exact EFT-item matching, preventing a name ending in `I` from corrupting the corresponding `II` item.
  - Added validation for loaded state and persisted fitting baselines; CPU/PG totals are rebuilt from validated entries.
  - Prevented stale asynchronous calculations after fit edits; an empty or invalid current fit is no longer treated as zero fitting usage.
  - Enforced the `1–9999` multiplier range both during live entry and state restoration.
  - Improved ESI metadata caching and added a clipboard fallback suitable for local-file execution.
  - Clarified privacy wording and the actual ESI/Fuzzwork network exchange.
- **release-1.3**
  - Added price comparison across Jita, Amarr, Dodixie, Rens, and Hek. One action loads every hub; clicking a hub card switches list prices.
  - Added estimate-completeness indicators. Missing goods retain a text warning and receive visible red tinting; incomplete hub totals are marked as such.
  - Added station-name copying to hub cards and item-name copying to shopping-list rows.
  - Embedded a practical EVE SDE catalogue of identical faction alternatives: 481 groups and 1,226 items. The same catalogue is distributed as a separate JSON file.
  - Added prices and in-fit replacement actions for identical alternatives.
  - Added the fourth “Make it cheaper” mode with per-row alternative lookup. Only price, CPU, and Powergrid are checked; other attributes may differ and may be worse.
  - Propulsion candidates are restricted to the same size class, while all candidates must share the same inventory and market groups.
  - Added explicit baseline capture, total current CPU/PG, and deltas from the original fit.
  - Split candidates into identical alternatives, options within the original budget, options using released reserve, and options above budget.
  - CPU/PG released by one replacement is considered for later replacements; the original budget changes only after an explicit action.
  - Improved slot classification through ESI Dogma effects and ordered the list by high, mid, and low slots, rigs, subsystems, drones, and charges.
  - Added “Clear all fits” and additional loading- and incomplete-data safeguards.
- **release-1.2**
  - Added a complete-fit copy button next to the paste action for each fit field.
- **release-1.1**
  - Added a third EFT-fit field.
  - “Fit merge” and “Refit” use every populated fit; “Top-up” treats fit 1 as existing and fits 2 and 3 as alternative targets.
  - Added internal fit tabs for narrow layouts, side-by-side fields on wide screens, and a larger maximum page width.
  - Automatic state names include the full headers of every populated fit.
  - Renamed “Two ships” to “Fit merge.”
- **release-1.0**
  - Renamed list-copy actions to “Copy full list” and “Copy remaining for Multibuy.”
  - Optimized the interface for a 14-inch MacBook Pro and mobile screens.
- **v12–v2**
  - Incrementally added RU/EN localization, local states, on-demand Jita estimates, remaining-purchase cost, Amarr/Caldari/Gallente/Minmatar themes, import/export, EVE-section grouping, EFT diagnostics, responsive layout, and summary-card improvements.

## 2. Current-version features

- **Local execution.** The main application is one HTML file with no installer, build step, or server layer. The embedded identical-alternative catalogue is available offline.
- **One to three EFT fits.** Each fit can be pasted, copied, or cleared; all fields can also be cleared together. Extra blank lines, tabs, and surrounding whitespace are normalized.
- **Four calculation modes.** Merge, minimal refit package, top-up to two alternative targets, and fit-1 cost-reduction analysis.
- **Correct slot-versus-cargo handling.** Total quantity drives procurement, while CPU/PG calculations and replacements use only items found in EFT fitting sections.
- **Multiplier.** Shopping quantities can be scaled for multiple packages, from 1 through 9999.
- **Composition controls.** Hulls and charges can be included or excluded; purchased items can be hidden; grouping can be disabled.
- **EVE classification.** Items are organized into hulls, high/mid/low slots, rigs, subsystems, drones and fighters, charges and scripts, implants, cargo, and other categories.
- **Input validation.** Invalid headers, unparsed lines, unknown items, and incomplete network-derived results are reported.
- **Purchase tracking.** Every row can be checked off; item lines, units, percentage, and remaining purchase value update automatically.
- **Prices and trade hubs.** Fuzzwork minimum sell prices are loaded for Jita, Amarr, Dodixie, Rens, and Hek. Hub cards switch displayed prices and copy the full station name for EVE.
- **Availability indication.** Missing prices are highlighted on both item rows and hub totals, so an incomplete total cannot be mistaken for a complete estimate.
- **Identical alternatives.** A local SDE-derived catalogue suggests interchangeable faction items and can replace them in fits.
- **“Make it cheaper.”** Cheaper candidates of the same group and size class are loaded dynamically for a selected fitted module. Price, CPU, PG, savings, and impact on the original fitting budget are shown separately. This is not a combat-performance comparison: other attributes may be worse.
- **Copy actions.** Copy a fit, item name, station, full human-readable list, or the unchecked remainder in EVE Multibuy `Name<TAB>Quantity` format.
- **Context persistence.** Working state is stored automatically in `localStorage`; named states can be created, updated, deleted, exported, and imported as JSON.
- **Automatic naming.** The default state name uses the complete bracketed headers of populated fits and remains editable.
- **Localization and themes.** Russian and English interfaces and all four empire-faction themes are available and persisted.
- **Responsive layout.** Three fits appear side by side on wide screens and switch through internal tabs when width is limited.
- **Privacy.** Complete fit contents and headers, quantities, checks, and saved states remain local. Network requests occur only after price-loading or cost-analysis actions and contain individual item names or numeric IDs required by ESI and Fuzzwork.
