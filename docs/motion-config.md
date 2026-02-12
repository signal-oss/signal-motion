# Motion Config

The Motion Config is the foundational contract of Signal Motion.

It defines:

- Duration tokens
- Easing tokens
- Semantic motion presets
- Transform semantics
- Accessibility behavior
- Runtime resolution rules

Both the CSS utility layer and the runtime engine consume this configuration.

Signal Motion is token-driven by design.
Arbitrary animation values are discouraged.

---

# 1. Design Principles

1. System > flexibility
2. Tokens > arbitrary values
3. Semantic presets > raw transforms
4. Accessibility is first-class
5. CSS and runtime share the same source of truth

---

# 2. Core Type Definitions

````ts
export interface MotionConfig {
  durations: DurationScale
  easings: EasingScale
  presets: PresetScale
  global?: GlobalMotionSettings
}

export type DurationScale = Record<string, number>
export type EasingScale = Record<string, string>

export type PresetScale = Record<string, MotionPreset>

export interface MotionPreset {
  from: MotionStyles
  to: MotionStyles
  defaultDuration?: keyof DurationScale
  defaultEasing?: keyof EasingScale
}

export interface MotionStyles {
  opacity?: number
  x?: number
  y?: number
  scale?: number
  rotate?: number
}

export interface GlobalMotionSettings {
  reducedMotionStrategy?: "skip" | "shorten" | "replace"
  shortenFactor?: number
}
---

# 3. Transform Semantics

Signal Motion abstracts transforms into semantic axes:

| Property | Meaning                     |
| -------- | --------------------------- |
| x        | Horizontal translation (px) |
| y        | Vertical translation (px)   |
| scale    | Uniform scaling             |
| rotate   | Rotation (deg)              |
| opacity  | Opacity (0–1)               |

Internally, transforms are compiled into:

```css
transform: translateX(...) translateY(...) scale(...) rotate(...)
````

## This keeps the API semantic and predictable.

# 4. Default Duration Scale

```ts
durations: {
  instant: 80,
  fast: 120,
  base: 200,
  slow: 320,
  expressive: 420
}
```

Rationale:

<100ms → perceived as immediate

120–220ms → micro interaction range

## 320ms+ → structural transitions

# 5. Default Easing Scale

```ts
easings: {
  linear: "linear",
  easeIn: "cubic-bezier(0.4, 0, 1, 1)",
  easeOut: "cubic-bezier(0, 0, 0.2, 1)",
  easeInOut: "cubic-bezier(0.4, 0, 0.2, 1)",
  spring: "cubic-bezier(0.175, 0.885, 0.32, 1.275)"
}
```

---

# 6. Semantic Presets

Presets define common motion patterns:

```ts
presets: {
  // Fade in from nothing
  fade: {
    from: { opacity: 0 },
    to: { opacity: 1 },
    defaultDuration: "base",
    defaultEasing: "easeOut"
  },

  // Slide up from below
  slideUp: {
    from: { y: 20, opacity: 0 },
    to: { y: 0, opacity: 1 },
    defaultDuration: "base",
    defaultEasing: "easeOut"
  },

  // Scale up from center
  scaleUp: {
    from: { scale: 0.95, opacity: 0 },
    to: { scale: 1, opacity: 1 },
    defaultDuration: "base",
    defaultEasing: "easeOut"
  },

  // Spring-based pop
  pop: {
    from: { scale: 0.9 },
    to: { scale: 1 },
    defaultDuration: "fast",
    defaultEasing: "spring"
  }
}
```

---

# 7. Global Settings

```ts
global: {
  reducedMotionStrategy: "shorten",
  shortenFactor: 0.5
}
```

---

# 8. Runtime Resolution

When a preset is used:

```ts
// Runtime engine resolves this to:
{
  duration: 200,
  easing: "easeOut",
  keyframes: [
    { opacity: 0, transform: "translateY(20px)" },
    { opacity: 1, transform: "translateY(0)" }
  ]
}
```

---

# 9. Example Motion Config

```ts
export const motionConfig: MotionConfig = {
  durations: {
    fast: 120,
    base: 200,
    slow: 320,
  },

  easings: {
    easeOut: "cubic-bezier(0, 0, 0.2, 1)",
    spring: "cubic-bezier(0.175, 0.885, 0.32, 1.275)",
  },

  presets: {
    fade: {
      from: { opacity: 0 },
      to: { opacity: 1 },
      defaultDuration: "base",
      defaultEasing: "easeOut",
    },

    slideUp: {
      from: { y: 20, opacity: 0 },
      to: { y: 0, opacity: 1 },
      defaultDuration: "base",
      defaultEasing: "easeOut",
    },

    pop: {
      from: { scale: 0.9 },
      to: { scale: 1 },
      defaultDuration: "fast",
      defaultEasing: "spring",
    },
  },

  global: {
    reducedMotionStrategy: "shorten",
    shortenFactor: 0.5,
  },
};
```
