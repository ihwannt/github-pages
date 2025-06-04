<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Kisah Ihwan King Heart - Versi Suara & Cerita</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background: #f2e7f9;
    margin: 0;
    padding: 0;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    min-height: 100vh;
    color: #333;
  }
  .container {
    max-width: 600px;
    background: white;
    padding: 20px;
    margin-top: 30px;
    border-radius: 12px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }
  #text {
    font-size: 18px;
    min-height: 140px;
    margin-bottom: 20px;
    transition: opacity 0.5s;
  }
  .fade {
    opacity: 0;
  }
  #char-img {
    width: 100%;
    max-height: 300px;
    object-fit: contain;
    border-radius: 12px;
    margin-bottom: 20px;
  }
  .game-box {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }
  .choice-button {
    padding: 12px;
    background: #a56de0;
    border: none;
    color: white;
    border-radius: 8px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  .choice-button:hover {
    background: #854ec1;
  }
  .music-controls {
    margin-top: 15px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .music-controls button {
    padding: 6px 12px;
    font-size: 14px;
    border: none;
    border-radius: 6px;
    background: #7a4d99;
    color: white;
    cursor: pointer;
  }
  .music-controls button:hover {
    background: #623a7a;
  }
</style>
</head>
<body>
  <div class="container">
    <div id="text"></div>
    <img id="char-img" src="" alt="Karakter" style="display:none"/>
    <div class="game-box"></div>
    <div class="music-controls">
      <button id="btn-play">Play Musik</button>
      <button id="btn-pause" style="display:none;">Pause Musik</button>
    </div>
    <audio id="bg-music" loop>
      <source src="https://cdn.pixabay.com/download/audio/2022/11/26/audio_4a97070f2d.mp3?filename=chill-beats-ambient-11276.mp3" type="audio/mpeg" />
      <!-- Bebas diganti dengan link musik lain -->
    </audio>
    <audio id="click-sound">
      <source src="https://cdn.pixabay.com/download/audio/2022/03/25/audio_5a96a5d2bb.mp3?filename=mouse-click-12645.mp3" type="audio/mpeg" />
      <!-- Efek klik -->
    </audio>
  </div>

<script>
  let scoreRisti = 0;
  let scoreAsti = 0;
  const text = document.getElementById("text");
  const charImg = document.getElementById("char-img");
  const gameBox = document.querySelector(".game-box");
  const bgMusic = document.getElementById("bg-music");
  const clickSound = document.getElementById("click-sound");
  const btnPlay = document.getElementById("btn-play");
  const btnPause = document.getElementById("btn-pause");

  btnPlay.onclick = () => {
    bgMusic.play();
    btnPlay.style.display = "none";
    btnPause.style.display = "inline-block";
  };
  btnPause.onclick = () => {
    bgMusic.pause();
    btnPause.style.display = "none";
    btnPlay.style.display = "inline-block";
  };

  function playClick() {
    clickSound.currentTime = 0;
    clickSound.play();
  }

  function setScene(html, imgUrl, buttons = []) {
    text.classList.remove("fade");
    void text.offsetWidth;
    text.classList.add("fade");

    text.innerHTML = html;

    if (imgUrl) {
      charImg.src = imgUrl;
      charImg.style.display = "block";
    } else {
      charImg.style.display = "none";
    }

    const oldButtons = document.querySelectorAll(".choice-button");
    oldButtons.forEach(btn => btn.remove());

    buttons.forEach(([label, nextStep]) => {
      const btn = document.createElement("button");
      btn.className = "choice-button";
      btn.textContent = label;
      btn.onclick = () => {
        playClick();
        step(nextStep);
      };
      gameBox.appendChild(btn);
    });
  }

  function step(pilihan) {
    switch (pilihan) {
      case 1:
        scoreRisti++;
        setScene(
          `Ihwan membuka notifikasi itu dan tiba-tiba muncul chat dari seseorang bernama <b>Risti</b>.<br><br>
          "Ihwan... apa kamu masih ingat janjimu di SMA dulu?"<br><br>
          Ihwan mulai bingung dan jantungnya berdetak kencang...`,
          "https://cdn.pixabay.com/photo/2021/12/11/18/43/girl-6863646_1280.png",
          [["Balas: 'Risti? Janji yang mana ya?'", 3], ["Diam saja dan kepoin profilnya", 4]]
        );
        break;
      case 2:
        scoreAsti++;
        setScene(
          `Ihwan memilih tidur lagi. Dalam mimpinya, dia masuk ke dunia aneh penuh cahaya merah muda.<br><br>
          Tiba-tiba muncul seorang cewek galak bernama <b>Asti</b>.<br><br>
          "Hei! Kamu telat datang ke janji kita!"<br><br>
          Ihwan: "Janji apa ya...?"<br><br>
          Asti menatap tajam sambil nyubit pipi Ihwan...`,
          "https://cdn.pixabay.com/photo/2022/06/30/13/20/girl-7293744_1280.png",
          [["Minta maaf sambil bingung", 5], ["Lari dari Asti!", 6]]
        );
        break;
      case 3:
        scoreRisti++;
        setScene(
          `"Janji di bukit belakang sekolah... kamu bilang bakal balik lagi 5 tahun setelah kelulusan."<br><br>
          Ihwan menatap jam. Hari ini... tepat 5 tahun sejak mereka lulus!<br><br>
          "Kamu masih mau menepati janji itu?" tanya Risti.`,
          null,
          [["Temui Risti di bukit itu", 7], ["Tolak, bilang kamu sibuk", 8]]
        );
        break;
      case 4:
        scoreRisti++;
        setScene(
          `Ihwan membuka profil Risti. Banyak foto-foto kenangan masa SMA, termasuk satu foto...<br><br>
          Mereka berdua di bukit, tersenyum dengan tulisan tangan: "5 tahun lagi, di tempat ini."<br><br>
          "Apa aku pernah janji sekuat itu...?" pikir Ihwan.`,
          null,
          [["Langsung ke bukit itu diam-diam", 7], ["Chat: 'Maaf, aku nggak siap ketemu'", 8]]
        );
        break;
      case 5:
        scoreAsti++;
        setScene(
          `"Maaf... aku nggak ingat janji itu, tapi—"<br><br>
          Asti memotong: "Waktu di dunia mimpi ini aneh. Kamu mungkin lupa, tapi aku menunggumu di sini setiap malam."<br><br>
          Cahaya di sekeliling berubah jadi ungu pekat.`,
          null,
          [["Tanya apa yang sebenarnya terjadi", 9], ["Coba bangun dari mimpi", 10]]
        );
        break;
      case 6:
        scoreAsti++;
        setScene(
          `Ihwan berlari, tapi dunia di sekitarnya seperti melengkung. Dia kembali ke tempat yang sama, dan Asti berdiri di depan pintu merah besar.<br><br>
          "Kalau kamu masuk ke sini... kamu akan tahu semuanya."<br><br>`,
          null,
          [["Masuk pintu merah", 9], ["Menolak masuk dan teriak 'Bangun!'", 10]]
        );
        break;
      case 7:
        setScene(
          `Ihwan sampai di bukit. Angin berhembus pelan. Di sana, Risti sudah menunggu, mengenakan baju merah muda yang sama seperti di foto lama.<br><br>
          Mereka duduk bersama dan berbicara lama, mengungkap rasa yang tertahan selama 5 tahun...<br><br>
          <b>Ending: Cinta yang Tak Pernah Luntur</b> ❤️`,
          "https://cdn.pixabay.com/photo/2023/04/24/20/39/couple-7949206_1280.jpg"
        );
        break;
      case 8:
        setScene(
          `Ihwan memutuskan untuk tidak bertemu. Risti hanya menjawab, "Baiklah... Mungkin memang hanya aku yang masih berharap."<br><br>
          Sejak itu, notifikasi dari Risti tidak pernah muncul lagi...<br><br>
          <b>Ending: Janji yang Terkubur Waktu</b> 💔`,
          null
        );
        break;
      case 9:
        setScene(
          `Asti membawa Ihwan ke ruang cahaya. Di dalamnya ada kenangan: potongan mimpi, waktu yang dibekukan, dan... momen saat Ihwan kecil menyelamatkan Asti dari kecelakaan.<br><br>
          "Aku... roh dari masa lalu yang terus menunggumu di dunia tidur."<br><br>
          Air mata mengalir di pipi Ihwan.`,
          null,
          [["Peluk Asti dan ucapkan terima kasih", 11], ["Tinggalkan dia dan pergi dari dunia mimpi", 12]]
        );
        break;
      case 10:
        setScene(
          `Ihwan mencoba bangun. Tubuhnya berat... tapi perlahan dunia mimpi runtuh.<br><br>
          Saat membuka mata, dia merasa aneh... di tangannya ada pita merah... milik Asti?<br><br>
          <b>Ending: Kenangan dari Dunia Lain</b> 🌙`,
          null
        );
        break;
      case 11:
        setScene(
          `Ihwan memeluk Asti. Dunia di sekitar menjadi hangat, berubah jadi taman bunga.<br><br>
          "Mulai malam ini... aku takkan menghilang lagi," bisik Asti.<br><br>
          Sejak itu, setiap mimpi Ihwan selalu ditemani senyum manis Asti...<br><br>
          <b>Ending: Penjaga Mimpi</b> 💖`,
          null
        );
        break;
      case 12:
        setScene(
          `Ihwan meninggalkan Asti, yang tersenyum sedih di kejauhan.<br><br>
          Dunia mimpi tertutup, dan dia tak pernah melihat Asti lagi...<br><br>
          Namun setiap kali tidur, hatinya terasa kosong.<br><br>
          <b>Ending: Yang Tak Sempat Dijaga</b> 🌌`,
          null
        );
        break;
      default:
        setScene(
          `Selamat datang di Kisah Ihwan King Heart!<br><br>
          Klik salah satu tombol di bawah untuk memulai cerita.`,
          null,
          [["Mulai cerita dengan Risti", 1], ["Mulai cerita dengan Asti", 2]]
        );
    }
  }

  // Mulai game di awal
  step();
</script>
</body>
</html>
