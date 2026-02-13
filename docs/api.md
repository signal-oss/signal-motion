# Public API

Signal Motion exposes a minimal, deterministic API for React.

The API is intentionally small.

Signal Motion prioritizes:

- Semantic presets
- Token-driven configuration
- Lifecycle-aware transitions
- Predictable overrides

---

# Installation

```bash
npm install @signal/motion-react
```

# Core Components

## Motion Component

    `<Motion />`

```tsx
<Motion preset="slideUp" speed="base" easing="easeOut">
  <Panel />
</Motion>
```

## Props

```tsx
interface MotionProps {
  preset: string;

  speed?: string; // duration token
  easing?: string; // easing token

  as?: React.ElementType; // wrapper element
  className?: string;
  style?: React.CSSProperties;

  onStart?: () => void;
  onComplete?: () => void;

  children: React.ReactNode;
}
```

## Motion.Provider

```tsx
<Motion.Provider
  strategy="skip"
  tokens={{
    duration: {
      base: 200,
    },
    easing: {
      easeOut: "cubic-bezier(0, 0, 0.2, 1)",
    },
  }}
>
  <App />
</Motion.Provider>
```

## Behavior

- Resolves preset from MotionConfig
- Resolves duration token
- Resolves easing token
- Generates deterministic keyframes
- Executes via WAAPI
- Applies reduced-motion policy
- Cancels animation on unmount

## Enter / Exit Animation

    `<Animate />`

```tsx
<Animate when={isOpen} enter="slideUp" exit="fade">
  <Panel />
</Animate>
```

For conditional mounting transitions.

## Props

```tsx
interface AnimateProps {
  when: boolean;

  enter: string;
  exit?: string;

  speed?: string;
  easing?: string;

  children: React.ReactNode;
}
```

## Behavior

When `when` changes:

`true →` → run enter preset

`false →` → run exit preset before unmount

DOM removal occurs after exit animation completes.
