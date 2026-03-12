# HMI Alarm Design — Agent Instructions

When designing alarm presentation and management in HMI displays, follow these rules.

## Core Alarm Principles

1. **Alarms demand action.** An alarm indicates an equipment malfunction, process deviation, or abnormal condition requiring operator response.
2. **Alerts inform.** An alert indicates a condition requiring awareness but not immediate action. Alerts are presented separately from alarms.
3. **Alarm colors are sacred.** Colors designated for alarms must NEVER be used for any other purpose in the HMI.

## Visual Alarm Presentation

### Color Reservation
- Define specific colors for each alarm priority level in the alarm philosophy
- These colors are EXCLUSIVELY for alarms — no exceptions
- Common convention (facility-specific):
  - Red: highest priority / critical safety
  - Yellow/Amber: high priority / warning
  - Other colors per facility philosophy
- Non-alarm elements must NEVER use alarm colors, even if they "look nice"

### Alarm State Indicators

| State | Visual Treatment |
|-------|-----------------|
| Unacknowledged alarm | BLINKING indicator (draws immediate attention) |
| Acknowledged, still active | STEADY indicator in alarm color |
| Returned to normal, unacknowledged | Blinking or distinct visual state |
| Cleared (acknowledged + returned to normal) | No alarm indication |

### Alarm Priority Indication
- Each priority level must have a unique combination of:
  - Visual indication (color, shape, size, position)
  - Audible indication (distinct tone/pattern per priority)
- Visual priority indication is MANDATORY
- Audible priority indication is strongly recommended
- In environments where audible is not used, visual priority must be sufficient alone

### Redundancy Rules
- Color must NOT be the sole alarm indicator
- Always pair alarm color with at least one of:
  - Shape (e.g., triangle for high priority)
  - Text label (alarm name and priority)
  - Brightness/contrast difference
  - Size difference
  - Position (alarm bar, dedicated area)
  - Blinking/flashing state

## Alarm Placement by Display Level

### Level 1 (Overview)
- Show ALL top-priority alarms
- Position alarms adjacent to associated equipment/area
- Show acknowledged/unacknowledged status
- Show alarm count or severity summary per area
- Direction of change indicators for alarming parameters

### Level 2 (Operating)
- Show all TOP and MIDDLE priority alarms for the area
- Clear navigation cues to non-displayed lower priority alarms
- Alarms integrated into the process view near associated equipment

### Level 3 (Detail)
- Show ALL alarm priorities for depicted equipment
- Full interlock and permissive status
- Detailed alarm information

### Level 4 (Diagnostic)
- Detailed alarm configuration
- Trip logic details
- Alarm history and statistics

## Alarm Summary Display

### Access Requirements
- Accessible in **1 click from ANY display** in the entire HMI
- Ideally on a permanently visible dedicated monitor or panel
- No navigating away from the current working display to see alarms

### Content Requirements
- List of all active alarms
- Sortable by: time, priority, area/unit, alarm name
- Show for each alarm:
  - Alarm name/tag
  - Description
  - Priority
  - Current value
  - Alarm limit
  - Time of alarm
  - Acknowledged/unacknowledged status
  - Area/unit association

### Related Alarm Lists
- Shelved alarms list (alarms temporarily removed from active display)
- Out-of-service alarm list
- Suppressed alarm list
- Recent alarm history
- These lists may be accessible in more clicks than the main summary but should still be easily reachable

## Auditory Alarm Design

### General Requirements
- Audible signals must be audible from the normal operator position
- Must not be so loud as to distract operators at other consoles
- Must not startle operators or add significantly to overall noise
- Must not prevent communication between operators

### Auditory Signal Design
- Each signal: clear, unambiguous meaning
- Distinct tones/patterns for different priorities
- Provide localization cues (direct operator toward the relevant console/area)
- Support operators with partial hearing impairment:
  - Adjustable volume speakers
  - Earpiece option
  - Do not exceed hearing conservation limits

### Silencing
- Always provide a method to silence an audible alarm after acknowledgment
- If some signals must not be muted, implement appropriate control mechanisms
- Un-silenceable alarms should be rare and clearly justified

### Remote/Field Alarms
- If operator is not always at the console, provide alternate methods:
  - Area speakers
  - Pager/text notifications
  - Remote alarm panels
  - Mobile device notifications

## Alarm-Related Design Patterns

### Alarm Banner / Bar
A persistent strip (top or bottom of screen) showing most recent/highest priority alarms:
```
┌─────────────────────────────────────────────────────┐
│ [!] HIGH: TIC8700 > 986°F  │ [!] MED: FIC770 < 50 │ → Alarm Summary
├─────────────────────────────────────────────────────┤
│                                                     │
│              (Main display content)                 │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### Alarm Integration in Process Displays
- Show alarm state directly on the equipment/instrument symbol
- Color the relevant indicator, add blinking for unacknowledged
- Clicking an alarmed item should provide alarm detail (faceplate/popup)

### Alarm-Driven Navigation
- Clicking an alarm in the alarm summary should navigate to the relevant display
- The target display should be the most useful level for that alarm type:
  - Process alarms → Level 2 or 3 display for that area
  - Equipment alarms → Level 3 detail for that equipment
  - Safety alarms → Level 3 or 4 with interlock detail
