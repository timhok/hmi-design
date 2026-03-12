# HMI Color & Visual Design — Agent Instructions

When designing or reviewing HMI display visuals, follow these rules.

## Background Design

- **Default background: light gray** (unsaturated, neutral)
- Purpose: limit chromatic distortion, ensure foreground salience
- NEVER use black — causes excessive contrast and eye strain under prolonged use
- NEVER use saturated colors as backgrounds
- Background must provide acceptable contrast in ALL expected ambient lighting conditions (control room, field, outdoor)
- When deploying across multiple lighting environments, design and test for the worst-case condition

## Foreground-Background Interaction

- All foreground/background combinations must have sufficient contrast
- Test by converting to grayscale — if elements merge, contrast is insufficient
- Important information must be more perceptually salient (brighter, larger, more saturated) than less important information

## Color Usage Hierarchy

Assign color based on importance:

```
Most Noticeable Colors → Most Important Information
├── Alarm colors (reserved exclusively)
│   ├── Red: highest priority alarms / critical safety
│   ├── Yellow/Amber: medium priority alarms / warnings
│   └── (Specific colors per facility alarm philosophy)
├── Abnormal condition indicators
├── Active process deviations
├── Key process state changes
└── Routine information → Least saturated / neutral colors
```

### Hard Rules:
1. Alarm colors are SACRED — never use them for decoration, labels, static elements, or non-alarm purposes
2. Color must NEVER be the only differentiator — always pair with at least one of: shape, text, size, brightness, texture, position
3. Maximum ~6-8 distinct colors for coding purposes (beyond this, humans can't reliably distinguish)
4. Consistent meaning: same color = same meaning across ALL displays, NO exceptions
5. No color gradients on static/non-dynamic elements
6. Color gradients may highlight dynamic elements (e.g., fill levels, temperature progression)

## Color-Blindness Design

Common deficiencies and accommodations:

| Deficiency | Affected Colors | Design Strategy |
|-----------|----------------|-----------------|
| Red-Green (most common, ~8% males) | Red, Green | Differentiate with brightness; use shape/text redundancy |
| Green-Yellow | Green, Yellow | Use brightness difference; add pattern/texture |
| White-Cyan | White, Cyan | Avoid using both as adjacent indicators |
| Age-related lens yellowing | Blues, Purples appear gray | Avoid blue/purple for critical indicators when user population includes older operators |

### Accommodation Techniques:
- Use brightness/contrast variation alongside color
- Add shape coding (triangle=warning, circle=status, square=info)
- Add text labels on colored indicators
- Test all designs in simulated colorblind modes (protanopia, deuteranopia, tritanopia)
- Consider age-related focus issues: avoid requiring rapid near-far refocusing; consider bifocal-friendly monitor placement

## Ambient Lighting Considerations

- Design for the ACTUAL control room lighting (typically controlled indoor lighting)
- If HMI will be used in bright outdoor environments, increase contrast and reduce color count
- Screen luminance should match ambient environment — prevent eyestrain
- Avoid excessive contrast between display brightness and surrounding environment

## Information Density

Match density to display purpose:

| Display Level | Density | Guidance |
|--------------|---------|----------|
| Level 1 (Overview) | Low-Medium | Key indicators only, scannable in seconds |
| Level 2 (Operating) | Medium | All routine monitoring and control |
| Level 3 (Detail) | Medium-High | Full P&ID detail, all loops and interlocks |
| Level 4 (Diagnostic) | Variable | Focused detail, often in popups |

### When a display is too dense:
1. Consolidate raw data into summarized indicators (e.g., calculated health index instead of 10 raw values)
2. Switch to a more efficient display style (bar chart vs. table of numbers)
3. Move secondary information to on-demand popups
4. Split into multiple displays

### Spatial Organization:
- Align elements to a consistent grid
- Group related data spatially — proximity implies relationship
- Use boxes/containers to group related but non-adjacent information
- Consistent placement: same type of information in the same screen location across all displays

## Animation & Visual Dynamics

### Blinking (element appears/disappears):
- ONLY for unacknowledged alarm indication
- Provide acknowledgment mechanism to stop blinking
- NEVER blink text or numbers

### Flashing (color alternation):
- ONLY for abnormal situations requiring operator action
- Once acknowledged or addressed: stop flashing
- NEVER flash text or numbers

### Motion:
- Use for simulating equipment movement (rotating pumps, flowing fluids) SPARINGLY
- Excessive motion is distracting
- Motion should serve a functional purpose, not decoration

### Golden Rule: If nothing requires operator action, NOTHING on the display should be moving, blinking, or flashing.

## Typography

- **Body text**: Mixed case / title case (NOT ALL CAPS)
- **Emphasis**: Bold or size increase (NOT underlining, NOT all-caps paragraphs)
- **Underlines**: Reserved ONLY for hyperlinks
- **Font selection**: Must be readable from normal operator distance; clear distinction between 1/I/L and 0/O
- **Numbers**:
  - Suppress leading zeros on whole numbers
  - Show leading zero between -1 and 1 (e.g., 0.5, not .5)
  - Always show engineering units
  - Match decimal precision to measurement accuracy
  - Right-align numeric columns for easy scanning
- **Orientation**: Horizontal always; vertical only when absolutely necessary
- **Abbreviations**: Only if part of standard operator vocabulary
