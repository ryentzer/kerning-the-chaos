# The quiet school: Electronic Materials Office

**Date:** October 18, 2026
**Site:** electronicmaterialsoffice.com
**Question:** What makes the animation on this site feel subtle but polished?

## The stack

Hand-written, unminified JavaScript in one 40KB file, plus self-hosted GSAP 3.12.7 core. No ScrollTrigger, no SplitText, no smooth scroll, no WebGL.

## One reveal system

```css
.reveal { opacity: 0; transform: translateY(24px); will-change: transform, opacity; }
.gsap-fallback .reveal { opacity: 1; transform: none; }
```

```js
const io = new IntersectionObserver(entries => entries.forEach(entry => {
  if (!entry.isIntersecting) return;
  io.unobserve(entry.target);                       // reveal once
  gsap.to(entry.target, {
    opacity: 1, y: 0, duration: 0.6,
    onComplete: () => gsap.set(entry.target, { clearProps: "transform,opacity" })
  });
}), { rootMargin: "0px 0px -15% 0px" });
```

- Single items: 0.6s. Card rows: 0.4s, staggered 0.1s. Groups: staggered 0.2s on desktop, all at once at 768px and below.
- Inline styles are cleared after each reveal, so the page ends in pure CSS.

## Tactile details

- Cards scale to 1.02 on hover and 0.99 when pressed. Buttons press to 0.95–0.98.
- The fixed header slides in over 0.2s after the hero scrolls away.
- Videos play only near the middle of the viewport. Pause buttons have a progress ring made with the stroke-dash technique.
- Five custom cursor SVGs (default, pointer, text, grab, grabbing).
- Haptics on phones through `navigator.vibrate`, with a double pulse on the Reserve button.

## Resilience

One switch disables all motion if GSAP fails to load **or** the visitor prefers reduced motion. It adds a `gsap-fallback` class, and CSS shows everything at once.

## A bug worth learning from

The code passes CSS-style easing strings like `'cubic-bezier(0.25, 0.1, 0.25, 1)'` to GSAP. Tested against the GSAP library: core GSAP doesn't parse that syntax without the CustomEase plugin and silently falls back to its default, `power1.out`. The curves look nearly the same over 0.6s, so nobody notices, but the curve written isn't the curve that runs.

## Lesson

Subtle is a system: one easing feel, two or three durations, one 24px distance, and press feedback of a percent or two. The craft is in the consistency.
