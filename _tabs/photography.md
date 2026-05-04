---
layout: default
title: Photography
order: 4
---

<style>

  /* ════════════════════════════════════════════════════════════════════════
     PAGE HEADER
     ──────────────────────────────────────────────────────────────────────── */
  .photo-page-header {
    margin-bottom: 3rem;
    border-bottom: 2px solid var(--border);
    padding-bottom: 1.5rem;
  }

  .photo-page-header h1 {
    font-family: var(--font-display);
    font-size: clamp(3.5rem, 10vw, 7rem);
    line-height: 0.9;
    letter-spacing: 0.02em;
    margin-bottom: 0.5rem;
  }

  /* Bauhaus colored accent bar under the title */
  .photo-page-header .accent-bar {
    display: flex;
    gap: 0;
    height: 6px;
    margin-top: 1rem;
  }

  .accent-bar span:nth-child(1) { background: var(--accent-red);    flex: 3; }
  .accent-bar span:nth-child(2) { background: var(--accent-blue);   flex: 1; }
  .accent-bar span:nth-child(3) { background: var(--accent-yellow); flex: 2; }

  .photo-page-header p {
    font-size: 0.8rem;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    opacity: 0.6;
    margin-top: 0.75rem;
  }

  /* Loading / error state */
  #gallery-status {
    font-family: var(--font-body);
    font-size: 0.8rem;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    opacity: 0.5;
    padding: 4rem 0;
    text-align: center;
  }


  /* ════════════════════════════════════════════════════════════════════════
     MASONRY GALLERY
     ──────────────────────────────────────────────────────────────────────
     HOW CSS COLUMNS MASONRY WORKS:
     Instead of a grid (which forces equal-height rows), `columns` flows
     items top-to-bottom in each column, like a newspaper. Images keep their
     natural aspect ratios. Zero JavaScript needed for the layout itself.

     `break-inside: avoid` on each item prevents an image from being split
     across two columns.
  ════════════════════════════════════════════════════════════════════════ */
  .gallery-grid {
    columns: 3 280px;   /* 3 columns, min 280px each — responsive automatically */
    column-gap: 12px;
  }

  /* Each photo card */
  .photo-card {
    break-inside: avoid;        /* don't split a card across columns */
    margin-bottom: 12px;
    position: relative;
    cursor: pointer;
    border: 2px solid var(--border);
    box-shadow: 3px 3px 0px var(--border);
    overflow: hidden;
    background: var(--surface);

    /* Snap-up animation on hover (neobrutalism signature move) */
    transition: transform 0.15s ease, box-shadow 0.15s ease;
  }

  .photo-card:hover {
    transform: translate(-3px, -3px);
    box-shadow: 6px 6px 0px var(--border);
  }

  .photo-card img {
    display: block;
    width: 100%;
    height: auto;
    transition: filter 0.25s ease;
  }

  /* Darken image slightly on hover so the overlay text reads well */
  .photo-card:hover img { filter: brightness(0.45); }


  /* ── HOVER OVERLAY ───────────────────────────────────────────────────
     Sits on top of the image. Hidden by default (opacity: 0).
     Fades in when the card is hovered.
  ──────────────────────────────────────────────────────────────────── */
  .photo-overlay {
    position: absolute;
    inset: 0;                   /* shorthand for top/right/bottom/left: 0 */
    padding: 1rem;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;  /* text anchored to bottom */

    opacity: 0;
    transition: opacity 0.25s ease;
    pointer-events: none;       /* don't block clicks when hidden */
  }

  .photo-card:hover .photo-overlay { opacity: 1; }

  .overlay-name {
    font-family: var(--font-display);
    font-size: 1.2rem;
    color: #F5F0E8;
    letter-spacing: 0.06em;
    line-height: 1.1;
    margin-bottom: 0.35rem;
    /* Hard text-shadow so name is legible on any photo */
    text-shadow: 2px 2px 0px rgba(0,0,0,0.8);
  }

  .overlay-desc {
    font-size: 0.7rem;
    color: #F5F0E8;
    opacity: 0.85;
    line-height: 1.4;
    margin-bottom: 0.4rem;
  }

  .overlay-date {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--accent-yellow);
  }

  /* Small red corner tag — "click to expand" hint */
  .photo-card::after {
    content: '↗';
    position: absolute;
    top: 8px;
    right: 8px;
    background: var(--accent-red);
    color: #F5F0E8;
    font-size: 0.7rem;
    font-weight: 700;
    padding: 2px 6px;
    opacity: 0;
    transition: opacity 0.2s;
  }
  .photo-card:hover::after { opacity: 1; }


  /* ════════════════════════════════════════════════════════════════════════
     LIGHTBOX  (full-screen modal)
     ──────────────────────────────────────────────────────────────────────
     The lightbox has three layers:
       1. #lightbox-backdrop  — dark overlay, click to close
       2. #lightbox-panel     — the white/dark box with the image
       3. #lightbox-toolbar   — X, zoom+, zoom- buttons
  ════════════════════════════════════════════════════════════════════════ */
  #lightbox-backdrop {
    position: fixed;
    inset: 0;
    background: rgba(0, 0, 0, 0.88);
    z-index: 1000;
    display: flex;
    align-items: center;
    justify-content: center;

    opacity: 0;
    pointer-events: none;
    transition: opacity 0.2s ease;
  }

  #lightbox-backdrop.open {
    opacity: 1;
    pointer-events: all;
  }

  #lightbox-panel {
    position: relative;
    max-width: 90vw;
    max-height: 90vh;
    /* Stop clicks on the panel from closing the backdrop */
    background: var(--surface);
    border: 2px solid var(--border);
    box-shadow: 8px 8px 0px var(--border);
    overflow: hidden;
    cursor: grab;
  }

  #lightbox-panel.dragging { cursor: grabbing; }

  /* The actual image — transform-origin center so zoom scales from middle */
  #lightbox-img {
    display: block;
    max-width: 85vw;
    max-height: 80vh;
    object-fit: contain;
    transform-origin: center center;
    transition: transform 0.2s ease;
    user-select: none;          /* prevent browser image-drag ghost */
    -webkit-user-drag: none;
    pointer-events: none;       /* so drag events hit the panel, not the img */
  }

  /* ── TOOLBAR ─────────────────────────────────────────────────────────
     Fixed strip above the image. Three buttons: close (X), zoom in, zoom out.
  ──────────────────────────────────────────────────────────────────── */
  #lightbox-toolbar {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    gap: 0;
    background: var(--surface);
    border-bottom: 2px solid var(--border);
    z-index: 10;
  }

  .lb-btn {
    background: var(--surface);
    color: var(--ink);
    border: none;
    border-left: 2px solid var(--border);
    font-family: var(--font-body);
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    cursor: pointer;
    padding: 0.5rem 1rem;
    transition: background 0.12s;
    line-height: 1;
  }

  .lb-btn:hover { background: var(--accent-yellow); }

  /* Close button is red */
  #lb-close:hover {
    background: var(--accent-red);
    color: #F5F0E8;
  }

  /* Image sits below the toolbar — add padding-top equal to toolbar height */
  #lightbox-img-wrap {
    padding-top: 42px;   /* matches toolbar height */
    overflow: hidden;
  }

  /* ── LIGHTBOX CAPTION ────────────────────────────────────────────── */
  #lightbox-caption {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background: var(--surface);
    border-top: 2px solid var(--border);
    padding: 0.6rem 1rem;
    display: flex;
    justify-content: space-between;
    align-items: baseline;
    gap: 1rem;
  }

  #lb-caption-name {
    font-family: var(--font-display);
    font-size: 1.1rem;
    letter-spacing: 0.04em;
  }

  #lb-caption-date {
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--accent-red);
    white-space: nowrap;
  }

  @media (max-width: 600px) {
    .gallery-grid { columns: 2 160px; column-gap: 8px; }
    .photo-card   { margin-bottom: 8px; }
  }

