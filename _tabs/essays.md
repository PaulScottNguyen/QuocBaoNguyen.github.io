---
layout: default
title: Essays
order: 2
---

<style>

/* ════════════════════════════════════════════════════════════════════════
   PAGE HEADER
════════════════════════════════════════════════════════════════════════ */
main { padding-top: 0 !important; }

.essays-header {
  padding: 2rem 0 1.5rem;
  border-bottom: 2px solid var(--border);
  margin-bottom: 0;
}

.essays-header h1 {
  font-family: var(--font-display);
  font-size: clamp(3.5rem, 10vw, 7rem);
  line-height: 0.9;
  letter-spacing: 0.02em;
}

.essays-header .accent-bar {
  display: flex;
  height: 6px;
  margin-top: 1rem;
}
.accent-bar span:nth-child(1) { background: var(--accent-red);    flex: 3; }
.accent-bar span:nth-child(2) { background: var(--accent-blue);   flex: 1; }
.accent-bar span:nth-child(3) { background: var(--accent-yellow); flex: 2; }

.essays-bio {
  margin-top: 1rem;
  font-size: 0.85rem;
  line-height: 1.7;
  max-width: 600px;
  opacity: 0.65;
  letter-spacing: 0.02em;
}

#essay-count {
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  opacity: 0.45;
  margin-top: 0.5rem;
}


/* ════════════════════════════════════════════════════════════════════════
   SHELF SECTION
   ──────────────────────────────────────────────────────────────────────
   Skeuomorphism meets Brutalism:
   - Real wood grain (CSS gradients + repeating lines)
   - Hard Bauhaus borders on each book
   - Books stand on a physical plank
════════════════════════════════════════════════════════════════════════ */
.shelf-section {
  position: relative;
  padding: 3rem 0 0;
  margin-bottom: 3rem;
}

/* The back wall of the shelf — subtly darker */
.shelf-wall {
  background: var(--bg);
  border: 2px solid var(--border);
  border-bottom: none;
  padding: 2rem 2rem 0;
  min-height: 260px;
  display: flex;
  align-items: flex-end;
}

.books-row {
  display: flex;
  gap: 1.25rem;
  align-items: flex-end;
  flex-wrap: wrap;
  padding-bottom: 0;
  width: 100%;
}

/* ── WOODEN SHELF PLANK ──────────────────────────────────────────────
   Built entirely in CSS — no images.
   Multiple gradient layers simulate wood grain.
──────────────────────────────────────────────────────────────────── */
.shelf-plank {
  height: 28px;
  border: 2px solid #5a3a08;
  border-top-color: #e8c060;
  position: relative;
  overflow: hidden;

  /* Main wood color gradient */
  background:
    /* Highlight at top */
    linear-gradient(180deg,
      rgba(255,220,100,0.25) 0%,
      transparent 20%
    ),
    /* Base wood */
    linear-gradient(180deg,
      #d4a843 0%,
      #c49030 20%,
      #b07820 40%,
      #c49030 60%,
      #9a6818 80%,
      #7a5010 100%
    );

  box-shadow:
    0 6px 16px rgba(0,0,0,0.55),
    0 2px 4px rgba(0,0,0,0.3),
    inset 0 1px 2px rgba(255,220,120,0.3);
}

/* Wood grain lines */
.shelf-plank::before {
  content: '';
  position: absolute;
  inset: 0;
  background: repeating-linear-gradient(
    90deg,
    transparent             0px,
    transparent             35px,
    rgba(0,0,0,0.06)        35px,
    rgba(0,0,0,0.06)        37px,
    transparent             37px,
    transparent             60px,
    rgba(255,255,255,0.05)  60px,
    rgba(255,255,255,0.05)  62px,
    transparent             62px,
    transparent             95px,
    rgba(0,0,0,0.04)        95px,
    rgba(0,0,0,0.04)        96px
  );
}

/* Shadow under the plank edge */
.shelf-plank::after {
  content: '';
  position: absolute;
  bottom: -8px;
  left: 0; right: 0;
  height: 8px;
  background: linear-gradient(180deg, rgba(0,0,0,0.35) 0%, transparent 100%);
}


