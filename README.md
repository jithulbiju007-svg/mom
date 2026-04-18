<!DOCTYPE html>
<html lang="en">
<head>
    <title>Happy Birthday Mom</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.5.1/dist/confetti.browser.min.js"></script>

    <style>
        :root {
            --primary: #d63384;
            --secondary: #f8bbd0;
            --accent: #ff9a9e;
            --glass: rgba(255, 255, 255, 0.82);
            --gold: #d4af37;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(-45deg, #ff9a9e, #fad0c4, #fbc2eb, #a1c4fd);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            margin: 0;
            padding: 0;
            min-height: 100vh;
            overflow-x: hidden;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Keep your original background confetti canvas behind everything */
        .confetti-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }

        .header {
            padding: 80px 20px 40px 20px;
            text-align: center;
            position: relative;
            z-index: 1;
        }

        .header h1 {
            font-family: 'Dancing Script', cursive;
            font-size: 4.5em;
            color: #fff;
            margin: 0;
            text-shadow: 2px 4px 10px rgba(0,0,0,0.1);
            animation: floating 3s ease-in-out infinite;
        }

        @keyframes floating {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        .header .heart {
            color: #ff4d6d;
            display: inline-block;
            animation: heartbeat 1.2s infinite;
        }

        @keyframes heartbeat {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.3); }
        }

        .section {
            margin: 30px auto;
            max-width: 750px;
            background: var(--glass);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.08);
            padding: 40px 30px;
            text-align: center;
            border: 1px solid rgba(255, 255, 255, 0.4);
            position: relative;
            z-index: 1;
            transition: transform 0.3s ease;
        }

        .section:hover {
            transform: translateY(-5px);
        }

        h2 {
            font-family: 'Dancing Script', cursive;
            color: var(--primary);
            font-size: 2.5em;
            margin-top: 0;
        }

        p {
            font-size: 1.1em;
            color: #555;
            line-height: 1.7;
        }

        .button {
            display: inline-block;
            background: linear-gradient(45deg, #ee0979, #ff6a00);
            color: #fff;
            border: none;
            border-radius: 50px;
            padding: 16px 35px;
            font-size: 1.1em;
            font-weight: 600;
            cursor: pointer;
            box-shadow: 0 8px 20px rgba(238, 9, 121, 0.25);
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 20px;
        }

        .button:hover {
            transform: scale(1.05) translateY(-2px);
            box-shadow: 0 12px 25px rgba(238, 9, 121, 0.35);
        }

        /* --- Gift Content Design --- */
        #giftContent {
            display: none;
            margin-top: 35px;
            padding-top: 30px;
            border-top: 2px dashed var(--accent);
        }

        #typedMessage {
            font-family: 'Dancing Script', cursive;
            color: var(--primary);
            font-size: 2.2em;
            min-height: 50px;
            margin: 20px 0;
            font-weight: bold;
        }

        .slideshow img {
            width: 280px;
            height: 280px;
            object-fit: cover;
            border-radius: 50%;
            border: 8px solid white;
            box-shadow: 0 10px 30px rgba(0,0,0,0.15);
        }

        /* --- Memory Grid --- */
        .memories {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
            gap: 20px;
            margin-top: 30px;
        }

        .memories img {
            width: 100%;
            aspect-ratio: 1;
            object-fit: cover;
            border-radius: 20px;
            border: 4px solid white;
            box-shadow: 0 8px 15px rgba(0,0,0,0.1);
            transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
        }

        .memories img:hover {
            transform: scale(1.1) rotate(-3deg);
            border-color: var(--accent);
        }

        /* --- Modal Styling --- */
        #messageModal {
            display: none;
            position: fixed;
            z-index: 2000;
            left: 0; top: 0; width: 100vw; height: 100vh;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(8px);
            align-items: center;
            justify-content: center;
        }

        #messageModal .modal-content {
            background: #fff;
            border-radius: 35px;
            padding: 40px;
            text-align: center;
            max-width: 450px;
            box-shadow: 0 20px 50px rgba(0,0,0,0.2);
            position: relative;
        }

        #modalText {
            font-family: 'Dancing Script', cursive;
            font-size: 2em;
            color: var(--primary);
        }

        .close {
            position: absolute;
            top: 15px; right: 25px;
            font-size: 1.8em;
            color: #aaa;
            cursor: pointer;
        }

        .footer {
            text-align: center;
            color: white;
            padding: 60px 0 40px;
            font-family: 'Dancing Script', cursive;
            font-size: 2.2em;
            text-shadow: 1px 2px 5px rgba(0,0,0,0.1);
        }

        @media (max-width: 600px) {
            .header h1 { font-size: 2.8em; }
            .section { margin: 15px; padding: 25px 15px; }
            .slideshow img { width: 200px; height: 200px; }
        }
    </style>
</head>
<body>

<canvas class="confetti-bg"></canvas>

<div class="header">
    <h1>Happy Birthday Mom <span class="heart">❤️</span></h1>
    <div style="font-size:1.3em; color: white; opacity: 0.9; margin-top: 10px;">Celebrating our Queen</div>