.photo-bio {
  margin-top: 1rem;
  font-size: 0.85rem;
  line-height: 1.7;
  max-width: 600px;
  opacity: 0.75;
  text-transform: none;
  letter-spacing: 0.02em;
}

/* Override the default main padding just for this page */
main {
  padding-top: 1.5rem;
}

</style>


<!-- ╔══════════════════════════════════════════════════════════════════════╗
     ║  PAGE HEADER                                                         ║
     ╚══════════════════════════════════════════════════════════════════════╝ -->
<div class="photo-page-header">
  <h1>Photography</h1>
  <div class="accent-bar">
    <span></span><span></span><span></span>
  </div>
  <p class="photo-bio">Photography is my creative outlet. I love capturing moments and stories. These photos of mine you are about to see will help you visualize who I am as a person hehe'v'./p>
  <p id="photo-count">Loading from Google Drive…</p>
</div>

<!-- ╔══════════════════════════════════════════════════════════════════════╗
     ║  GALLERY                                                             ║
     ╚══════════════════════════════════════════════════════════════════════╝ -->
<div id="gallery-status"></div>
<div class="gallery-grid" id="gallery-grid"></div>


<!-- ╔══════════════════════════════════════════════════════════════════════╗
     ║  LIGHTBOX                                                            ║
     ╚══════════════════════════════════════════════════════════════════════╝ -->
