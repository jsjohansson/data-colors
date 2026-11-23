# Data dictionary: Color Galaxy color data, version 2.0.0

Field-by-field reference for the CSV files. Every count, range and list of values below is measured from the files. The example column shows the color **Tomato #ff6347** (color_id 29059). Machine-readable version: [datapackage.json](datapackage.json).

## Files

| File | Grain | Rows | Fields | Key | Size |
|---|---|---:|---:|---|---:|
| `colors.csv` | One row per named color: names, codes in every color model, groupings, picker boxes and related colors. | 31,996 | 97 | color_id | 21.3 MB |
| `color_relationship_shade.csv` | One row per color and shade: its 9 shades (10% steps toward black) in long form for charts and tables. | 287,964 | 7 | color_id, position | 10.9 MB |
| `color_relationship_tint.csv` | One row per color and tint: its 9 tints (10% steps toward white) in long form. | 287,964 | 7 | color_id, position | 10.6 MB |
| `color_relationship_palettes.csv` | One row per color and palette color: the 5-color Complementary (palette_1) and Neutral pairing (palette_6) palettes in long form. | 319,960 | 7 | color_id, relation, position | 13.7 MB |
| `color_galaxy.csv` | One row per color: X/Y positions for the galaxy and Milky Way charts and box positions for the color picker, each for all colors and for each of the four color sets. | 31,996 | 44 | color_id | 4.1 MB |

All files: comma-separated, UTF-8 with a byte-order mark, header row, Windows (CRLF) line endings, blank = no value. Every other file relates to `colors.csv` on `color_id`.

## colors.csv

One row per named color: names, codes in every color model, groupings, picker boxes and related colors.

31,996 rows, 97 fields. Key: color_id.

### Identity and names

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `color_id` | integer | Unique id 1-31,996, in name A-Z order (accents folded, case ignored, ties by hex). Primary key; joins every file. | 1 to 31,996 | 29059 |
| `name` | string | Color name. The 139 official HTML/CSS colors use their CSS name (e.g. Wheat); all others use the meodai/color-names name. Not unique (some CSS names also exist in meodai at another hex): key on color_id or hex. | 31,973 distinct | Tomato |
| `meodai_name` | string | Name as published by meodai/color-names. Differs from name for CSS colors renamed to their CSS name; blank for the 3 CSS-only colors. | 31,993 distinct; 3 blank | Bruschetta Tomato |
| `hex` | string | Hex color, #rrggbb, lowercase. Unique. | 31,996 distinct (unique) | #ff6347 |
| `hex_code` | string | Hex color without #, uppercase (RRGGBB). Unique. | 31,996 distinct (unique) | FF6347 |
| `is_css_named` | integer | 1 if the color is an official CSS/HTML named color, else 0. | 0 / 1 (139 ones) | 1 |
| `css_keywords` | string | CSS keyword(s) for this hex, separated by '; ' (e.g. 'aqua; cyan'); blank if not a CSS color. | 139 distinct; 31,857 blank | tomato |
| `css_name` | string | CSS display name in CamelCase (gray spelling preferred over grey); blank if not a CSS color. | 139 distinct; 31,857 blank | Tomato |
| `css_group` | string | W3Schools color group of the CSS color; blank if not a CSS color. | Green (22), Brown (18), Purple (18), White (17), Blue (16), Yellow (11), Gray (10), Red (9), Cyan (7), Pink (6), Orange (5); 31,857 blank | Orange |

### RGB

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `r` | integer | Red channel, 0-255. | 0 to 255 | 255 |
| `g` | integer | Green channel, 0-255. | 0 to 255 | 99 |
| `b` | integer | Blue channel, 0-255. | 0 to 255 | 71 |
| `rgb_share_r` | number | Red share of R+G+B, % (the 'RGB %' shown on color-hex.com); 0 for black. | 0 to 100 | 60.0 |
| `rgb_share_g` | number | Green share of R+G+B, %; 0 for black. | 0 to 100 | 23.29 |
| `rgb_share_b` | number | Blue share of R+G+B, %; 0 for black. | 0 to 100 | 16.71 |
| `rgb_pct_r` | number | Red as % of 255. | 0 to 100 | 100.0 |
| `rgb_pct_g` | number | Green as % of 255. | 0 to 100 | 38.82 |
| `rgb_pct_b` | number | Blue as % of 255. | 0 to 100 | 27.84 |

