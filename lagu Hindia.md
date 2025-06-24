# kholid
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Music Player</title>
  <link href="https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
      padding: 0;
      margin: 0;
    }

    body {
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(to right, #000000, #434343);
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      color: #fff;
    }

    .player {
      background: #1e1e1e;
      padding: 30px;
      border-radius: 25px;
      box-shadow: 0 10px 50px rgba(0, 0, 0, 0.6);
      width: 360px;
      text-align: center;
    }

    .cover img {
      width: 100%;
      height: auto;
      border-radius: 20px;
      object-fit: contain;
      box-shadow: 0 6px 20px rgba(0, 0, 0, 0.7);
    }

    h3 {
      margin: 15px 0 5px;
      font-size: 1.4rem;
    }

    p {
      color: #bbb;
      font-size: 0.95rem;
    }

    .play-button, .repeat-button {
      margin: 20px 10px;
      font-size: 2.2rem;
      cursor: pointer;
      transition: 0.3s;
      display: inline-block;
    }

    .play-button:hover, .repeat-button:hover {
      color: #1db954;
      transform: scale(1.3);
    }

    input[type="range"] {
      width: 100%;
      appearance: none;
      height: 6px;
      background: #444;
      border-radius: 5px;
      outline: none;
      margin-top: 15px;
    }

    input[type="range"]::-webkit-slider-thumb {
      appearance: none;
      width: 16px;
      height: 16px;
      border-radius: 50%;
      background: #1db954;
      box-shadow: 0 0 5px #1db954;
      cursor: pointer;
    }

    .time {
      display: flex;
      justify-content: space-between;
      font-size: 0.8rem;
      color: #aaa;
      margin-top: 5px;
    }

    .visualizer {
      display: flex;
      justify-content: center;
      gap: 5px;
      margin-top: 20px;
    }

    .bar {
      width: 5px;
      height: 15px;
      background: #1db954;
      border-radius: 3px;
      animation: bounce 1s infinite ease-in-out;
    }

    .bar:nth-child(2) { animation-delay: 0.1s; }
    .bar:nth-child(3) { animation-delay: 0.2s; }
    .bar:nth-child(4) { animation-delay: 0.3s; }
    .bar:nth-child(5) { animation-delay: 0.4s; }

    @keyframes bounce {
      0%, 100% { height: 15px; }
      50% { height: 35px; }
    }

    .credits {
      margin-top: 25px;
      font-size: 0.85rem;
      color: #888;
      line-height: 1.5;
    }
  </style>
</head>
<body>

<div class="player">
  <div class="cover">
    <img src="https://files.catbox.moe/iss168.jpg" alt="Cover Art">
  </div>
  <h3>Hindia - Doves, '25 on Blank Canvas</h3>
  <p>Mixtape Visualizer</p>

  <div class="play-button">
    <i class='bx bx-play' id="play-button"></i>
  </div>
  <div class="repeat-button">
    <i class='bx bx-repeat' id="repeat-button"></i>
  </div>

  <input type="range" id="progress" value="0">
  <div class="time">
    <span id="current-time">0:00</span>
    <span id="duration">0:00</span>
  </div>

  <div class="visualizer">
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
    <div class="bar"></div>
  </div>

  <div class="credits">
    <p>Pemilik Musik : Baskara Putra</p>
    <p>Pembuat Coding Web : M.Kholid FirzaTullah</p>
  </div>
</div>

<audio id="song" src="https://files.catbox.moe/xmxogc.mp3"></audio>

<script>
  const song = document.getElementById("song");
  const progress = document.getElementById("progress");
  const playBtn = document.getElementById("play-button");
  const repeatBtn = document.getElementById("repeat-button");
  const currentTimeEl = document.getElementById("current-time");
  const durationEl = document.getElementById("duration");

  function formatTime(seconds) {
    const mins = Math.floor(seconds / 60);
    const secs = Math.floor(seconds % 60);
    return `${mins}:${secs < 10 ? '0' : ''}${secs}`;
  }

  playBtn.addEventListener("click", () => {
    if (song.paused) {
      song.play();
      playBtn.classList.replace("bx-play", "bx-pause");
    } else {
      song.pause();
      playBtn.classList.replace("bx-pause", "bx-play");
    }
  });

  repeatBtn.addEventListener("click", () => {
    song.loop = !song.loop;
    repeatBtn.style.color = song.loop ? "#1db954" : "";
  });

  song.addEventListener("timeupdate", () => {
    progress.value = song.currentTime;
    currentTimeEl.textContent = formatTime(song.currentTime);
  });

  progress.addEventListener("input", () => {
    song.currentTime = progress.value;
  });

  song.addEventListener("loadedmetadata", () => {
    progress.max = song.duration;
    durationEl.textContent = formatTime(song.duration);
  });
</script>

</body>
</html>
