<!-- artspo:book title="The Artbook library" url="https://artbook.dev/library/" built="2026-10-18 15:50" format="1" -->
# The Artbook library

An Artspo book: 4 design languages, 25 techniques and 0 works, rebuilt from measurements of real websites. Every recipe is a generic reconstruction, not a site's code.

**For agents.** Each pattern below stands on its own: take one section to use one move, or read the whole book as a style reference. Follow the rules at the end. To add this book to an Artspo library, run the artspo skill's importer: `python3 import_book.py https://artbook.dev/library/artbook.md`.

## Contents

- Languages: Cinematic media canvas, Humane editorial, Research index, Retro machine pop
- Techniques, color: Accent rationing, Analog grain, Color-indexed sections, Highlighter marks, Warm-tinted depth
- Techniques, layout: Announcement bar, Artifact as hero, Benchmark as headline, Numbered sections, Object carousel hero, Ruled structure
- Techniques, motion: Ambient breathing glow, Cinematic entrance, Develop reveal, Inertial smooth scroll, Four-tier motion timing, Narrated proof, Soft rise reveal, Springs for characters only, Static by design
- Techniques, shape: Hard edges, flat depth
- Techniques, type: Machine-voice labels, One family, scale does the work, Oversized tight display, Serif display, sans UI

## Languages

<!-- artspo:pattern id="cinematic-media-canvas" kind="language" status="emerging" -->
### Cinematic media canvas

_A screening room. Dark, media-first, and things develop into view instead of sliding in._

> **Emerging:** one strong example so far. Treat it as a sketch until another clip confirms it.

#### Defining traits

- **Color.** A light dotted canvas for the hero (#FAFAFA) cutting to near-black working sections (#0E0E0E / #202020 / #2A2A2A); one hot accent (#F04E23) and one soft highlight (#FFF78B).
- **Type.** Serif display (56px, -0.02em, line-height 1) over a neutral sans; the serif signals 'creative', the sans 'tool'.
- **Imagery.** Media is the content: a curved 3D carousel of real outputs, node graphs of workflows.
- **Motion.** Cinematic entrances (1500ms expo-out, scale 1.2 → 1), tiles that 'develop' from a brightness flash, breathing glow on the card that sells, animated film-grain noise. Smooth scroll throughout.

#### Techniques it uses

- Cinematic entrance: The hero arrives slowly (about 1.5s), scaling down from 1.2 while it fades in on a long expo-out, like a camera settling.
- Develop reveal: Images appear overexposed and settle to normal, like a photo developing, staggered across a grid.
- Ambient breathing glow: A slow loop (3.5–5s) gently pulsing opacity and scale on a glow behind the thing that matters: the hero object, or the plan you want chosen.
- Analog grain: A paper, film or halftone texture over flat color, to take the digital sterility off a page.
- Object carousel hero: The hero is a row of objects or media with the focused one centered and full, and its neighbors scaled down and faded.
- Serif display, sans UI: Headlines in a text serif with tight tracking; everything you interact with in a neutral sans.
- Inertial smooth scroll: Scroll is taken over by a smoothing library, so the page glides with momentum.
- Accent rationing: One saturated color is reserved for the action and the data.
- Artifact as hero: The hero shows the product's literal interaction (the prompt box you type into, the one-line diff you'd make, the code and what it compiles into), not a screenshot or an abstraction.

#### Starter tokens

```css
--canvas: #FAFAFA;  --stage: #0E0E0E;  --stage-2: #202020;  --stage-line: #2A2A2A;
--hot: #F04E23;  --glow: #FFF78B;
--radius: 2px 4px 6px 8px;   /* small, many */
--t-entrance: 1500ms cubic-bezier(0.16, 1, 0.3, 1);  --entrance-from: scale(1.2);
--t-develop: 750ms cubic-bezier(0, 0.55, 0.45, 1);   --stagger-tiles: by scroll position;
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #0E0E0E; color: #FAFAFA; text-align: center; padding-top: 34px; }
h1 { font: 400 40px/1 "Iowan Old Style", "Charter", Georgia, serif; letter-spacing: -0.02em; margin: 0 0 8px; animation: settle 1500ms cubic-bezier(0.16,1,0.3,1) both; }
.sub { color: #9a9a9a; font-size: 14px; animation: settle 1500ms cubic-bezier(0.16,1,0.3,1) 200ms both; }
@keyframes settle { from { opacity: 0; transform: scale(1.2); } }
.row { display: flex; gap: 8px; justify-content: center; margin-top: 26px; perspective: 600px; }
.row i { width: 92px; height: 120px; border-radius: 4px; background: var(--g); animation: develop 750ms cubic-bezier(0,0.55,0.45,1) both; animation-delay: calc(700ms + var(--i) * 140ms); }
.row i:nth-child(1) { transform: rotateY(28deg); } .row i:nth-child(5) { transform: rotateY(-28deg); }
@keyframes develop { from { filter: brightness(1000%) sepia(20%); } }
.chip { display: inline-block; margin-top: 18px; background: #FFF78B; color: #0E0E0E; border-radius: 4px; padding: 6px 10px; font-size: 12px; }
</style>
<div class="s"><h1>Picture it. Then watch it land.</h1><div class="sub">One prompt, every model, shown as it renders.</div>
<div class="row"><i style="--i:0;--g:linear-gradient(160deg,#2d4a63,#c08a5a)"></i><i style="--i:1;--g:linear-gradient(200deg,#5b2a3e,#e0b36a)"></i><i style="--i:2;--g:linear-gradient(170deg,#163a2c,#9fd0a6)"></i><i style="--i:3;--g:linear-gradient(190deg,#33244f,#d78bd0)"></i><i style="--i:4;--g:linear-gradient(150deg,#4a3a20,#f0d080)"></i></div>
<span class="chip">Try it free</span></div>
```

#### Use when

Products whose output is visual (media, design, video), where showing the work is the argument.

#### Avoid when

Text-heavy products. Without strong media this is just a dark page with slow fades.

Measured on: Melius, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="humane-editorial" kind="language" status="established" -->
### Humane editorial

_A well-made magazine about technology that feels human: calm, warm, crafted. The product is technical, but the page leads with feeling._

#### Defining traits

- **Type.** Serif display with a sans for UI (Jog: Source Serif 4 56/500 at -0.022em, line-height 1.04; Handwired: Iowan Old Style 60/400 at the same -0.022em; Era: IvyOra serif for almost all text). Mono shows up only where the product is code.
- **Color.** Warm paper (#F4EBDA, 72% of Jog; #F3EEE4 behind Handwired's #FFFDF8 cards) or airy white (84% of Era); brown-black ink instead of pure black (#4B4036, #5F564D); one quiet accent (Era's green #369169, Handwired's rust #A64D1D).
- **Imagery.** Art, objects or a crafted artifact as the hero, not UI chrome: an impressionist painting framed in a card (Jog), glowing translucent bags (Era), a code block that becomes a hand-drawn wiring diagram (Handwired).
- **Shape.** Soft but not bubbly: 6px controls, pill tags, one large hero card; warm-tinted shadows or glows instead of gray ones.
- **Motion.** Slow and quiet, or none: 550–900ms ease-out fades with 18px rises and 40–70ms staggers; ambient breathing loops of 4s or more; springs only on objects. Handwired shows the language holds up fully static, with only 120/280ms hover transitions.

#### Techniques it uses

- Serif display, sans UI: Headlines in a text serif with tight tracking; everything you interact with in a neutral sans.
- Analog grain: A paper, film or halftone texture over flat color, to take the digital sterility off a page.
- Warm-tinted depth: Shadows and lines are tinted with the ground color's hue instead of gray, so elevation feels like paper lifting, not plastic.
- Soft rise reveal: Content fades in while rising a short distance, with a strong ease-out and a small stagger.
- Ambient breathing glow: A slow loop (3.5–5s) gently pulsing opacity and scale on a glow behind the thing that matters: the hero object, or the plan you want chosen.
- Object carousel hero: The hero is a row of objects or media with the focused one centered and full, and its neighbors scaled down and faded.
- Artifact as hero: The hero shows the product's literal interaction (the prompt box you type into, the one-line diff you'd make, the code and what it compiles into), not a screenshot or an abstraction.
- Narrated proof: The hero artifact acts out the claim in sequence: strike the old value, type the new one, blink a caret.
- Springs for characters only: An overshooting spring (back-out) is reserved for characters and objects: mascots, products, carousel items.

