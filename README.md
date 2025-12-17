<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Julki Dwie</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #0f0f14;
    color: white;
    text-align: center;
}

header {
    padding: 50px 20px;
    background: linear-gradient(135deg, #ff4fd8, #7a4dff);
}

header h1 {
    font-size: 42px;
    margin-bottom: 10px;
}

section {
    padding: 40px 20px;
}

.box {
    max-width: 900px;
    margin: auto;
}

textarea {
    width: 100%;
    height: 100px;
    border-radius: 10px;
    border: none;
    padding: 10px;
    margin-top: 10px;
}

button {
    background: #ff4fd8;
    border: none;
    padding: 12px 25px;
    color: white;
    border-radius: 30px;
    cursor: pointer;
    margin-top: 10px;
}

img {
    max-width: 100%;
    border-radius: 15px;
    margin-top: 20px;
}

video {
    width: 100%;
    border-radius: 15px;
    margin-top: 20px;
}

footer {
    padding: 20px;
    opacity: 0.6;
}
</style>
</head>

<body>

<header>
    <h1>👯‍♀️ Julki Dwie</h1>
    <p>Julka Miłek & Julia Chomicz</p>
</header>

<section class="box">
    <h2>💬 Nasze śmieszne teksty</h2>
    <textarea id="textInput" placeholder="Napisz coś śmiesznego..."></textarea>
    <button onclick="saveText()">Zapisz</button>
    <p id="savedText"></p>
</section>

<section class="box">
    <h2>📸 Zdjęcie dnia (co 24h)</h2>
    <input type="file" id="photoInput">
    <button onclick="savePhoto()">Dodaj zdjęcie</button>
    <img id="dailyPhoto">
</section>

<section class="box">
    <h2>🎥 Nasze filmiki</h2>
    <input type="file" id="videoInput">
    <button onclick="saveVideo()">Dodaj film</button>
    <video id="video" controls></video>
</section>

<footer>
    © 2025 Julki Dwie 💗
</footer>

<script>
function saveText() {
    const text = document.getElementById("textInput").value;
    localStorage.setItem("funText", text);
    document.getElementById("savedText").innerText = text;
}

document.getElementById("savedText").innerText =
    localStorage.getItem("funText") || "";

function savePhoto() {
    const file = document.getElementById("photoInput").files[0];
    if (!file) return;

    const reader = new FileReader();
    reader.onload = function () {
        const now = Date.now();
        localStorage.setItem("photoTime", now);
        localStorage.setItem("dailyPhoto", reader.result);
        document.getElementById("dailyPhoto").src = reader.result;
    };
    reader.readAsDataURL(file);
}

const photoTime = localStorage.getItem("photoTime");
if (photoTime && Date.now() - photoTime < 86400000) {
    document.getElementById("dailyPhoto").src =
        localStorage.getItem("dailyPhoto");
}

function saveVideo() {
    const file = document.getElementById("videoInput").files[0];
    if (!file) return;

    const url = URL.createObjectURL(file);
    document.getElementById("video").src = url;
}
</script>

</body>
</html>
