<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Surprise Graduation Letter</title>
  <style>
    body {
      margin: 0;
      font-family: 'Georgia', serif;
      background: linear-gradient(to right, #fdfbfb, #ebedee);
      overflow: hidden;
    }

    .container {
      max-width: 800px;
      margin: 60px auto;
      background: white;
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 0 25px rgba(0, 0, 0, 0.15);
      text-align: center;
      position: relative;
      z-index: 2;
    }

    h1 {
      font-size: 2.8rem;
      color: #2d3436;
      margin-bottom: 20px;
      animation: popIn 1s ease;
    }

    .letter {
      font-size: 1.2rem;
      line-height: 1.6;
      color: #34495e;
      white-space: pre-line;
      display: inline-block;
      text-align: left;
      min-height: 200px;
    }

    .signature {
      margin-top: 40px;
      font-style: italic;
      font-size: 1.2rem;
      color: #2c3e50;
    }

    #cap {
      width: 100px;
      position: absolute;
      top: -40px;
      left: calc(50% - 50px);
      animation: dropIn 1s ease-out forwards;
    }

    @keyframes dropIn {
      0% { transform: translateY(-200px) rotate(-45deg); opacity: 0; }
      100% { transform: translateY(0) rotate(0); opacity: 1; }
    }

    @keyframes popIn {
      0% { transform: scale(0.8); opacity: 0; }
      100% { transform: scale(1); opacity: 1; }
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      pointer-events: none;
      z-index: 1;
    }

    .print-btn {
      margin-top: 30px;
      padding: 10px 20px;
      font-size: 1rem;
      background: #0984e3;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background 0.3s;
    }

    .print-btn:hover {
      background: #74b9ff;
    }
  </style>
</head>
<body>

  <img id="cap" src="https://cdn-icons-png.flaticon.com/512/3135/3135789.png" alt="Graduation Cap">

  <div class="container">
    <h1>🎓 Surprise! You Did It!</h1>
    <div class="letter" id="letterText"></div>
    <div class="signature">— With Love, Your School ❤️</div>
    <button class="print-btn" onclick="window.print()">🖨️ Print Letter</button>
  </div>

  <canvas id="confetti"></canvas>

  <!-- Background Music -->
  <audio autoplay loop>
    <source src="https://www.bensound.com/bensound-music/bensound-sunny.mp3" type="audio/mpeg">
    Your browser does not support the audio tag.
  </audio>

  <script>
    // Typewriter Effect
    const text = `
Dear [Graduate Name],

🎉 Surprise! You’ve officially graduated! 🎉

All the hard work, sleepless nights, and endless dedication has brought you here — and we couldn't be more proud of you.

Remember this moment. You’ve earned every second of celebration.

Step boldly into the future — the world is waiting for your magic ✨

Congratulations again, Superstar! 🌟
`;

    let i = 0;
    const speed = 35;
    function typeWriter() {
      if (i < text.length) {
        document.getElementById("letterText").innerHTML += text.charAt(i);
        i++;
        setTimeout(typeWriter, speed);
      }
    }
    window.onload = () => {
      typeWriter();
      startConfetti();
    };

    // Confetti Surprise!
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");
    let pieces = [];

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }

    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    function createPiece() {
      return {
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height - canvas.height,
        size: Math.random() * 10 + 5,
        color: `hsl(${Math.random() * 360}, 100%, 50%)`,
        speed: Math.random() * 3 + 2
      };
    }

    for (let i = 0; i < 150; i++) {
      pieces.push(createPiece());
    }

    function update() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      pieces.forEach(p => {
        p.y += p.speed;
        if (p.y > canvas.height) {
          p.y = -10;
          p.x = Math.random() * canvas.width;
        }
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fillStyle = p.color;
        ctx.fill();
      });
      requestAnimationFrame(update);
    }

    function startConfetti() {
      update();
    }
  </script>

</body>
</html>
