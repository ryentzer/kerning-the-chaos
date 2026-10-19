# Deconstructing three reveal sites

**Date:** October 17, 2026
**Question:** How do Oryzo, Design is Funny and the Anime.js site make text and sections come into view?
**Method:** Loaded each site in a headless browser, saved every script it downloaded, and searched the bundles for library fingerprints, option names and ease strings. Minified code scrambles variable names but keeps strings, option keys and numbers.

## The big idea

Scroll can play two roles. It can be a **trigger** that starts a timed animation, or it can be the **clock** that directly sets how far along the animation is. Choosing between them changes how a site feels more than any ease does.

## Oryzo (Lusion): scroll as the clock

- Custom engine on Three.js (`ScrollManager`, `ScrollDomRange`, `ScreenPaintDistortion`, `MSDFTextGeometry`).
- GSAP SplitText 3.14.2 used only to split text. No ScrollTrigger, no Lenis.
- No reveal tweens. Every frame, each character's style is computed from scroll progress with a clamped range map:

```js
function fit(v, inMin, inMax, outMin, outMax, ease) {
  let t = Math.min(1, Math.max(0, (v - inMin) / (inMax - inMin)));
  if (ease) t = ease(t);
  return outMin + t * (outMax - outMin);
}
// per character i of n
const e = i / (n - 1);
char.style.opacity = fit(p, 0.5 + e * 0.2, 1.5 + e * 0.2, 0, 1);
char.style.transform = `translate3d(${fit(p, 0.5 + e * 0.2, 1.5 + e * 0.2, 1, 0, cubicOut)}em,0,0)`;
```

- Each character gets its own window of progress. Spread and window width are the whole design vocabulary.
- Motion in `em`, blur switched off on mobile layouts.

## Design is Funny (Daniele Buffa): scroll as a trigger

- Next.js, GSAP + ScrollTrigger + SplitText 3.11.5, Lenis, Three.js.
- Trigger: `ScrollTrigger.create({ start: "25% bottom", once: true, onEnter })`.
- Heading: split `chars,words`, words masked; chars from `yPercent: 60, rotateX: 70, autoAlpha: 0`, origin bottom, `2.5s expo.out`, stagger `0.03`.
- Paragraph: words from `yPercent: 40, rotateX: 60`, stagger `0.01–0.05`.
- Nav hover roll: chars `yPercent: -100`, `0.7s expo.inOut`, stagger `0.012`.
- Image curtain: outer `yPercent 100 → 0`, inner `yPercent -100 → 0` + `scale 1.3 → 1`, `1s expo.inOut`.
- Lenis: `duration: 0.75`, easing `t => Math.min(1, 1.001 - Math.pow(2, -10 * t))`.
- Characters get `rotate(0.01deg)` to stop subpixel jitter on long eases.

## Anime.js site: the library's own observer

- Anime.js 4.5.0 with `onScroll` and `splitText`, Three.js for the exploded drawing.
- Observers like `onScroll({ enter: "top top", leave: "bottom bottom", sync: .9 })`.
- Threshold order is **container first, then target**, the reverse of ScrollTrigger.
- `sync` below 1 smooths, and lower is heavier.
- Line splitting waits for `document.fonts.ready`, so build line animations inside `split.addEffect()`.

## Where this went

These findings became the guide `guides/anatomy-of-a-reveal.html`.
