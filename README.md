<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Download Hub - Direct Link Previewer & Downloader</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body {
    font-family: Arial, sans-serif;
    background-color: #0b1120;
    color: #f8fafc;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  header {
    position: sticky;
    top: 0;
    z-index: 10;
    background: #172033;
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-bottom: 1px solid #334155;
  }
  header h1 { font-size: 20px; font-weight: bold; }
  .menu-btn {
    background: #2563eb;
    color: white;
    border: none;
    padding: 10px 16px;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
  }
  main {
    flex: 1;
    width: 94%;
    max-width: 850px;
    margin: 25px auto;
  }
  .hero {
    text-align: center;
    padding: 25px 15px;
    background: #172554;
    border-radius: 12px;
    margin-bottom: 25px;
    border: 1px solid #1e40af;
  }
  .hero h2 { font-size: 22px; margin-bottom: 8px; }
  .muted { color: #bdc9dc; font-size: 14px; }
  
  .card-panel {
    background: #172033;
    border: 1px solid #334155;
    border-radius: 12px;
    padding: 22px;
    margin-bottom: 25px;
  }
  .input-label { display: block; font-weight: bold; margin-bottom: 10px; }
  .input-group {
    display: flex;
    gap: 8px;
  }
  .input-group input {
    flex: 1;
    padding: 12px 14px;
    border-radius: 8px;
    border: 1px solid #475569;
    background: #0b1120;
    color: white;
    font-size: 15px;
  }
  button.action-btn {
    border: none;
    border-radius: 8px;
    padding: 12px 18px;
    color: white;
    background: #2563eb;
    cursor: pointer;
    font-weight: bold;
    white-space: nowrap;
  }
  button.secondary-btn {
    background: #334155;
  }
  
  .sample-links {
    margin-top: 15px;
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    align-items: center;
  }
  .sample-chip {
    background: #263449;
    padding: 6px 12px;
    border-radius: 20px;
    font-size: 13px;
    cursor: pointer;
    border: 1px solid #475569;
  }
  
  .preview-section {
    margin-top: 25px;
    display: none;
    text-align: center;
  }
  .preview-section.active { display: block; }
  
  .media-wrapper {
    background: #0b1120;
    border-radius: 10px;
    padding: 15px;
    margin: 15px 0;
    border: 1px solid #334155;
    max-height: 450px;
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
  }
  .media-wrapper img, .media-wrapper video {
    max-width: 100%;
    max-height: 400px;
    border-radius: 8px;
    object-fit: contain;
  }
  .media-wrapper iframe {
    width: 100%;
    height: 400px;
    border: none;
    border-radius: 8px;
  }
  .audio-player-box {
    width: 100%;
    padding: 20px;
    text-align: center;
  }
  .audio-player-box audio { width: 100%; }

  .download-btn {
    display: inline-block;
    width: 100%;
    text-align: center;
    text-decoration: none;
    color: white;
    background: #16a34a;
    padding: 14px;
    border-radius: 8px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    border: none;
    margin-top: 10px;
  }

  .status-msg {
    margin-top: 10px;
    font-size: 14px;
    color: #ef4444;
  }
  .progress-bar {
    width: 100%;
    height: 8px;
    background: #334155;
    border-radius: 4px;
    overflow: hidden;
    margin-top: 10px;
    display: none;
  }
  .progress-fill {
    height: 100%;
    background: #16a34a;
    width: 0%;
    transition: width 0.2s;
  }

  footer {
    text-align: center;
    padding: 20px;
    color: #bdc9dc;
    border-top: 1px solid #334155;
    margin-top: auto;
  }
  
  @media(max-width: 600px) {
    .input-group { flex-direction: column; }
    button.action-btn { width: 100%; }
  }
</style>
</head>
<body>

<header>
  <h1>📥 My Download Hub</h1>
</header>

<main>
  <div class="hero">
    <h2>अपनी वेबसाइट पर ही प्रिव्यू देखें और डाउनलोड करें ❤️</h2>
    <p class="muted">किसी भी फोटो, वीडियो, MP3 या PDF का सीधा लिंक यहाँ डालें।</p>
  </div>

  <div class="card-panel">
    <label for="urlInput" class="input-label">फाइल/मीडिया का लिंक पेस्ट करें (URL):</label>
    <div class="input-group">
      <input id="urlInput" type="url" placeholder="https://example.com/file.mp4 या photo.jpg">
      <button class="action-btn secondary-btn" id="pasteBtn">📋 Paste</button>
      <button class="action-btn" id="fetchBtn">🔍 Preview & Download</button>
    </div>

    <!-- तुरंत टेस्ट करने के लिए सैंपल लिंक्स -->
    <div class="sample-links">
      <span class="muted">टेस्ट करें:</span>
      <span class="sample-chip" onclick="setLink('https://images.unsplash.com/photo-1575936123452-b67c3203c357?w=800', 'image')">🖼️ HD Photo</span>
      <span class="sample-chip" onclick="setLink('https://www.w3schools.com/html/mov_bbb.mp4', 'video')">🎬 MP4 Video</span>
      <span class="sample-chip" onclick="setLink('https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3', 'audio')">🎵 MP3 Audio</span>
    </div>

    <p id="statusMsg" class="status-msg"></p>

    <!-- इन-साइट प्रिव्यू सेक्शन (यहीं पर मीडिया दिखेगी) -->
    <div class="preview-section" id="previewSection">
      <h3 id="previewTitle" style="margin-bottom: 10px;">मीडिया प्रिव्यू</h3>
      
      <div class="media-wrapper" id="mediaContainer">
        <!-- फोटो/वीडियो/ऑडियो यहाँ लोड होगा -->
      </div>

      <div class="progress-bar" id="progressBar">
        <div class="progress-fill" id="progressFill"></div>
      </div>

      <button id="downloadBtn" class="download-btn">⬇ Direct Download File</button>
    </div>
  </div>
</main>

<footer>
  © <span id="year"></span> My Download Hub - All Rights Reserved
</footer>

<script>
"use strict";

const $= id => document.getElementById(id);$("year").textContent = new Date().getFullYear();

let currentMediaUrl = "";

// Paste बटन का काम
$("pasteBtn").addEventListener("click", async () => {
  try {
    const text = await navigator.clipboard.readText();
    $("urlInput").value = text;
  } catch (err) {
    alert("क्लिपबोर्ड एक्सेस करने की अनुमति नहीं मिली। कृपया खुद पेस्ट करें।");
  }
});

// टेस्ट लिंक्स सेट करने के लिए
function setLink(url, type) {
  $("urlInput").value = url;
  processLink();
}

// लिंक को प्रोसेस करके प्रिव्यू दिखाना
function processLink() {
  const url = $("urlInput").value.trim();
  const statusMsg = $("statusMsg");
  const previewSection = $("previewSection");
  const mediaContainer = $("mediaContainer");

  statusMsg.textContent = "";
  previewSection.classList.remove("active");
  mediaContainer.innerHTML = "";

  if (!url) {
    statusMsg.textContent = "कृपया पहले कोई लिंक दर्ज करें!";
    return;
  }

  currentMediaUrl = url;
  const cleanUrl = url.split('?')[0].toLowerCase();

  // 1. Photo Preview
  if (cleanUrl.match(/\.(jpeg|jpg|png|webp|gif|svg)$/i) || url.includes("images.unsplash.com")) {
    const img = document.createElement("img");
    img.src = url;
    img.alt = "Preview Photo";
    img.onerror = () => { statusMsg.textContent = "फोटो लोड नहीं हो सकी। लिंक चेक करें।"; };
    mediaContainer.appendChild(img);
    previewSection.classList.add("active");
  } 
  // 2. Video Preview
  else if (cleanUrl.match(/\.(mp4|webm|ogg)$/i) || url.includes("mov_bbb")) {
    const video = document.createElement("video");
    video.src = url;
    video.controls = true;
    video.autoplay = true;
    mediaContainer.appendChild(video);
    previewSection.classList.add("active");
  } 
  // 3. Audio Preview
  else if (cleanUrl.match(/\.(mp3|wav|m4a)$/i) || url.includes("soundhelix")) {
    const audioBox = document.createElement("div");
    audioBox.className = "audio-player-box";
    audioBox.innerHTML = `
      <div style="font-size:50px; margin-bottom:10px;">🎵</div>
      <audio controls autoplay src="${url}"></audio>
    `;
    mediaContainer.appendChild(audioBox);
    previewSection.classList.add("active");
  } 
  // 4. PDF / Other Files
  else if (cleanUrl.endsWith(".pdf")) {
    const iframe = document.createElement("iframe");
    iframe.src = url;
    mediaContainer.appendChild(iframe);
    previewSection.classList.add("active");
  } 
  // 5. General Direct Links
  else {
    mediaContainer.innerHTML = `<p style="padding:20px; color:#bdc9dc;">📦 फ़ाइल प्रिव्यू उपलब्ध नहीं है, लेकिन आप इसे नीचे दिए गए बटन से सीधे अपनी डिवाइस में डाउनलोड कर सकते हैं।</p>`;
    previewSection.classList.add("active");
  }
}

$("fetchBtn").addEventListener("click", processLink);

// बिना किसी दूसरी वेबसाइट पर गए सीधे मोबाइल/कंप्यूटर में डाउनलोड करने का तरीका (Blob Download)
$("downloadBtn").addEventListener("click", async () => {
  if (!currentMediaUrl) return;

  const downloadBtn = $("downloadBtn");
  const progressBar = $("progressBar");
  const progressFill = $("progressFill");

  downloadBtn.disabled = true;
  downloadBtn.textContent = "⏳ Downloading...";
  progressBar.style.display = "block";
  progressFill.style.width = "20%";

  try {
    const response = await fetch(currentMediaUrl);
    progressFill.style.width = "60%";
    const blob = await response.blob();
    progressFill.style.width = "100%";

    // फाइल का नाम निकालना
    let fileName = currentMediaUrl.split('/').pop().split('?')[0];
    if (!fileName || fileName.length > 30) fileName = "downloaded_file";

    const blobUrl = window.URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.style.display = "none";
    a.href = blobUrl;
    a.download = fileName;
    document.body.appendChild(a);
    a.click();
    
    window.URL.revokeObjectURL(blobUrl);
    document.body.removeChild(a);

    downloadBtn.textContent = "✅ Download Complete!";
    setTimeout(() => {
      downloadBtn.disabled = false;
      downloadBtn.textContent = "⬇ Direct Download File";
      progressBar.style.display = "none";
      progressFill.style.width = "0%";
    }, 2000);

  } catch (error) {
    // अगर सर्वर पर CORS सिक्योरिटी लगी हो, तो डायरेक्ट डाउनलोड लिंक खोलें
    const a = document.createElement("a");
    a.href = currentMediaUrl;
    a.download = "download";
    a.target = "_blank";
    a.click();

    downloadBtn.disabled = false;
    downloadBtn.textContent = "⬇ Direct Download File";
    progressBar.style.display = "none";
  }
});
</script>

</body>
</html>