/* ── BOOK CARD ────────────────────────────────────────────────────────
   Each book is a 3/4 aspect ratio card with:
   - A "spine" illusion via ::before pseudo-element
   - A bottom shadow via ::after
   - Bauhaus-style cover with geometric shapes
──────────────────────────────────────────────────────────────────── */
.book-card {
  position: relative;
  width: 148px;
  flex-shrink: 0;
  cursor: pointer;
  transition: transform 0.35s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.book-card:hover {
  transform: translateY(-18px);
  z-index: 10;
}

/* Left spine — simulates book thickness */
.book-card::before {
  content: '';
  position: absolute;
  left: -7px;
  top: 6px;
  bottom: -6px;
  width: 7px;
  background: linear-gradient(
    90deg,
    rgba(0,0,0,0.7) 0%,
    rgba(0,0,0,0.4) 100%
  );
  transform: skewY(0.3deg);
  z-index: 0;
}

/* Bottom depth shadow */
.book-card::after {
  content: '';
  position: absolute;
  bottom: -6px;
  left: -7px;
  right: 0;
  height: 7px;
  background: rgba(0,0,0,0.45);
  transform: skewX(-0.5deg);
  z-index: 0;
}

.book-cover {
  width: 100%;
  aspect-ratio: 3/4;
  border: 2px solid var(--border);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
  z-index: 1;
  background: var(--surface);
  box-shadow: 2px 0 6px rgba(0,0,0,0.25);
}

/* Color band takes the top 45% */
.book-band {
  height: 45%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
}

/* Bauhaus geometric shape in the band */
.book-shape {
  width: 52px;
  height: 52px;
  border: 3px solid rgba(255,255,255,0.55);
  flex-shrink: 0;
}

.book-shape.circle   { border-radius: 50%; }
.book-shape.square   { border-radius: 0; }
.book-shape.triangle {
  width: 0; height: 0;
  border-left: 26px solid transparent;
  border-right: 26px solid transparent;
  border-bottom: 46px solid rgba(255,255,255,0.4);
  background: none;
}

/* Text area */
.book-text {
  padding: 0.6rem 0.65rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
}

.book-title {
  font-family: var(--font-display);
  font-size: 0.95rem;
  letter-spacing: 0.03em;
  line-height: 1.1;
  color: var(--ink);
  /* Clamp to 3 lines */
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.book-meta {
  font-size: 0.55rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  opacity: 0.45;
  margin-top: 0.4rem;
  color: var(--ink);
}

/* Loading skeleton */
.book-card.loading .book-cover {
  background: var(--surface);
  animation: shimmer 1.4s infinite;
}

@keyframes shimmer {
  0%,100% { opacity: 0.6; }
  50%      { opacity: 1; }
}

#shelf-status {
  font-size: 0.8rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  opacity: 0.45;
  padding: 3rem 0;
  width: 100%;
  text-align: center;
}


/* ════════════════════════════════════════════════════════════════════════
   READER OVERLAY
   ──────────────────────────────────────────────────────────────────────
   Three layers:
     1. #reader-overlay  — dark backdrop
     2. #reader-panel    — the paper/book frame
     3. #reader-paper    — the textured page area
════════════════════════════════════════════════════════════════════════ */
#reader-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.88);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;

  opacity: 0;
  pointer-events: none;
  transition: opacity 0.25s ease;
}

#reader-overlay.open {
  opacity: 1;
  pointer-events: all;
}

/* ── macOS SWIRL OPEN ANIMATION ─────────────────────────────────────
   Starts tiny + rotated + blurred, springs to full size.
   cubic-bezier(0.34, 1.56, 0.64, 1) = spring with slight overshoot.
──────────────────────────────────────────────────────────────────── */
@keyframes macOSOpen {
  0% {
    opacity: 0;
    transform: scale(0.05) rotate(12deg);
    filter: blur(24px);
  }
  65% {
    opacity: 1;
    transform: scale(1.04) rotate(-0.8deg);
    filter: blur(0);
  }
  100% {
    opacity: 1;
    transform: scale(1) rotate(0deg);
    filter: blur(0);
  }
}

