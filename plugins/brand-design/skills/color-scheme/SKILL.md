---
description: Visualize and pick brand colors interactively. In visualization mode, given a set of colors, builds shareable URLs for realtimecolors.com (live website preview) and coolors.co (palette editor). In extraction mode, given a URL from either site, parses the colors out for use by other skills. Invoke when the user wants to preview, explore, or extract colors from realtimecolors.com or coolors.co.
---

# Color Scheme

You help the user visualize and work with colors using two specialist websites:
- **realtimecolors.com** — renders a sample webpage with 5 semantic color roles (text, background, primary, secondary, accent) so users can see how their palette behaves in a real UI context.
- **coolors.co** — an interactive palette editor where users can lock, shuffle, and refine colors.

Detect the user's intent and run the correct mode:

---

## Mode Detection

| Input | Mode |
|-------|------|
| A `coolors.co` or `realtimecolors.com` URL | **Extraction** — parse colors from the URL |
| A list of colors, hex codes, or a reference to a brand brief / visual identity document | **Visualization** — build URLs for both sites |
| Ambiguous input | Ask: "Do you want to visualize these colors on a real website, or are you sharing a URL to extract colors from?" |

---

## Mode A — Visualization (Colors → URLs)

### Step 1: Collect colors

Accept colors in any of these forms:
- Hex codes with or without `#` (e.g., `#1A2B3C` or `1a2b3c`)
- CSS color names (convert to hex before building URLs)
- A reference to a `visual-identity.md` or `brand-brief.md` — read the file and extract the color palette
- A natural-language description of the palette (e.g., "navy, warm white, coral") — make your best conversion to hex and confirm with the user

If colors are missing semantic roles, infer them using these heuristics:
- **Background**: the lightest or most neutral color
- **Text**: the darkest color that contrasts well with Background (at least 4.5:1 ratio)
- **Primary**: the most saturated / most "brand" color — the one you'd use for a CTA button
- **Secondary**: a supporting brand color, less dominant than Primary
- **Accent**: a highlight color — often complementary or analogous to Primary, used for links and highlights

If only a few colors are provided:
- **Fewer than 5**: derive the missing roles. State what you inferred so the user can correct you.
  - If only 1 color: derive a full palette using color theory (complementary, analogous, or triadic harmony)
  - If 2–4 colors: fill the gaps by tinting/shading existing colors or suggesting complementary values
- **More than 5**: use all colors for the coolors URL; for realtimecolors, pick the 5 that best fill the semantic roles and note which were omitted

Always confirm the role mapping before building URLs if it is ambiguous:
> "I'm mapping your colors as: Text `#1a1a1a`, Background `#f5f0eb`, Primary `#e84c2b`, Secondary `#7c6057`, Accent `#3fbf8a`. Does that look right?"

### Step 2: Normalize hex values

- Strip `#` prefix if present
- Convert to lowercase 6-digit hex (e.g., `FFF` → `ffffff`, `#ABC123` → `abc123`)
- Resolve CSS color names to hex (e.g., `coral` → `ff7f50`)

### Step 3: Build URLs

**realtimecolors.com URL**

```
https://www.realtimecolors.com/?colors={text}-{bg}-{primary}-{secondary}-{accent}&fonts={heading}-{body}
```

- Order is **fixed**: text, background, primary, secondary, accent
- Hex values: lowercase 6-digit, no `#`, hyphen-separated
- `fonts` parameter: two Google Font names, hyphen-separated, spaces URL-encoded as `+`
  - If fonts are specified (from visual-identity.md or user input), use them
  - If not specified, omit the `&fonts=...` portion entirely (the site uses its own default)
  - Example with fonts: `&fonts=Inter-Lora` or `&fonts=Source+Sans+3-Source+Serif+4`

**coolors.co URL**

```
https://coolors.co/{hex1}-{hex2}-{hex3}-{hex4}-{hex5}
```

- List all brand colors in palette order (most to least dominant)
- Hex values: lowercase 6-digit, no `#`, hyphen-separated
- Supports 2–10 colors; 5 is standard

### Step 4: Present results

Output in this format:

---

**Your Color Roles**

| Role | Name (if known) | Hex |
|------|----------------|-----|
| Text | — | `#1a1a1a` |
| Background | — | `#f5f0eb` |
| Primary | — | `#e84c2b` |
| Secondary | — | `#7c6057` |
| Accent | — | `#3fbf8a` |

**Visualize & Edit**

