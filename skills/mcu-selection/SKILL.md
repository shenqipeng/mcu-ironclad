---
name: mcu-selection
description: "MCU selection from 650+ database(Artery,GigaDevice,Fudan Micro,WCH,XHSC,SiLabs,MindMotion,APT). Chain: upstream←product-requirements(hw needs),brainstorming(design phase); downstream→brainstorming(MCU constrains design),writing-plans(toolchain/peripheral refs). Trigger: MCU,microcontroller,firmware,embedded,GD32,STM32,EFR32,CH32,AT32,MM32. Skip if: MCU already chosen,software-only"
---

# MCU Selection Skill

## Overview

This skill helps select optimal microcontrollers from a comprehensive database of 650+ entry-level and mainstream models across 8 manufacturers. It uses **interactive Q&A** to guide the user through parameter selection, narrowing candidates step by step until suitable models are found.

## Database Coverage (Schema B v2.0)

| Manufacturer | Count | Series |
|---|---|---|
| **GigaDevice** | 283 | GD32F10x, GD32F1x0, GD32F3x0, GD32E23x, GD32VF103, GD32C2x1, GD32E232, GD32E502, GD32E1x3, GD32C1x3, GD32L23x |
| **Fudan Micro** | 109 | FM33LC0xx, FM33LG0xx, FM33LE0xx, FM33LF0xx, FM33A0xx, FM33FR0xx, FM33FG0xx, FM33FK5xx |
| **SiLabs** | 71 | EFR32BG21/22/24/27, EFM32PG22/23/26/28 |
| **WCH** | 84 | CH32V003/103/203/208/303/305/307, CH32X035, CH32L103, CH56x/57x/58x/59x/595, CH641 |
| **MindMotion** | 36 | MM32F0010—F327, MM32L0xx, MM32SPIN |
| **Artery** | 23 | AT32F403/F413/F415/F421/F425/F402/F405, AT32L021/L010 |
| **XHSC** | 27 | HC32F0xx, HC32F1xx, HC32L0xx/1xx/2xx, HC32M1xx/3xx, HC32A0xx |
| **APT** | 18 | APT32F101/F102/F103/F110/F035 |
| **TOTAL** | **651** | |

**Schema B fields**: `part_number`, `series`, `core`, `flash_kb`, `ram_kb`, `max_freq_mhz`, `pins`, `gpio`, `packages[]`, `adc_channels`, `adc_resolution`, `uart`, `spi`, `i2c`, `can`, `usb`, `ethernet`, `peripherals[]`, `temperature_range`, `voltage_range`, `notes`

## Workflow — Interactive Q&A

### Phase 0: Pre-fill from Context

If invoked downstream of `product-requirements` or `brainstorming`, extract known hardware requirements from the conversation context and **pre-fill** those parameters. Announce the pre-filled values and skip the corresponding questions.

Example: If PRD specifies "3x UART, CAN bus, 64KB Flash", pre-fill `uart>=3, can=true, flash_kb>=64` and skip those questions.

### Phase 1: Guided Questioning (one question at a time)

Ask questions **one at a time** in the following order. After each answer, run the filter and show the **remaining candidate count**. The user can always answer "any" or "doesn't matter" to skip a question.

**Q1: Core architecture**
> What core architecture do you need?
> Options: Cortex-M0/M0+ (ultra-low-cost) / Cortex-M3 (mainstream) / Cortex-M4 (DSP/FPU) / Cortex-M33 (trustzone) / RISC-V (open ISA) / Any
>
> _Hint: Cortex-M0+ for simple tasks, Cortex-M3 for general purpose, Cortex-M4 if you need DSP/FPU, RISC-V for open-source toolchain preference._

**Q2: Required communication interfaces**
> Which communication interfaces must the MCU have? (select all that apply)
> Options: UART / SPI / I2C / CAN / USB / Ethernet / None required
>
> _Specify minimum counts if needed, e.g. "at least 2 UART"._

**Q3: Flash / RAM minimums**
> What are your minimum Flash and RAM requirements?
> Options: Flash ≤32KB / 64KB / 128KB / 256KB / 512KB / 1MB+ | RAM ≤8KB / 16KB / 32KB / 64KB+
>
> _Enter as "Flash ≥128KB, RAM ≥16KB" or "doesn't matter"._

**Q4: Pin count and package**
> Any pin count or package requirements?
> Options: ≤20 pins / 32-48 pins / 64 pins / 100+ pins / Any | Package: LQFP / QFN / TSSOP / BGA / Any
>
> _Physical PCB space constraint? E.g. "QFN32 only" or "at least 48 pins"._

**Q5: ADC requirements**
> Do you need ADC? What resolution and channel count?
> Options: No ADC / 10-bit / 12-bit / 16-bit / ≥4 channels / ≥8 channels / ≥16 channels
>
> _Skip if no analog sensing needed._

**Q6: Manufacturer preference**
> Any preferred or excluded manufacturers?
> Options: GigaDevice / Fudan / SiLabs / WCH / MindMotion / Artery / XHSC / APT / Any
>
> _Reasons to prefer: supply chain, familiar ecosystem, pin-compatibility. Reasons to exclude: bad experience, no local stock._