@keyframes macOSClose {
  0%   { transform: scale(1) rotate(0deg);   opacity: 1; filter: blur(0); }
  100% { transform: scale(0.05) rotate(12deg); opacity: 0; filter: blur(24px); }
}

#reader-panel {
  width: min(740px, 92vw);
  height: min(880px, 90vh);
  display: flex;
  flex-direction: column;
  border: 2px solid var(--border);
  box-shadow:
    10px 10px 0px var(--border),
    0 32px 80px rgba(0,0,0,0.7);
  overflow: hidden;
  transform-origin: center center;
}

#reader-panel.anim-open  { animation: macOSOpen  0.55s cubic-bezier(0.34,1.56,0.64,1) forwards; }
#reader-panel.anim-close { animation: macOSClose 0.35s cubic-bezier(0.4,0,1,1) forwards; }

/* ── READER TOOLBAR ─────────────────────────────────────────────── */
#reader-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: var(--surface);
  border-bottom: 2px solid var(--border);
  padding: 0;
  flex-shrink: 0;
  height: 44px;
}

.rd-btn {
  background: var(--surface);
  color: var(--ink);
  border: none;
  border-right: 2px solid var(--border);
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  padding: 0 1.1rem;
  height: 100%;
  transition: background 0.12s;
  white-space: nowrap;
}

.rd-btn:last-child    { border-right: none; border-left: 2px solid var(--border); }
.rd-btn:hover         { background: var(--accent-yellow); }
#rd-close:hover       { background: var(--accent-red); color: #f5f0e8; }
.rd-btn:disabled      { opacity: 0.25; cursor: not-allowed; }
.rd-btn:disabled:hover { background: var(--surface); }

#rd-title {
  font-family: var(--font-display);
  font-size: 1rem;
  letter-spacing: 0.06em;
  flex: 1;
  padding: 0 1rem;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

#rd-page-info {
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  opacity: 0.45;
  padding: 0 1rem;
  white-space: nowrap;
}


/* ── PAPER AREA ──────────────────────────────────────────────────────
   The newspaper-textured area where PDF pages render.
   Two CSS layers:
     1. Aged paper color + horizontal print lines
     2. SVG grain overlay (::after) for tactile texture
──────────────────────────────────────────────────────────────────── */
#reader-paper {
  flex: 1;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;

  /* Aged newsprint base */
  background-color: #f2e4c0;

  /* Subtle horizontal print lines — like a newspaper */
  background-image: repeating-linear-gradient(
    180deg,
    transparent          0px,
    transparent          23px,
    rgba(0,0,0,0.055)    23px,
    rgba(0,0,0,0.055)    24px
  );
}

/* Dark mode: aged but dark paper */
[data-theme="dark"] #reader-paper {
  background-color: #1c1810;
  background-image: repeating-linear-gradient(
    180deg,
    transparent            0px,
    transparent            23px,
    rgba(255,255,255,0.03) 23px,
    rgba(255,255,255,0.03) 24px
  );
}

/* Grain texture overlay — SVG feTurbulence rendered as data URI */
#reader-paper::after {
  content: '';
  position: absolute;
  inset: 0;
  /* Inline SVG noise pattern */
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='250' height='250'%3E%3Cfilter id='g'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.72' numOctaves='4' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='250' height='250' filter='url(%23g)' opacity='0.12'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 250px 250px;
  pointer-events: none;
  mix-blend-mode: multiply;
  z-index: 10;
}

[data-theme="dark"] #reader-paper::after {
  mix-blend-mode: screen;
  opacity: 0.4;
}

/* Loading spinner inside reader */
#reader-loading {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: inherit;
  z-index: 20;
  font-family: var(--font-body);
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  opacity: 0.45;
  color: #5a4a20;
}

[data-theme="dark"] #reader-loading { color: #c8b880; }


