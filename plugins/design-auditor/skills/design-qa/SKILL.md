---
name: design-qa
description: "Unified design QA orchestrator combining pixel-perfect Figma matching, 13-point visual checklist, AI slop detection, and scored assessment. Use when finishing UI work, reviewing designs, or comparing rendered output to any visual reference. Triggers on: QA this, check this component, verify visual match, design review, visual QA, pixel perfect check."
---

# Design QA

Unified design quality assurance workflow. Orchestrates visual comparison, structured checklist evaluation, AI slop detection, and scored assessment into a single pass.

## Mode Selection

Auto-detect mode from context, or let the user specify:

| Mode                     | Trigger                                            | Primary workflow                                      |
| ------------------------ | -------------------------------------------------- | ----------------------------------------------------- |
| **A: Figma Match**       | Figma URL provided                                 | Pixel-perfect CSS refinement via `visual-qa` workflow |
| **B: Visual Comparison** | Screenshot, live site URL, or design spec provided | Compare rendered output to any reference              |
| **C: General Audit**     | No reference — standalone quality check            | Audit against checklist + scoring only                |

## Workflow

### Step 1: Capture Reference

- **Mode A:** Use Figma MCP (`get_design_context` / `get_screenshot`) to get the design
- **Mode B:** Use the provided screenshot, URL (via Playwright screenshot), or spec
- **Mode C:** Skip — no reference needed

### Step 2: Capture Rendered Output

Take a Playwright screenshot of the implemented component/page at relevant breakpoints:

- Mobile: 375px
- Tablet: 768px
- Desktop: 1440px

### Step 3: Run 13-Point Checklist

Evaluate each dimension. Mark as PASS, FAIL, or N/A with specific issues noted.

| #   | Dimension                    | What to check                                                                     |
| --- | ---------------------------- | --------------------------------------------------------------------------------- |
| 1   | **Overall Layout**           | Grid alignment, section ordering, content hierarchy matches reference             |
| 2   | **Typography**               | Font family, weight, size, line-height, letter-spacing, text transform            |
| 3   | **Colors**                   | Background, text, border, accent colors match; no hardcoded values outside tokens |
| 4   | **Spacing**                  | Margins, padding, gaps between elements; consistent use of spacing scale          |
| 5   | **Sizing**                   | Width, height, aspect ratios of containers, images, icons                         |
| 6   | **Borders & Corners**        | Border width, style, color, border-radius values                                  |
| 7   | **Shadows & Effects**        | Box-shadow, backdrop-filter, opacity, blur values                                 |
| 8   | **Interactive States**       | Hover, focus, active, disabled states present and styled correctly                |
| 9   | **Icons & Images**           | Correct assets, proper sizing, alt text, loading behavior                         |
| 10  | **Responsive Behavior**      | Layout adapts correctly across breakpoints; no horizontal scroll                  |
| 11  | **Overflow & Clipping**      | Text truncation, scroll containers, content doesn't escape bounds                 |
| 12  | **Z-index & Stacking**       | Modals, dropdowns, tooltips layer correctly; no unintended overlap                |
| 13  | **Transitions & Animations** | Smooth, purposeful motion; no janky or missing transitions                        |

### Step 4: AI Slop Detection

Pass/fail gate: "Would someone immediately identify this as AI-generated?"

**Fingerprint checklist** — flag if 3+ are present:

- [ ] Purple-to-blue gradient as primary palette
- [ ] Three equal-width cards in a row with icon + heading + description
- [ ] Generic Inter/system font with no typographic hierarchy
- [ ] Only Lucide/Heroicons with no custom or brand icons
- [ ] Buzzwords: "Elevate", "Seamless", "Unleash", "Transform", "Empower"
- [ ] Pure black (#000) text on pure white (#fff) background
- [ ] Perfectly symmetric layout with no intentional asymmetry
- [ ] Stock-photo-style hero with generic overlay text
- [ ] Default shadow/rounded-lg on every card with no variation
- [ ] No micro-interactions or hover states beyond color change

**Result:** PASS (< 3 flags) or FAIL (3+ flags) — list specific flags found.

### Step 5: Score Assessment

Starting score: **100**

| Severity | Deduction | Examples                                                                    |
| -------- | --------- | --------------------------------------------------------------------------- |
| Critical | -10 each  | Broken layout, missing content, accessibility failure, wrong colors         |
| Major    | -5 each   | Spacing off by >8px, wrong font weight, missing hover state                 |
| Minor    | -2 each   | 1-2px alignment drift, slight color shade difference, minor radius mismatch |

**Thresholds:**

- 90-100: Ship it
- 80-89: Minor fixes needed
- 70-79: Significant issues — fix before shipping
- Below 70: Major rework needed

### Step 6: Fix & Iterate

If score < 90 or any FAIL on checklist:

1. Fix issues in priority order (Critical → Major → Minor)
2. Re-capture screenshot
3. Re-evaluate affected checklist items
4. Re-score
5. Repeat (max 5 rounds)

### Step 7: Final Report

Output a structured report:

```
## Design QA Report

**Mode:** [A/B/C]
**Component:** [name]
**Score:** [X/100]
**AI Slop:** [PASS/FAIL]
**Rounds:** [N]

### Checklist Results
| # | Dimension | Status | Notes |
|---|-----------|--------|-------|

### Issues Found
- [Critical] ...
- [Major] ...
- [Minor] ...

### Changes Made
- [list of CSS/code changes per round]
```

## When to Delegate

- For **deep Figma CSS iteration** (Mode A), invoke `visual-qa` for the iterative screenshot-compare-fix loop
- For **comprehensive 17-rule professional audit**, invoke `design-auditor` directly
- For **UX-level critique** (not pixel-level), invoke `impeccable:critique`
- For **technical accessibility/performance audit**, invoke `impeccable:audit`

This skill orchestrates the common case. Use the specialized skills when you need depth in a specific area.
