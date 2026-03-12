# HMI Display Hierarchy & Styles — Agent Instructions

When designing HMI display systems, structure displays in a 4-level hierarchy and select the appropriate display style for each.

## The 4-Level Display Hierarchy

### Level 1 — Overview / Dashboard
**Purpose:** Continuous awareness of the entire span of control

**Requirements:**
- Single display showing ALL key parameters for operator's full scope
- May span multiple monitors if all are simultaneously visible
- Continuously displayed (dedicated monitor when possible)

**Must Include:**
- Key process parameters with actual values
- Abnormal status with deviation severity and direction of change
- All top-priority alarms, positioned near associated equipment
- Embedded sparkline/mini trends on critical variables
- Status of related utilities, upstream/downstream areas
- Cost/performance KPIs if relevant

**Must NOT Include:**
- Control actions (no setpoint changes from Level 1)
- Excessive detail — this display must be scannable in seconds

**Design Pattern:**
```
┌─────────────────────────────────────────────────────┐
│                  PLANT OVERVIEW                      │
├──────────┬──────────┬──────────┬─────────────────────┤
│ Area A   │ Area B   │ Area C   │ Utilities / KPIs    │
│          │          │          │                     │
│ Key val  │ Key val  │ Key val  │ Cost $/hr           │
│ ~trend~  │ ~trend~  │ ~trend~  │ Key deviations      │
│ Alarm?   │ Alarm?   │ Alarm?   │ Upstream/downstream │
│ Status   │ Status   │ Status   │                     │
└──────────┴──────────┴──────────┴─────────────────────┘
```

### Level 2 — Unit/Area Operating Displays
**Purpose:** Primary working displays for routine monitoring and control

**Requirements:**
- One major system or subsystem per display
- Contains ALL controllers and indicators for routine operations
- Task-based: operator handles most work here with minimal navigation
- Includes start-up/shutdown task-specific views

**Must Include:**
- All high and medium priority alarms for the area
- Clear navigation cues for non-displayed low priority alarms
- Primary controllers for the process area
- Enough information to control under most normal conditions

**Design Pattern:**
```
┌─────────────────────────────────────────────────────┐
│              BOILER HOUSE OPERATIONS                 │
├────────────┬────────────┬────────────┬───────────────┤
│ Boiler 1   │ Boiler 2   │ Boiler 3   │ Common        │
│ Status:ON  │ Status:ON  │ Status:OFF │ Systems       │
│ [Fuel Gas] │ [Fuel Gas] │ [Fuel Gas] │               │
│ [O2]       │ [O2]       │ [O2]       │ [Steam Hdr P] │
│ [Steam F]  │ [Steam F]  │ [Steam F]  │ [BFW]         │
│ [Drum L]   │ [Drum L]   │ [Drum L]   │ [Cost $/hr]   │
│ Controllers│ Controllers│ Controllers│               │
└────────────┴────────────┴────────────┴───────────────┘
```

### Level 3 — Detail / Troubleshooting Displays
**Purpose:** Detailed views for non-routine operations and diagnostics

**Requirements:**
- P&ID-style or schematic detail of specific equipment
- All control loops, indicators, and interlocks
- Used for lineup changes, equipment switching, diagnostics
- Task-based: support troubleshooting workflows

**Must Include:**
- All alarm priorities for depicted equipment
- Interlock and permissive status
- Detailed equipment state information

### Level 4 — Diagnostic / Reference Displays
**Purpose:** Deepest detail level for point data, procedures, help

**Characteristics:**
- Operating procedures for individual equipment
- Help information for equipment control and diagnostics
- Detailed safety shutdown information
- Interlock and permissive logic details
- Often displayed as popups or faceplates (not full-screen)
- Not primarily for control, but control access may exist

---

## Display Styles

Select the most effective style based on functional requirements and data characteristics.

### Process Display (P&ID / PFD Style)
**Use for:** Showing equipment, piping, and instrumentation relationships
- Graphic representation of process equipment
- Shows physical flow and connections
- Most common style for Level 2 and Level 3 displays
- Equipment symbols should follow standard ISA symbology

### Functional Overview / Dashboard
**Use for:** KPIs, cross-area performance summaries
- Representation of functional relationships between data
- Sparklines, bar charts, gauges, digital readouts
- Best for Level 1 displays
- Focus on trends and deviations, not raw numbers

### Schematic Overview
**Use for:** Operator's span of control at a glance
- Informational overview of the entire area
- Simplified equipment representation
- Good for Level 1 and high-level Level 2

### List / Table
**Use for:** Tabular data that doesn't benefit from graphical representation
- Equipment lists, calibration tables, parameter tables
- Rows of text and numeric data
- May include small equipment symbols inline

### Trend / Graph
**Use for:** Showing data evolution over time
- Real-time or historical data charts
- Statistical process control charts
- Include reference lines for normal/alarm ranges
- Time axis should match process dynamics

### Group (Faceplate Array)
**Use for:** Monitoring multiple similar controllers side-by-side
- Array of standardized controller faceplates
- Each shows SP, PV, OP, mode, bar graph
- Great for comparing parallel equipment (all flow valves, all temperature loops)

### Topology / Location
**Use for:** Physical or logical system layout
- Network diagrams, electrical one-line diagrams
- Fire detection zone maps
- Physical building/plant layouts with status indicators

### Logic Monitor
**Use for:** Visualizing control logic
- Boolean / function block diagrams
- Ladder logic displays
- Sequence diagrams
- Show live state of inputs/outputs

### Procedural
**Use for:** Step-by-step operational sequences
- Sequential function charts
- Procedure checklists with electronic signatures
- Trip check procedures
- Show current step, completed steps, remaining steps

### Health / Diagnostic
**Use for:** System infrastructure monitoring
- Network health, server status, controller status
- Communication path monitoring
- Battery/UPS status

### Alarm List
**Use for:** Alarm management
- Active alarm summary (sortable by priority, time, area)
- Shelved alarm list
- Out-of-service alarm list
- Event/message logs

### Video
**Use for:** Live or recorded process monitoring
- CCTV feeds
- Process cameras
- Security monitoring

---

## Navigation Between Levels

```
Level 1 (Overview) ←→ Level 2 (Operating)
        ↕                     ↕
                        Level 3 (Detail)
                              ↕
                        Level 4 (Diagnostic)
```

- Drill DOWN: click on area/equipment to see more detail
- Drill UP: always provide a "back to overview" path
- Lateral: navigate between peer systems at the same level
- Yoking: clicking an item can simultaneously update multiple screens/panels

### Click Budget:
| Destination | Max Clicks |
|-------------|-----------|
| Any critical display | 1-2 |
| Any non-critical display | 3 |
| Alarm summary | 1 (always) |
| System diagnostics | 1-2 |
