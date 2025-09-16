
<head>
   <head><!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-FLJE98C8M9"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-FLJE98C8M9');
</script></head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>incisid pixel hearts</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: repeating-linear-gradient(135deg, #fce4ec, #fce4ec 10px, #f8bbd0 10px, #f8bbd0 20px);
      font-family: 'Cursive', 'Comic Sans MS', cursive;
      text-align: center;
      touch-action: manipulation;
    }

    h1, h2, #counter {
      text-transform: lowercase;
    }

    #topbar {
      margin-top: 10px;
      line-height: 1.2;
    }

    h1 {
      font-size: 3.8em;
      color: #d45a7b;
      display: block;
      margin: 0;
      font-family: "Snell Roundhand", "Brush Script MT", cursive;
    }

    .subinfo {
      position: absolute;
      bottom: 70px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 1em;
      color: #3e1d24;
      font-weight: bold;
      display: flex;
      flex-direction: column;
      align-items: center;
      font-family: 'Cursive', 'Comic Sans MS', cursive;
      z-index: 1001;
    }

    #counter {
      font-size: 1em;
      font-weight: bold;
      color: #3e1d24;
      font-style: italic;
    }

    #celebration {
      position: absolute;
      top: 40%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 2em;
      color: #d50000;
      font-family: 'Cursive', 'Comic Sans MS', cursive;
      display: none;
      z-index: 1002;
    }

    #gameCanvas {
      display: block;
      margin: 0 auto;
      background-color: transparent;
      position: relative;
      z-index: 1;
      touch-action: manipulation;
    }

    .note {
      position: absolute;
      font-size: 1rem;
      font-family: 'Cursive', 'Comic Sans MS', cursive;
      color: #6d4c41;
      background: #ffe0e0;
      padding: 6px 10px;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      opacity: 0;
      animation: fadeIn 0.4s ease forwards;
      pointer-events: none;
      text-transform: lowercase;
      z-index: 10000;
      transform: translate(-50%, -100%);
    }

    @keyframes fadeIn {
      to {
        opacity: 1;
      }
    }

    #restartButton, #startButton {
      position: absolute;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background-color: #f8bbd0;
      color: #6d4c41;
      border: none;
      font-size: 1em;
      font-family: 'Cursive', 'Comic Sans MS', cursive;
      padding: 10px 20px;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.2);
      cursor: pointer;
      text-transform: lowercase;
      z-index: 1000;
    }
  </style>
