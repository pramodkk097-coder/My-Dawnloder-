<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#111827">
<title>My Download Hub</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#0b1120;color:#f8fafc}
header{position:sticky;top:0;z-index:5;background:#172033;padding:15px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid #334155}
header h1{font-size:20px;margin:0}
button,input{font:inherit}
button{border:0;border-radius:8px;padding:11px 14px;color:white;background:#2563eb;cursor:pointer}
main{width:94%;max-width:1050px;margin:20px auto}
.hero{text-align:center;padding:25px 12px;background:#172554}
.muted{color:#bdc9dc}
.search{display:flex;gap:8px;margin:18px 0}
.search input{flex:1;min-width:0;padding:12px;border-radius:8px;border:1px solid #475569;background:#172033;color:white}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(220px,1fr));gap:15px}
.card,.panel{padding:15px;background:#172033;border:1px solid #334155;border-radius:12px;overflow-wrap:anywhere}
.card h3{font-size:18px;margin:10px 0 5px 0}
.card img{width:100%;height:170px;object-fit:cover;background:#0b1120;border-radius:8px}
.actions{display:flex;gap:8px;flex-wrap:wrap;margin-top:12px}
.btn{display:inline-block;text-decoration:none;color:white;background:#16a34a;padding:11px;border-radius:8px;text-align:center;flex:1}
.view{background:#2563eb}
.icon{font-size:48px;text-align:center;padding:20px 0;background:#0b1120;border-radius:8px}
.page{display:none}
.page.active{display:block}
.drawer{display:none;position:fixed;z-index:20;top:0;right:0;width:290px;max-width:85%;height:100%;overflow:auto;background:#111827;padding:18px;box-shadow:0 0 0 9999px #0009}
.drawer.open{display:block}
.menuitem{display:block;width:100%;text-align:left;margin:9px 0;background:#263449}
.avatar{width:100px;height:100px;border-radius:50%;object-fit:cover}
footer{text-align:center;padding:25px;color:#bdc9dc}
.hidden{display:none!important}
@media(max-width:480px){.search{flex-wrap:wrap}.search input{flex-basis:100%}.search button{flex:1}}
</style>
</head>

<body>

<header>
  <h1>📥 My Download Hub</h1>
  <button id="openMenu" aria-label="Open menu">☰</button>
</header>

<div class="hero">
  <h2>Welcome to My Website ❤️</h2>
  <p class="muted">Photos, Videos, PDF, MP3 और ZIP डाउनलोड करें।</p>
</div>

<nav class="drawer" id="drawer">
  <h2>👤 My Menu</h2>
  <button id="closeMenu">✖ Close Menu</button>
  <button class="menuitem" data-page="profile">👤 1. Profile</button>
  <button class="menuitem" data-page="gallery">🖼️ 2. Gallery</button>
  <button class="menuitem" data-page="videos">🎬 3. Videos</button>
  <button class="menuitem" data-page="visitors">👥 4. Visitors</button>
  <button class="menuitem" data-page="about">ℹ️ 5. About Me</button>
  <button class="menuitem" data-page="home">🏠 Home</button>
</nav>

<main>

<section class="page active" id="home">
  <div class="search">
    <input id="searchInput" type="search" placeholder="फोटो या फाइल खोजें (उदा: mp4, photo, pdf)...">
    <button id="searchBtn">🔍 Search</button>
    <button id="resetBtn" style="background:#475569">Reset</button>
  </div>

  <h2>📁 All Files</h2>
  <p class="muted">किसी फ़ाइल को देखने या डाउनलोड करने के लिए बटन दबाएँ।</p>
  <div class="grid" id="fileGrid"></div>
  <p id="noResults" class="hidden">कोई फ़ाइल नहीं मिली।</p>
</section>

<section class="page" id="profile">
  <div class="panel">
    <h2>👤 My Profile</h2>
    <img class="avatar" src="downloads/profile.jpg" alt="Profile photo" onerror="this.style.display='none'">
    <h3 id="profileName">Your Name</h3>
    <p class="muted">Website Owner</p>
  </div>
</section>

<section class="page" id="gallery">
  <h2>🖼️ Photo Gallery</h2>
  <div class="grid" id="photoGrid"></div>
</section>

<section class="page" id="videos">
  <h2>🎬 Video Gallery</h2>
  <p class="muted">यहाँ वीडियो देखें या डाउनलोड करें।</p>
  <div class="grid" id="videoGrid"></div>
</section>

<section class="page" id="visitors">
  <div class="panel">
    <h2>👥 Visitors</h2>
    <h1 id="visitorCount">0</h1>
    <p class="muted">यह केवल इसी ब्राउज़र का स्थानीय काउंटर है, सभी विज़िटर की साझा गिनती नहीं।</p>
  </div>
</section>

<section class="page" id="about">
  <div class="panel">
    <h2>ℹ️ About Me</h2>
    <h3 id="aboutName">Your Name</h3>
    <p>नमस्ते! मेरी वेबसाइट पर आपका स्वागत है। यहाँ फोटो, वीडियो और अन्य फ़ाइलें उपलब्ध हैं।</p>
  </div>
</section>

</main>

<footer>© <span id="year"></span> My Download Hub</footer>

<script>
"use strict";

const PROFILE_NAME = "Your Name";

const FILES = [
  {name:"Sample JPG Photo", type:"JPG", path:"downloads/photo.jpg", image:true},
  {name:"Sample PNG Photo", type:"PNG", path:"downloads/photo.png", image:true},
  {name:"Sample JPEG Photo", type:"JPEG", path:"downloads/photo.jpeg", image:true},
  {name:"Sample WebP Photo", type:"WEBP", path:"downloads/photo.webp", image:true},
  {name:"Sample PDF", type:"PDF", path:"downloads/sample.pdf"},
  {name:"Sample MP3 Audio", type:"MP3", path:"downloads/sample.mp3"},
  {name:"Sample MP4 Video", type:"MP4", path:"downloads/sample.mp4", video:true},
  {name:"Sample ZIP File", type:"ZIP", path:"downloads/sample.zip"}
];

const $ = id => document.getElementById(id);

$("profileName").textContent = PROFILE_NAME;
$("aboutName").textContent = PROFILE_NAME;
$("year").textContent = new Date().getFullYear();

function makeCard(file) {
  const card = document.createElement("article");
  card.className = "card";

  if(file.image) {
    const img = document.createElement("img");
    img.src = file.path;
    img.alt = file.name;
    img.loading = "lazy";
    img.onerror = () => { img.alt = "Photo not found"; };
    card.appendChild(img);
  } else {
    // नॉर्मल फ़ाइल आइकॉन (वीडियो को भी सामान्य आइकॉन की तरह दिखाया गया है)
    const icon = document.createElement("div");
    icon.className = "icon";
    icon.textContent = ({
      PDF:"📄", MP3:"🎵", ZIP:"📦", MP4:"🎬"
    })[file.type] || "📁";
    card.appendChild(icon);
  }

  const title = document.createElement("h3");
  title.textContent = file.name;
  card.appendChild(title);

  const detail = document.createElement("p");
  detail.className = "muted";
  detail.textContent = file.type + " File";
  card.appendChild(detail);

  const actions = document.createElement("div");
  actions.className = "actions";

  // व्यू / ओपन बटन
  const view = document.createElement("a");
  view.className = "btn view";
  view.href = file.path;
  view.target = "_blank";
  view.rel = "noopener";
  view.textContent = "👁️ View";
  actions.appendChild(view);

  // डाउनलोड बटन
  const download = document.createElement("a");
  download.className = "btn";
  download.href = file.path;
  download.setAttribute("download", file.path.split("/").pop());
  download.textContent = "⬇ Download";
  actions.appendChild(download);

  card.appendChild(actions);
  return card;
}

function renderFiles() {
  const query = $("searchInput").value.trim().toLowerCase();

  $("fileGrid").replaceChildren();
  $("photoGrid").replaceChildren();
  $("videoGrid").replaceChildren();

  let found = 0;

  FILES.forEach(file => {
    // नाम, टाइप और पाथ में सर्च मैचिंग
    const matches = query === "" || 
      file.name.toLowerCase().includes(query) ||
      file.type.toLowerCase().includes(query) ||
      file.path.toLowerCase().includes(query);

    if(!matches) return;

    found++;
    $("fileGrid").appendChild(makeCard(file));

    if(file.image) {
      $("photoGrid").appendChild(makeCard(file));
    }

    if(file.video) {
      $("videoGrid").appendChild(makeCard(file));
    }
  });

  $("noResults").classList.toggle("hidden", found !== 0);
}

// सर्च इवेंट्स
$("searchBtn").addEventListener("click", renderFiles);
$("searchInput").addEventListener("keyup", renderFiles);
$("searchInput").addEventListener("input", renderFiles);

$("resetBtn").addEventListener("click", () => {
  $("searchInput").value = "";
  renderFiles();
});

function showPage(id) {
  document.querySelectorAll(".page").forEach(page => {
    page.classList.toggle("active", page.id === id);
  });

  $("drawer").classList.remove("open");
  window.scrollTo(0, 0);
}

document.querySelectorAll("[data-page]").forEach(button => {
  button.addEventListener("click", () => {
    showPage(button.dataset.page);
  });
});

$("openMenu").addEventListener("click", () => {
  $("drawer").classList.add("open");
});

$("closeMenu").addEventListener("click", () => {
  $("drawer").classList.remove("open");
});

try {
  const key = "downloadHubVisits";
  const count = Number(localStorage.getItem(key) || 0) + 1;
  localStorage.setItem(key, String(count));
  $("visitorCount").textContent = count.toLocaleString("en-IN");
} catch(error) {
  $("visitorCount").textContent = "Unavailable";
}

renderFiles();
</script>

</body>
</html>