/* ── PAGE FLIP CANVASES ──────────────────────────────────────────────
   Two canvases stacked. The active one is on top.
   Flip animation: active rotates out (rotateY → 90deg),
   then staging rotates in (rotateY from -90deg → 0).
   Both share the same perspective container.
──────────────────────────────────────────────────────────────────── */
.canvas-wrapper {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  perspective: 1400px;
  z-index: 2;
}

.canvas-wrapper canvas {
  display: block;
  max-width: calc(100% - 2rem);
  max-height: calc(100% - 2rem);
  box-shadow: 0 4px 24px rgba(0,0,0,0.25);
  transform-origin: center center;
  backface-visibility: hidden;
}

/* Page flip keyframes — forward (next page) */
@keyframes flipOutFwd {
  from { transform: perspective(1400px) rotateY(0deg); }
  to   { transform: perspective(1400px) rotateY(-90deg); }
}
@keyframes flipInFwd {
  from { transform: perspective(1400px) rotateY(90deg); }
  to   { transform: perspective(1400px) rotateY(0deg); }
}

/* Page flip keyframes — backward (prev page) */
@keyframes flipOutBwd {
  from { transform: perspective(1400px) rotateY(0deg); }
  to   { transform: perspective(1400px) rotateY(90deg); }
}
@keyframes flipInBwd {
  from { transform: perspective(1400px) rotateY(-90deg); }
  to   { transform: perspective(1400px) rotateY(0deg); }
}

.flip-out-fwd { animation: flipOutFwd 0.3s ease-in  forwards; }
.flip-out-bwd { animation: flipOutBwd 0.3s ease-in  forwards; }
/* flip-in starts after flip-out reaches 90deg (0.28s delay) */
.flip-in-fwd  {
  transform: perspective(1400px) rotateY(90deg);
  animation: flipInFwd 0.3s ease-out 0.28s forwards;
}
.flip-in-bwd  {
  transform: perspective(1400px) rotateY(-90deg);
  animation: flipInBwd 0.3s ease-out 0.28s forwards;
}


/* ════════════════════════════════════════════════════════════════════
   MOBILE
════════════════════════════════════════════════════════════════════ */
@media (max-width: 600px) {
  .shelf-wall     { padding: 1.5rem 1rem 0; }
  .books-row      { gap: 0.75rem; }
  .book-card      { width: 110px; }
  #reader-panel   { width: 98vw; height: 95vh; }
  .rd-btn         { padding: 0 0.6rem; font-size: 0.65rem; }
}

</style>


<!-- ╔══════════════════════════════════════════════════════════╗
     ║  PAGE HEADER                                             ║
     ╚══════════════════════════════════════════════════════════╝ -->
<div class="essays-header">
  <h1>Essays</h1>
  <div class="accent-bar">
    <span></span><span></span><span></span>
  </div>
  <p class="essays-bio">Long-form writing on things I think about. Ideas, observations, whatever demands to be written down.</p>
  <p id="essay-count">Loading…</p>
</div>


<!-- ╔══════════════════════════════════════════════════════════╗
     ║  SHELF                                                   ║
     ╚══════════════════════════════════════════════════════════╝ -->
<div class="shelf-section">
  <div class="shelf-wall">
    <div id="books-row" class="books-row">
      <div id="shelf-status"></div>
    </div>
  </div>
  <div class="shelf-plank"></div>
</div>


<!-- ╔══════════════════════════════════════════════════════════╗
     ║  READER OVERLAY                                          ║
     ╚══════════════════════════════════════════════════════════╝ -->
<div id="reader-overlay" role="dialog" aria-modal="true" aria-label="Essay reader">
  <div id="reader-panel">

    <!-- Toolbar -->
    <div id="reader-toolbar">
      <button class="rd-btn" id="rd-prev" aria-label="Previous page">← PREV</button>
      <span id="rd-title"></span>
      <span id="rd-page-info">— / —</span>
      <button class="rd-btn" id="rd-next" aria-label="Next page">NEXT →</button>
      <button class="rd-btn" id="rd-close" aria-label="Close">✕</button>
    </div>

    <!-- Paper with PDF canvases -->
    <div id="reader-paper">
      <div id="reader-loading">Opening…</div>

      <!-- Canvas A -->
      <div class="canvas-wrapper" id="wrapper-a" style="z-index:3">
        <canvas id="canvas-a"></canvas>
      </div>

      <!-- Canvas B (staging — behind A initially) -->
      <div class="canvas-wrapper" id="wrapper-b" style="z-index:2">
        <canvas id="canvas-b"></canvas>
      </div>
    </div>

  </div>
