# EVE Fit Procurement release-1.0

> **Purpose.** EVE Fit Procurement helps EVE Online pilots and logistics coordinators turn ship fits into clear procurement lists. It simplifies ship preparation, refitting, and purchasing missing equipment, makes buying progress easier to track, and reduces manual calculations and errors.
>
> Three working modes are available: **“Two ships”** combines both fits for a joint purchase; **“Refit”** builds a set sufficient for either fit without duplicating shared items beyond the required quantity; **“Top-up”** compares the existing fit on the left with the target fit on the right and lists only the missing items.
>
> When needed, the utility can load minimum sell prices for the Jita trade hub through **Fuzzwork**. These prices are used to estimate individual items and fits, the total purchase cost, and the cost of items that remain to be purchased. Price loading runs only when explicitly requested and requires an internet connection.
>
> Complete fit contents, fit names, and saved states are never transmitted to the internet. The utility makes no outgoing network requests until the user starts price loading. During price calculation, only the item names or IDs required by the public EVE ESI and Fuzzwork APIs for type and price lookup are transmitted.

## 1. Version history

- **release-1.0**
  - Renamed the copy actions to “Copy full list” and “Copy remaining for Multibuy” so their behavior is immediately clear.
  - Optimized button proportions and text wrapping for a 14-inch MacBook Pro and mobile screens.
- **v12**
  - Added the `I’M` / “Я —” prefix to the faction-theme selector.
  - Tightened the top bar for laptop widths and hid the extra prefix on narrow screens.
- **v11**
  - Rebuilt the shopping-list header as two compact levels for the title and actions.
  - Aligned all three action buttons in one row and removed unused empty space.
- **v10**
  - Fixed inconsistent heights of the two fit headings.
  - Fit-role labels no longer wrap; long status text is truncated with an ellipsis.
- **v9**
  - Rearranged summary cards into a 2 × 2 grid.
  - Prevented large price values from overflowing their cards.
  - Promoted the remaining purchase cost to the primary Jita estimate value.
- **v8**
  - Added grouping by EVE categories: hulls, slots, rigs, subsystems, drones, charges, implants, cargo, and other groups.
  - Used EFT section structure and ESI metadata to improve classification.
  - Added malformed-line diagnostics and warnings for unknown items.
  - Added copying of remaining items in EVE Multibuy format.
  - Expanded purchase progress with item, unit, and ISK totals.
  - Added JSON export and import for saved states.
- **v7**
  - Optimized recalculation, state saving, and input handling.
  - Improved name normalization and parsing of partially malformed fits.
  - Fixed the empty-list state of the price estimate.
  - Improved summary-metric layout.
- **v6**
  - Localized `Procurement console` as “Панель закупок” in the Russian interface.
- **v5**
  - Made the remaining purchase cost the main large value in the Jita estimate.
  - Moved the full list cost to the secondary line.
- **v4**
  - Added themes for the four empire factions: Amarr, Caldari, Gallente, and Minmatar.
  - Persisted the selected theme between launches.
  - Converted interface accents and the responsive top bar to shared theme variables.
- **v3**
  - Added a separate remaining-purchase value to the Jita estimate.
  - The remaining cost now updates automatically when items are marked as purchased.
- **v2**
  - First named release of the self-contained local HTML application.
  - Included two EFT inputs, three calculation modes, a multiplier, purchase tracking, local saved states, RU/EN localization, and on-demand Jita pricing.

## 2. Current-version features

- **Runs entirely as a local page.** The application is a single HTML file that opens directly in a modern browser without installation or a server layer.
- **One or two EFT fits.** Fits can be entered manually or pasted with a button. Extra blank lines, tabs, and leading or trailing whitespace are normalized automatically.
- **Three calculation modes.**
  - “Two ships” adds quantities from both fits.
  - “Refit” uses the larger quantity for each matching item.
  - “Top-up” treats the left fit as existing equipment and the right fit as the target, returning only missing quantities.
- **Multiplier.** The result can be scaled for multiple identical ship packages.
- **Composition controls.** Hulls and charges can be included or excluded; purchased items can be hidden; list grouping can be enabled or disabled.
- **Purpose-based grouping.** Items are organized into hulls, Low/Mid/High slots, rigs, subsystems, drones and fighters, charges and scripts, implants and boosters, cargo, and other categories.
- **Data validation.** The application reports invalid fit headers, unparsed lines, and items that cannot be resolved through ESI.
- **Clear source indication.** Color markers identify items found only in fit 1, only in fit 2, or in both fits.
- **Purchase tracking.** Each item can be marked as purchased. The summary shows progress by percentage, item lines, and units; after prices are loaded it also shows purchased and total ISK value.
- **Jita estimate.** A manual action loads minimum Jita sell prices from Fuzzwork. The page shows item prices, full fit values, total list cost, and remaining purchase cost. Values automatically use thousands, millions, or billions of ISK.
- **Copy actions.** “Copy full list” creates a human-readable list in `Name xQuantity` format. “Copy remaining for Multibuy” excludes checked items and uses `Name<TAB>Quantity` for direct pasting into the EVE client.
- **Search and filtering.** The generated list can be filtered by item name.
- **Automatic working-state persistence.** Fits, mode, multiplier, options, and purchase checks are stored in `localStorage` and restored on the next launch.
- **Named states.** A state can be saved, opened, updated, or deleted. Its editable default name is built from the complete bracketed headers of both fits.
- **Backups.** Named states can be exported to JSON and imported later.
- **Two languages.** The complete interface is available in Russian and English, and the selection persists between launches.
- **Four themes.** Amarr, Caldari, Gallente, and Minmatar color themes are available, with the selected theme persisted locally.
- **Responsive layout.** The interface is designed for desktops, a 14-inch MacBook Pro, and mobile screens.
- **Privacy and networking.** Fit text and saved states remain in the browser. Network requests occur only when prices are manually loaded; item names or IDs are sent to the public EVE ESI and Fuzzwork APIs.