<div id="lightbox-backdrop" role="dialog" aria-modal="true" aria-label="Photo viewer">

  <div id="lightbox-panel" role="document">

    <!-- Toolbar: zoom out | zoom in | close -->
    <div id="lightbox-toolbar">
      <button class="lb-btn" id="lb-zoom-out" aria-label="Zoom out">−  ZOOM</button>
      <button class="lb-btn" id="lb-zoom-in"  aria-label="Zoom in"> +  ZOOM</button>
      <button class="lb-btn" id="lb-close"    aria-label="Close">✕  CLOSE</button>
    </div>

    <div id="lightbox-img-wrap">
      <img id="lightbox-img" src="" alt="">
    </div>

    <div id="lightbox-caption">
      <span id="lb-caption-name"></span>
      <span id="lb-caption-date"></span>
    </div>

  </div>
</div>


<!-- ╔══════════════════════════════════════════════════════════════════════╗
     ║  JAVASCRIPT                                                          ║
     ╚══════════════════════════════════════════════════════════════════════╝ -->
<script>

/* ════════════════════════════════════════════════════════════════════════════
   CONFIGURATION  ← YOU EDIT THESE TWO VALUES
   ────────────────────────────────────────────────────────────────────────────
   DRIVE_FOLDER_ID: The ID in your folder's share URL.
     e.g. https://drive.google.com/drive/folders/1a2B3c4D5e6F  →  "1a2B3c4D5e6F"

   DRIVE_API_KEY: A restricted key from Google Cloud Console.
     Guide: https://developers.google.com/drive/api/guides/api-specific-auth
     Restrict it to: HTTP referrers → yourusername.github.io/*
                     API → Google Drive API
     This key is public (in your HTML) but scoped so it can only list files
     in public folders — it cannot read private data or write anything.
════════════════════════════════════════════════════════════════════════════ */
{% raw %}
const DRIVE_FOLDER_ID = '1RCGH-pNLrFkwy7MRgRAWXYDLOz19oqbm';
const DRIVE_API_KEY   = 'AIzaSyBhAAVs73HLulmFTodnFuo4m5OCn5lzKhg';


