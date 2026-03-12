# HMI Performance Requirements — Agent Instructions

When specifying or evaluating HMI system performance, apply these requirements.

## Display Performance

### Call-Up Time
Time from navigation action to fully-rendered display with live data.

| Display Type | Target | Notes |
|-------------|--------|-------|
| Operational displays (L1-L3) | 3-5 seconds | All elements rendered with live data |
| Faceplates / Popups | 1-2 seconds | Small, focused content |
| Trend displays | 5-10 seconds acceptable | Large data sets; show graphic first, populate data progressively |
| Remote access displays | May be slower | Show structure first, data populates as it arrives |
| Alarm summary | 1 second | Must be near-instant |

**Design strategies to improve call-up time:**
- Cache frequently-accessed displays
- Pre-load display data for cached displays
- Group static elements into single objects
- Show display structure immediately, populate dynamic data progressively
- Overview and alarm displays on dedicated monitors eliminate call-up time entirely

### Display Refresh Rate
How often live data updates on a displayed screen.

| Display Type | Refresh Rate | Rationale |
|-------------|-------------|-----------|
| Faceplates / Controller detail | 2-3 seconds | Close monitoring of control loops |
| Process displays (L2-L3) | 5 seconds | Standard monitoring |
| Overview displays (L1) | 5 seconds | Trend indicators update to match |
| Trend charts | 1-5 seconds | Match process dynamics |

**Rules:**
- Refresh rate must match process dynamics — at least 50% of the fastest expected response time
- This allows operators to detect sustained oscillations during process transitions
- Sub-second refresh is almost never helpful and causes distracting jittery numbers
- Historical trend data updates can be slower

### Write Time
Time from operator action to controller receiving the value.
- Should be near-instantaneous for most systems
- Provide immediate visual feedback on the HMI (show the entered value before controller confirmation)
- Actual confirmed value returns on next refresh cycle

### Write Refresh Time
Time from operator action to visual confirmation on the HMI.
- Should provide immediate feedback (value entered shown instantly)
- True controller confirmation comes on next data refresh
- For critical actions, explicitly show "pending" state until controller confirms

## System Categories and Expected Performance

### High-Speed Machine Control
- HMI tightly coupled to machine
- Very fast response required (sub-second in some cases)
- Examples: packaging lines, CNC, robotics
- Refresh rates may need to be sub-second for machine state

### Process Systems (Small)
- Single PLC/DCS/PAC
- Dozens to hundreds of I/O points
- Examples: packaging line, building boiler, small water treatment
- Standard 1-5 second refresh rates

### Process Systems (Large)
- Multiple controllers, large geographic area
- Thousands of I/O points
- Examples: chemical plant, refinery, large water treatment
- Standard 1-5 second refresh rates
- Call-up time more critical due to larger display sets

### SCADA
- Supervisory system linking multiple subsystems
- Examples: pipeline control, city water distribution, mill control
- Multi-site overview displays for transport and inventory
- Drill-down to individual site details
- Communication latency is a factor

### Geographically Widespread RTU Systems
- Scanning in minutes (not seconds)
- Communication over radio, public networks, satellite
- Examples: transmission substations, pipeline valve stations
- Display refresh aligns with scan rate
- Communication failure indication is critical

## Navigation Performance

| Metric | Target |
|--------|--------|
| Critical displays | 1-2 clicks |
| Non-critical displays | 3 clicks max |
| Alarm summary | 1 click (always) |
| System diagnostics | 1-2 clicks |
| Operator switching | 5 seconds |
| Language change | 5 seconds (if supported) |

## Stress Testing

Design and test HMI performance under stress conditions:
- Maximum alarm load (alarm flood scenario)
- Maximum number of simultaneous users
- Maximum display call-up rate (rapid navigation during upset)
- Network degradation
- Controller communication failure
- Confirm performance targets are met under these conditions