#### Starter tokens

```css
--ground: #F4EBDA;  --ground-raised: #FAF5EC;  --ink: #2A2119;  --ink-body: #4B4036;  --ink-muted: #A99B8B;
--line: 1px solid #D9CDB9;
--shadow-soft: 0 1px 2px rgba(52, 40, 18, 0.07);  --shadow-lift: 0 30px 80px -30px rgba(20, 14, 4, 0.55);
--radius-control: 6px;  --radius-tag: 999px;
--font-display: "<text serif>", Georgia, serif;   /* tracking -0.02em, leading 1.04 */
--font-ui: "<humanist sans>", system-ui;   --font-code: "<mono>", ui-monospace;
--t-reveal: 550ms cubic-bezier(0.22, 1, 0.36, 1);  --stagger: 40ms;  --rise: 18px;
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F4EBDA; color: #2A2119; display: grid; grid-template-columns: 1.1fr 1fr; gap: 28px; align-items: center; }
h1 { font: 500 40px/1.04 "Iowan Old Style", "Charter", Georgia, serif; letter-spacing: -0.022em; margin: 0 0 12px; }
p { color: #4B4036; margin: 0 0 18px; max-width: 34ch; }
.btn { display: inline-block; background: #1F1814; color: #F5F0E7; border-radius: 6px; padding: 10px 16px; font-size: 14px; }
.tag { display: inline-block; border: 1px solid #D9CDB9; border-radius: 999px; padding: 2px 10px; font-size: 12px; color: #4B4036; margin-bottom: 14px; }
.card { background: #FAF5EC; border-radius: 10px; padding: 18px; box-shadow: 0 1px 2px rgba(52,40,18,.07), 0 0 0 1px rgb(191,176,150), 0 30px 80px -30px rgba(20,14,4,.55); font: 13px/1.7 ui-monospace, "SF Mono", Menlo, Consolas, monospace; }
.del { color: #9a3b2b; } .ins { color: #2f6b3f; }
.r { opacity: 0; transform: translateY(18px); animation: rise 550ms cubic-bezier(0.22,1,0.36,1) forwards; animation-delay: calc(var(--i) * 40ms + 150ms); }
@keyframes rise { to { opacity: 1; transform: none; } }
</style>
<div class="s"><div><span class="tag r" style="--i:0">Field notes</span>
<h1 class="r" style="--i:1">Quiet tools for careful work.</h1>
<p class="r" style="--i:2">Change one line. Everything else stays where you left it.</p>
<span class="btn r" style="--i:3">Start writing</span></div>
<div class="card r" style="--i:4"><div class="cap">settings.yml</div><div class="del">− plan: legacy</div><div class="ins">+ plan: fieldnote</div></div></div>
```

#### Use when

Products that want trust through calm: developer tools that sell on taste, consumer AI, anything priced on quality rather than features.

#### Avoid when

Dense dashboards, or anything that must feel fast and aggressive. Serif plus slow motion reads as considered, not urgent.

Measured on: Jog, Era, Handwired.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="research-index" kind="language" status="established" -->
### Research index

_A lab notebook made public. Numbered, ruled, precise, confident. Color works as an index or a highlighter, never as decoration._

#### Defining traits

- **Structure.** Numbered sections (01, 02 …), hairline or 2px rules, uppercase mono labels; the page reads like a document with chapters.
- **Type.** One grotesk family carries every role, with hierarchy from size alone (Hone: 13px → 120px, all FT Aktual). Variant: light grotesk plus mono labels (Preference Model: Lausanne 300 + Martian Mono uppercase).
- **Color.** Neutral ground (white / light gray / black) plus a highlighter accent: Hone's lime #BCF891 / #3BD966, or Preference Model's set of index chips (pink, yellow, orange, cyan, green), one per section.
- **Shape.** 0–2px radii, no shadows. Depth comes from color bands, never elevation.
- **Motion.** Either none at all (Preference Model has no load or scroll motion) or a strict system (Hone: 200ms micro, 400ms reveals, back-out springs only on the mascot). Never decorative drift.

#### Techniques it uses

- Numbered sections: Sections numbered 01, 02 … like chapters, so a long page reads as an ordered argument and not a scroll of features.
- Ruled structure: Hairline rules divide columns, list rows and FAQ entries, so the grid is visible like a printed table.
- One family, scale does the work: A single grotesk family for every role, with hierarchy made only through size and space.
- Machine-voice labels: A mono or pixel face as a secondary voice for labels, metadata, numbers and code.
- Highlighter marks: Key words get a flat background block like a marker pen, so emphasis comes from color behind the text instead of weight or size.
- Color-indexed sections: Each section gets its own color as wayfinding, either a chip next to the section number or a full-bleed band, so color tells you where you are.
- Hard edges, flat depth: Square corners (0–2px) and no shadows.
- Static by design: Little or no scroll motion, as a deliberate choice: content is simply there.
- Springs for characters only: An overshooting spring (back-out) is reserved for characters and objects: mascots, products, carousel items.

#### Starter tokens

```css
--ground: #FFFFFF;  --ground-alt: #E8E8E8;  --ink: #000000;  --ink-muted: #6B8683;
--highlight: #BCF891;              /* or one chip color per section */
--rule: 1px solid #000000;         /* Hone variant: 2px solid #CEE4E2 */
--radius: 0;                       /* max 2px */
--font-sans: "<one grotesk>", system-ui;  --font-mono: "<mono>", ui-monospace;
--scale: 13px 16px 18px 28px 48px 67px 120px;
--t-micro: 200ms cubic-bezier(0.33, 1, 0.68, 1);
--t-reveal: 400ms cubic-bezier(0.38, 0.005, 0.215, 1);
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #000; font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; }
.top { display: flex; justify-content: space-between; font: 500 11px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .05em; border-bottom: 1px solid #000; padding-bottom: 10px; }
h1 { font-size: 44px; font-weight: 400; line-height: 1.02; letter-spacing: -0.01em; margin: 22px 0 26px; max-width: 15ch; }
mark { background: #BCF891; color: inherit; padding: 0 .1em; }
.cols { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
.cols > div { border-top: 1px solid #000; padding-top: 12px; font-size: 13px; color: #333; }
.n { display: inline-block; font: 500 12px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; padding: 4px 5px; margin-bottom: 10px; }
</style>
<div class="s"><div class="top"><span>FIELDNOTE / RESEARCH</span><span>INDEX 01–03</span></div>
<h1>Measurement is <mark>the product</mark>, not a feature.</h1>
<div class="cols"><div><span class="n" style="background:#FAB3F6">01</span><br>Every claim ships with the run that produced it.</div>
<div><span class="n" style="background:#F5D547">02</span><br>Methods are public. Results are versioned.</div>
<div><span class="n" style="background:#F05A2A;color:#fff">03</span><br>Errors are listed before wins.</div></div></div>
```

#### Use when

Research-heavy, technical or trust-critical products: infrastructure, data, protocols, anything where 'we are rigorous' is the pitch.

#### Avoid when

Consumer warmth, or emotional products. It reads cold without a highlight color or a character (Hone uses mascot faces to warm it).

Measured on: Hone, Preference Model.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="retro-machine-pop" kind="language" status="emerging" -->
### Retro machine pop

_Loud, funny, nostalgic computing. It's confident enough to joke ('We raised a really big Series A')._

> **Emerging:** one strong example so far. Treat it as a sketch until another clip confirms it.

#### Defining traits