</div>


<!-- PDF.js from cdnjs -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>

{% raw %}
<script>

/* ════════════════════════════════════════════════════════════════════════
   CONFIGURATION  ← edit these two values
════════════════════════════════════════════════════════════════════════ */
const ESSAYS_FOLDER_ID = '1aHmGyDIR1M8kSIv2Es-YK3scooYng_Ar';
const DRIVE_API_KEY    = 'AIzaSyBhAAVs73HLulmFTodnFuo4m5OCn5lzKhg';  // same key as photography


/* ════════════════════════════════════════════════════════════════════════
   PDF.JS SETUP
   The workerSrc must match the version of pdf.min.js loaded above.
════════════════════════════════════════════════════════════════════════ */
pdfjsLib.GlobalWorkerOptions.workerSrc =
  'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';


/* ════════════════════════════════════════════════════════════════════════
   STATE
════════════════════════════════════════════════════════════════════════ */
let pdfDoc      = null;
let currentPage = 1;
let totalPages  = 0;
let isFlipping  = false;
let activeSlot  = 'a';   // which canvas-wrapper is on top


/* ════════════════════════════════════════════════════════════════════════
   FETCH ESSAY LIST FROM DRIVE
   We filter for PDFs and Google Docs.
   orderBy=name sorts alphabetically — change to createdTime desc
   if you'd rather show newest first.
════════════════════════════════════════════════════════════════════════ */
async function fetchEssays() {
  const status = document.getElementById('shelf-status');
  const count  = document.getElementById('essay-count');

  const q = encodeURIComponent(
    `'${ESSAYS_FOLDER_ID}' in parents ` +
    `and (mimeType='application/pdf') ` +
    `and trashed=false`
  );
  const fields = 'files(id,name,description,createdTime,size)';
  const url    = `https://www.googleapis.com/drive/v3/files?q=${q}&fields=${fields}&key=${DRIVE_API_KEY}&orderBy=createdTime+desc&pageSize=50`;

  try {
    const res  = await fetch(url);
    if (!res.ok) {
      const err = await res.json();
      throw new Error(err.error?.message || 'Drive API error');
    }

    const data  = await res.json();
    const files = data.files || [];

    status.remove();

    if (files.length === 0) {
      document.getElementById('books-row').textContent = 'No essays found in this folder.';
      count.textContent = '0 essays';
      return;
    }

    count.textContent = `${files.length} essay${files.length !== 1 ? 's' : ''}`;
    files.forEach((file, i) => renderBookCard(file, i));

  } catch (err) {
    console.error(err);
    status.textContent = `Could not load essays: ${err.message}`;
    count.textContent  = 'Error';
  }
}


/* ════════════════════════════════════════════════════════════════════════
   RENDER A BOOK CARD
   Bauhaus covers: alternating accent colors, rotating geometric shapes.
════════════════════════════════════════════════════════════════════════ */
const BAND_COLORS = [
  'var(--accent-red)',
  'var(--accent-blue)',
  'var(--accent-yellow)',
];
const SHAPES = ['circle', 'square', 'triangle'];

function renderBookCard(file, index) {
  const row      = document.getElementById('books-row');
  const color    = BAND_COLORS[index % BAND_COLORS.length];
  const shape    = SHAPES[index % SHAPES.length];
  const name     = stripExtension(file.name);
  const dateStr  = formatDate(file.createdTime);

  const card = document.createElement('div');
  card.className = 'book-card';
  card.setAttribute('role', 'button');
  card.setAttribute('tabindex', '0');
  card.setAttribute('aria-label', `Open essay: ${name}`);

  card.innerHTML = `
    <div class="book-cover">
      <div class="book-band" style="background:${color}">
        <div class="book-shape ${shape}"></div>
      </div>
      <div class="book-text">
        <div class="book-title">${name}</div>
        <div class="book-meta">${dateStr}</div>
      </div>
    </div>
  `;

  card.addEventListener('click', () => openEssay(file.id, name));
  card.addEventListener('keydown', e => {
    if (e.key === 'Enter' || e.key === ' ') openEssay(file.id, name);
  });

  row.appendChild(card);
}


