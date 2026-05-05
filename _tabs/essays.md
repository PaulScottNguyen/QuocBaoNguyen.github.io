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
  border-bottom: 4px solid var(--ink, #000); /* Thickened for brutalism */
  margin-bottom: 0;
}

.essays-header h1 {
  font-family: var(--font-display);
  font-size: clamp(3.5rem, 10vw, 7rem);
  line-height: 0.9;
  letter-spacing: -0.02em; /* Tighter tracking for bold brutalist look */
  text-transform: uppercase;
}

.essays-header .accent-bar {
  display: flex;
  height: 12px; /* Thicker bar */
  margin-top: 1rem;
  border: 2px solid var(--ink, #000);
}
.accent-bar span:nth-child(1) { background: var(--accent-red, #ff3b30);    flex: 3; border-right: 2px solid var(--ink, #000); }
.accent-bar span:nth-child(2) { background: var(--accent-blue, #007aff);   flex: 1; border-right: 2px solid var(--ink, #000); }
.accent-bar span:nth-child(3) { background: var(--accent-yellow, #ffcc00); flex: 2; }

.essays-bio {
  margin-top: 1.5rem;
  font-size: 0.95rem;
  line-height: 1.6;
  max-width: 600px;
  font-weight: 600;
  letter-spacing: 0.02em;
}

#essay-count {
  font-size: 0.85rem;
  font-weight: 800;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-top: 1rem;
  background: var(--ink, #000);
  color: var(--surface, #fff);
  display: inline-block;
  padding: 4px 10px;
}


/* ════════════════════════════════════════════════════════════════════════
   SHELF SECTION
════════════════════════════════════════════════════════════════════════ */
.shelf-section {
  position: relative;
  padding: 3rem 0 0;
  margin-bottom: 3rem;
}

.shelf-wall {
  background: var(--bg);
  border: 4px solid var(--ink, #000);
  border-bottom: none;
  padding: 2rem 2rem 0;
  min-height: 260px;
  display: flex;
  align-items: flex-end;
}

.books-row {
  display: flex;
  gap: 1.5rem;
  align-items: flex-end;
  flex-wrap: wrap;
  padding-bottom: 0;
  width: 100%;
}

.shelf-plank {
  height: 32px;
  border: 4px solid var(--ink, #000);
  position: relative;
  overflow: hidden;
  background: var(--accent-yellow, #ffcc00);
  box-shadow: 
    8px 8px 0px rgba(0,0,0,1); /* Brutalist hard shadow */
}


/* ── BOOK CARD ──────────────────────────────────────────────────────── */
.book-card {
  position: relative;
  width: 148px;
  flex-shrink: 0;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.book-card:hover {
  transform: translate(-4px, -8px);
  z-index: 10;
}

.book-cover {
  width: 100%;
  aspect-ratio: 3/4;
  border: 3px solid var(--ink, #000);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  position: relative;
  z-index: 1;
  background: var(--surface, #fff);
  box-shadow: 6px 6px 0px rgba(0,0,0,1); /* Hard brutalist shadow */
  transition: box-shadow 0.2s ease;
}

.book-card:hover .book-cover {
  box-shadow: 12px 12px 0px rgba(0,0,0,1);
}

.book-band {
  height: 45%;
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  border-bottom: 3px solid var(--ink, #000);
}

.book-shape {
  width: 52px;
  height: 52px;
  border: 4px solid var(--ink, #000);
  background: var(--surface, #fff);
  flex-shrink: 0;
}

.book-shape.circle   { border-radius: 50%; }
.book-shape.square   { border-radius: 0; }
.book-shape.triangle {
  width: 0; height: 0;
  border-left: 26px solid transparent;
  border-right: 26px solid transparent;
  border-bottom: 46px solid var(--ink, #000);
  background: none;
}

.book-text {
  padding: 0.75rem 0.65rem;
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  overflow: hidden;
}

.book-title {
  font-family: var(--font-display);
  font-size: 1rem;
  font-weight: 800;
  letter-spacing: 0.02em;
  line-height: 1.1;
  color: var(--ink, #000);
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.book-meta {
  font-size: 0.6rem;
  font-weight: 800;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--ink, #000);
  border-top: 2px solid var(--ink, #000);
  padding-top: 0.25rem;
}


/* ════════════════════════════════════════════════════════════════════════
   READER OVERLAY
════════════════════════════════════════════════════════════════════════ */
#reader-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.85);
  backdrop-filter: blur(4px);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}

#reader-overlay.open {
  opacity: 1;
  pointer-events: all;
}

/* FIX: Ensure overlay fades out smoothly without flashing content */
#reader-overlay.closing {
  opacity: 0 !important;
  pointer-events: none;
}

@keyframes macOSOpen {
  0% { opacity: 0; transform: scale(0.95) translateY(20px); }
  100% { opacity: 1; transform: scale(1) translateY(0); }
}

@keyframes macOSClose {
  0%   { opacity: 1; transform: scale(1) translateY(0); }
  100% { opacity: 0; transform: scale(0.95) translateY(20px); }
}

#reader-panel {
  width: min(780px, 94vw);
  height: min(900px, 92vh);
  display: flex;
  flex-direction: column;
  background: var(--surface, #fff);
  border: 4px solid var(--ink, #000); /* Bauhaus border */
  box-shadow: 16px 16px 0px rgba(0,0,0,1); /* Brutalist block shadow */
  overflow: hidden;
  will-change: transform, opacity;
}

#reader-panel.anim-open  { animation: macOSOpen  0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards; }
#reader-panel.anim-close { animation: macOSClose 0.3s cubic-bezier(0.4, 0, 1, 1) forwards; }

#reader-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: var(--accent-yellow, #ffcc00); /* Bauhaus Pop */
  border-bottom: 4px solid var(--ink, #000);
  padding: 0;
  flex-shrink: 0;
  height: 54px;
}

.rd-btn {
  background: transparent;
  color: var(--ink, #000);
  border: none;
  border-right: 4px solid var(--ink, #000);
  font-family: var(--font-body);
  font-size: 0.85rem;
  font-weight: 800;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  cursor: pointer;
  padding: 0 1.5rem;
  height: 100%;
  transition: background 0.1s, color 0.1s;
  white-space: nowrap;
}

.rd-btn:last-child    { border-right: none; border-left: 4px solid var(--ink, #000); background: var(--accent-red, #ff3b30); color: #fff;}
.rd-btn:hover         { background: var(--ink, #000); color: var(--surface, #fff); }
#rd-close:hover       { background: #000; color: #fff; }
.rd-btn:disabled      { opacity: 0.4; cursor: not-allowed; background: transparent; color: var(--ink, #000); }

#rd-title {
  font-family: var(--font-display);
  font-weight: 800;
  font-size: 1.1rem;
  letter-spacing: 0.04em;
  flex: 1;
  padding: 0 1rem;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  text-align: center;
}

#rd-page-info {
  font-size: 0.85rem;
  font-weight: 800;
  background: var(--ink, #000);
  color: #fff;
  padding: 4px 10px;
  border-radius: 20px;
  margin: 0 1rem;
  white-space: nowrap;
}


/* ── READER PAPER ───────────────────────────────────────────────────── */
#reader-paper {
  flex: 1;
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #e5e5e5; /* Base board */
}

[data-theme="dark"] #reader-paper { background-color: #1a1a1a; }

/* FIX: Texture sits explicitly OVER the pages now */
#paper-texture {
  position: absolute;
  inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='250' height='250'%3E%3Cfilter id='g'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='4' stitchTiles='stitch'/%3E%3CfeColorMatrix type='saturate' values='0'/%3E%3C/filter%3E%3Crect width='250' height='250' filter='url(%23g)' opacity='0.08'/%3E%3C/svg%3E");
  background-repeat: repeat;
  background-size: 250px 250px;
  pointer-events: none;
  mix-blend-mode: multiply;
  z-index: 100;
}
[data-theme="dark"] #paper-texture { 
  mix-blend-mode: screen; 
  opacity: 0.2; 
}

#reader-loading {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: inherit;
  z-index: 20;
  font-weight: 800;
  font-size: 1.2rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}

.page-wrapper {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  perspective: 2500px; /* Stronger perspective for 3D curl */
  z-index: 2;
  will-change: transform, opacity;
}

.page-shell {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  box-sizing: border-box;
}

.reader-page-canvas {
  display: block;
  max-width: calc(100% - 2rem);
  max-height: calc(100% - 2rem);
  width: auto;
  height: auto;
  /* FIX: Ensure pure white for inversion baseline & brutalist borders */
  background: #ffffff; 
  border: 3px solid var(--ink, #000);
  box-shadow: 12px 12px 0px rgba(0,0,0,0.85); /* Hard shadow */
  transform-origin: 50% 50%;
  backface-visibility: hidden;
}

/* FIX: Dark mode PDF conversion */
[data-theme="dark"] .reader-page-canvas {
  /* Inverts the canvas, retains the white background as pitch black and text as white. Hue-rotate saves image colors */
  filter: invert(1) hue-rotate(180deg) brightness(0.95) contrast(1.1);
  box-shadow: 12px 12px 0px rgba(0,0,0,1);
  border-color: #333;
}

/* iOS 5-6 Style Diagonal Curl Motion */
/* Lift down-right corner and roll to upper-left */
@keyframes rollOutNext {
  0%   { transform: rotate3d(-1, 1, 0, 0deg); opacity: 1; }
  35%  { opacity: 1; }
  100% { transform: rotate3d(-1, 1, 0, 110deg) translate3d(-15%, -15%, 250px); opacity: 0; }
}

@keyframes rollInPrev {
  0%   { transform: rotate3d(-1, 1, 0, 110deg) translate3d(-15%, -15%, 250px); opacity: 0; }
  65%  { opacity: 1; }
  100% { transform: rotate3d(-1, 1, 0, 0deg); opacity: 1; }
}

@keyframes stayHidden { 0%, 100% { opacity: 0; } }
@keyframes stayVisible { 0%, 100% { opacity: 1; } }

.turn-out-next { animation: rollOutNext 0.6s cubic-bezier(0.3, 0.1, 0.2, 1) forwards; transform-origin: 50% 50%; }
.turn-in-next  { animation: stayVisible 0.6s forwards; }

.turn-out-prev { animation: stayVisible 0.6s forwards; }
.turn-in-prev  { animation: rollInPrev 0.6s cubic-bezier(0.3, 0.1, 0.2, 1) forwards; transform-origin: 50% 50%; }


/* ════════════════════════════════════════════════════════════════════
   MOBILE
════════════════════════════════════════════════════════════════════ */
@media (max-width: 600px) {
  .essays-header h1 { font-size: 3rem; }
  .book-card      { width: 120px; }
  #reader-panel   { width: 98vw; height: 96vh; border-width: 2px; }
  .rd-btn         { padding: 0 0.8rem; font-size: 0.75rem; border-right-width: 2px; }
  .page-shell     { padding: 0.5rem; }
  .reader-page-canvas { box-shadow: 6px 6px 0px rgba(0,0,0,0.85); border-width: 2px;}
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

    <!-- PDF canvases -->
    <div id="reader-paper">
      <!-- Fixed texture layer sits purely above the canvases -->
      <div id="paper-texture"></div>
      <div id="reader-loading">Opening…</div>

      <div class="page-wrapper" id="wrapper-a" style="z-index:3">
        <div class="page-shell">
          <canvas id="canvas-a" class="reader-page-canvas"></canvas>
        </div>
      </div>

      <div class="page-wrapper" id="wrapper-b" style="z-index:2">
        <div class="page-shell">
          <canvas id="canvas-b" class="reader-page-canvas"></canvas>
        </div>
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
════════════════════════════════════════════════════════════════════════ */
pdfjsLib.GlobalWorkerOptions.workerSrc =
  'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';


/* ════════════════════════════════════════════════════════════════════════
   STATE
════════════════════════════════════════════════════════════════════════ */
let pdfDoc      = null;
let currentPage  = 1;
let totalPages   = 0;
let isFlipping   = false;
let activeSlot   = 'a';   // which canvas-wrapper is on top


/* ════════════════════════════════════════════════════════════════════════
   FETCH ESSAY LIST FROM DRIVE
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
    const res = await fetch(url);
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
════════════════════════════════════════════════════════════════════════ */
async function openEssay(fileId, title) {
  const overlay = document.getElementById('reader-overlay');
  const panel   = document.getElementById('reader-panel');
  const loading = document.getElementById('reader-loading');
  const rdTitle = document.getElementById('rd-title');

  pdfDoc = null;
  currentPage = 1;
  totalPages = 0;
  activeSlot = 'a';
  isFlipping = false;

  overlay.classList.remove('closing');
  overlay.classList.add('open');
  panel.classList.remove('anim-close');
  panel.classList.add('anim-open');
  panel.addEventListener('animationend', () => panel.classList.remove('anim-open'), { once: true });

  document.getElementById('wrapper-a').style.zIndex = '3';
  document.getElementById('wrapper-b').style.zIndex = '2';
  clearCanvas('a');
  clearCanvas('b');

  loading.style.display = 'flex';
  loading.textContent   = 'Opening…';
  rdTitle.textContent   = title;
  updatePageInfo();
  updateNavButtons();

  document.body.style.overflow = 'hidden';

  try {
    const pdfUrl = `https://www.googleapis.com/drive/v3/files/${fileId}?alt=media&key=${DRIVE_API_KEY}`;
    const res    = await fetch(pdfUrl);
    if (!res.ok) throw new Error(`HTTP ${res.status}`);

    const buffer = await res.arrayBuffer();
    pdfDoc       = await pdfjsLib.getDocument({ data: buffer }).promise;
    totalPages   = pdfDoc.numPages;
    currentPage  = 1;

    await renderToSlot(currentPage, 'a');
    loading.style.display = 'none';
    updatePageInfo();
    updateNavButtons(false);

  } catch (err) {
    console.error('PDF load error:', err);
    loading.textContent = `Could not open PDF: ${err.message}`;
  }
}


/* ════════════════════════════════════════════════════════════════════════
   SHARP PDF RENDERING
════════════════════════════════════════════════════════════════════════ */
async function renderToSlot(pageNum, slot) {
  if (!pdfDoc) return;

  const canvas = document.getElementById(`canvas-${slot}`);
  const paper   = document.getElementById('reader-paper');
  const page    = await pdfDoc.getPage(pageNum);

  const dpr = Math.max(1, window.devicePixelRatio || 1);
  const paperW = paper.clientWidth - 40;
  const paperH = paper.clientHeight - 40;

  const base = page.getViewport({ scale: 1 });
  const scale = Math.min(paperW / base.width, paperH / base.height);
  const viewport = page.getViewport({ scale });

  const renderWidth  = Math.floor(viewport.width * dpr);
  const renderHeight = Math.floor(viewport.height * dpr);

  canvas.width = renderWidth;
  canvas.height = renderHeight;
  canvas.style.width = `${Math.floor(viewport.width)}px`;
  canvas.style.height = `${Math.floor(viewport.height)}px`;

  const context = canvas.getContext('2d', { alpha: false });
  context.setTransform(dpr, 0, 0, dpr, 0, 0);
  context.imageSmoothingEnabled = true;

  await page.render({
    canvasContext: context,
    viewport,
    transform: [dpr, 0, 0, dpr, 0, 0]
  }).promise;
}

function clearCanvas(slot) {
  const c = document.getElementById(`canvas-${slot}`);
  const ctx = c.getContext('2d');
  ctx.clearRect(0, 0, c.width, c.height);
}


/* ════════════════════════════════════════════════════════════════════════
   PAGE TURN - Diagonal Peel
════════════════════════════════════════════════════════════════════════ */
async function flipPage(direction) {
  if (isFlipping || !pdfDoc) return;

  const nextPage = direction === 'next' ? currentPage + 1 : currentPage - 1;
  if (nextPage < 1 || nextPage > totalPages) return;

  isFlipping = true;
  updateNavButtons(true);

  const stagingSlot    = activeSlot === 'a' ? 'b' : 'a';
  const activeWrapper  = document.getElementById(`wrapper-${activeSlot}`);
  const stagingWrapper = document.getElementById(`wrapper-${stagingSlot}`);

  await renderToSlot(nextPage, stagingSlot);

  // Z-index handling for correct overlapping during animation
  if (direction === 'next') {
    stagingWrapper.style.zIndex = '2';
    activeWrapper.style.zIndex  = '3';
  } else {
    stagingWrapper.style.zIndex = '3';
    activeWrapper.style.zIndex  = '2';
  }

  const outClass = direction === 'next' ? 'turn-out-next' : 'turn-out-prev';
  const inClass  = direction === 'next' ? 'turn-in-next'  : 'turn-in-prev';

  activeWrapper.classList.remove('turn-out-next', 'turn-out-prev', 'turn-in-next', 'turn-in-prev');
  stagingWrapper.classList.remove('turn-out-next', 'turn-out-prev', 'turn-in-next', 'turn-in-prev');

  activeWrapper.classList.add(outClass);
  stagingWrapper.classList.add(inClass);

  setTimeout(() => {
    activeWrapper.classList.remove(outClass);
    stagingWrapper.classList.remove(inClass);
    
    // Reset to idle stack
    stagingWrapper.style.zIndex = '3';
    activeWrapper.style.zIndex  = '2';

    activeSlot  = stagingSlot;
    currentPage = nextPage;
    isFlipping  = false;

    updatePageInfo();
    updateNavButtons(false);
  }, 620); // Syncs with CSS animation timing + small buffer
}


/* ════════════════════════════════════════════════════════════════════════
   CLOSE
════════════════════════════════════════════════════════════════════════ */
function closeReader() {
  const overlay = document.getElementById('reader-overlay');
  const panel   = document.getElementById('reader-panel');

  if (!overlay.classList.contains('open') || overlay.classList.contains('closing')) return;

  // Add closing to overlay immediately to sync fade outs
  overlay.classList.add('closing');
  panel.classList.remove('anim-open');
  panel.classList.add('anim-close');

  panel.addEventListener('animationend', () => {
    overlay.classList.remove('open', 'closing');
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
    prev.disabled = true;
    next.disabled = true;
    return;
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