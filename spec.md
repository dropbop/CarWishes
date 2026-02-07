# SPEC.md — The List

## I. The Space

Close your eyes. You're standing in a corrugated steel building outside Kópavogur. It's 2:30 PM in December and it's been dark for an hour. The only light is a bank of industrial fluorescents — the kind that hum at 50Hz and turn everything slightly green-yellow. Half of them are dead. The ones that work cast hard pools of light separated by actual darkness. Not dim. Dark.

The floor is poured concrete that was never sealed. There are cracks filled with chalk dust and iron oxide. Somewhere, a space heater is losing a war against the North Atlantic. The walls are bare corrugated metal — galvanized, not painted — with condensation beading on the ridges. There's a smell: cold iron, rubber mats, chalk, diesel from the generator outside, and something faintly metallic that might be blood from someone's shins.

A man who weighs 180 kilograms is standing under one of the working fluorescents. He is holding 400 kilograms across his back. The bar is bending. The plates are iron, not rubber — old Eleiko competition plates with chipped paint, calibrated to the gram twenty years ago, now slightly rusted at the edges. He is completely silent. The only sound is the hum of the lights and the creak of the bar.

There is no music. There is no mirror. There is no branding. There are no motivational posters. There is a man, a bar, and gravity.

This is the energy of the website.

---

## II. Design Philosophy

**The aesthetic is weight.** Everything should feel like it has mass. Typography is heavy. Spacing is deliberate — not generous, not cramped, but *placed* like equipment on a platform. There's no decoration. Every element exists because it needs to. If it doesn't hold weight, it doesn't belong.

**The palette is what you'd actually see.** Not "dark theme with accent colors." Actual materials:
- The darkness of an unlit concrete room
- The flat warmth of a dying fluorescent tube
- The dull grey of raw steel
- The faint orange of surface rust
- The dirty white of old chalk on a dark surface

**The texture is industrial.** Subtle grain everywhere — not a Photoshop noise filter, but the visual equivalent of running your hand across unsealed concrete. The screen should feel *cold* somehow. Slightly rough. Like if you touched it you'd feel grit.

**The typography is blunt.** No serifs. No elegance. No ligatures. The typeface should feel like it was stamped into metal, not drawn with a pen. Heavy weight, tight tracking, uppercase where it matters. Think equipment serial numbers. Think weight class placards at a competition. Think the font on the side of a shipping container.

**The light is scarce.** Most of the page is dark. Text and content exist in pools of visibility, like standing under one of those fluorescent strips. The edges of things fade. There's no hard container — content emerges from and recedes into darkness. The background is not a flat color. It has depth. It breathes slightly.

---

## III. Content Architecture

This is a list. That's it. The information hierarchy is:

```
THE LIST (title — heavy, unavoidable, like a slab of iron)
  ├── Datestamp (when the list was born — small, chalked, fading)
  ├── Car 1
  │     └── Name only. No image. No description. Just the name.
  ├── Car 2
  ├── ...
  └── Car N
```

Each car entry is a line. Not a card. Not a tile. A line. Like a training log. Like chalk tallies on a wall. Like a manifest.

Cars that have been acquired get a single, brutal indicator — not a checkbox, not a strikethrough. Something heavier. A stamp. A brand. Think: the mark a blacksmith puts on finished work.

Cars removed from the list simply cease to exist. No "retired" section. No graveyard. If you don't want it anymore, it was never here.

---

## IV. Technical Specification

### Stack
- Single `index.html` file
- All CSS inline in a `<style>` block
- All data in a `const` array at the top of a `<script>` block
- No build step. No dependencies. No framework. No CDN fonts.
- Hosted on GitHub Pages (or opened as a local file — must work both ways)

### Data Structure
```javascript
const LIST_CREATED = "2025-02-07";

const CARS = [
  { name: "B5 Audi S4", year: null, status: "want" },
  { name: "W140 S-Class", year: null, status: "want" },
  { name: "Diablo SV", year: null, status: "want" },
  { name: "Ferrari 348ts", year: null, status: "want" },
  { name: "Pre-LP Gallardo", year: null, status: "want" },
  { name: "E39 M5", year: null, status: "want" },
  { name: "Early R8", year: null, status: "want" },
  { name: "E60 M5", year: null, status: "want" },
  { name: "AMG Hammer Wagon", year: null, status: "want" },
  { name: "C6 Corvette", year: null, status: "want" },
  { name: "996 or 997 911", year: null, status: "want" },
  { name: "Toyota Century (90s)", year: null, status: "want" },
  { name: "CT4-V or CT5-V Blackwing", year: null, status: "want" },
  { name: "WS6 Trans Am", year: null, status: "want" },
];
// status: "want" | "owned" | (or just delete the entry)
// year: optional model year or year acquired — null if not relevant
```

