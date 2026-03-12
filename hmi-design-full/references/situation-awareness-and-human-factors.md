# HMI Situation Awareness & Human Factors — Agent Instructions

When designing HMI systems, apply these human factors engineering principles to support operator cognition and situation awareness.

## Situation Awareness Model

Operators must maintain three levels of awareness at all times:

1. **Perception** — What is happening in the process right now?
2. **Comprehension** — What does the current state mean?
3. **Projection** — What will happen next if no action is taken?

The HMI must actively support all three levels. Inadequate situation awareness is a primary factor in accidents attributed to human error.

## Design for Situation Awareness

### When Everything Is Normal
- Display should exhibit **minimal sensory stimuli**
- Calm, quiet visual state — muted colors, no animation
- "Dark screen" philosophy: normal = visually quiet; abnormal = visually loud
- The operator should be able to confirm "everything is fine" in a single glance at Level 1

### When Things Deviate
- As deviation increases, visual/audible signals must increase in salience proportionally
- Progressive alerting:
  - Minor deviation → subtle color change, trend direction indicator
  - Approaching alarm → more prominent visual change
  - At alarm → alarm color + blinking + audible
  - Critical → maximum salience, multiple simultaneous cues

### Preventing Tunnel Vision
- Operators fixating on one problem while missing others is a major risk
- Level 1 overview must remain visible at all times (dedicated monitor)
- Alarm summary must be accessible in 1 click from anywhere
- Display design should present context — not just the value in alarm, but neighboring values, trends, and upstream/downstream status

## Cognitive Load Management

### Grouping and Chunking
- Group related data consistently — the brain processes groups as single objects
- Place data ON or NEAR the owning equipment symbol (mental association)
- Use boxes/containers to group non-adjacent related information
- Consistent grouping patterns across all displays

### Information Processing
- Present information in the format operators USE (not raw instrument values)
  - If the operator thinks in meters, show meters (not percent of range)
  - If the operator needs a compass direction, convert from degrees
  - If the operator needs to compare, align values visually
- No mental arithmetic required — the HMI does all conversions
- No memorization required — reference values, limits, and procedures available on-demand

### Workload Management
- Under low workload: displays must still support monitoring (prevent complacency)
- Under high workload: displays must prioritize critical information
- HMI should help operators PRIORITIZE during multiple simultaneous upsets:
  - Alarm priority clearly differentiated
  - Level 1 overview shows relative severity across areas
  - Navigation supports rapid switching between problem areas

## Key HFE Design Principles

### 1. Intuitive Operation
- Functions should be obvious to the user without training for basic operations
- Controls should behave as expected (slider up = increase, etc.)
- Consistent metaphors across the entire system

### 2. Task-Appropriate Information
- Each display shows information relevant to the task it supports
- Don't make operators navigate to find what they need for a specific task
- Level 2 displays should support routine tasks with minimal navigation
- Level 3 displays should support troubleshooting tasks with minimal navigation

### 3. Appropriate Format
- Information in forms appropriate to the operator's goals:
  - Trends when change over time matters
  - Bar charts for comparison across similar items
  - Numbers when exact values matter
  - Status indicators for on/off/fault states
  - Schematics when physical relationships matter

### 4. Supporting Information Availability
- Procedures: accessible from the relevant operating display
- Alarm response guides: linked from alarm indicators
- Equipment help: accessible from equipment symbols
- HMI user guides: available from help menu

### 5. User Terminology
- Use the OPERATOR'S language, not engineering jargon
- Tag names and descriptions should match field labels
- Abbreviations only if standard in the operator's vocabulary

## Sensory Design Limits

### Visual
- Design for the actual user population (age range, known deficiencies)
- Consider corrective lens effects on viewing angles (bifocals, progressives)
- Font size readable from normal operator distance
- Monitor placement adjustable for different operator heights and vision needs

### Auditory
- Alarms audible from normal position, not overwhelming
- Distinct tones for different priorities
- Don't prevent verbal communication between operators
- Support hearing-impaired operators (adjustable volume, earpieces, visual redundancy)

### Cognitive
- Maximum 6-8 color codes (beyond this, humans can't reliably distinguish)
- Maximum 7±2 items in a group before cognitive grouping breaks down
- Consistent placement = faster recognition (same data in same position across displays)
- Animation captures attention — use only when attention capture is the goal

## Abnormal Situation Design

### The HMI Must Support:
1. **Detection** — Operator notices something is wrong (visual/audible cues)
2. **Diagnosis** — Operator understands what is wrong and why (contextual information, trends, related values)
3. **Response** — Operator takes corrective action (controls accessible, procedures available)

### Design for Upsets:
- Consider all operating modes: normal, startup, shutdown, upset, emergency
- Separate overview displays for different operating modes (startup overview, shutdown overview)
- When switching modes, ensure all normal overview information remains visible in its usual position
- Test designs against realistic upset scenarios — not just normal operation

### Failure Visibility
- Display element failure: immediately apparent (e.g., "????", "COMM FAIL", distinct visual state)
- Data source failure: clearly indicated on the affected values
- Communication failure: system-level indication
- HMI hardware failure: redundancy plan documented
