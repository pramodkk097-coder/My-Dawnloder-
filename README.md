
<Ram Ram>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>My Download Website</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f1f5f9;
  color: #1e293b;
}

header {
  background: #1565c0;
  color: white;
  text-align: center;
  padding: 25px 10px;
}

header h1 {
  margin: 0 0 10px;
}

.search-area {
  display: flex;
  gap: 8px;
  justify-content: center;
  padding: 20px 10px;
}

#searchBox {
  width: 70%;
  max-width: 450px;
  padding: 12px;
  border: 1px solid #bbb;
  border-radius: 8px;
  font-size: 16px;
}

button, .download-btn {
  border: none;
  border-radius: 8px;
  padding: 11px 15px;
  color: white;
  background: #16a34a;
  cursor: pointer;
  font-size: 15px;
  text-decoration: none;
  display: inline-block;
  text-align: center;
}

.search-btn {
  background: #0d47a1;
}

.container {
  width: 94%;
  max-width: 950px;
  margin: auto;
}

.card {
  background: white;
  padding: 16px;
  margin: 15px 0;
  border-radius: 12px;
  box-shadow: 0 2px 8px #00000012;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 15px;
}

.file-info {
  min-width: 0;
}

.file-info h2 {
  font-size: 18px;
  margin: 0 0 8px;
}

.file-info p {
  font-size: 13px;
  color: #64748b;
  overflow-wrap: anywhere;
}

.photo {
  width: 100px;
  height: 85px;
  object-fit: cover;
  border-radius: 8px;
  background: #e2e8f0;
}

.actions {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.view-btn {
  background: #2563eb;
}

footer {
  text-align: center;
  padding: 25px;
  color: #64748b;
}

@media (max-width: 560px) {
  .card {
    flex-wrap: wrap;
  }

  .actions {
    width: 100%;
  }

  .actions a {
    flex: 1;
  }

  .search-area {
    flex-wrap: wrap;
  }

  #searchBox {
    width: 100%;
  }
}
</style>
</head>

<body>

<header>
  <h1>📥 My Download Website</h1>
  <p>Photo, JPG, PDF, MP3, MP4 और ZIP डाउनलोड करें</p>
</header>

<div class="search-area">
  <input
    type="search"
    id="searchBox"
    placeholder="फाइल या फोटो खोजें..."
    aria-label="फाइल खोजें"
  >

  <button class="search-btn" onclick="searchFiles()">
    🔍 Search
  </button>
</div>

<main class="container" id="fileList">

  <!-- JPG PHOTO -->
  <section class="card">
    <img class="photo"
         src="downloads/photo.jpg"
         alt="Sample photo">

    <div class="file-info">
      <h2>🖼️ JPG Photo</h2>
      <p>photo.jpg</p>
    </div>

    <div class="actions">
      <a class="download-btn view-btn"
         href="downloads/photo.jpg"
         target="_blank" rel="noopener">
        👁️ देखें
      </a>

      <a class="download-btn"
         href="downloads/photo.jpg"
         download="photo.jpg">
        ⬇ JPG Download
      </a>
    </div>
  </section>

  <!-- PDF -->
  <section class="card">
    <div class="file-info">
      <h2>📄 PDF File</h2>
      <p>sample.pdf</p>
    </div>

    <a class="download-btn"
       href="downloads/sample.pdf"
       download="sample.pdf">
      ⬇ PDF Download
    </a>
  </section>

  <!-- MP3 -->
  <section class="card">
    <div class="file-info">
      <h2>🎵 MP3 Audio</h2>
      <p>sample.mp3</p>
    </div>

    <a class="download-btn"
       href="downloads/sample.mp3"
       download="sample.mp3">
      ⬇ MP3 Download
    </a>
  </section>

  <!-- MP4 -->
  <section class="card">
    <div class="file-info">
      <h2>🎬 MP4 Video</h2>
      <p>sample.mp4</p>
    </div>

    <a class="download-btn"
       href="downloads/sample.mp4"
       download="sample.mp4">
      ⬇ MP4 Download
    </a>
  </section>

  <!-- ZIP -->
  <section class="card">
    <div class="file-info">
      <h2>📦 ZIP File</h2>
      <p>sample.zip</p>
    </div>

    <a class="download-btn"
       href="downloads/sample.zip"
       download="sample.zip">
      ⬇ ZIP Download
    </a>
  </section>

  <p id="noResults" style="display:none;text-align:center;">
    कोई फाइल नहीं मिली!
  </p>

</main>

<footer>
  © 2026 My Download Website
</footer>

<script>
function searchFiles() {
  const query = document
    .getElementById("searchBox")
    .value.trim()
    .toLowerCase();

  const cards = document.querySelectorAll("#fileList .card");
  let found = 0;

  cards.forEach(function(card) {
    const matches = card.innerText
      .toLowerCase()
      .includes(query);

    card.style.display = matches ? "flex" : "none";

    if (matches) found++;
  });

  document.getElementById("noResults").style.display =
    found === 0 ? "block" : "none";
}

document.getElementById("searchBox")
  .addEventListener("keydown", function(event) {
    if (event.key === "Enter") {
      searchFiles();
    }
  });
</script>

</body>
</html>
