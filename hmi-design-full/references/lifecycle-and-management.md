# HMI Lifecycle & Management — Agent Instructions

When planning or reviewing HMI system management, follow this lifecycle model.

## HMI Lifecycle Overview

```
SYSTEM STANDARDS → DESIGN → IMPLEMENT → OPERATE
       ↑              ↑                    │
       └── Continuous Improvement ─────────┘

       ═══ MOC + Audit + Validation (continuous) ═══
```

### Entry Points
1. **New system / Major changes:** Start at System Standards
2. **New displays / Display changes:** Start at Design

---

## Stage 1: System Standards

Three foundational documents that govern ALL HMI work:

### HMI Philosophy
- Strategic document with guiding principles
- Platform-independent (not tied to specific software)
- Covers: human factors alignment, user/task requirements, design standards, work practices, security model
- Should be understandable by new developers and users
- Rarely needs major updates once established

### HMI Style Guide
- Applies philosophy to concrete implementation guidance
- Includes: design rules, object behavior descriptions, color specifications, layout templates, display type guidance
- Should contain illustrations and examples
- Must be validated with proof-of-concept prototyping on target platform
- More frequently updated than philosophy (technology changes)

### HMI Toolkit
- Platform-specific library of design elements
- Templates, popups, faceplates, graphic symbols (static and dynamic)
- Built to implement the style guide
- Changes managed under change control
- May include separate toolkits for different platforms or applications

---

## Stage 2: Design

Four activities:

### Console Design
- Physical workspace: furniture, monitors, input devices
- Environmental factors: lighting, temperature, noise
- Number and size of monitors (determined by display hierarchy needs)
- Related equipment: phones, shutdown buttons, intercoms, cameras
- Ergonomics: viewing angles, reach, sit/stand options
- Reference: ISO 11064, HFES-100

### HMI System Design
- Platform selection
- Network architecture
- User roles and security model
- Third-party integrations

### User, Task & Functional Requirements
- Document ALL user types and their needs
- Primary users (operators) take precedence
- Task analysis: hierarchical, timeline, link analysis
- Cover: normal operation, startup, shutdown, abnormal conditions
- Include: help/procedure access needs, terminology, unit preferences

### Display Design
- Conceptual design with user input
- Two review cycles recommended:
  1. Layout review (basic content and structure)
  2. Final review (all information, interactions, and dynamics)
- Prototype complex applications
- Iterative refinement based on user feedback

---

## Stage 3: Implement

### Build Displays
- Created from toolkit components
- Custom scripting/configuration as needed
- Build and test in development system when practical

### Build Console
- Hardware installation and configuration
- OS and control system software setup
- Physical furniture and equipment

### Test
- Integrated system testing against requirements
- Usability testing with operators
- Use simulator if available for realistic upset scenarios
- Document: test plans, methodology, deficiency tracking

### Train
- Platform operation basics (symbols, navigation, alarms)
- Process-specific training
- Training methods: classroom, self-paced, simulator, on-the-job
- Document training requirements and records

### Commission
- Final testing with live process data
- Field verification and documentation
- User manuals and help systems in place

### Verify (Regulated Industries)
- Formal verification against requirements
- Documentation and approval gates

---

## Stage 4: Operate

### In Service
- HMI is live and operational
- All changes through Management of Change

### Maintain
- OS/security/platform updates
- Bug fixes and error corrections
- Process change modifications
- New functionality additions
- Regular backups (displays + configuration + control code)
- Documented restoration procedure (tested)

### Decommission
- Formal removal from service
- Documentation updates
- Testing and training if other parts remain active

---

## Continuous Work Processes

### Management of Change (MOC)
- ALL changes to in-service HMI go through MOC
- Enforce adherence to system standards (philosophy, style guide, toolkit)
- Revision control of toolkit components
- Document control for custom displays

### Audit
- Periodic verification of compliance with system standards
- Check that displays match style guide
- Verify navigation hierarchy is maintained
- Regulated industries may require documented audits on schedule

### Validation
- Continuous verification that HMI meets requirements
- Validation plan may specify verification at specific lifecycle stages
- Testing, documentation, and approval as required

---

## User Types and Requirements

Consider all user types during design:

| User Type | Role | HMI Needs |
|-----------|------|-----------|
| Operations | Monitor and control process | Full control access, all display levels |
| Maintenance | Troubleshoot equipment | Diagnostic views, device detail, forced values |
| Engineering | Modify HMI and control system | Configuration access, toolkit editing |
| Administrators | System and security management | User management, system settings |
| Management | Monitor plant performance | Read-only KPIs, dashboards |
| Analysts | Improve plant performance | Historical data, trends, reports |

**Rule:** Secondary users' needs must never impede primary users (operators). Create separate displays for secondary users if needs conflict.

## Scripting and Embedded Logic

- Define acceptable scripting levels in the style guide
- Handle ALL communication delays and failure modes in scripts
- Scripting on HMI computers is LESS reliable than controller logic
- Control logic and automated procedures should run in the controller, NOT in HMI scripts
- Distributed display-based scripting is hard to manage — use sparingly
- Document all custom scripting under change control
