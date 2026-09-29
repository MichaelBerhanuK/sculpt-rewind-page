# Deferred preview controls

The footer preview panel was removed from `landing_branded.html` for the public page. The page still starts with `hide-extras hide-testimonials`, so designer notes and testimonials remain hidden.

## Font face and alternate display-font styles

Keep the existing Fuzzy Bubbles font face: the five small feature cards use it directly. Restore this additional font face and the alternate body classes if the font picker returns.

```css
@font-face {
  /* static face, but declared across the 400-700 range so the browser uses it for
     bold headings instead of synthesising a fake bold from the regular weight */
  font-family: 'SculptHand';
  src: url('branding/SculptHand-Regular.otf') format('opentype');
  font-weight: 400 700; font-display: swap;
}

body.font-fuzzy{--display-font:'FuzzyBubbles',ui-rounded,system-ui,sans-serif;}
body.font-sculpthand{--display-font:'SculptHand',ui-rounded,system-ui,sans-serif;--hand-stroke:.4px;}
/* Sculpt Hand ships as a single regular weight, so display type set in it reads lighter
   than DynaPuff or Fuzzy Bubbles. A hairline stroke in the text colour lands about halfway
   back to their weight without the smeared counters of a synthesised bold.
   Dial it with --hand-stroke: .3px is barely there, .6px starts to fill in the letterforms. */
body.font-sculpthand h1,
body.font-sculpthand h2,
body.font-sculpthand h3,
body.font-sculpthand .brandfont,
body.font-sculpthand .kicker,
body.font-sculpthand .hand,
body.font-sculpthand .tagline,
body.font-sculpthand .performance-stat{-webkit-text-stroke:var(--hand-stroke) currentColor;}
/* the feature row keeps its own face, so it keeps its own weight too */
body.font-sculpthand .featrow h3{-webkit-text-stroke:0;}
```

## Panel CSS

```css
.font-control{display:grid;grid-template-columns:1fr;gap:5px;min-width:190px;color:var(--ink);}
.font-control span{font-weight:650;}
.font-control select{width:100%;font:inherit;color:var(--ink);background:var(--cream);border:1px solid var(--border);
  border-radius:8px;padding:6px 28px 6px 8px;cursor:pointer;}
.footer-controls{display:grid;gap:8px;min-width:220px;padding:12px 14px;background:var(--card);
  border:1px solid var(--border);border-radius:12px;color:var(--ink);}
.footer-controls > span{font-weight:700;}
.footer-controls label:not(.font-control){display:flex;align-items:center;gap:8px;cursor:pointer;}
.footer-controls input{width:15px;height:15px;cursor:pointer;accent-color:var(--orange);}

@media (max-width:560px){
  .footer-controls{width:100%;}
  .font-control{width:100%;}
}
```

## Panel HTML

Place this inside `<footer>`, after `.footer-meta`.

```html
<div class="footer-controls" aria-label="Preview controls">
  <span>Preview controls</span>
  <label class="font-control" for="font-picker">
    <span>Main title font</span>
    <select id="font-picker">
      <option value="dynapuff">DynaPuff</option>
      <option value="fuzzy">Fuzzy Bubbles</option>
      <option value="sculpthand">Sculpt Hand</option>
    </select>
  </label>
  <label><input type="checkbox" id="extras"> Show designer notes</label>
  <label><input type="checkbox" id="testimonials"> Show testimonials</label>
</div>
```

## Panel JavaScript

Place this at the start of the existing `<script>` block.

```js
var cb = document.getElementById('extras');
cb.addEventListener('change', function () {
  document.body.classList.toggle('hide-extras', !cb.checked);
});

var fontPicker = document.getElementById('font-picker');
var fontClasses = {dynapuff: '', fuzzy: 'font-fuzzy', sculpthand: 'font-sculpthand'};
fontPicker.addEventListener('change', function () {
  document.body.classList.remove('font-fuzzy', 'font-sculpthand');
  var cls = fontClasses[fontPicker.value];
  if (cls) document.body.classList.add(cls);
});

var testimonialsCb = document.getElementById('testimonials');
testimonialsCb.addEventListener('change', function () {
  document.body.classList.toggle('hide-testimonials', !testimonialsCb.checked);
});
```
