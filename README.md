
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Easy Downloader</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f4f8;
      text-align: center;
      padding: 25px 12px;
    }
    .box {
      max-width: 420px;
      margin: 35px auto;
      padding: 22px;
      background: white;
      border-radius: 15px;
      box-shadow: 0 4px 15px #0002;
    }
    input, button {
      box-sizing: border-box;
      width: 100%;
      padding: 13px;
      margin-top: 12px;
      border-radius: 8px;
      font-size: 16px;
    }
    input { border: 1px solid #bbb; }
    button {
      background: #1769e0;
      color: white;
      border: 0;
    }
    #message { overflow-wrap: anywhere; }
  </style>
</head>
<body>
  <div class="box">
    <h1>Easy Downloader</h1>
    <p>Apna direct file link yahan paste karein.</p>
    <input id="url" type="url" placeholder="https://example.com/file.mp4">
    <button onclick="downloadFile()">Download</button>
    <p id="message"></p>
  </div>

  <script>
    
function downloadFile(
  
async function downloadFile() {
  const input = document.getElementById("url");
  const message = document.getElementById("message");
  const url = input.value.trim();

  if (!/^https?:\/\//i.test(url)) {
    message.textContent = "Sahi https:// ya http:// link daalein.";
    return;
  }

  message.textContent = "Thoda Ruke Jai shree Ram...";

  try {
    const response = await fetch(url);

    if (!response.ok) {
      throw new Error("Download nahi ho saka");
    }

    const blob = await response.blob();
    const objectUrl = URL.createObjectURL(blob);
    const link = document.createElement("a");

    const filename =
      decodeURIComponent(url.split("/").pop().split("?")[0]) ||
      "download";

    link.href = objectUrl;
    link.download = filename;
    document.body.appendChild(link);
    link.click();
    link.remove();

    setTimeout(() => URL.revokeObjectURL(objectUrl), 60000);
    message.textContent = "Download shuru ho gaya!";
  } catch (error) {
    message.textContent =
      "Direct download block hua. Neeche link kholkar try karein.";

    const link = document.createElement("a");
    link.href = url;
    link.target = "_blank";
    link.rel = "noopener noreferrer";
    link.textContent = "File ka link kholein";
    message.appendChild(document.createElement("br"));
    message.appendChild(link);
  }
}
    


      message.textContent =
        "Link kholne ki koshish ki gayi. Agar download na ho, to khula hua page check karein.";
    }
  </script>
</body>
</html>