/* ════════════════════════════════════════════════════════════════════════════
   GOOGLE DRIVE API
   ────────────────────────────────────────────────────────────────────────────
   Drive API v3 /files endpoint lets you list files in a folder.
   We ask for these fields on each file:
     id               → used to build the image URL
     name             → shown in hover overlay and lightbox caption
     description      → custom description you add in Drive (File → Details)
     createdTime      → ISO 8601 timestamp e.g. "2024-11-03T10:22:00.000Z"
     imageMediaMetadata.width/height  → so we could know portrait vs landscape
                                        (not used for layout but useful later)

   The thumbnail URL pattern:
     https://lh3.googleusercontent.com/d/FILE_ID=s800
     The "=s800" suffix is a size parameter (max dimension in px).
     Use =s600 for grid thumbnails, =s1600 for lightbox full-res.
════════════════════════════════════════════════════════════════════════════ */
async function fetchDrivePhotos() {
  const status = document.getElementById('gallery-status');
  const grid   = document.getElementById('gallery-grid');
  const count  = document.getElementById('photo-count');

  // Build the API URL
  // q= filters to: images inside the specified folder, not trashed
  const fields = 'files(id,name,description,createdTime,imageMediaMetadata)';
  const q      = encodeURIComponent(`'${DRIVE_FOLDER_ID}' in parents and mimeType contains 'image/' and trashed = false`);
  const url    = `https://www.googleapis.com/drive/v3/files?q=${q}&fields=${fields}&key=${DRIVE_API_KEY}&pageSize=100&orderBy=createdTime desc`;

  try {
    const response = await fetch(url);

    // If the API key or folder ID is wrong, Drive returns an error object
    if (!response.ok) {
      const err = await response.json();
      throw new Error(err.error?.message || 'Drive API error');
    }

    const data  = await response.json();
    const files = data.files || [];

    if (files.length === 0) {
      status.textContent = 'No photos found in this folder.';
      return;
    }

    // Clear loading text and render
    status.textContent = '';
    count.textContent  = `${files.length} photo${files.length !== 1 ? 's' : ''}`;
    files.forEach((file, index) => renderCard(file, index, grid));

  } catch (err) {
    console.error('Drive fetch error:', err);
    status.innerHTML = `
      <strong>Could not load photos.</strong><br>
      Check DRIVE_FOLDER_ID and DRIVE_API_KEY in photography.html.<br>
      <small style="opacity:.5">${err.message}</small>
    `;
    count.textContent = 'Error loading photos';
  }
}


/* ════════════════════════════════════════════════════════════════════════════
   RENDER A SINGLE PHOTO CARD
════════════════════════════════════════════════════════════════════════════ */
function renderCard(file, index, container) {
  // Thumbnail URL — =s600 means 600px on the longest side
  const thumbUrl  = `https://lh3.googleusercontent.com/d/${file.id}=s600`;
  // Full-res URL for the lightbox
  const fullUrl   = `https://lh3.googleusercontent.com/d/${file.id}=s1600`;
  // Format the date from ISO 8601 to something readable
  const dateStr   = formatDate(file.createdTime);
  // Use the Drive file description if set; otherwise empty
  const desc      = file.description || '';
  // Strip the file extension from the name for display
  const name      = stripExtension(file.name);

  const card = document.createElement('div');
  card.className = 'photo-card';

  // Stagger the fade-in animation using CSS animation-delay
  card.style.animationDelay = `${index * 60}ms`;

  card.innerHTML = `
    <img
      src="${thumbUrl}"
      alt="${name}"
      loading="lazy"
    >
    <div class="photo-overlay">
      <div class="overlay-name">${name}</div>
      ${desc ? `<div class="overlay-desc">${desc}</div>` : ''}
      <div class="overlay-date">${dateStr}</div>
    </div>
  `;

  // Click opens the lightbox
  card.addEventListener('click', () => openLightbox(fullUrl, name, dateStr));

  container.appendChild(card);
}


/* ── HELPERS ─────────────────────────────────────────────────────────────── */

function formatDate(iso) {
  if (!iso) return '';
  const d = new Date(iso);
  // e.g. "03 May 2025"
  return d.toLocaleDateString('en-GB', { day: '2-digit', month: 'short', year: 'numeric' });
}

function stripExtension(name) {
  return name.replace(/\.[^.]+$/, '');
}


/* ════════════════════════════════════════════════════════════════════════════
   LIGHTBOX  —  open / close / zoom / drag
════════════════════════════════════════════════════════════════════════════ */
const backdrop = document.getElementById('lightbox-backdrop');
const panel    = document.getElementById('lightbox-panel');
const img      = document.getElementById('lightbox-img');
const capName  = document.getElementById('lb-caption-name');
const capDate  = document.getElementById('lb-caption-date');

let currentScale = 1;       // zoom level (1 = 100%)
const ZOOM_STEP  = 0.3;
const ZOOM_MIN   = 0.5;
const ZOOM_MAX   = 4;