### HSL and HSV

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `hsl_h` | number | HSL hue, degrees 0-360. | 0 to 359.76 | 9.13 |
| `hsl_s` | number | HSL saturation, %. | 0 to 100 | 100.0 |
| `hsl_l` | number | HSL lightness, %. | 0 to 100 | 63.92 |
| `hsv_h` | number | HSV hue, degrees 0-360 (same as hsl_h). | 0 to 359.76 | 9.13 |
| `hsv_s` | number | HSV saturation, %. | 0 to 100 | 72.16 |
| `hsv_v` | number | HSV value (brightness), %. | 0 to 100 | 100.0 |

### CMYK

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `cmyk_c` | integer | Cyan, % (device-independent formula: K = 1 - max(R,G,B)/255, C = (1 - R/255 - K) / (1 - K)). | 0 to 100 | 0 |
| `cmyk_m` | integer | Magenta, %. | 0 to 100 | 61 |
| `cmyk_y` | integer | Yellow, %. | 0 to 100 | 72 |
| `cmyk_k` | integer | Key (black), %. | 0 to 100 | 0 |

### CIE color spaces

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `xyz_x` | number | CIE XYZ X (D65, 0-100). | 0 to 95.05 | 46.8392 |
| `xyz_y` | number | CIE XYZ Y (luminance, 0-100). | 0 to 100 | 30.6386 |
| `xyz_z` | number | CIE XYZ Z (D65). | 0 to 108.9 | 9.4064 |
| `yxy_Y` | number | CIE Yxy luminance Y (same as xyz_y). | 0 to 100 | 30.6386 |
| `yxy_x` | number | CIE xy chromaticity x = X / (X+Y+Z); 0 for black. | 0 to 0.6401 | 0.5391 |
| `yxy_y` | number | CIE xy chromaticity y = Y / (X+Y+Z); 0 for black. | 0 to 0.6 | 0.3526 |
| `hunter_l` | number | Hunter Lab L. | 0 to 100 | 55.3522 |
| `hunter_a` | number | Hunter Lab a (red +, green -). | -72.5183 to 104.9207 | 54.181 |
| `hunter_b` | number | Hunter Lab b (yellow +, blue -). | -190.9231 to 58.9005 | 28.6709 |
| `lab_l` | number | CIE L\* lightness, 0-100 (D65). | 0 to 100 | 62.2014 |
| `lab_a` | number | CIE a\* (red +, green -). | -86.1846 to 98.2542 | 57.8613 |
| `lab_b` | number | CIE b\* (yellow +, blue -). | -107.8637 to 94.4825 | 46.4167 |
| `lch_c` | number | CIE LCh chroma C\*: colorfulness, 0 for grays. | 0 to 133.8159 | 74.1784 |
| `lch_h` | number | CIE LCh hue angle, degrees 0-360. | 0 to 360 | 38.74 |

### Web and accessibility

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `web_safe_hex` | string | Nearest of the 216 web-safe colors (each channel rounded to a multiple of 51). | 216 distinct | #ff6633 |
| `is_web_safe` | integer | 1 if the color is itself web-safe, else 0. | 0 / 1 (147 ones) | 0 |
| `dominant_channel` | string | Largest RGB channel; ties are joined with '/' (e.g. 'Red/Green'); 'Neutral' when R = G = B. | Red (17,619), Blue (7,394), Green (6,045), Red/Green (378), Green/Blue (280), Red/Blue (167), Neutral (113) | Red |
| `relative_luminance` | number | WCAG relative luminance, 0 (black) to 1 (white). | 0 to 1 | 0.3064 |
| `contrast_vs_white` | number | WCAG contrast ratio against white text, 1-21. | 1 to 21 | 2.95 |
| `contrast_vs_black` | number | WCAG contrast ratio against black text, 1-21. | 1 to 21 | 7.13 |
| `best_text_color` | string | White or Black, whichever has the higher contrast on this color. | Black (23,089), White (8,907) | Black |
| `css_rgb` | string | Ready-to-paste CSS value, e.g. rgb(255, 99, 71). | 31,996 distinct (unique) | rgb(255, 99, 71) |
| `css_hsl` | string | Ready-to-paste CSS value, e.g. hsl(9, 100%, 64%) (rounded). | 31,073 distinct | hsl(9, 100%, 64%) |