/* ════════════════════════════════════════════════════════════════════════
   OPEN ESSAY
   1. Show the reader overlay with macOS open animation
   2. Download PDF via Drive API alt=media (has CORS headers for public files)
   3. Render page 1
════════════════════════════════════════════════════════════════════════ */
async function openEssay(fileId, title) {
  const overlay = document.getElementById('reader-overlay');
  const panel   = document.getElementById('reader-panel');
  const loading = document.getElementById('reader-loading');
  const rdTitle = document.getElementById('rd-title');

  // Reset state
  pdfDoc = null; currentPage = 1; totalPages = 0; activeSlot = 'a';
  document.getElementById('wrapper-a').style.zIndex = '3';
  document.getElementById('wrapper-b').style.zIndex = '2';
  clearCanvas('a'); clearCanvas('b');
  loading.style.display = 'flex';
  rdTitle.textContent   = title;
  updatePageInfo();

  // Animate open
  overlay.classList.add('open');
  panel.classList.remove('anim-close');
  panel.classList.add('anim-open');
  panel.addEventListener('animationend', () => panel.classList.remove('anim-open'), { once: true });

  document.body.style.overflow = 'hidden';

  // Fetch PDF via Drive API (returns binary with proper CORS headers)
  try {
    const pdfUrl  = `https://www.googleapis.com/drive/v3/files/${fileId}?alt=media&key=${DRIVE_API_KEY}`;
    const res     = await fetch(pdfUrl);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);
    const buffer  = await res.arrayBuffer();
    pdfDoc        = await pdfjsLib.getDocument({ data: buffer }).promise;
    totalPages    = pdfDoc.numPages;
    currentPage   = 1;

    await renderToSlot(currentPage, 'a');
    loading.style.display = 'none';
    updatePageInfo();
    updateNavButtons();

  } catch (err) {
    console.error('PDF load error:', err);
    loading.textContent = `Could not open PDF: ${err.message}`;
  }
}


/* ════════════════════════════════════════════════════════════════════════
   RENDER A PAGE TO A CANVAS SLOT
   Scales the page to fit within the paper area (like object-fit: contain).
════════════════════════════════════════════════════════════════════════ */
async function renderToSlot(pageNum, slot) {
  const canvas  = document.getElementById(`canvas-${slot}`);
  const paper   = document.getElementById('reader-paper');
  const page    = await pdfDoc.getPage(pageNum);

  const paperW  = paper.clientWidth  - 32;
  const paperH  = paper.clientHeight - 32;
  const base    = page.getViewport({ scale: 1 });
  const scale   = Math.min(paperW / base.width, paperH / base.height);
  const vp      = page.getViewport({ scale });

  canvas.width  = vp.width;
  canvas.height = vp.height;

  await page.render({ canvasContext: canvas.getContext('2d'), viewport: vp }).promise;
}

function clearCanvas(slot) {
  const c = document.getElementById(`canvas-${slot}`);
  c.getContext('2d').clearRect(0, 0, c.width, c.height);
}


