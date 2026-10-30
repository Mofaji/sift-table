# Sift Table

A Power BI custom visual: a table with a filter under every column header.

Pick values in a header and Sift Table sends a real report filter to Power BI, the way a slicer does. Other visuals on the page follow it, and bookmarks capture it.

## Use it in your report

1. Download [`SiftTable.pbiviz`](SiftTable.pbiviz).
2. In Power BI Desktop, open the Visualizations pane, select **...** > **Import a visual from a file**, and pick the file.
3. Add Sift Table to a page and drag columns and measures into **Columns**, left to right.
4. Shape it in the Format pane: **Style**, **Filters and search**, **Column layout**, **Totals and grouping** and **Specific column**.

## Try the demo report

1. Download or clone this repository.
2. Open `SiftTable.pbip` in a recent version of Power BI Desktop. The visual is already inside the report.
3. Select **Refresh** once. The 1,200 fake orders are stored in the model, so there is no data source to connect.

The demo is one page, **Live demo**, with the table on the whole canvas. Product opens a product page, Status is coloured by a measure, and Delivery Days shows traffic lights.

## Features

### Filters

| Column type | Filter under the header |
| --- | --- |
| Text | Searchable value list with counts, Select shown, Invert and (Blank). Values with no rows left under the other filters drop out of the list, like Excel; one click brings them back |
| Number | Min / max, drag across a histogram, Above average, Top 10%, Bottom 10%, or a value list |
| Date | From / to, presets anchored on the latest date in the data (Last 7 / 30 days, This month, This quarter, YTD, Last year), a month strip you can drag across |

- A filter on a model column becomes a report filter. A filter on a measure, and the search box, narrow this table only.
- Choose per column in **Specific column > Filter**: Report, This table only, or Off.
- One chip per active filter. A solid dot means it filters the report; a dashed ring means this table only.
- Bookmarks, Reset to default and the saved report bring the report filters back.
- The `{ }` panel shows the exact filter JSON Power BI receives.

### Table

- Sort, resize (double-click to fit), move, freeze and hide columns.
- Hiding a column combines rows on the visible ones, the way the native table regroups when a field is removed. The totals row stays exact. A measure re-totalled outside the model is marked `≈`. Switch it off in **Column layout**.
- Group rows with subtotals. Totals row with Sum, Average, Min, Max, Count, Count distinct or None per column.
- Virtual scrolling or pages. 30,000 rows per load, with Load more or loading everything automatically. Search, sort order and value lists are worked out once per data load, so large tables stay responsive.

### Cells

- The model's format strings, or a per-column override.
- Data bars, conditional colour (higher or lower is better), and icons: arrows, traffic lights, or up / down by sign.
- **Colour from a field**: a measure returns a hex code such as `#0F8F4F`, shown as text colour, background or a pill. This works like fx **Field value**, on text columns too.
- **Link from a field**: show one value and open another. A cell shows "@user" and opens the profile URL from a field you keep hidden.

### Style and output

- Presets Mint, Slate, Paper, Night and High contrast. Follows Windows high-contrast mode.
- **Interface size**: the toolbar, filters and menus follow the values text size, or a fixed 100–250%, so they stay readable on 4K canvases.
- Export CSV, Copy rows, and row selection that cross-highlights the report.

## Security

- **No network access.** The visual makes no requests of its own and does not ask for the WebAccess privilege. Nothing loads from outside the report.
- **One optional privilege**, `ExportContent`, for Export CSV. If your Power BI admin switches exports off, the visual says so.
- **No HTML injection.** The visual builds its DOM with `createElement` and `textContent` only: no `innerHTML`, `eval` or dynamic code.
- **Links** open only `http://` and `https://` addresses, through Power BI's own `launchUrl`. **Colours** from a field must be hex codes; anything else is ignored.
- **Exports are safe to open in Excel.** Text that starts like a formula (`=`, `+`, `-`, `@`) gets a leading `'`, so a cell such as `=HYPERLINK(...)` stays text.
- **Layout is saved in the report**, in the visual's own properties, not in browser storage.

## Good to know

- Only model columns can filter the report. A filter on a measure narrows the table only.
- Cells follow the model's format, so a `$#,0` column shows each row rounded. The totals row, Copy rows and Export CSV all use the exact values, so a SUM in Excel matches the totals row. Copied and exported numbers come through plain, such as `0.437` for 44%.
- Set **Total** to None for rates and percentages. A row average is not the rate of the total, so the demo leaves Margin % without one.
- A date column needs the Date or Date/Time data type to get the date filter. With auto date/time on, pick the plain field, not **Date Hierarchy**.
- Some organisations block custom visuals that do not come from AppSource. That is an admin setting in the Power BI tenant.

## Credits

Built by [faizaan.me](https://faizaan.me) · contact@faizaan.me

Released under the [MIT License](LICENSE). Includes powerbi-models, powerbi-visuals-api and powerbi-visuals-utils-formattingmodel, © Microsoft Corporation, MIT License.
