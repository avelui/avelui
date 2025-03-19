<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>¿Quieres ser mi novio?</title>
    <style>
        body {
            background: linear-gradient(135deg, #ff758c, #ff7eb3);
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            color: white;
            font-family: Arial, sans-serif;
            overflow: hidden;
        }
        .container {
            background: rgba(255, 255, 255, 0.3);
            padding: 30px;
            border-radius: 20px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.3);
            transition: opacity 0.5s;
            position: relative;
            animation: bounce 1.5s infinite alternate;
        }
        h1 {
            font-size: 3em;
            margin-bottom: 20px;
            color: #fff;
            text-shadow: 3px 3px 6px rgba(0, 0, 0, 0.4);
        }
        .image-container {
            margin-top: 15px;
        }
        .image-container img {
            width: 320px;
            height: auto;
            border-radius: 15px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
        }
        .buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        button {
            font-size: 1.2em;
            padding: 15px 30px;
            border: none;
            border-radius: 15px;
            cursor: pointer;
            transition: 0.3s;
            font-weight: bold;
        }
        .yes {
            background: #ff4d79;
            color: white;
            box-shadow: 0 5px 15px rgba(255, 77, 121, 0.4);
        }
        .yes:hover {
            background: #ff2e63;
            transform: scale(1.1);
        }
        .no {
            background: #ffffff;
            color: #ff4d79;
            box-shadow: 0 5px 15px rgba(255, 255, 255, 0.3);
        }
        .no:hover {
            transform: translateX(30px);
        }
        .heart {
            position: absolute;
            font-size: 30px;
            color: red;
            animation: float 2s linear infinite;
        }
        @keyframes float {
            0% { transform: translateY(0); opacity: 1; }
            100% { transform: translateY(-120px); opacity: 0; }
        }
        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(10px); }
        }
        .hidden {
            display: none;
        }
        .fireworks {
            position: fixed;
            width: 100%;
            height: 100%;
            pointer-events: none;
        }
    </style>
</head>
<body>
    <canvas class="fireworks" id="fireworks"></canvas>
    <div class="container" id="mainContainer">
        <h1>¿Quieres ser mi novio? </h1>
        <div class="image-container">
            <img src="https://i.pinimg.com/474x/b1/23/8f/b1238f0be4d07c95884ae03ac994897c.jpg" alt="Imagen personalizada" id="customImage">
        </div>
        <div class="buttons">
            <button class="yes" onclick="showLove()">Sí</button>
            <button class="no" onclick="moveButton(this)">No</button>
        </div>
    </div>
    <div class="hidden" id="loveMessage">
        <h1>¡TE AMOOOOOOOOO!</h1>
        <div class="image-container">
            <img src="https://pbs.twimg.com/media/FQ4aR8ZX0AIlW7u.jpg" alt="Pareja feliz">
        </div>
    </div>
    <script>
        function moveButton(button) {
            button.style.position = 'absolute';
            button.style.left = Math.random() * window.innerWidth + 'px';
            button.style.top = Math.random() * window.innerHeight + 'px';
        }
        
        function showLove() {
            document.getElementById('mainContainer').style.opacity = '0';
            setTimeout(() => {
                document.getElementById('mainContainer').classList.add('hidden');
                document.getElementById('loveMessage').classList.remove('hidden');
                startFireworks();
            }, 500);
            for (let i = 0; i < 20; i++) {
                let heart = document.createElement('div');
                heart.innerHTML = '❤️';
                heart.classList.add('heart');
                document.body.appendChild(heart);
                heart.style.left = Math.random() * window.innerWidth + 'px';
                heart.style.top = Math.random() * window.innerHeight + 'px';
                setTimeout(() => heart.remove(), 2000);
            }
        }
        
        function startFireworks() {
            const canvas = document.getElementById("fireworks");
            const ctx = canvas.getContext("2d");
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
            let particles = [];
            function createParticle() {
                let p = {
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height,
                    size: Math.random() * 4 + 1,
                    speedY: Math.random() * 2 - 1,
                    color: `hsl(${Math.random() * 360}, 100%, 70%)`
                };
                particles.push(p);
            }
            function updateParticles() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                particles.forEach((p, i) => {
                    p.y += p.speedY;
                    ctx.beginPath();
                    ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                    ctx.fillStyle = p.color;
                    ctx.fill();
                    if (p.y < 0) particles.splice(i, 1);
                });
                if (particles.length < 100) createParticle();
                requestAnimationFrame(updateParticles);
            }
            updateParticles();
        }
    </script>
</body>
</html>
