---
name: web-design-guidelines
description: Review and craft UI code complying with Vercel Web Interface Guidelines. Use when auditing UX, touch/mobile ergonomics, accessibility, focus states, animations, layout shifts, dark mode, and frontend polish.
---

# Web Interface Guidelines & UI Best Practices (Vercel Labs)

This skill provides comprehensive design and engineering rules based on Vercel's Web Interface Guidelines. Apply these rules whenever designing new interfaces, refactoring components, or auditing frontends for production-grade craft.

## Rules Checklist

### 1. Touch & Mobile Ergonomics
- `touch-action: manipulation` on buttons, interactive chips, and controls (prevents double-tap zoom delay on mobile).
- `overscroll-behavior: contain` in modals, bottom sheets, drawers, and nested scrollable containers (prevents scroll chaining and page bounce).
- `-webkit-tap-highlight-color: transparent` (or intentional accent color) to avoid ugly grey highlight flashes on tap.
- Set minimum touch target size to 44×44px (or 48×48px) with at least 8px spacing between tap targets.
- Full-bleed layouts on mobile must respect `env(safe-area-inset-top)` and `env(safe-area-inset-bottom)` for notches and home indicators.
- Avoid horizontal viewport blowout: set `overflow-x: hidden` on parent containers and check that wide content (like chord diagrams or fretboards) is wrapped in dedicated horizontal scroll containers.

### 2. Accessibility & Semantics
- Icon-only buttons MUST have a descriptive `aria-label`.
- Form controls must have an associated `<label>` or `aria-label`.
- Interactive elements must be keyboard-accessible (`<button>`, `<a>`), never plain `<div onclick>`.
- Decorative icons must have `aria-hidden="true"`.
- Live/async updates (status messages, toasts, audio states) need `aria-live="polite"`.
- Images must have meaningful `alt` text, or `alt=""` if purely decorative.

### 3. Focus States & Interaction
- Interactive elements must have clear focus rings: `focus-visible:ring-2` or equivalent outline.
- Never set `outline: none` without providing a visible `:focus-visible` replacement.
- Use `:focus-visible` over `:focus` to prevent permanent focus rings after mouse clicks or screen taps.
- Group compound controls using `:focus-within`.

### 4. Animation & Motion
- Always respect `prefers-reduced-motion` media queries.
- Animate only compositor-friendly properties: `transform` and `opacity`.
- Avoid `transition: all`; explicitly list the transition properties (`transition: transform 0.2s ease, opacity 0.2s ease`).
- For SVGs: apply transforms on `<g>` wrappers with `transform-box: fill-box; transform-origin: center`.
- Animations should be interruptible and feel snappy (< 300ms for UI responses).

### 5. Dark Mode & Theming
- Include `color-scheme: dark` on `<html>` or `<body>` so native elements (scrollbars, form inputs) match dark mode.
- Avoid pure pitch black `#000000` for surface cards; use deep obsidian tones (`#090d16`, `#0e131f`) with subtle borders (`rgba(255, 255, 255, 0.08)`) and vibrant neon accents for depth and visual hierarchy.
- Ensure text contrast meets WCAG AA (at least 4.5:1 for body text, 3:1 for large display headers).

### 6. Typography & Content
- Use `…` (ellipsis character) instead of `...` (three periods).
- Use `text-wrap: balance` or `text-wrap: pretty` on headlines to avoid orphan words.
- Use `font-variant-numeric: tabular-nums` for counters, numbers, BPM displays, and timers.
- Prevent layout shifts (CLS): reserve aspect ratios and heights for dynamically loaded graphics or interactive canvases.