- **[Preview on a real website →](https://www.realtimecolors.com/?colors=...)** — realtimecolors.com shows your palette applied to a sample page. Use it to check whether the colors read well together in context.

- **[Edit in Coolors →](https://coolors.co/...)** — opens the palette in Coolors where you can lock colors you love and shuffle the rest, adjust shades, or explore variations.

---

Tip: Copy the Coolors or Realtime Colors URL to share your palette or pass it back into this skill to extract the refined colors once you're happy with them.

---

## Mode B — Extraction (URL → Colors)

Given a URL from either site, parse the colors and output them in a structured format for use by other skills.

### Parsing realtimecolors.com

URL pattern: `https://www.realtimecolors.com/?colors={c1}-{c2}-{c3}-{c4}-{c5}&fonts={f1}-{f2}`

1. Extract the `colors` query parameter value
2. Split by `-` to get exactly 5 hex values
3. Map to roles in fixed order: `text`, `background`, `primary`, `secondary`, `accent`
4. If a `fonts` parameter is present, extract and decode the two font names

### Parsing coolors.co

URL pattern: `https://coolors.co/{hex1}-{hex2}-...-{hexN}`

1. Take the URL path after `coolors.co/`
2. Strip any trailing segments that are not hex (e.g., `/palette`, `/generate`)
3. Split by `-` — each 6-character segment is one hex color
4. Label them: `color-1`, `color-2`, etc. (no semantic roles — Coolors is role-agnostic)

### Output format

Present the extracted colors as a clean block that can be referenced by other skills (e.g., visual-identity):

---

**Extracted Colors from [site name]**

**Source:** `[original URL]`

| Role | Hex | Preview |
|------|-----|---------|
| Text | `#1a1a1a` | ██ |
| Background | `#f5f0eb` | ░░ |
| Primary | `#e84c2b` | ▓▓ |
| Secondary | `#7c6057` | ▒▒ |
| Accent | `#3fbf8a` | ▓▓ |

*(For coolors.co, roles are unlabeled — label them by assigning to your brand's color roles)*

**Fonts (if present):** Heading: `[font name]` / Body: `[font name]`

---

**Ready to use:** You can pass these colors to `/visual-identity` to build out a full brand color system, or use them in any design document.

---

## URL Format Reference

### realtimecolors.com

```
https://www.realtimecolors.com/?colors={text}-{bg}-{primary}-{secondary}-{accent}
https://www.realtimecolors.com/?colors={text}-{bg}-{primary}-{secondary}-{accent}&fonts={heading}-{body}
```

| Parameter | Format | Example |
|-----------|--------|---------|
| `colors` | 5 hex codes, lowercase, no `#`, hyphen-separated | `1a1a1a-f5f0eb-e84c2b-7c6057-3fbf8a` |
| `fonts` (optional) | 2 Google Font names, hyphen-separated, spaces as `+` | `Inter-Lora` or `Source+Sans+3-Source+Serif+4` |

Color order (fixed):
1. **text** — foreground / type color
2. **background** — page base
3. **primary** — main CTA, primary buttons, dominant brand color
4. **secondary** — supporting buttons, cards, secondary brand color
5. **accent** — highlights, links, decorative elements

### coolors.co

```
https://coolors.co/{hex1}-{hex2}-{hex3}-{hex4}-{hex5}
```

| Aspect | Detail |
|--------|--------|
| Format | 2–10 hex codes, lowercase, no `#`, hyphen-separated |
| Roles | None — order is palette order only |
| Example | `https://coolors.co/1a1a1a-f5f0eb-e84c2b-7c6057-3fbf8a` |

---

## Edge Cases & Notes

- **Missing semantic roles**: When colors don't come with explicit roles, state your mapping assumptions clearly and invite correction before presenting the final URLs.
- **Too few colors for realtimecolors**: If fewer than 5 colors are provided, derive the missing ones from the existing colors (tints, shades, complements). Prefer generating a plausible palette over asking too many questions.
- **Hex precision**: Always normalize to lowercase 6-digit hex before inserting into URLs. Shorthand (3-digit) hex must be expanded.
- **Font names with spaces**: Use `+` (not `%20`) when encoding spaces in the `fonts` parameter for realtimecolors.com.
- **coolors.co path only**: Only split on `-` for the path portion of the URL. Ignore query params.
- **Realtimecolors sub-paths**: The `colors` and `fonts` params work on any page of the site, not just `/?`. Use `https://www.realtimecolors.com/?...` as the canonical base.
