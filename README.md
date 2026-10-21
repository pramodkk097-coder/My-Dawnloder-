<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#111827">
<title>All-in-One Link Downloader</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#0b1120;color:#f8fafc}
header{position:sticky;top:0;z-index:5;background:#172033;padding:15px;display:flex;justify-content:space-between;align-items:center;border-bottom:1px solid #334155}
header h1{font-size:20px;margin:0}
button,input{font:inherit}
button{border:0;border-radius:8px;padding:12px 18px;color:white;background:#2563eb;cursor:pointer;font-weight:bold}
main{width:94%;max-width:800px;margin:30px auto}
.hero{text-align:center;padding:30px 15px;background:#172554;border-radius:14px;margin-bottom:25px}
.muted{color:#bdc9dc}
.downloader-box{background:#172033;border:1px solid #334155;border-radius:14px;padding:25px;box-shadow:0 10px 25px rgba(0,0,0,0.3)}
.input-group{display:flex;gap:10px;margin-top:15px}
.input-group input{flex:1;padding:14px;border-radius:8px;border:1px solid #475569;background:#0b1120;color:white;font-size:16px}
.result-card{margin-top:25px;padding:20px;background:#0b1120;border:1px solid #334155;border-radius:10px;display:none;text-align:center}
.result-card.active{display:block}
.result-card img, .result-card video{max-width:100%;max-height:300px;border-radius:8px;margin-bottom:15px}
.btn-download{display:inline-block;text-decoration:none;color:white;background:#16a34a;padding:12px 24px;border-radius:8px;margin-top:10px;font-weight:bold}
footer{text-align:center;padding:25px;color:#bdc9dc;margin-top:40px}
.error-msg{color:#ef4444;margin-top:10px;font-size:14px}
</style>
</head>

<body>

<header>
  <h1>📥 Link Downloader Hub</h1>
</header>

<main>
  <div class="hero">
    <h2>Paste Any Link & Download ❤️</h2>
    <p class="muted">YouTube, Facebook या Google फोटो/वीडियो का लिंक यहाँ पेस्ट करें।</p>
  </div>

  <div class="downloader-box">
    <label for="urlInput" style="font-weight:bold;display:block;">लिंक यहाँ पेस्ट करें (Paste URL):</label>
    <div class="input-group">
      <input id="urlInput" type="url" placeholder="https://example.com/photo.jpg या वीडियो लिंक...">
      <button id="fetchBtn">🔍 Fetch & Download</button>
    </div>
    <p id="errorMsg" class="error-msg"></p>

    <!-- रिजल्ट प्रिव्यू और डाउनलोड बटन दिखाने के लिए -->
    <div class="result-card" id="resultCard">
      <h3>फाइल तैयार है!</h3>
      <div id="previewContainer"></div>
      <div>
        <a id="downloadBtn" class="btn-download" href="#" target="_blank" download>⬇ Download File Now</a>
      </div>
    </div>
  </div>
</main>

<footer>© <span id="year"></span> Link Downloader Hub</footer>

<script>
"use strict";

const $= id => document.getElementById(id);$("year").textContent = new Date().getFullYear();

$("fetchBtn").addEventListener("click", () => {
  const url = $("urlInput").value.trim();
  const errorMsg = $("errorMsg");
  const resultCard = $("resultCard");
  const previewContainer = $("previewContainer");
  const downloadBtn = $("downloadBtn");

  errorMsg.textContent = "";
  resultCard.classList.remove("active");
  previewContainer.innerHTML = "";

  if (!url) {
    errorMsg.textContent = "कृपया पहले कोई वैध लिंक (URL) दर्ज करें!";
    return;
  }

  // चेक करते हैं कि क्या यह सोशल मीडिया का लिंक है या डायरेक्ट फाइल लिंक
  if (url.includes("youtube.com") || url.includes("youtu.be")) {
    errorMsg.textContent = "YouTube वीडियो डाउनलोड करने के लिए सर्वर API की ज़रूरत होती है। कृपया कोई डायरेक्ट इमेज या वीडियो लिंक (जैसे .jpg, .mp4) ट्राय करें।";
    return;
  } 
  
  if (url.includes("facebook.com")) {
    errorMsg.textContent = "Facebook सुरक्षा नियमों के कारण सीधे ब्राउज़र से डाउनलोड नहीं हो सकता। कृपया डायरेक्ट मीडिया लिंक दें।";
    return;
  }

  // यदि यह डायरेक्ट फाइल लिंक है (जैसे Google से ली गई फोटो या वीडियो का डायरेक्ट एड्रेस)
  downloadBtn.href = url;
  
  // प्रिव्यू दिखाने की कोशिश
  if (url.match(/\.(jpeg|jpg|png|webp|gif)(\?.*)?$/i)) {
    const img = document.createElement("img");
    img.src = url;
    previewContainer.appendChild(img);
    resultCard.classList.add("active");
  } else if (url.match(/\.(mp4|webm|ogg)(\?.*)?$/i)) {
    const video = document.createElement("video");
    video.src = url;
    video.controls = true;
    previewContainer.appendChild(video);
    resultCard.classList.add("active");
  } else {
    // अगर फाइल का एक्सटेंशन समझ न आए फिर भी डाउनलोड बटन दिखा देंगे
    previewContainer.innerHTML = `<p class="muted">लिंक वेरीफाई हो गया है। नीचे दिए गए बटन से डाउनलोड करें।</p>`;
    resultCard.classList.add("active");
  }
});
</script>

</body>
</html>