### Groupings

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `shade_group` | string | Basic color family from CIE L\* and C\*, HSL hue and HSV value. C\* under 8: White (L\* 93+), Black (L\* under 12) or Gray. Very pale tints are White, faintly tinted mid and dark colors (C\* under 13, L\* under 80) are Gray. The rest go by hue, with browns split from oranges, yellows and muted reds by brightness and chroma, and pinks from reds by lightness. A calculated rule, not a human label: it agrees with W3Schools' groups for 122 of 141 CSS colors. | Gray (7,262), Brown (6,959), Green (3,203), Blue (2,944), Red (2,159), Pink (1,871), Purple (1,790), Cyan (1,728), Yellow (1,585), Orange (1,221), White (1,167), Black (107) | Orange |
| `hue_family` | string | 12-step color wheel (30-degree slices of HSL hue, Red centered on 0), or Neutral when chroma is under 8. | Orange (7,483), Neutral (5,264), Red (3,777), Yellow (3,220), Azure (2,624), Cyan (2,175), Rose (1,529), Chartreuse (1,281), Spring Green (1,182), Blue (999), Green (853), Violet (816), Magenta (793) | Red |
| `temperature` | string | Warm (hue under 80 or from 330), Cool, or Neutral (chroma under 8). | Warm (15,697), Cool (11,035), Neutral (5,264) | Warm |
| `lightness_band` | string | Dark (L\* under 35), Medium (35-70) or Light (70 and up). | Medium (14,300), Light (14,101), Dark (3,595) | Medium |
| `saturation_band` | string | Muted (C\* under 20), Moderate (20-50) or Vivid (50 and up). | Muted (14,864), Moderate (11,433), Vivid (5,699) | Vivid |
| `style` | string | First matching rule: Neutral (C\* < 8); Neon (HSV saturation >= 85%, value >= 90%, C\* >= 70); Pastel (L\* >= 78, C\* < 40); Earth Tone (hue 15-100, L\* 20-70, C\* 10-50); Jewel Tone (L\* 20-55, C\* >= 45); Dark (L\* < 20); Muted (C\* < 30); otherwise Bright. | Muted (6,894), Bright (6,406), Pastel (5,959), Neutral (5,264), Earth Tone (3,745), Jewel Tone (2,286), Neon (905), Dark (537) | Bright |
| `nearest_css_name` | string | Closest CSS named color by OKLab distance (the color itself for CSS colors). | 139 distinct | Tomato |
| `nearest_css_group` | string | W3Schools group of nearest_css_name. | Gray (10,834), Brown (6,603), Blue (2,794), Green (2,756), Yellow (1,905), Red (1,770), Purple (1,753), White (1,682), Pink (877), Orange (614), Cyan (408) | Orange |

### Color picker (hue x saturation)

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `picker_cell_id` | integer | Cell of a 36 x 20 hue-by-saturation grid (10 degrees of hue by 5 points of HSV saturation), numbered 1-720 in reading order from the top-left (full color on top, white at the bottom). Pure grays fall in the bottom-left cell. | 1 to 720 | 181 |
| `picker_box_col` | integer | Full picker box column, 1-108 (3 per 10-degree hue column), left to right through the hues. Colors are spread evenly inside their hue column, so this is a rank, not an exact hue. | 1 to 108 | 3 |
| `picker_box_row` | integer | Full picker box row, 1-60, from white (1) to full color (60), by saturation rank inside the column; pure grays sit along row 1. | 1 to 60 | 47 |
| `picker_box_top` | integer | 1 on the one color each of the 6,480 boxes shows (its brightest), else 0. Filter to 1 to draw the box picker. | 0 / 1 (6,480 ones) | 1 |

