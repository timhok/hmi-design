# HMI Navigation & User Interaction — Agent Instructions

When designing HMI navigation and user interaction patterns, follow these rules.

## Navigation Design

### Core Principles
1. **Minimize clicks.** Every additional click during an upset is a delay in response.
2. **Never require typing display names.** All navigation must be clickable/selectable.
3. **Consistency.** Same navigation methods and visual cues across ALL displays.
4. **Support abnormal workflows.** Navigation must work for emergency scenarios, not just normal operations.
5. **Multiple methods.** Provide at least 2-3 ways to reach any display (redundancy).

### Performance Targets

| Action | Maximum |
|--------|---------|
| Reach any critical display | 1-2 clicks |
| Reach any non-critical display | 3 clicks |
| Open alarm summary | 1 click from ANY display |
| Open system diagnostics | 1-2 clicks |
| Switch operators/login | 5 seconds |
| Display fully loaded with live data | 3-5 seconds |

### Navigation Design Types

**Hierarchical (Most Common)**
- Information organized by physical/logical process structure
- Inverted tree: broader scope at top, more detail at bottom
- Depth: number of hierarchy levels (recommend max 4)
- Breadth: number of options per node
- Natural drill-down from overview → area → equipment → detail

**Relational**
- Multiple cross-links between nodes based on functional relationships
- Best for: utility systems, distributed systems where navigation path varies by situation
- Includes lateral (side-to-side) links between related systems
- Example: from a steam header, navigate to any producer or consumer

**Sequential**
- Displays organized in a series following process flow
- Best for: batch processes where product flows through stages
- Navigate left-to-right following the process sequence

### Navigation Methods to Implement

Provide a mix of these methods:

| Method | Description |
|--------|-------------|
| Embedded hyperlinks | Click equipment/areas on the display to drill down |
| Display symbol links | Graphic symbols that are navigation targets (distinct visual coding) |
| Menus | Pull-down or flat menus for display selection |
| Trees | Folder-tree style navigation panel |
| Tabs | Tab bar for peer-level display switching |
| Toolbars/Ribbons | Persistent navigation buttons |
| Context menus | Right-click menus on equipment/areas |
| Keyboard shortcuts | Function keys or custom key mappings |
| Buttons | Dedicated navigation buttons on displays |
| Yoking | Single action updates multiple screens/panels simultaneously |
| Show/hide | Toggle detailed information visibility without navigating away |

### Visual Coding for Navigation

- Navigation targets (clickable links): DISTINCT, CONSISTENT visual style
- Selectable items (data entry points): DIFFERENT distinct style from navigation
- Process-action buttons: VISUALLY DIFFERENT from navigation buttons
- Use cursor change (e.g., hand cursor) to indicate clickable items

### Yoking (Linked Navigation)
When an operator selects an item or calls up a display, yoking automatically updates related content on other monitors:
- Select a piece of equipment → related trend appears on trend monitor
- Navigate to an area → alarm list filters to that area
- Essential for multi-monitor setups

---

## User Interaction Design

### Data Entry Conventions

Apply consistently across ALL displays:

1. **Visual indicators:**
   - Inset/recessed fields for data entry points
   - Clear highlight on currently selected field
   - Grayed items for unavailable fields
   - Hand cursor on selectable/editable items
   - Visual format clues (placeholder text showing expected format)

2. **Validation:**
   - Reject wrong-format entries immediately
   - Provide clear, specific error explanation (not just "invalid input")
   - For critical entries: enforce acceptable range limits
   - For non-critical entries: optionally allow out-of-range with reason capture

3. **Feedback:**
   - Immediate visual confirmation of all data entry
   - Show the entered value and confirm acceptance
   - For process-affecting changes: show before/after values

### Number Display and Entry

| Rule | Example |
|------|---------|
| Suppress leading zeros on whole numbers | `42` not `042` |
| Show leading zero between -1 and 1 | `0.5` not `.5` |
| Always show engineering units | `42.3 PSI` |
| Match decimal precision to measurement accuracy | See range table below |
| Present in directly usable form | Never require operator to convert units |
| Right-align numeric columns | For easy scanning |
| Avoid rapid decimal point shifting | Suppress auto-rescaling jitter |

**Decimal Formatting by Range:**

| Engineering Range | Format |
|-------------------|--------|
| 100 - 9999 | XXXX |
| 10 - 99.99 | XX.X |
| 1 - 9.999 | X.XX |
| 0 - 0.999 | X.XXX |

### Command Entry (Process-Affecting Actions)

**Critical Safety Rules:**
1. **No single-click process actions.** Commands affecting the process MUST require multiple input actions (never a single inadvertent click).
2. **Confirmation before execution.** Multi-step commands must show a summary of ALL actions for confirmation before executing.
3. **Cancel/Undo.** Always provide a way to cancel during the change process, or quickly recover to prior state, or both.
4. **Visibility.** All inputs and effects of a command must be visible to the operator.

**Design patterns:**
- Select → Confirm → Execute (minimum for routine changes)
- Select → Review → Confirm → Execute (for significant changes)
- Password/biometric → Select → Confirm → Execute (for critical/safety changes)

### Button Design

1. Label text: clear, on or immediately adjacent to the button
2. Dynamic labels: use active voice verb phrases (e.g., "Stop Pump", "Open Valve")
3. Size: large enough for rapid, accurate selection with the pointing device in use
4. Process buttons: visually distinct from navigation buttons
5. Unavailable buttons: remain visible but visually coded as unavailable (grayed)
6. Sequential buttons: only make available when appropriate in sequence (or reject incorrect order with feedback)
7. Feedback: always confirm button execution visually

### Faceplates and Popups

1. **Auto-close timeout:** Configure a timeout period after no user interaction
2. **Override:** Operator can always override the timeout to keep popup open
3. **Positioning:** Must not cover critical display information (or be draggable)
4. **Focus clarity:** When multiple popups are open, clearly indicate which has keyboard focus
5. **Consistency:** All popups follow the same interaction patterns as the rest of the HMI

### Error Avoidance

- Confirmation steps for critical/irreversible actions
- Range enforcement on critical entries
- Allow out-of-range entries for non-critical values with reason capture
- Don't over-confirm — excessive confirmations cause operators to click through blindly
- Confirmation methods:
  - Dialog boxes with explicit accept/reject
  - Password or electronic signature
  - Biometric confirmation
  - Explicit text entry of confirmation value

---

## User Access and Security

### Role-Based Access Patterns

| User Type | Typical Access |
|-----------|---------------|
| Operator | Full monitoring, process control within scope |
| Maintenance | Monitoring + diagnostic views + forced value capability |
| Engineer | Full monitoring + configuration changes |
| Administrator | User management, security settings |
| Management | Read-only monitoring, KPI dashboards |

### Security Features to Implement
- Temporary privilege elevation (log-over without full logout)
- Role-based display and action restrictions
- Location-based content restriction (field terminal vs. control room)
- Electronic signatures for auditable actions
- Authentication notes (require reason for critical control actions)
- Auto-timeout to logged-out state after inactivity
