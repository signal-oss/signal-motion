# Introduction

Signal Motion is a hybrid, token-driven motion system built for product-grade UX.

It standardizes animation behavior across applications by combining:

- Utility-first motion classes (CSS layer)
- A WAAPI-driven runtime engine
- Semantic presets aligned with product intent

Signal Motion is not an animation playground.  
It is motion infrastructure.

---

# Why Signal Motion?

Most animation libraries optimize for flexibility.

Signal Motion optimizes for:

- Predictability
- Design system alignment
- Token-driven motion
- Product state transitions
- Governance and accessibility

In many teams, motion becomes inconsistent over time:

- Arbitrary durations
- Random cubic-bezier curves
- Inconsistent enter/exit behavior
- Accessibility drift

Signal Motion prevents that.

---

# The Hybrid Model

Signal Motion combines two layers intentionally.

## 1. CSS Utility Layer

Designed for:

- Micro-interactions
- Hover states
- Simple transitions
- Design system consistency

Example:

```tsx
<div className="motion-fade motion-fast motion-easeOut" />
```

## 2. Runtime Engine (WAAPI-first)

Designed for:

- Enter/exit transitions
- Mount/unmount animation
- Stateful motion
- Semantic presets
- Reduced-motion enforcement

Example:

```ts
<Motion preset="slideUp" speed="base">
  <Panel />
</Motion>
```

This layer:

- Resolves motion tokens
- Compiles semantic transforms
- Executes animations via the Web Animations API
- Enforces accessibility policies

# Core Principles

Signal Motion is built on five non-negotiable principles:

- System > flexibility
- Tokens > arbitrary values
- Semantic presets > raw transforms
- Accessibility is first-class
- Motion must be governable

Motion is part of product behavior.
It must be consistent, measurable, and enforceable.

# What Signal Motion Is Not

# Signal Motion is not:

- A physics-heavy animation engine
- A freeform motion DSL
- A visual animation editor
- A design tool replacement

# It is product-focused motion infrastructure.

# Designed for Product Teams

Signal Motion is built for: - Design system maintainers - Product engineers - UX-focused frontend teams - Organizations that care about consistency

# It scales from:

- Small component libraries
  to
- Multi-surface product ecosystems

# Future Direction

Signal Motion is structured to support:

- Motion analytics
- Preset usage tracking
- Unsafe motion detection
- Performance auditing
- Design system governance

Motion is not just styling.
It is structured behavioral metadata.

---