### Shades and tints

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `shade_1` | string | Shade 1: the color mixed 10% toward black (each channel floor(v x 0.9)). | 31,719 distinct | #e5593f |
| `shade_2` | string | Shade 2: the color mixed 20% toward black (each channel floor(v x 0.8)). | 31,394 distinct | #cc4f38 |
| `shade_3` | string | Shade 3: the color mixed 30% toward black (each channel floor(v x 0.7)). | 30,978 distinct | #b24531 |
| `shade_4` | string | Shade 4: the color mixed 40% toward black (each channel floor(v x 0.6)). | 30,523 distinct | #993b2a |
| `shade_5` | string | Shade 5: the color mixed 50% toward black (each channel floor(v x 0.5)). | 29,897 distinct | #7f3123 |
| `shade_6` | string | Shade 6: the color mixed 60% toward black (each channel floor(v x 0.4)). | 28,144 distinct | #66271c |
| `shade_7` | string | Shade 7: the color mixed 70% toward black (each channel floor(v x 0.3)). | 25,222 distinct | #4c1d15 |
| `shade_8` | string | Shade 8: the color mixed 80% toward black (each channel floor(v x 0.2)). | 19,596 distinct | #33130e |
| `shade_9` | string | Shade 9: the color mixed 90% toward black (each channel floor(v x 0.1)). | 8,324 distinct | #190907 |
| `tint_1` | string | Tint 1: the color mixed 10% toward white (each channel floor(v x 0.9 + 255 x 0.1)). | 31,757 distinct | #ff7259 |
| `tint_2` | string | Tint 2: the color mixed 20% toward white (each channel floor(v x 0.8 + 255 x 0.2)). | 31,414 distinct | #ff826b |
| `tint_3` | string | Tint 3: the color mixed 30% toward white (each channel floor(v x 0.7 + 255 x 0.3)). | 31,049 distinct | #ff917e |
| `tint_4` | string | Tint 4: the color mixed 40% toward white (each channel floor(v x 0.6 + 255 x 0.4)). | 30,523 distinct | #ffa190 |
| `tint_5` | string | Tint 5: the color mixed 50% toward white (each channel floor(v x 0.5 + 255 x 0.5)). | 29,954 distinct | #ffb1a3 |
| `tint_6` | string | Tint 6: the color mixed 60% toward white (each channel floor(v x 0.4 + 255 x 0.6)). | 28,144 distinct | #ffc0b5 |
| `tint_7` | string | Tint 7: the color mixed 70% toward white (each channel floor(v x 0.3 + 255 x 0.7)). | 25,323 distinct | #ffd0c7 |
| `tint_8` | string | Tint 8: the color mixed 80% toward white (each channel floor(v x 0.2 + 255 x 0.8)). | 19,596 distinct | #ffdfda |
| `tint_9` | string | Tint 9: the color mixed 90% toward white (each channel floor(v x 0.1 + 255 x 0.9)). | 8,757 distinct | #ffefec |

### Monochromatic

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `monochromatic_1` | string | Same HSL hue and saturation, lightness -15 points. | 31,380 distinct | #fa2600 |
| `monochromatic_2` | string | Same HSL hue and saturation, lightness -10 points. | 31,707 distinct | #ff3814 |
| `monochromatic_3` | string | Same HSL hue and saturation, lightness -5 points. | 31,900 distinct | #ff4d2e |
| `monochromatic_4` | string | Same HSL hue and saturation, lightness +5 points. | 31,119 distinct | #ff7961 |
| `monochromatic_5` | string | Same HSL hue and saturation, lightness +10 points. | 28,817 distinct | #ff8e7a |
| `monochromatic_6` | string | Same HSL hue and saturation, lightness +15 points. | 26,385 distinct | #ffa494 |

### Palette 1: Complementary

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `palette_1_1` | string | Complementary palette color 1: the base color. | 31,996 distinct (unique) | #ff6347 |
| `palette_1_2` | string | Complementary palette color 2: a light version (HSL lightness 55% of the way to white). | 29,448 distinct | #ffb9ac |
| `palette_1_3` | string | Complementary palette color 3: a dark version (HSL lightness reduced by 45%). | 31,512 distinct | #b31b00 |
| `palette_1_4` | string | Complementary palette color 4: the complement (each channel max + min - value). | 31,996 distinct (unique) | #47e3ff |
| `palette_1_5` | string | Complementary palette color 5: a light complement (55% of the way to white). | 29,450 distinct | #acf2ff |