**Q7: Environmental constraints (if still needed)**
> Any voltage or temperature range requirements?
> Options: Wide voltage (1.8~5.5V) / Narrow voltage (2.0~3.6V) / Industrial temp (-40~85°C) / Extended temp (-40~105°C) / Automotive (-40~125°C) / Any
>
> _Skip if standard industrial conditions apply._

### Phase 2: Early Termination Rules

Stop asking questions and proceed to results when ANY of these conditions is met:
1. **Candidate count ≤ 5** — few enough to compare directly
2. **User says "that's enough" or "show me results"** — explicit stop
3. **All questions asked** — proceed with whatever filters are set

### Phase 3: Present Results

rank candidates and present as a comparison table.

**Ranking priority** (higher = more important):
1. All hard constraints met (mandatory — filter out if not)
2. Closest Flash/RAM match to requirement (+3 pts for efficient fit)
3. Interface count match (+2 pts per matched interface)
4. Manufacturer preference (+5 pts if preferred, -2 pts if excluded)
5. Package preference match (+2 pts)

**Output format:**

```
# MCU Selection Results

## Your Requirements
- Core: [selected]
- Interfaces: [selected]
- Flash ≥ [X]KB, RAM ≥ [Y]KB
- Package: [selected]
- ADC: [selected]
- Manufacturer: [selected]

## Top Candidates (out of [N] matches)

| # | Part Number | Mfr | Core | Flash | RAM | Freq | Pins | Key Peripherals | Package |
|---|---|---|---|---|---|---|---|---|---|
| 1 | [PN] | [M] | [C] | [F]KB | [R]KB | [M]MHz | [P] | [peri list] | [pkg] |
| 2 | ... | | | | | | | | |
| 3 | ... | | | | | | | | |

## Recommendation
**[Part Number]** — [1-2 sentences why this is the best fit]

### Why this one?
- [Specific advantage matching user's needs]
- [Trade-off note if applicable]
```

## Special Cases

### No Matches
If filters eliminate all candidates:
1. Identify which filter eliminated the most models
2. Suggest relaxing that specific constraint
3. Show the closest match even if it doesn't meet all criteria
4. Never return an empty result — always show something

### Too Many Matches (50+)
If candidate count remains high after all questions:
1. Show a **summary table** grouped by manufacturer/core
2. Ask one more targeted question (e.g. "Do you need USB?" if that splits the list well)
3. Present top 5 from each major group

### Pre-filled Context from PRD
When invoked after `product-requirements`, the PRD may specify:
- Required peripherals → auto-fill Q2
- Flash/RAM estimates → auto-fill Q3
- Environmental conditions → auto-fill Q7
Announce what was pre-filled and confirm with user before skipping.

### User Already Has a Specific MCU in Mind
If user mentions a specific part number (e.g. "I'm thinking about GD32F103"):
1. Look it up in the database
2. Show its full spec
3. Ask if they want to see alternatives with similar specs
4. Present 2-3 comparable models from other manufacturers

## Usage Examples

### Example 1: From scratch (no context)
```
User: I need to pick an MCU for my project

Assistant: Let me help you narrow down the right MCU from our 651-model database.
We'll go through a few quick questions.

Q1: What core architecture do you need?
  - Cortex-M0/M0+ (ultra-low-cost, simple tasks)
  - Cortex-M3 (mainstream, general purpose)
  - Cortex-M4 (DSP/FPU, motor control)
  - RISC-V (open ISA, WCH ecosystem)
  - Any / doesn't matter

Currently: 651 candidates
```

### Example 2: With some context
```
User: 我需要带CAN和至少2路UART的MCU，Flash 128KB以上

Assistant: Got it! I've pre-filled some parameters:
  - CAN: required ✓
  - UART: ≥2 ✓
  - Flash: ≥128KB ✓
  Remaining candidates: 47

Let me ask a few more questions to narrow it down...

Q1: Core architecture preference?
  ...
```

### Example 3: With PRD context
```
(After product-requirements skill generated a PRD mentioning battery monitoring)

Assistant: Based on your PRD, I've pre-filled:
  - ADC ≥8 channels, ≥12-bit ✓
  - UART ≥2 ✓
  - Low power required ✓
  - Operating voltage 2.0~3.6V ✓
  Remaining candidates: 23

Let's quickly confirm the remaining choices...

Q1: Package preference?
  ...
```

## Files
- `references/mcu_database.json`: Full MCU database (651 models, Schema B)
- `scripts/price_query.py`: Price query tool for LCSC/HQChip
- `evals/evals.json`: Test cases for skill evaluation

## Workflow Linkage

**Position in superpowers workflow:** Parallel branch during brainstorming, or downstream of product-requirements.

**Upstream (feeds into this skill):**
- `product-requirements` — PRD may specify hardware requirements (peripherals, pin count, Flash/RAM, package). Pre-fill these into the interactive Q&A.
- `brainstorming` — During design exploration, if the project involves embedded/hardware, invoke this skill to constrain the design with a concrete MCU choice.

**Downstream (receives MCU selection result):**
- `brainstorming` — MCU selection result (peripheral limits, memory constraints, package options) feeds back into the design.
- `writing-plans` — Plan steps must reference the selected MCU's toolchain, peripheral configuration, and memory layout.

**Decision rule:** If "MCU", "microcontroller", "firmware", "embedded", or specific chip names appear in the task, invoke this skill during brainstorming. The selected MCU becomes a hard constraint for all downstream planning and execution.