// Drag state
let isDragging  = false;
let dragStart   = { x: 0, y: 0 };
let imgOffset   = { x: 0, y: 0 };  // current translate offset


function openLightbox(src, name, date) {
  img.src         = src;
  img.alt         = name;
  capName.textContent = name;
  capDate.textContent = date;
  currentScale    = 1;
  imgOffset       = { x: 0, y: 0 };
  applyTransform();
  backdrop.classList.add('open');
  document.body.style.overflow = 'hidden';  // prevent background scroll
}

function closeLightbox() {
  backdrop.classList.remove('open');
  document.body.style.overflow = '';
  // Small delay so the fade-out animation plays before we clear src
  setTimeout(() => { img.src = ''; }, 200);
}

function applyTransform() {
  img.style.transform = `translate(${imgOffset.x}px, ${imgOffset.y}px) scale(${currentScale})`;
}

function zoomBy(delta) {
  currentScale = Math.min(ZOOM_MAX, Math.max(ZOOM_MIN, currentScale + delta));
  // When zooming back to 1:1 reset any drag offset so image re-centers
  if (Math.abs(currentScale - 1) < 0.05) imgOffset = { x: 0, y: 0 };
  applyTransform();
}


/* ── BUTTON EVENTS ───────────────────────────────────────────────────────── */
document.getElementById('lb-zoom-in').addEventListener('click',  () => zoomBy( ZOOM_STEP));
document.getElementById('lb-zoom-out').addEventListener('click', () => zoomBy(-ZOOM_STEP));
document.getElementById('lb-close').addEventListener('click', closeLightbox);

// Click BACKDROP (not panel) → close
backdrop.addEventListener('click', (e) => {
  if (e.target === backdrop) closeLightbox();
});

// Keyboard: Escape closes, +/- zoom
document.addEventListener('keydown', (e) => {
  if (!backdrop.classList.contains('open')) return;
  if (e.key === 'Escape')    closeLightbox();
  if (e.key === '+' || e.key === '=') zoomBy( ZOOM_STEP);
  if (e.key === '-')                  zoomBy(-ZOOM_STEP);
});


/* ── DRAG TO PAN ─────────────────────────────────────────────────────────
   We track mousedown → mousemove → mouseup on the panel element.
   On each mousemove we compute (currentPos - startPos) and add it to the
   stored offset, then apply the combined translate+scale transform.
──────────────────────────────────────────────────────────────────────── */
panel.addEventListener('mousedown', (e) => {
  // Only drag with left button and only when zoomed in
  if (e.button !== 0 || currentScale <= 1) return;
  isDragging = true;
  dragStart  = { x: e.clientX - imgOffset.x, y: e.clientY - imgOffset.y };
  panel.classList.add('dragging');
  e.preventDefault();   // prevents text selection while dragging
});

document.addEventListener('mousemove', (e) => {
  if (!isDragging) return;
  imgOffset = {
    x: e.clientX - dragStart.x,
    y: e.clientY - dragStart.y,
  };
  applyTransform();
});

document.addEventListener('mouseup', () => {
  if (!isDragging) return;
  isDragging = false;
  panel.classList.remove('dragging');
});

/* Touch drag support (same logic, different event API) */
panel.addEventListener('touchstart', (e) => {
  if (currentScale <= 1) return;
  // If the user tapped a button, don't intercept — let the click fire normally
  if (e.target.closest('button')) return;
  const t = e.touches[0];
  isDragging = true;
  dragStart  = { x: t.clientX - imgOffset.x, y: t.clientY - imgOffset.y };
  e.preventDefault();
}, { passive: false });

document.addEventListener('touchmove', (e) => {
  if (!isDragging) return;
  const t = e.touches[0];
  imgOffset = { x: t.clientX - dragStart.x, y: t.clientY - dragStart.y };
  applyTransform();
}, { passive: false });

document.addEventListener('touchend', () => { isDragging = false; });


/* ════════════════════════════════════════════════════════════════════════════
   KICK IT OFF
════════════════════════════════════════════════════════════════════════════ */
fetchDrivePhotos();

</script>
{% endraw %}