### Palette 6: Neutral pairing

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `palette_6_1` | string | Neutral pairing palette color 1: the base color. | 31,996 distinct (unique) | #ff6347 |
| `palette_6_2` | string | Neutral pairing palette color 2: an off-white tinted toward its hue (HSL lightness 96%, saturation x 0.20). | 61 distinct | #f7f3f3 |
| `palette_6_3` | string | Neutral pairing palette color 3: a light gray (lightness 82%, saturation x 0.12). | 394 distinct | #d7cdcc |
| `palette_6_4` | string | Neutral pairing palette color 4: a slate (lightness 45%, saturation x 0.15). | 2,880 distinct | #846762 |
| `palette_6_5` | string | Neutral pairing palette color 5: a charcoal (lightness 15%, saturation x 0.25). | 1,094 distinct | #30201d |

## color_relationship_shade.csv

One row per color and shade: its 9 shades (10% steps toward black) in long form for charts and tables.

287,964 rows, 7 fields. Key: color_id, position.

### Keys

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `color_id` | integer | The color the row belongs to; joins colors.color_id. | 1 to 31,996 | 29059 |
| `relation` | string | Always shade. | shade (287,964) | shade |
| `position` | integer | Shade step 1-9: the color mixed 10% to 90% toward black; matches colors.shade_1 to shade_9. | 1 (31,996), 2 (31,996), 3 (31,996), 4 (31,996), 5 (31,996), 6 (31,996), 7 (31,996), 8 (31,996), 9 (31,996) | 1 |

### Related color

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `related_hex` | string | The related color, #rrggbb lowercase; same value as the matching column in colors.csv. | 207,592 distinct | #e5593f |
| `related_color_id` | integer | color_id of the named color with exactly this hex; blank when the related color has no name. | 3 to 31,972; 282,793 blank | (blank) |
| `related_swatch` | string | Nearest of 4,096 stand-in colors (each channel rounded to a multiple of 17; at most 8/255 off), so related colors can be colored with a 4,096-color palette. | 2,603 distinct | #dd5544 |
| `related_text` | string | White or Black, whichever reads better on related_hex (WCAG contrast). | White (223,519), Black (64,445) | Black |

## color_relationship_tint.csv

One row per color and tint: its 9 tints (10% steps toward white) in long form.

287,964 rows, 7 fields. Key: color_id, position.

### Keys

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `color_id` | integer | The color the row belongs to; joins colors.color_id. | 1 to 31,996 | 29059 |
| `relation` | string | Always tint. | tint (287,964) | tint |
| `position` | integer | Tint step 1-9: the color mixed 10% to 90% toward white; matches colors.tint_1 to tint_9. | 1 (31,996), 2 (31,996), 3 (31,996), 4 (31,996), 5 (31,996), 6 (31,996), 7 (31,996), 8 (31,996), 9 (31,996) | 1 |

### Related color

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `related_hex` | string | The related color, #rrggbb lowercase; same value as the matching column in colors.csv. | 188,081 distinct | #ff7259 |
| `related_color_id` | integer | color_id of the named color with exactly this hex; blank when the related color has no name. | 7 to 31,995; 275,375 blank | (blank) |
| `related_swatch` | string | Nearest of 4,096 stand-in colors (each channel rounded to a multiple of 17; at most 8/255 off), so related colors can be colored with a 4,096-color palette. | 3,148 distinct | #ff7755 |
| `related_text` | string | White or Black, whichever reads better on related_hex (WCAG contrast). | Black (275,177), White (12,787) | Black |

## color_relationship_palettes.csv

One row per color and palette color: the 5-color Complementary (palette_1) and Neutral pairing (palette_6) palettes in long form.

319,960 rows, 7 fields. Key: color_id, relation, position.

### Keys

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `color_id` | integer | The color the row belongs to; joins colors.color_id. | 1 to 31,996 | 29059 |
| `relation` | string | palette_1 (Complementary palette) or palette_6 (Neutral pairing palette). | palette_1 (159,980), palette_6 (159,980) | palette_1 |
| `position` | integer | Color 1-5 in the palette; matches colors.palette_1_1 to palette_1_5 and palette_6_1 to palette_6_5. | 1 (63,992), 2 (63,992), 3 (63,992), 4 (63,992), 5 (63,992) | 1 |