/* ════════════════════════════════════════════════════════════════════════
   PAGE FLIP
   Direction: 'next' or 'prev'
   
   HOW THE FLIP WORKS:
   - activeSlot is on top (z-index 3), stagingSlot is behind (z-index 2)
   - We render the new page on the staging canvas (invisible behind active)
   - Animate active OUT (rotateY to ±90deg)
   - Animate staging IN (rotateY from ±90deg to 0)
   - After animation: swap which slot is "active"
════════════════════════════════════════════════════════════════════════ */
async function flipPage(direction) {
  if (isFlipping || !pdfDoc) return;

  const nextPage = direction === 'next' ? currentPage + 1 : currentPage - 1;
  if (nextPage < 1 || nextPage > totalPages) return;

  isFlipping = true;
  updateNavButtons(true);

  const stagingSlot  = activeSlot === 'a' ? 'b' : 'a';
  const activeWrapper  = document.getElementById(`wrapper-${activeSlot}`);
  const stagingWrapper = document.getElementById(`wrapper-${stagingSlot}`);

  // Pre-render next page on staging (hidden behind active)
  await renderToSlot(nextPage, stagingSlot);
  stagingWrapper.style.zIndex = '2';
  activeWrapper.style.zIndex  = '3';

  const outClass = direction === 'next' ? 'flip-out-fwd' : 'flip-out-bwd';
  const inClass  = direction === 'next' ? 'flip-in-fwd'  : 'flip-in-bwd';

  // Remove any leftover animation classes
  activeWrapper.classList.remove('flip-out-fwd','flip-out-bwd','flip-in-fwd','flip-in-bwd');
  stagingWrapper.classList.remove('flip-out-fwd','flip-out-bwd','flip-in-fwd','flip-in-bwd');

  // Start animation
  activeWrapper.classList.add(outClass);
  stagingWrapper.classList.add(inClass);

  // Total duration = flip-out (0.3s) + delay (0.28s) + flip-in (0.3s) ≈ 600ms
  setTimeout(() => {
    // Swap slots
    activeWrapper.classList.remove(outClass);
    stagingWrapper.classList.remove(inClass);
    stagingWrapper.style.zIndex = '3';
    activeWrapper.style.zIndex  = '2';

    activeSlot  = stagingSlot;
    currentPage = nextPage;
    isFlipping  = false;

    updatePageInfo();
    updateNavButtons(false);
  }, 620);
}


/* ════════════════════════════════════════════════════════════════════════
   CLOSE
════════════════════════════════════════════════════════════════════════ */
function closeReader() {
  const overlay = document.getElementById('reader-overlay');
  const panel   = document.getElementById('reader-panel');

  panel.classList.add('anim-close');
  panel.addEventListener('animationend', () => {
    overlay.classList.remove('open');
    panel.classList.remove('anim-close');
    document.body.style.overflow = '';
    pdfDoc = null;
  }, { once: true });
}


/* ── UI HELPERS ──────────────────────────────────────────────────────── */

function updatePageInfo() {
  const el = document.getElementById('rd-page-info');
  el.textContent = pdfDoc ? `${currentPage} / ${totalPages}` : '— / —';
}

function updateNavButtons(disabled) {
  const prev = document.getElementById('rd-prev');
  const next = document.getElementById('rd-next');
  if (disabled) {
    prev.disabled = true; next.disabled = true; return;
  }
  prev.disabled = currentPage <= 1;
  next.disabled = currentPage >= totalPages;
}

function formatDate(iso) {
  if (!iso) return '';
  return new Date(iso).toLocaleDateString('en-GB', {
    day: '2-digit', month: 'short', year: 'numeric'
  });
}

function stripExtension(name) {
  return name.replace(/\.[^.]+$/, '');
}


/* ── EVENT LISTENERS ─────────────────────────────────────────────────── */

document.getElementById('rd-prev').addEventListener('click',  () => flipPage('prev'));
document.getElementById('rd-next').addEventListener('click',  () => flipPage('next'));
document.getElementById('rd-close').addEventListener('click', closeReader);

document.getElementById('reader-overlay').addEventListener('click', e => {
  if (e.target === document.getElementById('reader-overlay')) closeReader();
});

document.addEventListener('keydown', e => {
  const overlay = document.getElementById('reader-overlay');
  if (!overlay.classList.contains('open')) return;
  if (e.key === 'Escape')     closeReader();
  if (e.key === 'ArrowRight') flipPage('next');
  if (e.key === 'ArrowLeft')  flipPage('prev');
});


/* ── KICK OFF ────────────────────────────────────────────────────────── */
fetchEssays();

</script>
{% endraw %}