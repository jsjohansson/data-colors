# Color Galaxy color data

[Uploading Color Galaxy.twb…]()

<img width="1800" height="1000" alt="Color_Galaxy" src="https://github.com/user-attachments/assets/8d8d7256-1eb3-4d6f-933d-faedfa70b48c" />

**31,996 named colors** with their codes in every common color model, CSS and web-safe equivalents, accessibility contrast, color groupings, shades, tints and palettes, plus ready-made chart layouts: a spiral galaxy, a Milky Way ribbon and a hue-by-saturation color picker. Plain CSV files, built for Tableau and usable anywhere.

2026-11-18

- **[METADATA.md](METADATA.md)**: data dictionary, every field with its type, meaning, values and an example.
- **[datapackage.json](datapackage.json)**: the same metadata as a [Frictionless Tabular Data Package](https://specs.frictionlessdata.io/tabular-data-package/), with field types, constraints, keys and file checksums.

## Files

| File | One row per | Rows | Fields | Size |
|---|---|---:|---:|---:|
| `colors.csv` | named color | 31,996 | 97 | 21.3 MB |
| `color_relationship_shade.csv` | color and shade (9 per color) | 287,964 | 7 | 10.9 MB |
| `color_relationship_tint.csv` | color and tint (9 per color) | 287,964 | 7 | 10.6 MB |
| `color_relationship_palettes.csv` | color and palette color (Complementary and Neutral pairing, 5 each) | 319,960 | 7 | 13.7 MB |
| `color_galaxy.csv` | color: chart positions for the galaxy, Milky Way and picker | 31,996 | 44 | 4.1 MB |

All files are comma-separated, UTF-8 with a byte-order mark, Windows line endings, with a header row; an empty value means no value.

## How the files relate

```
colors.csv  (color_id, one row per color)
├── color_relationship_shade.csv      9 rows per color:  color_id → colors.color_id
├── color_relationship_tint.csv       9 rows per color:  color_id → colors.color_id
├── color_relationship_palettes.csv   10 rows per color: color_id → colors.color_id
│     (in all three, related_color_id → colors.color_id when the related color is itself named)
└── color_galaxy.csv                  1 row per color:   color_id → colors.color_id
```

Use `color_id` (or `hex`) as the key. `name` is not unique: 23 names belong to more than one color. *Tomato*, for example, is both the CSS color `#ff6347` and a meodai/color-names color `#ef4026`.

In Tableau, add the files from **one** text-file connection, make `colors.csv` the base table, and relate `color_galaxy.csv` (one-to-one) and each relationship file you need (one-to-many) on `color_id`.

## What's in `colors.csv`

| Group | Fields |
|---|---|
| Identity and names | `color_id`, `name`, `meodai_name`, `hex`, `hex_code`, CSS flags and names (`is_css_named`, `css_keywords`, `css_name`, `css_group`) |
| Color models | RGB (`r`, `g`, `b`, channel shares and percents), HSL, HSV, CMYK, CIE XYZ, Yxy, Hunter Lab, CIE Lab and LCh |
| Web and accessibility | nearest web-safe color, dominant channel, WCAG relative luminance, contrast against white and black, best text color, CSS `rgb()` and `hsl()` strings |
| Groupings | `shade_group` (12 families), `hue_family`, `temperature`, `lightness_band`, `saturation_band`, `style`, nearest CSS color and its group |
| Color picker | `picker_cell_id` (36 × 20 grid), `picker_box_col`, `picker_box_row`, `picker_box_top` (108 × 60 boxes) |
| Related colors | 9 shades, 9 tints, 6 monochromatic steps, and the 5-color Complementary and Neutral pairing palettes |

The three `color_relationship_*` files hold the shades, tints and both palettes again in long form (one row per related color, with `relation` and `position`), plus the named color each one matches, a 4,096-color stand-in for coloring marks, and the text color that reads on it.

## Chart layouts in `color_galaxy.csv`

Each layout comes in five sets, so one parameter can switch every chart between all colors and one family of colors:

| Set | `color_set` | Colors | shade_group members |
|---|---|---:|---|
| All colors | (every row) | 31,996 | all 12 groups |
| Red-Orange-Yellow | `ROY` | 4,965 | Red, Orange, Yellow |
| Green-Cyan-Blue | `GCB` | 7,875 | Green, Cyan, Blue |
| Purple-Pink | `PP` | 3,661 | Purple, Pink |
| White-Gray-Black | `WGB` | 8,536 | White, Gray, Black |

Brown (6,959 colors) belongs to no set: it appears in the all-colors layouts only, where it forms its own arm of the galaxy.

| Layout | All colors | Per set (blank outside the set) | Frame |
|---|---|---|---|
| Spiral galaxy | `galaxy_all_x`, `galaxy_all_y` | `galaxy_roy_x` … `galaxy_wgb_y` | X 0–160, Y 0–90 |
| Milky Way ribbon | `mw_all_x`, `mw_all_y`, draw order `mw_all_order` | `mw_roy_x` … `mw_wgb_y`, draw order `mw_set_order` | X 0–160, Y 0–90 |
| Color picker boxes | `picker_all_box_col`, `_row`, `_top` (108 × 60) | `picker_roy_box_col` … `picker_wgb_box_top` (54 × 30) | discrete columns × rows |

For example, with a string parameter **COLOR GROUP** holding ALL, ROY, GCB, PP and WGB:

```
CASE [COLOR GROUP]
    WHEN "ROY" THEN [galaxy_roy_x]
    WHEN "GCB" THEN [galaxy_gcb_x]
    WHEN "PP"  THEN [galaxy_pp_x]
    WHEN "WGB" THEN [galaxy_wgb_x]
    ELSE [galaxy_all_x]
END
```

The layouts are designed positions, not measurements: they place each color by its hue, lightness and chroma, and every small offset comes from a fixed hash of `color_id`, so positions are the same on every build.

## Sources

| Source | Used for |
|---|---|
| [meodai/color-names](https://github.com/meodai/color-names) v14.80.0, [full list](https://unpkg.com/color-name-list/dist/colornames.csv) (31,993 colors) and [best-of list](https://unpkg.com/color-name-list/dist/colornames.bestof.csv), MIT License | Color names and hex values. The list merges names from CSS, xkcd, Wikipedia, Crayola, ntc.js and community submissions. |
| [W3C CSS Color Module Level 4, named colors](https://www.w3.org/TR/css-color-4/#named-colors) | The 148 CSS color keywords (139 distinct colors): `is_css_named`, `css_keywords`, `css_name`. Three (olive, darkgray, goldenrod) are not in meodai/color-names and are added as their own rows. |
| [W3Schools HTML color groups](https://www.w3schools.com/colors/colors_groups.asp) | `css_group`, and the reference used to tune the calculated `shade_group`. |
| [color-hex.com](https://www.color-hex.com/) | Reference for the shade, tint, RGB-share and CMYK formulas, checked against its color pages. No data is taken from it. |

Every other field is calculated from the hex value, using these standard definitions:

- **sRGB → CIE XYZ:** IEC 61966-2-1 sRGB transfer curve and matrix, D65 white, scaled 0–100.
- **CIE L\*a\*b\* and LCh:** CIE 1976, D65 white (95.047, 100, 108.883).
- **Hunter Lab:** L = 10√Y, a = 17.5 (1.02X − Y) / √Y, b = 7 (Y − 0.847Z) / √Y.
- **Relative luminance and contrast ratio:** [WCAG 2.1](https://www.w3.org/TR/WCAG21/#dfn-relative-luminance).
- **Nearest named colors:** Euclidean distance in [OKLab](https://bottosson.github.io/posts/oklab/) (Björn Ottosson).

## Attribution

The color names come from **meodai/color-names**, © David Aerne and contributors, under the MIT License. Keep that copyright and permission notice when you redistribute the names. CSS color keywords are defined by the W3C CSS Color Module Level 4.

## Notes

- `shade_group` is a calculated rule, not a human label. It matches W3Schools' hand-made groups for 122 of the 141 CSS colors they list; the rest are borderline cases such as Teal (W3Schools: Green) and Maroon (W3Schools: Brown).
- `rgb_share_*` is each channel's share of R + G + B, the "RGB %" shown on color-hex.com; `rgb_pct_*` is the usual channel / 255.
- Tints reproduce color-hex.com's rounding exactly; for example, tint 2 of `#142952` is `#425374`.
- The pickers place colors by hue and saturation only; each box shows its brightest color, so dark and light colors of the same hue and saturation share a box.
- In the relationship files, `related_color_id` is mostly blank, because most shades, tints and palette colors are not named colors: it is filled for 5,171 shade rows, 12,589 tint rows and 78,429 palette rows.
