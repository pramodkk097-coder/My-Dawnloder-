# My-Dawnloder
<!DOCTYPE html>
<html lang="hi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Easy Downloader</title>
<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f0f4f8;color:#172033;min-height:100vh;display:grid;place-items:center;padding:20px}
.card{background:white;width:100%;max-width:480px;padding:28px 22px;border-radius:20px;box-shadow:0 8px 30px #17203318}
.logo{text-align:center;font-size:42px}
h1{text-align:center;margin:8px 0;color:#176b48}
p{text-align:center;color:#64748b;line-height:1.5}
label{display:block;font-weight:bold;margin:22px 0 8px}
input{width:100%;padding:14px;border:1px solid #cbd5e1;border-radius:10px;font-size:16px}
button,.open{display:block;width:100%;padding:14px;margin-top:12px;border:0;border-radius:10px;background:#16804a;color:white;font-weight:bold;font-size:16px;text-align:center;text-decoration:none;cursor:pointer}
.open{background:#e5f3eb;color:#176b48}
#msg{font-size:14px;overflow-wrap:anywhere}
small{display:block;color:#64748b;line-height:1.6;margin-top:18px}
</style>
</head>
<body>
<main class="card">
<div class="logo">⬇️</div>
<h1>Easy Downloader</h1>
<p>Apni file ka direct link daalein aur download karein.</p>
<form id="form">
<label for="url">File ka link</label>
<input id="url" type="url" placeholder="https://example.com/file.pdf" required>
<button type="submit">Download / Open File</button>
</form>
<a id="open" class="open" hidden target="_blank" rel="noopener noreferrer">Link kholein</a>
<p id="msg" role="status"></p>
<small>Yeh tool direct file links ke liye hai. Download kaam karna source website aur uski permissions par nirbhar karta hai. Private links aur login ki zaroorat wale links support nahi hote.</small>
</main>
<script>
const form=document.getElementById('form');
const input=document.getElementById('url');
const msg=document.getElementById('msg');
const openLink=document.getElementById('open');
form.addEventListener('submit',function(e){
e.preventDefault();
let u;
try{u=new URL(input.value.trim())}catch{
msg.textContent='Sahi link daalein.';return;
}
if(!['http:','https:'].includes(u.protocol)){
msg.textContent='Sirf http ya https links allowed hain.';return;
}
openLink.href=u.href;
openLink.hidden=false;
msg.textContent='Link taiyar hai. Agar file khud download na ho, Link kholein par tap karein.';
const a=document.createElement('a');
a.href=u.href;
a.rel='noopener noreferrer';
a.download='';
document.body.appendChild(a);
a.click();
a.remove();
});
</script>
</body>
</html>