### Related color

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `related_hex` | string | The related color, #rrggbb lowercase; same value as the matching column in colors.csv. | 150,796 distinct | #ff6347 |
| `related_color_id` | integer | color_id of the named color with exactly this hex; blank when the related color has no name. | 1 to 31,996; 241,531 blank | 29059 |
| `related_swatch` | string | Nearest of 4,096 stand-in colors (each channel rounded to a multiple of 17; at most 8/255 off), so related colors can be colored with a 4,096-color palette. | 3,982 distinct | #ff6644 |
| `related_text` | string | White or Black, whichever reads better on related_hex (WCAG contrast). | Black (213,403), White (106,557) | Black |

## color_galaxy.csv

One row per color: X/Y positions for the galaxy and Milky Way charts and box positions for the color picker, each for all colors and for each of the four color sets.

31,996 rows, 44 fields. Key: color_id.

### Keys

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `color_id` | integer | The color; joins colors.color_id (one row per color). | 1 to 31,996 | 29059 |
| `color_set` | string | The color's set: ROY (shade_group Red, Orange, Yellow), GCB (Green, Cyan, Blue), PP (Purple, Pink) or WGB (White, Gray, Black). Blank for Brown, which belongs to no set and appears only in the all-colors views. | WGB (8,536), GCB (7,875), ROY (4,965), PP (3,661); 6,959 blank | ROY |

### Galaxy, all colors

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `galaxy_all_part` | string | Part of the all-colors galaxy: Core (White), Haze (Gray, Black) or Arm (every other group). | Arm (23,460), Haze (7,369), Core (1,167) | Arm |
| `galaxy_all_x` | number | X of the all-colors spiral galaxy, chart units 0-160 (center 80). Nine arms 40 degrees apart in color-wheel order (Pink, Red, Orange, Brown, Yellow, Green, Cyan, Blue, Purple); lighter colors sit nearer the center; browns are placed by lightness rank so their arm runs from tans at the core to dark browns at the rim; muted colors spread wider than vivid ones. Small offsets come from a fixed hash of color_id, so positions never change between builds. | 35.384 to 124.653 | 75.417 |
| `galaxy_all_y` | number | Y of the all-colors galaxy, chart units 0-90 (center 45). | 0.581 to 90.041 | 23.377 |

### Galaxy, per set

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `galaxy_roy_x` | number | X in the Red-Orange-Yellow galaxy, 0-160; blank for colors outside the set. A spiral with a small core of the set's lightest colors and arms that run light (center) to dark (rim). | 36.447 to 123.603; 27,031 blank | 102.314 |
| `galaxy_roy_y` | number | Y in the Red-Orange-Yellow galaxy, 0-90; blank outside the set. | 4.028 to 86.271; 27,031 blank | 21.189 |
| `galaxy_gcb_x` | number | X in the Green-Cyan-Blue galaxy, 0-160; blank for colors outside the set. A spiral with a small core of the set's lightest colors and arms that run light (center) to dark (rim). | 36.585 to 123.66; 24,121 blank | (blank) |
| `galaxy_gcb_y` | number | Y in the Green-Cyan-Blue galaxy, 0-90; blank outside the set. | 3.371 to 86.481; 24,121 blank | (blank) |
| `galaxy_pp_x` | number | X in the Purple-Pink galaxy, 0-160; blank for colors outside the set. A spiral with a small core of the set's lightest colors and arms that run light (center) to dark (rim). | 39.124 to 121.275; 28,335 blank | (blank) |
| `galaxy_pp_y` | number | Y in the Purple-Pink galaxy, 0-90; blank outside the set. | 3.898 to 86.67; 28,335 blank | (blank) |
| `galaxy_wgb_x` | number | X in the White-Gray-Black galaxy, 0-160; blank for colors outside the set. A spiral with a small core of the set's lightest colors and arms that run light (center) to dark (rim). | 36.475 to 123.662; 23,460 blank | (blank) |
| `galaxy_wgb_y` | number | Y in the White-Gray-Black galaxy, 0-90; blank outside the set. | 2.841 to 86.379; 23,460 blank | (blank) |
| `galaxy_set_part` | string | Part of the color in its own set's galaxy: Core (the set's lightest 6%) or Arm. Blank for Brown. | Arm (23,535), Core (1,502); 6,959 blank | Arm |
| `galaxy_set_arm` | integer | Arm number 1-6 in the set's galaxy (blank for the core and for Brown). ROY and GCB have 6 arms (each color group twice, alternating), PP 4, WGB 6 (split by tint). | 1 (4,721), 4 (4,688), 3 (4,321), 2 (3,600), 6 (3,446), 5 (2,759); 8,461 blank | 2 |

