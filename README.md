
<!DOCTYPE Ram Ram>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#111827">

<title>My Download Hub</title>

<style>
:root {
  --bg: #0b1120;
  --panel: #151e30;
  --text: #f8fafc;
  --muted: #a9b6ca;
  --blue: #3b82f6;
  --green: #16a34a;
  --border: #29364c;
}
* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: var(--bg);
  color: var(--text);
}
button, input { font: inherit; }
button, a { -webkit-tap-highlight-color: transparent; }

header {
  position: sticky;
  top: 0;
  z-index: 10;
  background: #111827;
  border-bottom: 1px solid var(--border);
}
.nav {
  max-width: 1100px;
  margin: auto;
  min-height: 65px;
  padding: 12px 16px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}
.brand {
  font-size: 20px;
  font-weight: bold;
}
.brand span { color: #60a5fa; }
.menu-btn {
  border: 1px solid var(--border);
  background: var(--panel);
  color: white;
  padding: 10px 14px;
  border-radius: 10px;
  cursor: pointer;
  font-size: 20px;
}
.hero {
  text-align: center;
  padding: 35px 16px 25px;
  background: linear-gradient(140deg,#172554,#0b1120 75%);
}
.hero h1 { font-size: clamp(25px,5vw,40px); }
.hero p { color: var(--muted); line-height: 1.6; }

.container {
  width: 94%;
  max-width: 1050px;
  margin: 22px auto;
}
.search {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;
}
.search input {
  flex: 1;
  min-width: 0;
  padding: 13px;
  color: white;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 10px;
}
.btn {
  display: inline-block;
  padding: 11px 14px;
  color: white;
  background: var(--blue);
  text-decoration: none;
  border: 0;
  border-radius: 9px;
  cursor: pointer;
  text-align: center;
}
.green { background: var(--green); }
.gray { background: #334155; }
h2.section-title { font-size: 23px; }

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit,minmax(220px,1fr));
  gap: 16px;
}
.card {
  min-width: 0;
  padding: 15px;
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 14px;
}
.card h3 { margin: 10px 0; overflow-wrap: anywhere; }
.card p { color: var(--muted); font-size: 13px; }
.preview {
  width: 100%;
  height: 170px;
  object-fit: cover;
  background: #263449;
  border-radius: 9px;
}
.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-top: 14px;
}
.actions a { flex: 1; font-size: 14px; }
.file-icon { font-size: 45px; margin-top: 5px; }

.page { display: none; }
.page.active { display: block; }