</head>
<body>
  <div id="topbar">
    <h1>𝒾nci𝓈id pixel hearts</h1>
  </div>
  <canvas id="gameCanvas"></canvas>
  <div class="subinfo">
    <h2>(pop the hearts)</h2>
    <div id="counter">popped: 0 / 100</div>
  </div>
  <div id="celebration">yay! all hearts popped</div>
  <button id="startButton">start</button>
  <button id="restartButton" style="display: none;">restart</button>

  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');
    const counterDisplay = document.getElementById('counter');
    const restartButton = document.getElementById('restartButton');
    const startButton = document.getElementById('startButton');
    const celebration = document.getElementById('celebration');

    function setCanvasSize() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    setCanvasSize();
    window.addEventListener('resize', setCanvasSize);

    const affirmations = [
      "mi amor", "te amo inci", "te quiero mucho inci", "you are beautiful inci", "you are radiant inci", "my soulmate", "çox cəsarətlisən inci", "you are magical inci", "you've come a long way", "im so proud of you",
      "my baby", "im all yours", "inci & sid forever", "my eternal love", "you're my moon", "my moonlight", "keep going", "you're glowing", "you are doing so well!", "you're destined for the best",
      "yaxşı şeylər həmişə başınıza gələcək inci", "you are my baby", "my star", "mi estrella", "incilina", "you are divine", "sənin üçün darıxıram inci", "you are lovely", "you are everything to me", "my world",
      "mi florecita", "you inspire me", "i admire you", "i miss you so much", "i love you so much", "te quiero mucho", "özünüzə daha mehriban olun inci", "you are unique inci", "you are serene inci", "mi unica amor",
      "my only love", "you are perfect inci", "you are limitless inci", "mən sənə pərəstiş edirəm inci", "you are flawless", "you are the best", "my mircale", "you are luminous", "you are a blessing", "your energy is so captivating",
      "sən mənim günəşimsən inci", "you are vibrant", "you are abundant", "i love being yours", "i love you the most", "i miss you so much", "xoxo", "my electric love", "my diva", "you're doing amazing",
      "you're a darling", "mi luna", "mwah", "my favourite girl", "you got me captured mind and soul", "my forever", "i love you endlessly", "my eternal love", "my nerd", "all the best!",
      "mi miel", "you are blooming", "te amo", "mi universe", "my doll", "my precious", "my chess diva", "you are golden", "have faith in yourself", "xoxo",
      "kisses", "xoxo", "mi novia", "my ultimate", "xoxo", "mwah", "i miss you", "my soulmate", "my doll", "my perfect baby",
      "te amo mucho", "you are my summer miracle", "mən səni sevirəm inci", "sən zülmətin işığısan inci", "my safe place", "my happy place", "ay işığındasan inci", "you are ethereal", "you are celestial", "həyatımın sevgisi"
    ];

    let hearts = [];
    let poppedHearts = new Set();
    let animationFrame;

    function spawnHeart() {
      const x = Math.random() * canvas.width;
      const y = canvas.height + 50;
      const speedX = (Math.random() - 0.5) * 0.6;
      const speedY = -0.4 - Math.random() * 0.6;
      const index = Math.floor(Math.random() * affirmations.length);
      hearts.push({ x, y, speedX, speedY, index });
    }

    function drawHeart(ctx, x, y, size) {
      ctx.save();
      ctx.beginPath();
      ctx.moveTo(x, y);
      ctx.bezierCurveTo(x, y - size / 2, x - size, y - size / 2, x - size, y);
      ctx.bezierCurveTo(x - size, y + size, x, y + size * 1.5, x, y + size * 2);
      ctx.bezierCurveTo(x, y + size * 1.5, x + size, y + size, x + size, y);
      ctx.bezierCurveTo(x + size, y - size / 2, x, y - size / 2, x, y);
      ctx.fillStyle = 'rgba(153, 0, 51, 0.6)';
      ctx.fill();
      ctx.restore();
    }

    function drawHearts() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      hearts.forEach(h => {
        drawHeart(ctx, h.x, h.y, 48);
        h.x += h.speedX;
        h.y += h.speedY;
      });

      while (poppedHearts.size < 100 && hearts.length < 50) {
        spawnHeart();
      }

      if (poppedHearts.size === 100) {
        celebration.style.display = 'block';
      }

      animationFrame = requestAnimationFrame(drawHearts);
    }

    function updateCounter() {
      counterDisplay.textContent = `popped: ${poppedHearts.size} / 100`;
    }

    function handlePop(x, y) {
      for (let i = 0; i < hearts.length; i++) {
        let h = hearts[i];
        if (!poppedHearts.has(h) && x > h.x - 36 && x < h.x + 36 && y > h.y && y < h.y + 72) {
          poppedHearts.add(h);
          showNote(h.x, h.y - 60, affirmations[h.index]); // show note above heart
          updateCounter();
          hearts.splice(i, 1); // remove from hearts list
          return;
        }
      }
    }

    canvas.addEventListener('click', e => {
      const rect = canvas.getBoundingClientRect();
      handlePop(e.clientX - rect.left, e.clientY - rect.top);
    });

    canvas.addEventListener('touchstart', e => {
      const rect = canvas.getBoundingClientRect();
      const touch = e.touches[0];
      handlePop(touch.clientX - rect.left, touch.clientY - rect.top);
    });

    function showNote(x, y, text) {
      const note = document.createElement('div');
      note.className = 'note';
      note.innerText = text;
      note.style.left = `${x}px`;
      note.style.top = `${y}px`;
      document.body.appendChild(note);
      setTimeout(() => note.remove(), 4000);
    }

    restartButton.addEventListener('click', () => {
      hearts = [];
      poppedHearts.clear();
      updateCounter();
      celebration.style.display = 'none';
      for (let i = 0; i < 20; i++) spawnHeart();
    });

    startButton.addEventListener('click', () => {
      startButton.style.display = 'none';
      restartButton.style.display = 'block';
      for (let i = 0; i < 20; i++) spawnHeart();
      drawHearts();
      updateCounter();
    });
  </script>
</body>
</html>