### Milky Way, all colors

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `mw_all_part` | string | Star (chroma under 8, scattered over the sky) or Ribbon. | Ribbon (26,732), Star (5,264) | Ribbon |
| `mw_all_x` | number | X of the all-colors Milky Way, chart units 0-160: a twisting ribbon from lower left to upper right, hue along it (30 degrees at its widest point), lightness across 19 lanes. | 0.012 to 159.983 | 70.688 |
| `mw_all_y` | number | Y of the all-colors Milky Way, chart units 0-90. | 0.067 to 90 | 44.616 |
| `mw_all_order` | integer | Draw order 1-31,996: stars first, then ribbon colors dark to light. | 1 to 31,996 | 18142 |

### Milky Way, per set

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `mw_roy_x` | number | X in the Red-Orange-Yellow Milky Way, 0-160; blank outside the set. The set's own ribbon: hue along it, lightness across its lanes. | 0.338 to 159.612; 27,031 blank | 68.627 |
| `mw_roy_y` | number | Y in the Red-Orange-Yellow Milky Way, 0-90; blank outside the set. | 0.067 to 89.972; 27,031 blank | 54.668 |
| `mw_gcb_x` | number | X in the Green-Cyan-Blue Milky Way, 0-160; blank outside the set. The set's own ribbon: hue along it, lightness across its lanes. | 0.221 to 159.978; 24,121 blank | (blank) |
| `mw_gcb_y` | number | Y in the Green-Cyan-Blue Milky Way, 0-90; blank outside the set. | 0.007 to 89.986; 24,121 blank | (blank) |
| `mw_pp_x` | number | X in the Purple-Pink Milky Way, 0-160; blank outside the set. The set's own ribbon: hue along it, lightness across its lanes. | 0.348 to 159.705; 28,335 blank | (blank) |
| `mw_pp_y` | number | Y in the Purple-Pink Milky Way, 0-90; blank outside the set. | 0.09 to 89.944; 28,335 blank | (blank) |
| `mw_wgb_x` | number | X in the White-Gray-Black Milky Way, 0-160; blank outside the set. The set's own ribbon: hue along it, lightness across its lanes. | 0.012 to 159.983; 23,460 blank | (blank) |
| `mw_wgb_y` | number | Y in the White-Gray-Black Milky Way, 0-90; blank outside the set. | 0.104 to 90; 23,460 blank | (blank) |
| `mw_set_part` | string | Star (the set's most muted 16.5%) or Ribbon in its set's Milky Way. Blank for Brown. | Ribbon (20,918), Star (4,119); 6,959 blank | Ribbon |
| `mw_set_order` | integer | Draw order 1-25,037 across set members: stars first, then dark to light. Blank for Brown. | 1 to 25,037; 6,959 blank | 14169 |

### Picker, all colors

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `picker_all_box_col` | integer | Full picker box column 1-108 (same value as colors.picker_box_col). | 1 to 108 | 3 |
| `picker_all_box_row` | integer | Full picker box row 1-60, white (1) to full color (60) (same as colors.picker_box_row). | 1 to 60 | 47 |
| `picker_all_box_top` | integer | 1 on the color each of the 6,480 boxes shows (same as colors.picker_box_top). | 0 / 1 (6,480 ones) | 1 |

### Picker, per set

| Field | Type | Description | Values | Example (Tomato #ff6347) |
|---|---|---|---|---|
| `picker_roy_box_col` | integer | Box column 1-54 in the Red-Orange-Yellow picker, through the set's hues left to right; blank outside the set. | 1 to 54; 27,031 blank | 24 |
| `picker_roy_box_row` | integer | Box row 1-30 in the Red-Orange-Yellow picker, white (1) to full color (30); blank outside the set. | 1 to 30; 27,031 blank | 17 |
| `picker_roy_box_top` | integer | 1 on the color each of the 1,620 Red-Orange-Yellow boxes shows (its brightest), 0 for the others; blank outside the set. | 0 / 1 (1,620 ones); 27,031 blank | 1 |
| `picker_gcb_box_col` | integer | Box column 1-54 in the Green-Cyan-Blue picker, through the set's hues left to right; blank outside the set. | 1 to 54; 24,121 blank | (blank) |
| `picker_gcb_box_row` | integer | Box row 1-30 in the Green-Cyan-Blue picker, white (1) to full color (30); blank outside the set. | 1 to 30; 24,121 blank | (blank) |
| `picker_gcb_box_top` | integer | 1 on the color each of the 1,620 Green-Cyan-Blue boxes shows (its brightest), 0 for the others; blank outside the set. | 0 / 1 (1,620 ones); 24,121 blank | (blank) |
| `picker_pp_box_col` | integer | Box column 1-54 in the Purple-Pink picker, through the set's hues left to right; blank outside the set. | 1 to 54; 28,335 blank | (blank) |
| `picker_pp_box_row` | integer | Box row 1-30 in the Purple-Pink picker, white (1) to full color (30); blank outside the set. | 1 to 30; 28,335 blank | (blank) |
| `picker_pp_box_top` | integer | 1 on the color each of the 1,620 Purple-Pink boxes shows (its brightest), 0 for the others; blank outside the set. | 0 / 1 (1,620 ones); 28,335 blank | (blank) |
| `picker_wgb_box_col` | integer | Box column 1-54 in the White-Gray-Black picker, through the set's hues left to right; blank outside the set. | 1 to 54; 23,460 blank | (blank) |
| `picker_wgb_box_row` | integer | Box row 1-30 in the White-Gray-Black picker, white (1) to full color (30) (white to black for this set); blank outside the set. | 1 to 30; 23,460 blank | (blank) |
| `picker_wgb_box_top` | integer | 1 on the color each of the 1,620 White-Gray-Black boxes shows (its brightest), 0 for the others; blank outside the set. | 0 / 1 (1,620 ones); 23,460 blank | (blank) |

## Sources

- **[meodai/color-names v14.80.0 (MIT License, (c) David Aerne and contributors)](https://github.com/meodai/color-names)**: Color names and hex values: the full list (https://unpkg.com/color-name-list/dist/colornames.csv, 31,993 colors) and its hand-picked best-of list (https://unpkg.com/color-name-list/dist/colornames.bestof.csv). The list merges names from CSS, xkcd, Wikipedia, Crayola, ntc.js and community submissions.
- **[W3C CSS Color Module Level 4, named colors](https://www.w3.org/TR/css-color-4/#named-colors)**: The 148 CSS color keywords (139 distinct colors): is_css_named, css_keywords, css_name. Three of them (olive, darkgray, goldenrod) are not in meodai/color-names and are added as their own rows.
- **[W3Schools HTML color groups](https://www.w3schools.com/colors/colors_groups.asp)**: Group label of each CSS color (css_group), and the reference used to tune the calculated shade_group.
- **[color-hex.com](https://www.color-hex.com/)**: Reference for the shade, tint, RGB-share and CMYK formulas, checked against its color pages. No data is copied from it.

## Methods for calculated fields

Every field not listed under Sources is calculated from the hex value.

- **sRGB to CIE XYZ**: IEC 61966-2-1 sRGB transfer curve and matrix, D65 white, scaled 0-100
- **CIE L\*a\*b\* and LCh**: CIE 1976 L\*a\*b\* from XYZ with the D65 white (95.047, 100, 108.883); C\* = sqrt(a\*^2 + b\*^2), h = atan2(b\*, a\*)
- **Hunter Lab**: L = 10 sqrt(Y), a = 17.5 (1.02 X - Y) / sqrt(Y), b = 7 (Y - 0.847 Z) / sqrt(Y)
- **Relative luminance and contrast**: WCAG 2.1 definitions: https://www.w3.org/TR/WCAG21/#dfn-relative-luminance, https://www.w3.org/TR/WCAG21/#dfn-contrast-ratio
- **Nearest colors**: Euclidean distance in OKLab (Bjorn Ottosson, https://bottosson.github.io/posts/oklab/)
