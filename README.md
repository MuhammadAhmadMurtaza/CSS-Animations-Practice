<div align="center">

# 🎨 CSS Fundamentals: Keyframe Animations

**Two projects on choreographing motion with `@keyframes`: a physics-style bouncing ball and a multi-animation timeline**

</div>

---

## 📖 About This Repository

This repository contains mini-projects I built while learning CSS. Each folder holds a single `index.html` file, so every concept is easy to see, edit, and experiment with.

No frameworks, no build tools, no JavaScript. Just HTML and CSS.

---

## 📑 Table of Contents

1. [Project Structure](#-project-structure)
2. [Transitions vs Keyframe Animations](#-transitions-vs-keyframe-animations)
3. [Project 1: Bouncing Red Ball](#-project-1-bouncing-red-ball)
4. [Experiment 2: CSS Animation Properties](#-experiment-2-css-animation-properties)
5. [Animation Cheat Sheet](#-animation-cheat-sheet)
6. [How to Run](#-how-to-run)
7. [Key Takeaways](#-key-takeaways)
8. [Roadmap](#-roadmap)

---

## 📂 Project Structure

```
css-fundamentals/
│
├── 21-bouncing-ball/
│   └── index.html
│
├── 22-css-animations/
│   └── index.html
│
└── README.md
```

> 💡 Rename the folders to match your own layout. Each `index.html` is fully standalone.

---

## ⚖️ Transitions vs Keyframe Animations

<table>
  <tr>
    <th></th>
    <th>Transition</th>
    <th>Keyframe animation</th>
  </tr>
  <tr>
    <td><b>Needs a trigger?</b></td>
    <td>Yes (hover, class change, etc.)</td>
    <td>No. It can start on page load.</td>
  </tr>
  <tr>
    <td><b>Number of states</b></td>
    <td>Two: start and end</td>
    <td>As many stops as you like</td>
  </tr>
  <tr>
    <td><b>Looping</b></td>
    <td>No</td>
    <td>Yes, any number of times or <code>infinite</code></td>
  </tr>
  <tr>
    <td><b>Direction control</b></td>
    <td>Reverses automatically when the state changes back</td>
    <td>Full control with <code>animation-direction</code></td>
  </tr>
  <tr>
    <td><b>Best for</b></td>
    <td>Hover effects, simple state changes</td>
    <td>Loaders, bouncing, multi-step sequences, attention grabbers</td>
  </tr>
</table>

---

## 🏀 Project 1: Bouncing Red Ball

📁 `21-bouncing-ball/index.html`

### 🎯 Goal
Make a ball bounce across a container using **only CSS**, with each bounce lower and shorter than the last, like real physics.

### 🧱 The Setup

<table>
  <tr>
    <th>Element</th>
    <th>Key styles</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><code>.container</code></td>
    <td><code>800px × 450px</code>, blue, <code>position: relative</code>, <code>overflow: hidden</code></td>
    <td>The stage. <code>relative</code> makes it the anchor for the ball, and <code>hidden</code> clips anything that leaves it.</td>
  </tr>
  <tr>
    <td><code>.ball</code></td>
    <td><code>80px × 80px</code>, red, <code>border-radius: 50%</code>, <code>position: absolute</code></td>
    <td>A circle placed with <code>bottom</code> and <code>left</code> so the animation can move it.</td>
  </tr>
</table>

### 🔑 Concepts Covered

<table>
  <tr>
    <th>Concept</th>
    <th>Where it's used</th>
    <th>Why it matters</th>
  </tr>
  <tr>
    <td><code>@keyframes</code></td>
    <td><code>@keyframes bounce { ... }</code></td>
    <td>Defines the animation's stops as percentages of its duration.</td>
  </tr>
  <tr>
    <td>Percentage keyframes</td>
    <td><code>0%</code>, <code>15%</code>, <code>30%</code>, ... <code>100%</code></td>
    <td>Control exactly <b>when</b> each position is reached.</td>
  </tr>
  <tr>
    <td>Timing function per keyframe</td>
    <td><code>animation-timing-function</code> inside a keyframe</td>
    <td>Changes the easing for the segment <b>starting at that keyframe</b>.</td>
  </tr>
  <tr>
    <td>Grouped keyframes</td>
    <td><code>90%, 100% { ... }</code></td>
    <td>Two keyframes share one block of values. The ball holds still at the end.</td>
  </tr>
  <tr>
    <td>Iteration count</td>
    <td><code>animation: bounce 2s ease-in-out 3;</code></td>
    <td>Plays the whole sequence 3 times (6 seconds total).</td>
  </tr>
  <tr>
    <td>Absolute positioning</td>
    <td><code>left</code> and <code>bottom</code></td>
    <td>Animating position properties moves the ball inside its relative parent.</td>
  </tr>
</table>

### 🧪 Code Highlight

```css
.ball {
  width: 80px;
  height: 80px;
  background-color: red;
  border-radius: 50%;
  position: absolute;
  bottom: 0;
  left: 20px;
  animation: bounce 2s ease-in-out 3;
}

@keyframes bounce {
  0%   { left: 20px;  bottom: 0;     animation-timing-function: ease-out; }
  15%  {              bottom: 250px; animation-timing-function: ease-in;  }
  30%  { left: 200px; bottom: 0;     animation-timing-function: ease-out; }
  42%  {              bottom: 150px; animation-timing-function: ease-in;  }
  55%  { left: 380px; bottom: 0;     animation-timing-function: ease-out; }
  65%  {              bottom: 70px;  animation-timing-function: ease-in;  }
  75%  { left: 550px; bottom: 0;     animation-timing-function: ease-out; }
  82%  {              bottom: 25px;  animation-timing-function: ease-in;  }
  90%, 100% { left: 650px; bottom: 0; }
}
```

### 📊 The Bounce Breakdown

<table>
  <tr>
    <th>Bounce</th>
    <th>Time span</th>
    <th>Peak height</th>
    <th>Lands at</th>
    <th>Duration (of 2s)</th>
  </tr>
  <tr align="center">
    <td>1</td>
    <td>0% → 30%</td>
    <td>250px</td>
    <td><code>left: 200px</code></td>
    <td>0.6s</td>
  </tr>
  <tr align="center">
    <td>2</td>
    <td>30% → 55%</td>
    <td>150px</td>
    <td><code>left: 380px</code></td>
    <td>0.5s</td>
  </tr>
  <tr align="center">
    <td>3</td>
    <td>55% → 75%</td>
    <td>70px</td>
    <td><code>left: 550px</code></td>
    <td>0.4s</td>
  </tr>
  <tr align="center">
    <td>4</td>
    <td>75% → 90%</td>
    <td>25px</td>
    <td><code>left: 650px</code></td>
    <td>0.3s</td>
  </tr>
  <tr align="center">
    <td>Rest</td>
    <td>90% → 100%</td>
    <td>0px</td>
    <td><code>left: 650px</code></td>
    <td>0.2s</td>
  </tr>
</table>

### 🧠 Why It Looks Realistic

<table>
  <tr>
    <td>1️⃣</td>
    <td><b>Shrinking peaks:</b> 250px, 150px, 70px, 25px. The ball loses energy with each bounce.</td>
  </tr>
  <tr>
    <td>2️⃣</td>
    <td><b>Shrinking time:</b> each bounce spans a smaller slice of the animation (30%, 25%, 20%, 15%), so later bounces are quicker.</td>
  </tr>
  <tr>
    <td>3️⃣</td>
    <td><b>Gravity easing:</b> <code>ease-out</code> on the way up (fast, then slowing near the top) and <code>ease-in</code> on the way down (slow, then speeding up) imitate gravity.</td>
  </tr>
  <tr>
    <td>4️⃣</td>
    <td><b>Forward motion:</b> <code>left</code> increases steadily at each landing, so the ball travels across the stage while it bounces.</td>
  </tr>
</table>

### 🐛 Things to Watch

<table>
  <tr>
    <td>⚠️</td>
    <td><b>The ball snaps back.</b> With no <code>animation-fill-mode</code>, the ball returns to its normal styles (<code>left: 20px; bottom: 0</code>) when the animation ends, and each of the 3 loops also restarts from the left. To keep it at the end position, use <code>animation: bounce 2s ease-in-out 3 forwards;</code>.</td>
  </tr>
  <tr>
    <td>⚠️</td>
    <td><b>Performance:</b> animating <code>left</code> and <code>bottom</code> forces the browser to recalculate layout on every frame. Animating <code>transform</code> is smoother. See the improvement idea below.</td>
  </tr>
  <tr>
    <td>⚠️</td>
    <td><b>Accessibility:</b> some people get discomfort from motion. Respect their system setting with <code>prefers-reduced-motion</code> (see the cheat sheet).</td>
  </tr>
</table>

### 🚀 Improvement Idea: Use `transform` Instead

You can rebuild the same motion with `translate`, keeping the ball's `left` and `bottom` fixed. The mapping is simple:

<table>
  <tr>
    <th>Original</th>
    <th>Transform version</th>
  </tr>
  <tr>
    <td><code>left: 200px</code> (starting from 20px)</td>
    <td><code>translateX(180px)</code></td>
  </tr>
  <tr>
    <td><code>bottom: 250px</code> (starting from 0)</td>
    <td><code>translateY(-250px)</code></td>
  </tr>
  <tr>
    <td><code>bottom: 0</code></td>
    <td><code>translateY(0)</code></td>
  </tr>
</table>

```css
.ball {
  left: 20px;
  bottom: 0;
  animation: bounce 2s ease-in-out 3;
}

@keyframes bounce {
  0%  { transform: translate(0, 0);         animation-timing-function: ease-out; }
  15% { transform: translate(90px, -250px); animation-timing-function: ease-in;  }
  30% { transform: translate(180px, 0);     animation-timing-function: ease-out; }
  /* ...continue the same pattern for the remaining bounces */
}
```

> In a transform-based version, **every** keyframe must include the full `transform` value, including the horizontal part.

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Change the iteration count from `3` to `infinite` and watch it loop forever.
2. Add `forwards` at the end of the shorthand and see the ball stay at the end position.
3. Change `2s` to `4s` for a slow-motion bounce, or `1s` for a frantic one.
4. Remove the per-keyframe `animation-timing-function` lines. The motion becomes less natural and more floaty.
5. Change `border-radius: 50%` to `10px` and watch the ball become a bouncing square.
6. Add `.ball:hover { animation-play-state: paused; }` to freeze it on hover.
7. Add a squash effect: at each landing keyframe, add `transform: scaleY(0.8);`, and at each peak use `scaleY(1)`.
8. Make the bounces higher by raising the `bottom` values. Make sure they stay below the container height minus the ball's 80px.

</details>

---

## ⏯️ Experiment 2: CSS Animation Properties

📁 `22-css-animations/index.html`

### 🎯 Goal
Learn every part of the `animation` shorthand, run **two animations on one element**, and understand what happens when they overlap.

### 🔑 The Animation Properties

<table>
  <tr>
    <th>Property</th>
    <th>Example</th>
    <th>What it controls</th>
  </tr>
  <tr>
    <td><code>animation-name</code></td>
    <td><code>ahmadkaAnimation</code></td>
    <td>Which <code>@keyframes</code> block to use.</td>
  </tr>
  <tr>
    <td><code>animation-duration</code></td>
    <td><code>1s</code></td>
    <td>How long one cycle takes.</td>
  </tr>
  <tr>
    <td><code>animation-timing-function</code></td>
    <td><code>ease-in-out</code>, <code>cubic-bezier(0, 0, 0, 0.93)</code></td>
    <td>The speed curve between each pair of keyframes.</td>
  </tr>
  <tr>
    <td><code>animation-delay</code></td>
    <td><code>3s</code></td>
    <td>Wait time before the animation starts.</td>
  </tr>
  <tr>
    <td><code>animation-iteration-count</code></td>
    <td><code>1</code>, <code>3</code>, <code>infinite</code></td>
    <td>How many times it repeats.</td>
  </tr>
  <tr>
    <td><code>animation-direction</code></td>
    <td><code>alternate-reverse</code></td>
    <td>Whether it plays forward, backward, or back and forth.</td>
  </tr>
  <tr>
    <td><code>animation-fill-mode</code></td>
    <td><code>backwards</code></td>
    <td>What styles apply before the animation starts and after it ends.</td>
  </tr>
  <tr>
    <td><code>animation-play-state</code></td>
    <td><code>running</code> / <code>paused</code></td>
    <td>Pauses or resumes the animation.</td>
  </tr>
</table>

### 🧩 Shorthand Order

```css
animation: name duration timing-function delay iteration-count direction fill-mode;
```

> ℹ️ As with transitions, when there are two time values the **first is the duration** and the **second is the delay**.

### 🧪 Code Highlight

```css
.box {
  width: 34px;
  height: 45px;
  background-color: aqua;
  animation: ahmadkaAnimation 1s ease-in-out 3s 1 backwards,
             ahmad2 3s ease-in-out 3s 1;
}

@keyframes ahmadkaAnimation {
  from { background-color: red; }
  to   { background-color: yellow;
         transform: translateX(1000px); }
}

@keyframes ahmad2 {
  0%   { transform: rotate(100deg); }
  20%  { transform: rotate(200deg); }
  50%  { transform: rotate(220deg); }
  80%  { transform: rotate(300deg); }
  100% { transform: rotate(310deg); }
}
```

### 📋 Reading the First Animation

<table>
  <tr>
    <th><code>ahmadkaAnimation</code></th>
    <th><code>1s</code></th>
    <th><code>ease-in-out</code></th>
    <th><code>3s</code></th>
    <th><code>1</code></th>
    <th><code>backwards</code></th>
  </tr>
  <tr align="center">
    <td>name</td>
    <td>duration</td>
    <td>timing</td>
    <td>delay</td>
    <td>iterations</td>
    <td>fill mode</td>
  </tr>
</table>

### 🧭 Fill Modes

<table>
  <tr>
    <th>Value</th>
    <th>Effect</th>
  </tr>
  <tr>
    <td><code>none</code> (default)</td>
    <td>Nothing is applied before the start or after the end. The element snaps back to its normal styles.</td>
  </tr>
  <tr>
    <td><code>forwards</code></td>
    <td>Keeps the <b>last keyframe's</b> values after the animation ends.</td>
  </tr>
  <tr>
    <td><code>backwards</code></td>
    <td>Applies the <b>first keyframe's</b> values during the delay period.</td>
  </tr>
  <tr>
    <td><code>both</code></td>
    <td>Both of the above.</td>
  </tr>
</table>

### 🔀 Direction Values

<table>
  <tr>
    <th>Value</th>
    <th>Behavior</th>
  </tr>
  <tr>
    <td><code>normal</code></td>
    <td>Always plays from 0% to 100%.</td>
  </tr>
  <tr>
    <td><code>reverse</code></td>
    <td>Always plays from 100% to 0%.</td>
  </tr>
  <tr>
    <td><code>alternate</code></td>
    <td>Forward, then backward, then forward again. Needs 2 or more iterations to show the effect.</td>
  </tr>
  <tr>
    <td><code>alternate-reverse</code></td>
    <td>Backward first, then forward, and so on.</td>
  </tr>
</table>

### 🕒 Timeline of This Demo

Both animations have a `3s` delay, so here is what the box does from page load:

<table>
  <tr>
    <th>Time</th>
    <th>Background color</th>
    <th>Transform</th>
    <th>What's happening</th>
  </tr>
  <tr>
    <td><b>0s to 3s</b></td>
    <td>🟥 Red</td>
    <td>None</td>
    <td>Both animations are waiting. <code>backwards</code> applies the first animation's <code>from</code> color during its delay. The second animation has no fill mode, so it does nothing yet.</td>
  </tr>
  <tr>
    <td><b>3s to 4s</b></td>
    <td>🟥 → 🟨 Red to yellow</td>
    <td>Rotation starts at 100°</td>
    <td>Both animations are active. The color animation runs, and <code>ahmad2</code> starts rotating.</td>
  </tr>
  <tr>
    <td><b>4s to 6s</b></td>
    <td>🟦 Back to aqua</td>
    <td>Rotation continues to 310°</td>
    <td>The first animation is over. With no <code>forwards</code>, its color effect disappears. <code>ahmad2</code> is still running.</td>
  </tr>
  <tr>
    <td><b>After 6s</b></td>
    <td>🟦 Aqua</td>
    <td>None</td>
    <td>Everything resets because there is no <code>forwards</code> fill.</td>
  </tr>
</table>

### 🐛 Key Pitfall: Two Animations Fighting Over `transform`

<table>
  <tr>
    <td>⚠️</td>
    <td><code>ahmadkaAnimation</code> animates <code>transform: translateX(1000px)</code> and <code>ahmad2</code> animates <code>transform: rotate(...)</code>. When two active animations set the <b>same property</b>, the <b>later one in the list wins</b>. Here that is <code>ahmad2</code>, so during the overlap (3s to 4s) the box never slides. The <code>translateX(1000px)</code> is effectively ignored.</td>
  </tr>
</table>

**Fix 1: combine them into one keyframe set**

```css
@keyframes slideAndSpin {
  from {
    background-color: red;
    transform: translateX(0) rotate(100deg);
  }
  to {
    background-color: yellow;
    transform: translateX(300px) rotate(310deg);
  }
}
```

**Fix 2: use independent properties** (supported in modern browsers)

```css
@keyframes slide { to { translate: 300px 0; } }
@keyframes spin  { to { rotate: 310deg; } }

.box {
  animation: slide 1s ease-in-out 3s forwards,
             spin  3s ease-in-out 3s forwards;
}
```

Because `translate` and `rotate` are separate properties from `transform`, the two animations no longer conflict.

**Fix 3: split the work across two elements.** Animate the outer element's position and the inner element's rotation.

### 📝 Good to Know

<table>
  <tr>
    <td>💡</td>
    <td>The <code>animation-timing-function</code> applies <b>between each pair of keyframes</b>, not across the whole animation. So <code>ease-in-out</code> on a 5-keyframe animation eases in and out of every segment.</td>
  </tr>
  <tr>
    <td>💡</td>
    <td>If a keyframe block leaves out the starting value (like <code>from</code> without a <code>transform</code>), the browser uses the element's current value as the starting point.</td>
  </tr>
  <tr>
    <td>💡</td>
    <td>Comma-separated animations run <b>at the same time</b>. They are not a queue. To run one after another, use delays.</td>
  </tr>
  <tr>
    <td>💡</td>
    <td>A <code>translateX(1000px)</code> is wider than most screens. An element that moves that far can cause horizontal scrolling unless a parent has <code>overflow: hidden</code>.</td>
  </tr>
</table>

### 🔬 Try It Yourself

<details>
<summary><b>Click to expand the experiment steps</b></summary>

<br>

1. Uncomment the longhand properties one at a time and replace the shorthand to see what each controls.
2. Set `animation-iteration-count: infinite` and `animation-direction: alternate` for a ping-pong effect.
3. Add `forwards` to the end of each animation and see the final color and rotation stay in place.
4. Change the delay on `ahmad2` to `0s` so it starts immediately, and see how the two animations overlap differently.
5. Apply **Fix 1** above and watch the box finally slide across the page.
6. Try `animation-timing-function: cubic-bezier(0, 0, 0, 0.93);` (from the commented code) and compare it with `ease-in-out`.
7. Add `.box:hover { animation-play-state: paused; }` to pause on hover.
8. Try `steps(5)` as the timing function for a jumpy, frame-by-frame look.

</details>

---

## 📚 Animation Cheat Sheet

| Goal | Use |
|---|---|
| Loop forever | `animation-iteration-count: infinite;` |
| Play back and forth | `animation-direction: alternate;` |
| Stay at the final state | `animation-fill-mode: forwards;` |
| Start at the first keyframe during the delay | `animation-fill-mode: backwards;` |
| Pause on hover | `.el:hover { animation-play-state: paused; }` |
| Run several animations on one element | Comma-separate them: `animation: a 1s, b 2s;` |
| Respect users who prefer less motion | `@media (prefers-reduced-motion: reduce) { .el { animation: none; } }` |
| Smoothest properties to animate | `transform` and `opacity` |

---

## 🚀 How to Run

No installation needed.

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git

# 2. Move into the project
cd <your-repo-name>

# 3. Open any project in your browser
open 21-bouncing-ball/index.html      # macOS
start 21-bouncing-ball/index.html     # Windows
xdg-open 21-bouncing-ball/index.html  # Linux
```

💡 **Tip:** Use the VS Code **Live Server** extension to see changes instantly. In Chrome DevTools, open the **Animations** panel (`More tools → Animations`) to slow animations down and scrub through them.

---

## 🎓 Key Takeaways

<table>
  <tr>
    <td>✅</td>
    <td>Transitions go from A to B. <code>@keyframes</code> define the whole journey with as many stops as needed.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>A timing function declared inside a keyframe controls the segment starting at that keyframe. That is how the ball gets gravity-like easing.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Realistic motion comes from details: shrinking heights, shrinking durations, and the right easing.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>The shorthand order is name, duration, timing function, delay, iteration count, direction, fill mode.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td><code>animation-fill-mode</code> decides what the element looks like before the animation starts and after it ends. Without it, elements snap back.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>When two animations change the same property at once, the later one in the list wins.</td>
  </tr>
  <tr>
    <td>✅</td>
    <td>Prefer animating <code>transform</code> and <code>opacity</code>, and respect <code>prefers-reduced-motion</code>.</td>
  </tr>
</table>

---

## 🗺️ Roadmap

- [x] `display` property
- [x] Viewport units and box model
- [x] CSS specificity
- [x] `overflow`
- [x] Lists and `list-style`
- [x] `box-shadow` and `text-shadow`
- [x] Positioning (`relative`, `absolute`, `fixed`, `sticky`)
- [x] Card component
- [x] Media queries
- [x] CSS variables
- [x] Landing page project
- [x] Float and clear
- [x] Pseudo-elements and advanced selectors
- [x] Full page layout with sticky navbar
- [x] Flexbox fundamentals
- [x] CSS Grid fundamentals and template areas
- [x] Responsive grid download page
- [x] CSS transforms
- [x] CSS transitions
- [x] Keyframe animations
- [ ] Rebuild the bouncing ball using `transform`
- [ ] Responsive project combining Flexbox, Grid, media queries, and animation
- [ ] Grid auto-placement (`grid-auto-flow`, `grid-auto-rows`)
- [ ] Mobile-first workflow

---

<div align="center">

### ⭐ If you found this helpful, consider giving the repo a star!

Made with ❤️ while learning CSS

</div>