</div>

<div class="section">
    <h2>A Special Surprise</h2>
    <p>I put together something special just for you. Click the gift to see!</p>
    <button class="button" onclick="openGift()">🎁 Open Your Gift</button>
    
    <div id="giftContent">
        <div id="typedMessage"></div>
        <div class="slideshow">
            <img id="slideImage" src="photo1.jpeg" alt="Memory Slideshow">
        </div>
        <audio id="birthdayMusic">
            <source src="nastelbom-happy-birthday-471481.mp3" type="audio/mpeg">
        </audio>
    </div>
</div>

<div class="section">
    <h2>To the Best Mom</h2>
    <p>
        Thank you for your endless love and patience. You make the world a better place 
        just by being in it. You deserve the happiest of birthdays!
    </p>
    <button class="button" onclick="showModal()">A Little Secret</button>
</div>

<div class="section">
    <h2>Our Beautiful Memories</h2>
    <div class="memories">
        <img src="photo1.jpeg" alt="Memory 1" onclick="showMemory('A day to remember')">
        <img src="photo3.jpeg" alt="Memory 2" onclick="showMemory('Our favorite adventure')">
        <img src="photo4.jpeg" alt="Memory 3" onclick="showMemory('Sweet family moments')">
    </div>
</div>

<div class="footer">
    With all my love, always. ✨
</div>

<div id="messageModal">
    <div class="modal-content">
        <span class="close" onclick="hideModal()">&times;</span>
        <div id="modalText">
            🎁 You are my sunshine, Mom! Thank you for making every day brighter. Love you always! 🌟
        </div>
    </div>
</div>

<script>
/* --- ALL FEATURES PRESERVED --- */

// 1. Modal Logic
function showModal() {
    document.getElementById('messageModal').style.display = 'flex';
}
function hideModal() {
    document.getElementById('messageModal').style.display = 'none';
}
function showMemory(memory) {
    document.getElementById('modalText').innerHTML = '<b>' + memory + '</b>.<br><span style="font-size: 0.7em;">Thank you for these wonderful moments!</span>';
    showModal();
}

// 2. Background Confetti (The original drawing logic)
const canvas = document.querySelector('.confetti-bg');
const ctx = canvas.getContext('2d');
let confettiPieces = [];

function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
}
window.addEventListener('resize', resizeCanvas);
resizeCanvas();

function createConfetti() {
    confettiPieces = [];
    for (let i = 0; i < 60; i++) {
        confettiPieces.push({
            x: Math.random() * canvas.width,
            y: Math.random() * canvas.height,
            r: Math.random() * 6 + 4,
            color: ['#ee0979','#ff6a00','#fff','#fbc2eb','#d4af37'][Math.floor(Math.random()*5)],
            dx: Math.random() * 2 - 1,
            dy: Math.random() * 2 + 1
        });
    }
}
createConfetti();

function drawConfetti() {
    ctx.clearRect(0,0,canvas.width,canvas.height);
    confettiPieces.forEach(c => {
        ctx.beginPath();
        ctx.arc(c.x, c.y, c.r, 0, 2*Math.PI);
        ctx.fillStyle = c.color;
        ctx.fill();
        c.x += c.dx;
        c.y += c.dy;
        if (c.y > canvas.height) c.y = -10;
        if (c.x > canvas.width) c.x = 0;
        if (c.x < 0) c.x = canvas.width;
    });
    requestAnimationFrame(drawConfetti);
}
drawConfetti();

// 3. Gift Opening Logic
function openGift(){
    document.getElementById("giftContent").style.display="block";
    const audio = document.getElementById("birthdayMusic");
    audio.play().catch(e => console.log("Audio waiting for user interaction"));
    
    startTyping();
    startSlideshow();
    startFireworks();
}

// 4. Typing Animation
const message = "Happy Birthday Mom! You are the heart of our home. ❤️";
let charIndex = 0;

function startTyping(){
    const speed = 70;
    if(charIndex < message.length){
        document.getElementById("typedMessage").innerHTML += message.charAt(charIndex);
        charIndex++;
        setTimeout(startTyping, speed);
    }
}

// 5. Slideshow
const images = ["photo1.jpg","photo2.jpg","photo3.jpg"];
let slideIndex = 0;

function startSlideshow(){
    setInterval(()=>{
        slideIndex = (slideIndex + 1) % images.length;
        document.getElementById("slideImage").src = images[slideIndex];
    }, 2500);
}

// 6. Fireworks Feature
function startFireworks(){
    const duration = 5000;
    const animationEnd = Date.now() + duration;
    const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

    function randomInRange(min, max) {
      return Math.random() * (max - min) + min;
    }

    const interval = setInterval(function() {
      const timeLeft = animationEnd - Date.now();
      if (timeLeft <= 0) return clearInterval(interval);
      
      const particleCount = 50 * (timeLeft / duration);
      confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 } }));
      confetti(Object.assign({}, defaults, { particleCount, origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 } }));
    }, 250);
}
</script>

</body>
</html>
