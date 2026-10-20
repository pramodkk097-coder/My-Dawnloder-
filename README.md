
function downloadFile() {
  const input = document.getElementById("url");
  const message = document.getElementById("message");
  const url = input.value.trim();

  if (!/^https?:\/\//i.test(url)) {
    message.textContent = "Kripya sahi http ya https link daalein.";
    return;
  }

  message.textContent = "Download shuru karne ki koshish ho rahi hai...";

  const link = document.createElement("a");
  link.href = url;
  link.target = "_blank";
  link.rel = "noopener noreferrer";
  link.download = "";
  document.body.appendChild(link);
  link.click();
  link.remove();
}