- **Color.** One loud ground color covering about half the page (#F386A1, 42%), with near-black and white sections and an occasional green band.
- **Type.** Giant grotesk display at 150px with 0.8 line-height, title-cased; mono body at 12px; a terminal or pixel font for metadata.
- **Chrome.** Retro OS windows and dialog boxes as content frames; charts drawn in window chrome; halftone dot textures.
- **Shape.** Square corners everywhere; the only shadows are hard, dark, OS-style ones.
- **Motion.** Almost none: a loading bar and blinking dots. The page is loud, so the motion stays quiet.

#### Techniques it uses

- Oversized tight display: Display type far beyond comfortable size (120–150px) with leading below 1, so words become shapes.
- Machine-voice labels: A mono or pixel face as a secondary voice for labels, metadata, numbers and code.
- Hard edges, flat depth: Square corners (0–2px) and no shadows.
- Color-indexed sections: Each section gets its own color as wayfinding, either a chip next to the section number or a full-bleed band, so color tells you where you are.
- Analog grain: A paper, film or halftone texture over flat color, to take the digital sterility off a page.
- Benchmark as headline: The claim is a number against named competitors, set huge and backed by a chart right below it.
- Static by design: Little or no scroll motion, as a deliberate choice: content is simply there.

#### Starter tokens

```css
--ground: #F386A1;  --ground-dark: #161616;  --paper: #FEFEFE;  --ink: #1E1E1E;
--radius: 0;  --shadow-window: 0 8px 24px rgba(0, 0, 0, 0.53);
--font-display: "<condensed-ish grotesk>";   /* 150px, line-height 0.8, Title Case */
--font-body: "<mono>", ui-monospace;          /* 12px */
--font-meta: "<pixel/terminal face>";
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F386A1; color: #1E1E1E; }
.s::before { content: ""; position: absolute; inset: 0; background-image: radial-gradient(#1E1E1E 1px, transparent 1.4px); background-size: 9px 9px; opacity: .14; }
h1 { position: relative; font: 800 96px/.8 "Helvetica Neue", Helvetica, Arial, sans-serif; letter-spacing: -0.02em; margin: 0 0 22px; }
.win { position: relative; width: 300px; background: #FEFEFE; border: 2px solid #1E1E1E; box-shadow: 0 8px 24px rgba(0,0,0,.53); }
.bar { display: flex; justify-content: space-between; background: #1E1E1E; color: #FEFEFE; font: 500 11px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; padding: 5px 8px; }
.win p { font: 12px/1.5 ui-monospace, "SF Mono", Menlo, Consolas, monospace; margin: 0; padding: 12px; }
.meta { position: absolute; right: 28px; bottom: 24px; font: 700 12px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .1em; }
</style>
<div class="s"><h1>The Loud<br>Machine</h1>
<div class="win"><div class="bar"><span>README.TXT</span><span>_ □ ×</span></div><p>We built a computer that talks back. It is faster than the last one, and funnier.</p></div>
<div class="meta">v1.0 ▮ READY</div></div>
```

#### Use when

Launches that need to be remembered, developer communities, products with a strong voice.

#### Avoid when

Enterprise procurement audiences, or long-form trust content. Only one strong example so far, so treat it as a sketch, not a system.

Measured on: TypeSafe AI, Preference Model.
<!-- /artspo:pattern -->

## Techniques

<!-- artspo:pattern id="accent-rationing" kind="technique" facet="color" status="established" languages="cinematic-media-canvas" -->
### Accent rationing

One saturated color is reserved for the action and the data. Everything else is neutral, so the eye goes where the money is.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--accent: <one saturated hue>;
/* allowed on: primary CTA, active nav, key numbers, success states. Nowhere else. */
.button-primary { background: var(--accent); }
.stat { color: var(--accent); }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F6F6F4; color: #222; display: grid; grid-template-columns: 1fr 1fr; gap: 20px; align-items: start; }
.card { background: #fff; border: 1px solid #e3e3df; padding: 18px; }
.k { font-size: 12px; color: #777; } .v { font-size: 40px; font-weight: 600; letter-spacing: -0.02em; }
.v.hot { color: #F04E23; }
.btn { display: inline-block; margin-top: 14px; padding: 9px 14px; font-size: 14px; border: 1px solid #ccc; color: #444; }
.btn.hot { background: #F04E23; border-color: #F04E23; color: #fff; }
.nav { display: flex; gap: 14px; font-size: 13px; color: #888; grid-column: 1 / -1; } .nav b { color: #F04E23; font-weight: 500; }
</style>
<div class="s"><div class="nav"><b>Overview</b><span>Runs</span><span>Settings</span></div>
<div class="card"><div class="k">Cost per run</div><div class="v hot">$0.0012</div><div class="k">down from $0.006</div><span class="btn hot">Switch plan</span></div>
<div class="card"><div class="k">Runs this week</div><div class="v">18,204</div><div class="k">steady</div><span class="btn">Export</span></div>
<div class="cap" style="grid-column:1/-1">one hue · on the action, the key number, the active tab · nowhere else</div></div>
```

#### Use when

Any page with one conversion goal.

#### Avoid when

When you have several equal actions; rationing needs a single winner.

#### Pairs with

Highlighter marks, Hard edges, flat depth

Measured on: Hone, Melius, Clay (app home), Era.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="analog-grain" kind="technique" facet="color" status="established" languages="humane-editorial,retro-machine-pop,cinematic-media-canvas" -->
### Analog grain

A paper, film or halftone texture over flat color, to take the digital sterility off a page.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.grain::after { content: ""; position: fixed; inset: 0; pointer-events: none; opacity: .06;
  background-image: url("noise.png");      /* 128px tile */
  animation: grain 3s steps(5) infinite; }  /* optional: film-grain jitter */
@keyframes grain { 20% { background-position: 96px -64px } 40% { background-position: -80px 112px }
  60% { background-position: 128px 48px } 80% { background-position: -48px -96px } }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; background: #1b1b1b; }
.p { position: relative; min-height: 284px; display: grid; place-items: center; color: #F4EBDA; font: 500 30px/1.1 "Iowan Old Style", "Charter", Georgia, serif; overflow: hidden; }
.p.a { background: #3a4b3f; } .p.b { background: #3a4b3f; }
.p.b::after { content: ""; position: absolute; inset: -60px; pointer-events: none; opacity: .22; mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  animation: grain 3s steps(5) infinite; }
@keyframes grain { 20% { transform: translate(24px,-16px) } 40% { transform: translate(-20px,28px) } 60% { transform: translate(32px,12px) } 80% { transform: translate(-12px,-24px) } }
.p span { position: absolute; left: 12px; bottom: 10px; color: #F4EBDA; }
</style>
<div class="s"><div class="p a">Flat color<span class="cap">no texture</span></div><div class="p b">With grain<span class="cap">noise · 3s steps(5) jitter</span></div></div>
```

#### Use when

Warm or nostalgic brands; dark pages that feel too flat.

#### Avoid when

Dense data UI; texture under small text hurts legibility.

#### Pairs with

Serif display, sans UI, Warm-tinted depth

Measured on: Jog, Melius, TypeSafe AI.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="color-indexed-sections" kind="technique" facet="color" status="established" languages="research-index,retro-machine-pop" -->
### Color-indexed sections

Each section gets its own color as wayfinding, either a chip next to the section number or a full-bleed band, so color tells you where you are.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
section:nth-of-type(1) { --index: #F3B3F6; }  section:nth-of-type(2) { --index: #F5D547; }
section:nth-of-type(3) { --index: #F05A2A; }  /* … */
.section-num { background: var(--index); font-family: var(--font-pixel); }
/* band variant */ section.band { background: var(--index); }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; gap: 0; padding: 0; }
.sec { display: grid; grid-template-columns: 64px 1fr auto; align-items: center; gap: 18px; padding: 16px 28px; border-top: 1px solid #111; }
.n { font: 500 15px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; padding: 8px 0; text-align: center; background: var(--x); }
h3 { margin: 0; font-size: 22px; font-weight: 400; }
.band { background: var(--x); }
.band .n { background: #111; color: var(--x); }
</style>
<div class="s">
<div class="sec" style="--x:#FAB3F6"><span class="n">01</span><h3>About the lab</h3><span class="cap">chip</span></div>
<div class="sec" style="--x:#F5D547"><span class="n">02</span><h3>What we measure</h3><span class="cap">chip</span></div>
<div class="sec band" style="--x:#F05A2A"><span class="n">03</span><h3>Open problems</h3><span class="cap">band</span></div>
<div class="sec" style="--x:#8FD3FF"><span class="n">04</span><h3>Join us</h3><span class="cap">chip</span></div></div>
```

#### Use when

Long single pages with distinct chapters.

#### Avoid when

Short pages; with fewer than 4 sections it just looks random.

#### Pairs with

Numbered sections, Hard edges, flat depth

Measured on: Preference Model, TypeSafe AI, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="highlighter-marks" kind="technique" facet="color" status="established" languages="research-index" -->
### Highlighter marks

Key words get a flat background block like a marker pen, so emphasis comes from color behind the text instead of weight or size.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
mark, .hl { background: var(--highlight); color: inherit; padding: 0 0.15em; }
/* animated variant: grow the mark left to right */
.hl { background: linear-gradient(var(--highlight), var(--highlight)) no-repeat 0 0 / 0% 100%;
      transition: background-size 260ms ease-out; }
.hl.in { background-size: 100% 100%; }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; align-content: center; gap: 18px; }
p { font-size: 30px; line-height: 1.25; letter-spacing: -0.01em; margin: 0; max-width: 22ch; }
.hl { background: linear-gradient(#BCF891, #BCF891) no-repeat 0 0 / 0% 100%; padding: 0 .1em; animation: grow 260ms ease-out forwards; animation-delay: var(--d); }
@keyframes grow { to { background-size: 100% 100%; } }
.label { justify-self: start; background: #BCF891; font: 500 12px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; padding: 5px 7px; letter-spacing: .05em; }
</style>
<div class="s"><span class="label">02 / METHOD</span>
<p>An <span class="hl" style="--d:400ms">applied research lab</span> for teams that would rather <span class="hl" style="--d:900ms">measure than guess</span>.</p>
<span class="cap">one mark per screen · flat block behind the words · grows in 260ms ease-out</span></div>
```

#### Use when

Pointing at the one phrase that carries the pitch; labeling sections.

#### Avoid when

Long body copy. More than one mark per screen dilutes it.

#### Pairs with

Accent rationing, Numbered sections, Narrated proof

Measured on: Hone, Jog, Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="warm-tinted-depth" kind="technique" facet="color" status="established" languages="humane-editorial" -->
### Warm-tinted depth

Shadows and lines are tinted with the ground color's hue instead of gray, so elevation feels like paper lifting, not plastic.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--shadow-soft: 0 1px 2px rgba(52, 40, 18, .07), 0 0 0 1px rgb(191, 176, 150);
--shadow-lift: 0 30px 80px -30px rgba(20, 14, 4, .55);
--line: 1px solid #D9CDB9;
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F4EBDA; display: grid; grid-template-columns: 1fr 1fr; gap: 36px; align-items: center; padding: 40px; color: #2A2119; }
.c { background: #FAF5EC; border-radius: 10px; padding: 22px; min-height: 180px; display: grid; align-content: space-between; }
.gray { box-shadow: 0 1px 2px rgba(0,0,0,.12), 0 0 0 1px #c9c9c9, 0 30px 80px -30px rgba(0,0,0,.55); }
.warm { box-shadow: 0 1px 2px rgba(52,40,18,.07), 0 0 0 1px rgb(191,176,150), 0 30px 80px -30px rgba(20,14,4,.55); }
h4 { margin: 0; font: 500 22px/1.1 "Iowan Old Style", "Charter", Georgia, serif; }
</style>
<div class="s"><div class="c gray"><h4>Gray shadow</h4><span class="cap">rgba(0,0,0) · reads as plastic</span></div>
<div class="c warm"><h4>Warm-tinted</h4><span class="cap">rgba(52,40,18) · paper lifting</span></div></div>
```

#### Use when

Any warm or off-white ground.

#### Avoid when

Pure white or cool grays, where tinted shadows look dirty.

#### Pairs with

Analog grain, Serif display, sans UI

Measured on: Jog, Handwired.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="announcement-bar" kind="technique" facet="layout" status="established" -->
### Announcement bar

A thin full-width strip above the nav carrying the latest milestone (in this library, always a funding round) with one link.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
<aside class="announce">Raises $XM led by Y <a>Read more</a></aside>
.announce { font-size: 13px; padding: 8px; background: var(--ground-alt) or var(--glow); text-align: center; }
```

#### Variants

- TypeSafe turns the bar into a joke inside a retro dialog box, so the convention becomes part of the voice.

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { padding: 0; background: #fff; color: #111; }
.ann { background: #FFF78B; text-align: center; font-size: 13px; padding: 8px; }
.ann u { text-underline-offset: 2px; }
nav { display: flex; justify-content: space-between; padding: 14px 28px; border-bottom: 1px solid #eee; font-size: 14px; }
nav span { color: #666; margin-left: 18px; }
.hero { padding: 50px 28px; font-size: 40px; font-weight: 600; letter-spacing: -0.02em; line-height: 1.05; max-width: 18ch; }
</style>
<div class="s"><div class="ann">Fieldnote raises a Series A to build open evals · <u>Read more</u></div>
<nav><b>Fieldnote</b><div><span>Product</span><span>Research</span><span>Pricing</span></div></nav>
<div class="hero">The newest fact about you goes above everything else.</div></div>
```

#### Use when

Time-bound news.

#### Avoid when

Leaving it up after the news goes stale.

#### Pairs with

Retro machine pop

Measured on: Hone, Melius, TypeSafe AI.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="artifact-as-hero" kind="technique" facet="layout" status="established" languages="humane-editorial,cinematic-media-canvas" -->
### Artifact as hero

The hero shows the product's literal interaction (the prompt box you type into, the one-line diff you'd make, the code and what it compiles into), not a screenshot or an abstraction.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
/* prompt variant */ <form class="hero-prompt"><textarea placeholder="Describe what you want…"></textarea></form>
/* diff variant */ <pre class="diff"><del>- runs-on: ubuntu-latest</del><ins>+ runs-on: newtool</ins></pre>
/* transform variant */ <pre>input code</pre> → <pre>what it becomes</pre> → <svg class="diagram">…the same logic, drawn…</svg>
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #FBFAF7; color: #1d1b18; display: grid; grid-template-columns: 1fr 1.1fr; gap: 28px; align-items: center; }
h1 { font-size: 34px; font-weight: 600; letter-spacing: -0.02em; line-height: 1.05; margin: 0 0 10px; }
p { margin: 0; color: #555; font-size: 14px; }
.code { background: #1E1A16; color: #e9e2d6; border-radius: 8px; padding: 16px; font: 13px/1.8 ui-monospace, "SF Mono", Menlo, Consolas, monospace; }
.del { color: #e58a7a; } .ins { color: #9fd3a3; } .c { color: #8a8178; }
.prompt { margin-top: 12px; border: 1px solid #d8d4cc; border-radius: 10px; background: #fff; padding: 12px 14px; font-size: 14px; color: #888; }
</style>
<div class="s"><div><h1>Change one line. That's the whole migration.</h1><p>The hero is the thing you'd actually do, not a picture of the product.</p></div>
<div><div class="code"><div class="c"># deploy.yml</div><div class="del">− runner: legacy-large</div><div class="ins">+ runner: fieldnote</div></div>
<div class="prompt">Describe what you want to build…</div></div></div>
```

#### Use when

When adopting the product is literally one action.

#### Avoid when

Complex products whose first step isn't representative.

#### Pairs with

Narrated proof, Benchmark as headline

Measured on: Jog, Clay (app home), Melius, Handwired.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="benchmark-as-headline" kind="technique" facet="layout" status="established" languages="retro-machine-pop" -->
### Benchmark as headline

The claim is a number against named competitors, set huge and backed by a chart right below it.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
<h2 class="mega">80% less than X.</h2>
<figure class="bars">…one bar per competitor, yours highlighted with the accent…</figure>
<small>Method and date of the comparison</small>
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; }
h2 { font-size: 54px; font-weight: 600; letter-spacing: -0.03em; line-height: 1; margin: 0 0 20px; }
.bars { display: grid; gap: 8px; }
.b { display: grid; grid-template-columns: 110px 1fr 60px; align-items: center; gap: 10px; font-size: 13px; }
.b i { height: 16px; background: #cfcfcf; width: 0; animation: grow 900ms cubic-bezier(0.2,0.8,0.2,1) forwards; animation-delay: calc(var(--i) * 70ms + 200ms); }
.b.us i { background: #F04E23; } .b span:last-child { font-family: ui-monospace, "SF Mono", Menlo, Consolas, monospace; text-align: right; }
@keyframes grow { to { width: var(--w); } }
small { display: block; margin-top: 14px; color: #888; font-size: 11px; }
</style>
<div class="s"><h2>4× cheaper than Brand A.</h2><div class="bars">
<div class="b us"><span>Fieldnote</span><i style="--w:22%;--i:0"></i><span>$0.003</span></div>
<div class="b"><span>Brand A</span><i style="--w:88%;--i:1"></i><span>$0.012</span></div>
<div class="b"><span>Brand B</span><i style="--w:70%;--i:2"></i><span>$0.009</span></div></div>
<small>Price per runner-minute, list prices on 2026-10-01. Method on the pricing page.</small></div>
```

#### Use when

Products with a measurable edge.

#### Avoid when

When the number needs heavy caveats; the footnote has to be honest.

#### Pairs with

Accent rationing, Oversized tight display

Measured on: Jog, TypeSafe AI.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="numbered-sections" kind="technique" facet="layout" status="established" languages="research-index" -->
### Numbered sections

Sections numbered 01, 02 … like chapters, so a long page reads as an ordered argument and not a scroll of features.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
<section><span class="num">01</span><span class="label">ABOUT</span><h2>…</h2></section>
.num { font-variant-numeric: tabular-nums; }   /* pair with color-indexed chips or a highlighter */
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; gap: 0; }
.r { display: grid; grid-template-columns: 70px 120px 1fr; align-items: baseline; gap: 16px; padding: 16px 0; border-top: 1px solid #111; }
.num { font-size: 34px; font-variant-numeric: tabular-nums; letter-spacing: -0.02em; }
.lab { font: 500 11px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .06em; }
h3 { margin: 0; font-size: 20px; font-weight: 400; }
</style>
<div class="s"><div class="r"><span class="num">01</span><span class="lab">PROBLEM</span><h3>Models are good. Outcomes aren't.</h3></div>
<div class="r"><span class="num">02</span><span class="lab">APPROACH</span><h3>Engines that onboard themselves.</h3></div>
<div class="r"><span class="num">03</span><span class="lab">PROOF</span><h3>Three deployments, measured.</h3></div>
<div class="r"><span class="num">04</span><span class="lab">NEXT</span><h3>Where it breaks, and what we're doing about it.</h3></div></div>
```

#### Use when

Explaining a thesis or a process in order.

#### Avoid when

Pages without a real sequence; numbers promise an argument.

#### Pairs with

Color-indexed sections, Machine-voice labels, Ruled structure

Measured on: Preference Model, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="object-carousel-hero" kind="technique" facet="layout" status="established" languages="humane-editorial,cinematic-media-canvas" -->
### Object carousel hero

The hero is a row of objects or media with the focused one centered and full, and its neighbors scaled down and faded.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.item { transition: transform 500ms cubic-bezier(0.34, 1.56, 0.64, 1), opacity 500ms ease; }
.item:not(.focus) { transform: scale(.55); opacity: .55; }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #121212; display: grid; place-items: center; gap: 16px; }
.row { display: flex; align-items: center; gap: 4px; }
.it { width: 120px; height: 150px; border-radius: 28px; background: var(--g); transform: scale(.55); opacity: .55; transition: transform 500ms cubic-bezier(0.34,1.56,0.64,1), opacity 500ms ease; animation: pop 600ms cubic-bezier(0.34,1.56,0.64,1) both; animation-delay: calc(var(--i) * 80ms); }
.it.focus, .it:hover { transform: scale(1); opacity: 1; }
.row:hover .it.focus:not(:hover) { transform: scale(.55); opacity: .55; }
@keyframes pop { from { transform: scale(.2); opacity: 0; } }
</style>
<div class="s"><div class="row">
<i class="it" style="--i:0;--g:radial-gradient(circle at 35% 30%,#fff,#b9d7ff 45%,#6f8fd8)"></i>
<i class="it" style="--i:1;--g:radial-gradient(circle at 35% 30%,#fff,#ffd2e8 45%,#d77fb0)"></i>
<i class="it focus" style="--i:2;--g:radial-gradient(circle at 35% 30%,#fff,#d6f5c2 45%,#79c26a)"></i>
<i class="it" style="--i:3;--g:radial-gradient(circle at 35% 30%,#fff,#ffe9b0 45%,#e2a948)"></i>
<i class="it" style="--i:4;--g:radial-gradient(circle at 35% 30%,#fff,#e4d6ff 45%,#9a7ddc)"></i></div>
<span class="cap">hover an object to focus it · neighbors at scale 0.55, back-out spring</span></div>
```

#### Use when

Physical products, media outputs: things worth looking at.

#### Avoid when

SaaS without visual output.

#### Pairs with

Springs for characters only, Ambient breathing glow

Measured on: Era, Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="ruled-structure" kind="technique" facet="layout" status="established" languages="research-index" -->
### Ruled structure

Hairline rules divide columns, list rows and FAQ entries, so the grid is visible like a printed table.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.row + .row { border-top: 1px solid var(--rule); }
.cols > * { border-top: 1px solid var(--ink); padding-top: 24px; }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; }
.cols { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; margin-bottom: 22px; }
.cols > div { border-top: 1px solid #111; padding-top: 12px; font-size: 13px; color: #444; }
.cols b { display: block; color: #111; font-weight: 500; font-size: 15px; margin-bottom: 4px; }
.row { display: flex; justify-content: space-between; padding: 11px 0; font-size: 14px; }
.row + .row { border-top: 1px solid #d6d6d6; }
.row span:last-child { font-family: ui-monospace, "SF Mono", Menlo, Consolas, monospace; font-size: 12px; color: #666; }
</style>
<div class="s"><div class="cols"><div><b>Research</b>Long-horizon evaluation.</div><div><b>Product</b>Environments as a service.</div><div><b>Policy</b>Public methods, public errors.</div></div>
<div class="row"><span>How is a run priced?</span><span>+</span></div><div class="row"><span>Can we bring our own models?</span><span>+</span></div><div class="row"><span>Where does data live?</span><span>+</span></div></div>
```

#### Use when

FAQ, pricing tables, three-up value props.

#### Avoid when

Busy imagery-led layouts, where the rules fight the pictures.

#### Pairs with

Numbered sections, Hard edges, flat depth

Measured on: Preference Model, Hone, Jog.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="ambient-breathing-glow" kind="technique" facet="motion" status="established" languages="humane-editorial,cinematic-media-canvas" -->
### Ambient breathing glow

A slow loop (3.5–5s) gently pulsing opacity and scale on a glow behind the thing that matters: the hero object, or the plan you want chosen.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
@keyframes breathe { 0%, 100% { opacity: .22; transform: scale(1); } 50% { opacity: .4; transform: scale(1.03); } }
.glow { animation: breathe 4.2s ease-in-out infinite; }
@media (prefers-reduced-motion: reduce) { .glow { animation: none; } }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #0E0E0E; color: #FAFAFA; display: grid; place-items: center; }
.wrap { position: relative; width: 240px; height: 200px; display: grid; place-items: center; }
.glow { position: absolute; inset: 0; border-radius: 24px; background: radial-gradient(closest-side, #F04E23, transparent); filter: blur(18px); opacity: .22; animation: breathe 4.2s ease-in-out infinite; }
.card { position: relative; width: 200px; height: 150px; border-radius: 12px; background: #202020; border: 1px solid #F04E23; display: grid; place-items: center; font-size: 15px; }
@keyframes breathe { 0%, 100% { opacity: .22; transform: scale(1); } 50% { opacity: .45; transform: scale(1.04); } }
.cap { position: absolute; bottom: 18px; }
</style>
<div class="s"><div class="wrap"><div class="glow"></div><div class="card">The plan you want chosen</div></div><span class="cap">4.2s ease-in-out · infinite</span></div>
```

#### Use when

Drawing attention to one thing without moving it.

#### Avoid when

More than one glow per screen.

#### Pairs with

Object carousel hero, Accent rationing

Measured on: Era, Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="cinematic-entrance" kind="technique" facet="motion" status="emerging" languages="cinematic-media-canvas" -->
### Cinematic entrance

The hero arrives slowly (about 1.5s), scaling down from 1.2 while it fades in on a long expo-out, like a camera settling.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.hero-in { animation: settle 1500ms cubic-bezier(0.16, 1, 0.3, 1) both; }
@keyframes settle { from { opacity: 0; transform: scale(1.2); } }
.hero-sub { animation-delay: 200ms } .hero-proof { animation-delay: 500ms }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #0E0E0E; color: #FAFAFA; display: grid; place-items: center; text-align: center; align-content: center; gap: 10px; }
h1 { font: 400 52px/1 "Iowan Old Style", "Charter", Georgia, serif; letter-spacing: -0.02em; margin: 0; animation: settle 1500ms cubic-bezier(0.16,1,0.3,1) both; }
.sub { color: #aaa; animation: settle 1500ms cubic-bezier(0.16,1,0.3,1) 200ms both; }
.proof { color: #666; font-size: 12px; animation: settle 1200ms cubic-bezier(0.16,1,0.3,1) 500ms both; }
@keyframes settle { from { opacity: 0; transform: scale(1.2); } }
</style>
<div class="s"><h1>Make what you can picture</h1><div class="sub">The camera settles. The page begins.</div><div class="proof">1500ms expo-out · from scale 1.2 · +200ms · +500ms</div></div>
```

#### Use when

Media-first heroes, once per page.

#### Avoid when

Anything after the hero; slow entrances make scrolling feel sluggish.

#### Pairs with

Develop reveal, Inertial smooth scroll

Measured on: Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="develop-reveal" kind="technique" facet="motion" status="emerging" languages="cinematic-media-canvas" -->
### Develop reveal

Images appear overexposed and settle to normal, like a photo developing, staggered across a grid.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
@keyframes develop { from { filter: brightness(1000%) sepia(20%); } to { filter: brightness(100%) sepia(0%); } }
.tile.in { animation: develop 750ms cubic-bezier(0, 0.55, 0.45, 1) both; }  /* add .in as each tile enters the viewport */
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #0E0E0E; display: grid; grid-template-columns: repeat(3, 1fr); gap: 8px; padding: 18px; }
i { display: block; height: 146px; border-radius: 4px; background: var(--g); animation: develop 750ms cubic-bezier(0,0.55,0.45,1) both; animation-delay: calc(var(--i) * 240ms + 200ms); }
@keyframes develop { from { filter: brightness(1000%) sepia(20%); } to { filter: brightness(100%) sepia(0%); } }
</style>
<div class="s"><i style="--i:0;--g:linear-gradient(160deg,#2d4a63,#c08a5a)"></i><i style="--i:1;--g:linear-gradient(200deg,#5b2a3e,#e0b36a)"></i><i style="--i:2;--g:linear-gradient(170deg,#163a2c,#9fd0a6)"></i>
<i style="--i:3;--g:linear-gradient(190deg,#33244f,#d78bd0)"></i><i style="--i:4;--g:linear-gradient(150deg,#4a3a20,#f0d080)"></i><i style="--i:5;--g:linear-gradient(210deg,#1f3b4d,#7fc3d9)"></i></div>
```

#### Use when

Galleries of generated or photographic output.

#### Avoid when

UI cards or text; the flash only works on imagery.

#### Pairs with

Cinematic entrance, Object carousel hero

Measured on: Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="inertial-smooth-scroll" kind="technique" facet="motion" status="established" languages="cinematic-media-canvas" -->
### Inertial smooth scroll

Scroll is taken over by a smoothing library, so the page glides with momentum. It sets the pacing for every other scroll effect.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
// Lenis (or similar), tuned gently; honor reduced motion
if (!matchMedia('(prefers-reduced-motion: reduce)').matches) new Lenis({ lerp: 0.1 });
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; align-content: center; gap: 26px; }
.lane { position: relative; height: 40px; border-bottom: 1px dashed #ccc; }
.lane .l { position: absolute; left: 0; top: -4px; }
.dot { position: absolute; top: 14px; left: 0; width: 22px; height: 22px; border-radius: 50%; background: #111; }
.native .dot { animation: steps 2.4s steps(6, end) infinite; }
.lerp .dot { background: #3BD966; animation: glide 2.4s cubic-bezier(0.16,1,0.3,1) infinite; }
@keyframes steps { to { transform: translateX(560px); } }
@keyframes glide { to { transform: translateX(560px); } }
</style>
<div class="s"><div class="lane native"><span class="cap l">native wheel · jumps per notch</span><i class="dot"></i></div>
<div class="lane lerp"><span class="cap l">smoothed (lerp 0.1) · glides with momentum</span><i class="dot"></i></div></div>
```

#### Use when

Scroll-choreographed pages with pinned or scrubbed sections.

#### Avoid when

Docs and long reading pages; hijacked scroll annoys readers.

#### Pairs with

Cinematic entrance, Soft rise reveal

Measured on: Hone, Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="motion-timing-tiers" kind="technique" facet="motion" status="established" -->
### Four-tier motion timing

The 103 distinct durations measured across the eight clips cluster into four bands: 29 under 300ms, 41 between 300 and 800ms, 20 between 800 and 1600ms, 13 above. The bands blur at their edges, but picking a value from a band and keeping to it is most of a motion system.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--t-micro:    120–300ms   ease / material standard / cubic-out   (hover, toggles, small UI)
--t-reveal:   320–750ms   quint-out / cubic-out                 (scroll reveals, characters)
--t-entrance: 800–1500ms  expo-out / custom out                 (hero, data bars)
--t-ambient:  2–6s        linear / ease-in-out, infinite        (glows, grain, shimmer)
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; align-content: center; gap: 14px; }
.t { display: grid; grid-template-columns: 150px 1fr; align-items: center; gap: 12px; }
.track { position: relative; height: 26px; border-bottom: 1px solid #e3e3e3; }
.track i { position: absolute; left: 0; top: 4px; width: 18px; height: 18px; border-radius: 3px; background: #111; animation: go var(--d) var(--e) infinite alternate; }
@keyframes go { to { transform: translateX(480px); } }
.t b { display: block; font-weight: 500; } .t span { font: 11px ui-monospace, "SF Mono", Menlo, Consolas, monospace; color: #777; }
</style>
<div class="s">
<div class="t"><div><b>Micro</b><span>200ms · cubic-out</span></div><div class="track"><i style="--d:200ms;--e:cubic-bezier(0.33,1,0.68,1)"></i></div></div>
<div class="t"><div><b>Reveal</b><span>550ms · quint-out</span></div><div class="track"><i style="--d:550ms;--e:cubic-bezier(0.22,1,0.36,1)"></i></div></div>
<div class="t"><div><b>Entrance</b><span>1500ms · expo-out</span></div><div class="track"><i style="--d:1500ms;--e:cubic-bezier(0.16,1,0.3,1)"></i></div></div>
<div class="t"><div><b>Ambient</b><span>4.2s · ease-in-out</span></div><div class="track"><i style="--d:4200ms;--e:ease-in-out"></i></div></div></div>
```

#### Use when

Starting any motion spec.

#### Avoid when

Mixing tiers: a 600ms hover or a 200ms hero both feel wrong.

#### Pairs with

Soft rise reveal, Springs for characters only, Ambient breathing glow

Measured on: Jog, Clay (app home), Hone, Era, Melius.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="narrated-proof" kind="technique" facet="motion" status="emerging" languages="humane-editorial" -->
### Narrated proof

The hero artifact acts out the claim in sequence: strike the old value, type the new one, blink a caret. About 1.3s from first move to caret.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
del { animation: strike 260ms ease-out 700ms both; }   /* scaleX(0) → 1 on a line */
ins .ch { animation: type 1ms linear both; animation-delay: calc(1150ms + var(--i) * 100ms); }  /* visibility */
.caret { animation: caret 900ms linear 1250ms infinite; }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F4EBDA; display: grid; place-items: center; }
.f { width: 420px; background: #1F1814; color: #e9e2d6; border-radius: 10px; padding: 18px 20px; font: 15px/1.9 ui-monospace, "SF Mono", Menlo, Consolas, monospace; box-shadow: 0 30px 80px -30px rgba(20,14,4,.55); }
.name { color: #8a8178; font-size: 12px; }
.del { color: #e58a7a; position: relative; }
.del s { text-decoration: none; position: relative; }
.del s::after { content: ""; position: absolute; left: 0; right: 0; top: 52%; height: 2px; background: #e58a7a; transform: scaleX(0); transform-origin: left; animation: strike 260ms ease-out 700ms forwards; }
@keyframes strike { to { transform: scaleX(1); } }
.ins { color: #9fd3a3; }
.ch { visibility: hidden; animation: type 1ms linear forwards; animation-delay: calc(1150ms + var(--i) * 100ms); }
@keyframes type { to { visibility: visible; } }
.caret { display: inline-block; width: 8px; height: 17px; background: #9fd3a3; vertical-align: -3px; opacity: 0; animation: caret 900ms linear 1250ms infinite; }
@keyframes caret { 0%, 45% { opacity: 1; } 55%, 100% { opacity: 0; } }
</style>
<div class="s"><div class="f"><div class="name">settings.yml</div><div class="del">− plan: <s>legacy</s></div>
<div class="ins">+ plan: <span class="ch" style="--i:0">f</span><span class="ch" style="--i:1">i</span><span class="ch" style="--i:2">e</span><span class="ch" style="--i:3">l</span><span class="ch" style="--i:4">d</span><span class="caret"></span></div></div></div>
```

#### Use when

When the pitch fits in one before/after.

#### Avoid when

Multi-step stories; past about 2s, people stop watching.

#### Pairs with

Artifact as hero, Highlighter marks

Measured on: Jog.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="soft-rise-reveal" kind="technique" facet="motion" status="established" languages="humane-editorial" -->
### Soft rise reveal

Content fades in while rising a short distance, with a strong ease-out and a small stagger. It's the most common motion in the library.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.reveal { opacity: 0; transform: translateY(16px); }
.reveal.in { opacity: 1; transform: none;
  transition: opacity 600ms cubic-bezier(0.22, 1, 0.36, 1), transform 600ms cubic-bezier(0.22, 1, 0.36, 1);
  transition-delay: calc(var(--i) * 60ms); }
@media (prefers-reduced-motion: reduce) { .reveal { opacity: 1; transform: none; transition: none; } }
```

#### Variants

- Text: 12–18px rise, 50–70ms stagger.
- Large tiles: 16px rise plus scale 0.98, triggered tile by tile as they scroll in (Melius).

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #121212; display: grid; align-content: center; gap: 10px; }
p { margin: 0; font: 400 26px/1.25 "Iowan Old Style", "Charter", Georgia, serif; opacity: 0; transform: translateY(16px); animation: rise 600ms cubic-bezier(0.22,1,0.36,1) forwards; animation-delay: calc(var(--i) * 60ms + 200ms); }
@keyframes rise { to { opacity: 1; transform: none; } }
</style>
<div class="s"><p style="--i:0">Each line arrives a beat after the last.</p><p style="--i:1">It rises sixteen pixels while it fades in.</p><p style="--i:2">The ease-out is strong, so it settles softly.</p><p style="--i:3">Sixty milliseconds apart. Then nothing moves.</p>
<span class="cap" style="margin-top:10px">600ms quint-out · 16px rise · 60ms stagger</span></div>
```

#### Use when

Default reveal for text and cards.

#### Avoid when

Everything at once; when every element rises, nothing does.

#### Pairs with

Serif display, sans UI, Springs for characters only

Measured on: Era, Melius, Jog, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="spring-for-characters" kind="technique" facet="motion" status="established" languages="research-index,humane-editorial" -->
### Springs for characters only

An overshooting spring (back-out) is reserved for characters and objects: mascots, products, carousel items. Text and UI never spring.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--spring: cubic-bezier(0.34, 1.56, 0.64, 1);
.mascot, .object { transition: transform 420ms var(--spring); }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; align-content: center; gap: 22px; }
.lane { position: relative; height: 56px; border-bottom: 1px dashed #ccc; }
.lane .l { position: absolute; left: 0; top: -2px; }
.ball { position: absolute; left: 0; top: 14px; width: 40px; height: 40px; border-radius: 50%; animation: go 900ms both infinite alternate; animation-delay: 300ms; }
.spring .ball { background: #3BD966; animation-timing-function: cubic-bezier(0.34,1.56,0.64,1); }
.ease .ball { background: #bbb; animation-timing-function: cubic-bezier(0.33,1,0.68,1); }
@keyframes go { from { transform: translateX(0); } 60%, to { transform: translateX(560px); } }
</style>
<div class="s"><div class="lane spring"><span class="cap l">back-out spring · characters, objects</span><i class="ball"></i></div>
<div class="lane ease"><span class="cap l">cubic-out · everything else</span><i class="ball"></i></div></div>
```

#### Use when

Giving personality to one element class.

#### Avoid when

Body text, buttons or layout shifts; bouncy UI reads as a toy.

#### Pairs with

Object carousel hero, Soft rise reveal

Measured on: Hone, Era.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="static-by-design" kind="technique" facet="motion" status="established" languages="research-index,retro-machine-pop" -->
### Static by design

Little or no scroll motion, as a deliberate choice: content is simply there. Motion is limited to hover color and loaders.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
/* the whole motion system: */
a, button, .row { transition: color 300ms cubic-bezier(0.4, 0, 0.2, 1), background-color 300ms cubic-bezier(0.4, 0, 0.2, 1); }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; }
.r { display: flex; justify-content: space-between; padding: 14px 10px; border-top: 1px solid #ddd; font-size: 17px; transition: color 300ms cubic-bezier(0.4,0,0.2,1), background-color 300ms cubic-bezier(0.4,0,0.2,1); cursor: default; }
.r:hover { background: #000; color: #fff; }
.r span:last-child { font: 12px ui-monospace, "SF Mono", Menlo, Consolas, monospace; opacity: .6; }
</style>
<div class="s"><span class="cap">nothing moves on load or scroll · hover a row</span>
<div class="r" style="margin-top:12px"><span>Research</span><span>06 papers</span></div><div class="r"><span>Environments</span><span>14 suites</span></div><div class="r"><span>Team</span><span>11 people</span></div><div class="r"><span>Careers</span><span>3 roles</span></div></div>
```

#### Use when

Loud visual systems (motion would be too much), austere ones (motion would be off-voice), or pages where the artifact is already the show.

#### Avoid when

Pages whose story needs pacing.

#### Pairs with

Hard edges, flat depth, Oversized tight display

Measured on: Preference Model, TypeSafe AI, Handwired.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="hard-edges-flat-depth" kind="technique" facet="shape" status="established" languages="research-index,retro-machine-pop" -->
### Hard edges, flat depth

Square corners (0–2px) and no shadows. Hierarchy comes from color bands and rules, not elevation.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--radius: 0;   /* or 2px */
--shadow: none;
.card { border: 1px solid var(--rule-color); background: var(--ground-alt); }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #E8E8E8; display: grid; grid-template-columns: repeat(3, 1fr); gap: 0; padding: 0; color: #000; }
.c { padding: 24px; min-height: 340px; display: grid; align-content: space-between; border-right: 1px solid #000; }
.c:nth-child(2) { background: #fff; } .c:nth-child(3) { background: #000; color: #fff; border: 0; }
h4 { margin: 0; font-size: 22px; font-weight: 400; }
.btn { justify-self: start; border: 1px solid currentColor; padding: 8px 12px; font-size: 13px; }
</style>
<div class="s"><div class="c"><h4>Band one</h4><span class="cap">no radius · no shadow</span><span class="btn">Read</span></div>
<div class="c"><h4>Band two</h4><span class="cap">separation from color and rules</span><span class="btn">Read</span></div>
<div class="c"><h4>Band three</h4><span class="cap">depth = contrast</span><span class="btn">Read</span></div></div>
```

#### Use when

Rigor-signaling brands; dense information.

#### Avoid when

Friendly consumer products; it can read severe.

#### Pairs with

Ruled structure, Color-indexed sections

Measured on: Preference Model, TypeSafe AI, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="machine-voice-labels" kind="technique" facet="type" status="established" languages="research-index,retro-machine-pop" -->
### Machine-voice labels

A mono or pixel face as a secondary voice for labels, metadata, numbers and code. It's the machine talking, next to the human headline.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.label { font: 500 12px/1.4 var(--font-mono); text-transform: uppercase; letter-spacing: .04em; }
/* Preference Model variant: labels as identifiers → OUR_TEAM, JOIN_US */
.num { font-family: var(--font-pixel); }   /* section numerals */
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #111; display: grid; align-content: center; gap: 14px; }
.lab { font: 500 12px/1.4 ui-monospace, "SF Mono", Menlo, Consolas, monospace; text-transform: uppercase; letter-spacing: .04em; color: #555; }
h2 { font-size: 36px; font-weight: 500; letter-spacing: -0.015em; margin: 0; }
.row { display: flex; gap: 22px; font: 13px/1.4 ui-monospace, "SF Mono", Menlo, Consolas, monospace; color: #333; border-top: 1px solid #ddd; padding-top: 12px; }
.row b { font-weight: 500; color: #111; }
</style>
<div class="s"><span class="lab">OUR_TEAM · 04</span><h2>People who write the evals first.</h2>
<div class="row"><span>RUN_ID <b>7f3a-22</b></span><span>LATENCY <b>184ms</b></span><span>UPDATED <b>2026-10-15</b></span></div>
<span class="cap">human headline · mono for ids, numbers, metadata</span></div>
```

#### Use when

AI and dev products: anything where showing the machinery builds trust.

#### Avoid when

As body text past a sentence or two (TypeSafe's 12px mono body is the edge case).

#### Pairs with

Numbered sections, One family, scale does the work, Serif display, sans UI

Measured on: Preference Model, TypeSafe AI, Jog, Melius, Handwired.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="one-family-scale-hierarchy" kind="technique" facet="type" status="established" languages="research-index" -->
### One family, scale does the work

A single grotesk family for every role, with hierarchy made only through size and space. Big steps, few weights.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
--font: "<one grotesk>";  font-weight: 400 (500 for UI only)
--scale: 13 16 18 28 48 67 120;   /* ≈1.5× steps; top step is 7.5× body */
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #fff; color: #000; font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; font-weight: 400; display: grid; grid-template-columns: auto 1fr; gap: 6px 18px; align-items: baseline; padding-right: 0; }
.k { font: 11px/1 ui-monospace, "SF Mono", Menlo, Consolas, monospace; color: #888; text-align: right; }
.t { white-space: nowrap; letter-spacing: -0.01em; line-height: 1; }
</style>
<div class="s">
<span class="k">13</span><span class="t" style="font-size:13px">Captions and metadata</span>
<span class="k">16</span><span class="t" style="font-size:16px">Body copy, set plainly</span>
<span class="k">28</span><span class="t" style="font-size:28px">Section heads</span>
<span class="k">48</span><span class="t" style="font-size:48px">Page statements</span>
<span class="k">120</span><span class="t" style="font-size:120px">Scale</span></div>
```

#### Use when

Systematic, research-flavored brands; it's cheap to keep consistent.

#### Avoid when

When the family is generic; with one face, the face *is* the brand.

#### Pairs with

Oversized tight display, Numbered sections

Measured on: Hone, Preference Model.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="oversized-tight-display" kind="technique" facet="type" status="established" languages="retro-machine-pop" -->
### Oversized tight display

Display type far beyond comfortable size (120–150px) with leading below 1, so words become shapes.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
.mega { font-size: clamp(64px, 10vw, 150px); line-height: .8–.9; letter-spacing: -0.01em; text-wrap: balance; }
```

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #F386A1; color: #1E1E1E; padding: 22px 28px; }
.mega { font: 800 128px/.8 "Helvetica Neue", Helvetica, Arial, sans-serif; letter-spacing: -0.02em; margin: 0; }
.cap { margin-top: 18px; display: block; }
</style>
<div class="s"><p class="mega">Words As<br>Shapes</p><span class="cap">128px · line-height 0.8 · title case</span></div>
```

#### Use when

One statement per page that should be remembered.

#### Avoid when

More than once per page, or for anything longer than about 8 words.

#### Pairs with

One family, scale does the work, Static by design

Measured on: TypeSafe AI, Hone.
<!-- /artspo:pattern -->

<!-- artspo:pattern id="serif-display-sans-ui" kind="technique" facet="type" status="established" languages="humane-editorial,cinematic-media-canvas" -->
### Serif display, sans UI

Headlines in a text serif with tight tracking; everything you interact with in a neutral sans. The serif carries the voice, the sans does the work.

#### Recipe

_Rebuilt from measurements. A starting point, not any site's code._

```css
h1, h2 { font-family: var(--font-serif); font-weight: 400–500; letter-spacing: -0.02em; line-height: 1.0–1.04; }
body, button, input { font-family: var(--font-sans); }
```

#### Variants

- Era goes further and sets body copy in the serif too, with positive tracking (+0.043em) on the display.

#### Specimen

_A generic demo of the move, for reference: HTML and CSS, no scripts._

```html
<style>
:host { display: block; }
.s { box-sizing: border-box; min-height: 340px; padding: 28px; font: 15px/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif; position: relative; overflow: hidden; }
.s *, .s *::before, .s *::after { box-sizing: border-box; }
.cap { font: 500 11px/1.3 ui-monospace, "SF Mono", Menlo, Consolas, monospace; letter-spacing: .04em; text-transform: uppercase; opacity: .6; }
@media (prefers-reduced-motion: reduce) { .s *, .s *::before, .s *::after { animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; } }
.s { background: #FBFAF7; color: #1d1b18; display: grid; align-content: center; gap: 18px; }
h1 { font: 500 50px/1.02 "Iowan Old Style", "Charter", Georgia, serif; letter-spacing: -0.02em; margin: 0; max-width: 16ch; }
.ui { display: flex; gap: 10px; font-family: "Helvetica Neue", Helvetica, Arial, sans-serif; }
input { font: inherit; font-size: 14px; padding: 10px 12px; border: 1px solid #d8d4cc; border-radius: 6px; width: 260px; background: #fff; }
button { font: 500 14px "Helvetica Neue", Helvetica, Arial, sans-serif; padding: 10px 16px; border: 0; border-radius: 6px; background: #1d1b18; color: #fff; }
</style>
<div class="s"><span class="cap">serif carries the voice</span><h1>Software that reads like a good book.</h1>
<span class="cap">sans does the work</span><div class="ui"><input value="you@studio.com" aria-label="email"><button>Request access</button></div></div>
```

#### Use when

Signaling craft or editorial taste in a technical category.

#### Avoid when

Products where everything is UI; the serif ends up on nothing.

#### Pairs with

Soft rise reveal, Analog grain

Measured on: Jog, Melius, Era, Handwired.
<!-- /artspo:pattern -->

## Rules

Rebuild from these measurements, never from a real site's code, text, logos or imagery. A font in <angle brackets> is a placeholder: pick a licensed face of that kind. Respect prefers-reduced-motion.

_Made with Artspo: https://github.com/bryfeng/artspo_