.panel {
  background: var(--panel);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 22px;
  margin: 15px 0;
  overflow-wrap: anywhere;
}
.avatar {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  object-fit: cover;
  background: #334155;
}
.menu-overlay {
  position: fixed;
  inset: 0;
  background: #0009;
  z-index: 19;
  display: none;
}
.menu-overlay.open { display: block; }
.drawer {
  position: fixed;
  z-index: 20;
  top: 0;
  right: -310px;
  width: min(290px,85vw);
  height: 100%;
  padding: 22px;
  background: #111827;
  border-left: 1px solid var(--border);
  transition: right .25s ease;
}
.drawer.open { right: 0; }
.drawer-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
.menu-link {
  display: block;
  width: 100%;
  text-align: left;
  padding: 15px 12px;
  margin: 7px 0;
  border: 1px solid var(--border);
  border-radius: 10px;
  background: var(--panel);
  color: white;
  cursor: pointer;
}
.menu-link:hover { background: #263449; }
.notice {
  color: var(--muted);
  font-size: 13px;
  line-height: 1.7;
}
footer {
  text-align: center;
  color: var(--muted);
  border-top: 1px solid var(--border);
  padding: 25px 12px;
  margin-top: 35px;
}
footer a { color: #93c5fd; }
.hidden { display: none !important; }

@media(max-width:480px) {
  .brand { font-size: 17px; }
  .search { flex-wrap: wrap; }
  .search input { width: 100%; flex-basis: 100%; }
  .search .btn { flex: 1; }
}
</style>
</head>

<body>

<header>
  <div class="nav">
    <div class="brand">📥 My <span>Download Hub</span></div>
    <button class="menu-btn" id="menuOpen"
      aria-label="Open profile menu" aria-expanded="false">
      ☰
    </button>
  </div>
</header>

<div class="hero">
  <h1>Welcome to My Website</h1>
  <p>अपनी पसंद की फोटो और फ़ाइलें खोजें, देखें और डाउनलोड करें।</p>
</div>

<div class="menu-overlay" id="overlay"></div>

<aside class="drawer" id="drawer" aria-label="Profile menu">
  <div class="drawer-head">
    <strong>👤 My Profile Menu</strong>
    <button class="menu-btn" id="menuClose"
      aria-label="Close menu">✕</button>
  </div>

  <button class="menu-link" data-page="profile">👤 1. Profile</button>
  <button class="menu-link" data-page="gallery">🖼️ 2. Gallery</button>
  <button class="menu-link" data-page="visitors">👥 3. Visitors</button>
  <button class="menu-link" data-page="about">ℹ️ 4. About Me</button>
</aside>

<main class="container">

  <!-- HOME / SEARCH / DOWNLOAD -->
  <section class="page active" id="home">
    <div class="search">
      <input id="searchInput" type="search"
        placeholder="फोटो या फ़ाइल खोजें: JPG, PDF, MP3..."
        aria-label="Search files">
      <button class="btn" id="searchBtn">🔍 Search</button>
      <button class="btn gray" id="resetBtn">Reset</button>
    </div>

    <h2 class="section-title">📁 All Downloads</h2>
    <p class="notice">
      नीचे अपनी फ़ाइलों के नाम और सही लिंक सेट करें।
    </p>

    <div class="grid" id="downloadGrid"></div>

    <p id="noResults" class="panel hidden">
      😕 कोई फोटो या फ़ाइल नहीं मिली।
    </p>
  </section>

  <!-- PROFILE -->
  <section class="page" id="profile">
    <h2>👤 My Profile</h2>
    <div class="panel">
      <img class="avatar" src="downloads/profile.jpg"
        alt="Profile photo"
        onerror="this.style.display='none'">

      <h2 id="profileName">Your Name</h2>
      <p class="notice">Website Owner / Creator</p>
      <p>Welcome to my download website!</p>
      <button class="btn" data-goto="about">About Me →</button>
    </div>

    <p class="notice">
      अपना नाम और प्रोफाइल फोटो बदलने के लिए नीचे कोड में
      PROFILE SETTINGS देखें।
    </p>
  </section>

  <!-- GALLERY -->
  <section class="page" id="gallery">
    <h2>🖼️ My Gallery</h2>
    <p class="notice">फोटो देखने या डाउनलोड करने के लिए बटन दबाएँ।</p>
    <div class="grid" id="galleryGrid"></div>
  </section>

  <!-- VISITORS -->
  <section class="page" id="visitors">
    <h2>👥 Visitors</h2>
    <div class="panel">
      <h3>इस ब्राउज़र पर विज़िट</h3>
      <div id="visitorCount"
        style="font-size:40px;font-weight:bold;color:#60a5fa">
        0
      </div>
      <p class="notice">
        यह केवल इस ब्राउज़र में सेव होने वाला स्थानीय काउंटर है।
        यह सभी विज़िटर का वास्तविक साझा काउंट नहीं है।
      </p>
    </div>
  </section>

  <!-- ABOUT ME -->
  <section class="page" id="about">
    <h2>ℹ️ About Me</h2>
    <div class="panel">
      <h3 id="aboutName">Your Name</h3>
      <p id="aboutText">
        नमस्ते! यह मेरी वेबसाइट है। यहाँ आप फोटो, PDF, ऑडियो,
        वीडियो और ZIP फ़ाइलें पा सकते हैं।
      </p>
      <p class="notice">
        यहाँ अपना परिचय, काम, सोशल मीडिया या संपर्क लिंक जोड़ें।
      </p>
    </div>
  </section>

</main>

<footer>
  <p>© <span id="year"></span> My Download Hub</p>
  <p>Made with ❤️</p>
  <button class="btn gray" data-goto="home">🏠 Home</button>
</footer>

<script>
"use strict";

/* =========================================
   PROFILE SETTINGS
   अपनी जानकारी यहाँ बदलें
========================================= */

const PROFILE = {
  name: "Your Name",
  about: "नमस्ते! मेरा स्वागत है। यह मेरी वेबसाइट है।"
};

/* =========================================
   FILE SETTINGS
   GitHub Repository में downloads नाम का
   फ़ोल्डर बनाकर अपनी असली फ़ाइलें रखें।

   हर फ़ाइल के लिए name, type, path बदलें।
========================================= */

const FILES = [
  {
    name: "Sample Photo",
    type: "JPG",
    path: "downloads/photo.jpg",
    description: "JPG Photo Download",
    image: true
  },
  {
    name: "Sample PNG Image",
    type: "PNG",
    path: "downloads/photo.png",
    description: "PNG Image Download",
    image: true
  },
  {
    name: "Sample PDF",
    type: "PDF",
    path: "downloads/sample.pdf",
    description: "PDF Document"
  },
  {
    name: "Sample MP3",
    type: "MP3",
    path: "downloads/sample.mp3",
    description: "Audio File"
  },
  {
    name: "Sample MP4",
    type: "MP4",
    path: "downloads/sample.mp4",
    description: "Video File"
  },
  {
    name: "Sample ZIP",
    type: "ZIP",
    path: "downloads/sample.zip",
    description: "ZIP Archive"
  }
];

/* =========================================
   APP
========================================= */

const $ = id => document.getElementById(id);

$("profileName").textContent = PROFILE.name;
$("aboutName").textContent = PROFILE.name;
$("aboutText").textContent = PROFILE.about;
$("year").textContent = new Date().getFullYear();

function iconFor(type) {
  const icons = {
    JPG: "🖼️", JPEG: "🖼️", PNG: "🖼️",
    WEBP: "🖼️", GIF: "🖼️", PDF: "📄",
    MP3: "🎵", MP4: "🎬", ZIP: "📦"
  };
  return icons[type.toUpperCase()] || "📁";
}

function renderFiles() {
  const query = $("searchInput").value.trim().toLowerCase();
  const downloadGrid = $("downloadGrid");
  const galleryGrid = $("galleryGrid");

  downloadGrid.innerHTML = "";
  galleryGrid.innerHTML = "";

  let count = 0;

  FILES.forEach(file => {
    const text = (
      file.name + " " + file.type + " " + file.description
    ).toLowerCase();

    if (!text.includes(query)) return;

    count++;

    // Safe DOM elements; file names are treated as text.
    const card = document.createElement("article");
    card.className = "card";

    if (file.image) {
      const img = document.createElement("img");
      img.className = "preview";
      img.src = file.path;
      img.alt = file.name;
      img.loading = "lazy";
      img.onerror = () => {
        img.alt = "Image file not found";
        img.style.display = "none";
      };
      card.appendChild(img);
    } else {
      const icon = document.createElement("div");
      icon.className = "file-icon";
      icon.textContent = iconFor(file.type);
      card.appendChild(icon);
    }

    const title = document.createElement("h3");
    title.textContent = file.name;
    card.appendChild(title);

    const description = document.createElement("p");
    description.textContent = file.type + " · " + file.description;
    card.appendChild(description);

    const actions = document.createElement("div");
    actions.className = "actions";

    if (file.image) {
      const view = document.createElement("a");
      view.className = "btn";
      view.href = file.path;
      view.target = "_blank";
      view.rel = "noopener";
      view.textContent = "👁️ View";
      actions.appendChild(view);
    }

    const download = document.createElement("a");
    download.className = "btn green";
    download.href = file.path;
    download.download = file.path.split("/").pop();
    download.textContent = "⬇ Download";
    actions.appendChild(download);

    card.appendChild(actions);
    downloadGrid.appendChild(card);

    // Image files also appear in Gallery.
    if (file.image) {
      const galleryCard = card.cloneNode(true);
      galleryGrid.appendChild(galleryCard);
    }
  });

  $("noResults").classList.toggle("hidden", count !== 0);
}

$("searchBtn").addEventListener("click", renderFiles);
$("searchInput").addEventListener("input", renderFiles);

$("resetBtn").addEventListener("click", () => {
  $("searchInput").value = "";
  renderFiles();
});

/* PROFILE MENU */

function openMenu() {
  $("drawer").classList.add("open");
  $("overlay").classList.add("open");
  $("menuOpen").setAttribute("aria-expanded", "true");
}

function closeMenu() {
  $("drawer").classList.remove("open");
  $("overlay").classList.remove("open");
  $("menuOpen").setAttribute("aria-expanded", "false");
}

$("menuOpen").addEventListener("click", openMenu);
$("menuClose").addEventListener("click", closeMenu);
$("overlay").addEventListener("click", closeMenu);

function showPage(pageName) {
  document.querySelectorAll(".page").forEach(page => {
    page.classList.toggle("active", page.id === pageName);
  });

  closeMenu();
  window.scrollTo({ top: 0, behavior: "smooth" });
}

document.querySelectorAll("[data-page]").forEach(button => {
  button.addEventListener("click", () => {
    showPage(button.dataset.page);
  });
});

document.querySelectorAll("[data-goto]").forEach(button => {
  button.addEventListener("click", () => {
    showPage(button.dataset.goto);
  });
});

/* LOCAL VISITOR COUNTER
   यह केवल इसी ब्राउज़र की गिनती है।
*/

try {
  const key = "myDownloadHubVisits";
  let visits = Number(localStorage.getItem(key) || 0);
  visits++;
  localStorage.setItem(key, String(visits));
  $("visitorCount").textContent = visits.toLocaleString("en-IN");
} catch (error) {
  $("visitorCount").textContent = "Unavailable";
}

renderFiles();
</script>

</body>
</html>
