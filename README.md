My dawnloader 
<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>My Download Website</title>

  <meta name="description" content="PDF, MP3, MP4 और ZIP फाइलें आसानी से डाउनलोड करें।">

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
      background: #2563eb;
      color: white;
      text-align: center;
      padding: 30px 15px;
    }

    header h1 {
      margin: 0 0 10px;
      font-size: 30px;
    }

    header p {
      margin: 0;
      font-size: 16px;
    }

    .container {
      width: 92%;
      max-width: 900px;
      margin: 30px auto;
    }

    .card {
      background: white;
      padding: 22px;
      margin-bottom: 18px;
      border-radius: 12px;
      box-shadow: 0 3px 12px rgba(0, 0, 0, 0.08);
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 15px;
    }

    .file-info h2 {
      margin: 0 0 8px;
      font-size: 20px;
    }

    .file-info p {
      margin: 0;
      color: #64748b;
      font-size: 14px;
      overflow-wrap: anywhere;
    }

    .download-btn {
      display: inline-block;
      background: #16a34a;
      color: white;
      text-decoration: none;
      padding: 12px 18px;
      border-radius: 8px;
      font-weight: bold;
      white-space: nowrap;
      transition: background 0.2s;
    }

    .download-btn:hover {
      background: #15803d;
    }

    footer {
      text-align: center;
      padding: 20px;
      color: #64748b;
      font-size: 14px;
    }

    @media (max-width: 520px) {
      header h1 {
        font-size: 25px;
      }

      .card {
        flex-direction: column;
        align-items: flex-start;
      }

      .download-btn {
        width: 100%;
        text-align: center;
      }
    }
  </style>
</head>

<body>

  <header>
    <h1>My Download Website</h1>
    <p>PDF, MP3, MP4 और ZIP फ़ाइलें डाउनलोड करें</p>
  </header>

  <main class="container">

    <!-- PDF DOWNLOAD -->
    <section class="card">
      <div class="file-info">
        <h2>📄 PDF File</h2>
        <p>फ़ाइल: sample.pdf</p>
      </div>

      <a
        class="download-btn"
        href="downloads/sample.pdf"
        download="sample.pdf">
        ⬇ Download PDF
      </a>
    </section>

    <!-- MP3 DOWNLOAD -->
    <section class="card">
      <div class="file-info">
        <h2>🎵 MP3 Audio</h2>
        <p>फ़ाइल: sample.mp3</p>
      </div>

      <a
        class="download-btn"
        href="downloads/sample.mp3"
        download="sample.mp3">
        ⬇ Download MP3
      </a>
    </section>

    <!-- MP4 DOWNLOAD -->
    <section class="card">
      <div class="file-info">
        <h2>🎬 MP4 Video</h2>
        <p>फ़ाइल: sample.mp4</p>
      </div>

      <a
        class="download-btn"
        href="downloads/sample.mp4"
        download="sample.mp4">
        ⬇ Download MP4
      </a>
    </section>

    <!-- ZIP DOWNLOAD -->
    <section class="card">
      <div class="file-info">
        <h2>📦 ZIP File</h2>
        <p>फ़ाइल: sample.zip</p>
      </div>

      <a
        class="download-btn"
        href="downloads/sample.zip"
        download="sample.zip">
        ⬇ Download ZIP
      </a>
    </section>

  </main>

  <footer>
    <p>© 2026 My Download Website</p>
  </footer>

</body>
</html>