To add a car: add a line to the array. To remove one: delete it. To mark one owned: change status to `"owned"`. That's the entire CMS.

### Typography
- **Primary font:** System font stack, leaning on `Arial Black`, `Impact`, or whatever the heaviest sans-serif available is. No web fonts — this thing should load like a brick through a window.
- Fallback stack: `"Arial Black", "Arial Bold", Helvetica, sans-serif`
- If a heavier system font is desired, consider a single self-hosted `.woff2` — something like **Inter Black**, **Bebas Neue**, or **Oswald Bold**. Keep it to one file, one weight.
- Title: massive, uppercase, letter-spaced slightly
- List items: large, uppercase, slightly tracked, heavy weight
- Date/metadata: small, monospaced, muted — like a serial number stamped into the corner

### Color Palette
```css
:root {
  /* The darkness — not pure black, concrete-dark */
  --void: #0a0a0a;
  --concrete: #141413;
  --concrete-light: #1c1c1a;

  /* The light — fluorescent-warm, slightly sickly */
  --fluorescent: #d4c9a8;
  --fluorescent-dim: #8a8068;
  --fluorescent-ghost: #3d3a30;

  /* The iron — cold grey, metallic */
  --steel: #6b6b6b;
  --steel-dark: #2a2a2a;

  /* The rust — the only warmth */
  --rust: #8b4513;
  --rust-glow: #a0522d;

  /* Chalk — for subtle marks */
  --chalk: #c8c0ab;
  --chalk-faded: #4a4637;
}
```

### Layout & Spacing
- Max-width: `700px`, centered. The list doesn't need to fill a widescreen monitor. It should feel like a narrow column of light.
- Generous vertical padding top and bottom — the content floats in the middle of darkness.
- Each car entry: single line, left-aligned, with enough vertical space to breathe but not so much that it feels airy. Think: 1.4em line height with 0.6em margin between entries.
- No horizontal rules. No dividers. The space itself is the divider.

### Visual Effects (CSS only, subtle)
1. **Background grain:** CSS noise texture via a tiny repeating SVG or a pseudo-element with a CSS gradient trick. Very subtle. Like concrete texture at 5% opacity.

2. **Fluorescent flicker:** A CSS animation on the title or header area — not a literal flicker (that's annoying), but a very slow, barely perceptible opacity oscillation. Like a fluorescent tube that's almost dead. `animation: flicker 8s ease-in-out infinite`. Amplitude: 0.97 to 1.0 opacity. You should barely notice it. If you notice it immediately, it's too much.

3. **Light pool effect:** The content area has a very subtle radial gradient behind it — slightly lighter in the center, fading to pure darkness at the edges. Like a spotlight from above. Not a visible circle of light, just a *tendency* toward visibility in the center.

4. **Rust brand on owned cars:** Owned cars get a small mark — could be a Unicode character (▮, ◼, ✕) in `--rust` color, or a CSS-generated pseudo-element. Something that reads as "this one's done." Blunt. Permanent-looking.

5. **Entry weight:** Each car name should feel stamped. `text-shadow: 1px 1px 0 rgba(0,0,0,0.5)` — the faintest impression of depth, like letters pressed into sheet metal.

### Responsiveness
- Works on mobile. The list is already narrow. Just ensure the text doesn't break weirdly.
- No hamburger menu. No navigation. There's nothing to navigate to.
- On very small screens, the font just gets slightly smaller. That's it.

### Performance
- Total page weight target: under 15KB. Ideally under 10KB.
- No images (unless self-hosting one font file)
- First paint: instantaneous
- This page should load faster than the user's finger leaves the mouse button

---

## V. What This Is Not

- This is not a car blog
- This is not a gallery
- This is not interactive
- This is not social
- This is not trying to impress anyone
- This is a man's list, written in iron, kept in the dark

Build it like it weighs something.
