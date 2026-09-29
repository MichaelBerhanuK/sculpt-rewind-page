# Deferred landing-page features

These components were removed from the public landing page on 2026-09-29 while their claims are being held back. Keep this file and the referenced media assets so the sections can be restored later.

## Edit Mode changes

The GIF remains at `media/gif-edit-fast-bounce-720.gif`.

To restore the card, remove `single-feature` from the surrounding `.feature-pair` and add this article after the Vertex Paint article:

```html
<article class="feature-card">
  <div class="media history-gif">
    <img src="media/gif-edit-fast-bounce-720.gif" alt="Edit Mode changes being scrubbed back and forth through history">
  </div>
  <div class="feature-card-copy">
    <div class="kicker"><span class="ico">📐</span></div>
    <h3>Edit Mode changes</h3>
    <p>Revisit vertex moves and other Edit Mode changes without stepping backward blindly.</p>
  </div>
</article>
```

Restore the FAQ wording when the feature is ready:

```html
<p>It remembers your sculpt, masks, Face Sets, vertex painting, hidden areas and supported Edit Mode changes.</p>
```

The previous designer-note copy was:

```html
<div class="note"><b>Designer:</b> per-object history remains the primary differentiator. Vertex paint and Edit Mode are supporting proofs, grouped into a compact pair so the page does not repeat three oversized cards with the same visual weight.</div>
```

## 15M+ performance claim

### Section HTML

```html
<section class="sec">
  <span class="tag">8 · Performance assurance</span>
  <div class="panel performance-card">
    <div>
      <div class="hand">✦ It won't slow you down ✦</div>
      <div class="performance-stat">15M+<sup>*</sup></div>
      <h2>polygons, still scrubbable.</h2>
      <p style="margin-top:10px;font-size:14.5px;">* Tested on an RTX 4060 PC.</p>
    </div>
    <div class="media wide"><div>GIF: scrubbing a 15M+ polygon sculpt in real time<br>Blender's statistics overlay visible, poly count readable<br><b>no stutter, no lag</b></div></div>
  </div>
  <div class="note"><b>Designer:</b> closes the feature run on purpose. By now the visitor has seen how much gets recorded and is silently asking "surely this destroys my framerate?", so answer it before they move on. No data table; the claim plus one GIF is the whole section, polygon figure as a <b>headline number</b>.</div>
  <div class="note"><b>On this GIF:</b> it's <b>evidence, not decoration</b>. The poly counter must stay legible. Don't crop it out, shrink it below readable size, or overlay anything on that corner.</div>
</section>
```

### Section CSS

```css
.performance-card{display:grid;grid-template-columns:300px 1fr;gap:24px;align-items:center;
  background:var(--dark);color:#fff;padding:24px;}
.performance-card .hand{color:#f3a45c;}
.performance-card h2{color:#fff;}
.performance-card p{color:#c9c3bc;}
.performance-card p b{color:#fff !important;}
.performance-stat{font-family:var(--display-font);font-size:64px;
  line-height:.95;color:#f08a2a;margin:14px 0 8px;}
.performance-stat sup{font-family:ui-sans-serif,-apple-system,"Segoe UI",Inter,system-ui,sans-serif;
  font-size:.32em;vertical-align:top;position:relative;top:.12em;margin-left:2px;}

@media (max-width:760px){
  .performance-card{grid-template-columns:1fr;}
  .performance-stat{font-size:52px;}
}
```

### Supporting copy

The fifth feature-card description was:

```html
<p>Built for real production. Tested well past 15 million polygons.</p>
```

The facts strip included:

```html
<div class="card" style="text-align:center;"><b>15M+ polygons</b></div>
```

When restoring the facts card, change the facts grid from `g3` back to `g4`. Renumber the later designer tags if the performance section is restored in its former position.
