# Design Auditor Plugin

Audit any UI design against 17 professional rules. Get a scored report with clear, actionable feedback.

## What it does

Run `/design-auditor` (or just say "audit my design") to get an expert review covering:

- **Typography** — hierarchy, font pairing, size scale, line height, contrast
- **Color** — palette structure, WCAG contrast ratios, 60-30-10 rule, dark mode
- **Spacing** — 8-point grid, proximity, alignment, white space
- **Accessibility** — touch targets, focus states, screen reader support, WCAG AA/AAA
- **Animation** — duration, easing, reduced motion, purpose taxonomy
- **Navigation** — active states, breadcrumbs, mobile patterns
- **States** — loading, empty, error, disabled, success (the 9 states checklist)
- **Elevation** — shadow consistency, layering hierarchy
- **Corner radius** — nested radius rule, size-proportional radius
- **Iconography** — consistency, sizing, touch targets, labels
- **Microcopy** — button labels, error messages, tone consistency
- **Design tokens** — token health score, semantic naming, dark mode architecture
- **i18n** — text expansion, RTL support, date/number formats

## Works with

- **Figma MCP** — reads design data and screenshots directly from Figma
- **Code** — audits HTML, CSS, React, Vue, or any web code
- **Screenshots** — analyzes uploaded images
- **Descriptions** — audits based on written descriptions of a design

## Output

Each audit produces a scored report (0–100) with issues categorized as:

- 🔴 **Critical** — must fix (accessibility failures, contrast violations)
- 🟡 **Warning** — should fix (inconsistencies, missing states)
- 🟢 **Tip** — nice to fix (polish, best practices)

## Install

```bash
claude plugin add <your-github-username>/design-auditor-plugin
```

## Usage

```
# Audit a Figma design
"Audit this design" + paste Figma URL

# Audit code
"Check my component" while working on a file

# Audit a screenshot
"Review this UI" + share an image

# Quick triggers
"check my design", "review my UI", "is this accessible?",
"typography check", "color contrast", "design review"
```

## Requirements

- Claude Code
- No external dependencies (fully self-contained)
- Optional: Figma MCP for direct Figma file access
