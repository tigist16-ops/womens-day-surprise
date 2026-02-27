<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Women's Day Surprise 🎉</title>
    <style>
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            text-align: center;
            background: linear-gradient(135deg, #FFE5EC, #FFD6F0);
            color: #D6336C;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            margin: 0;
            overflow: hidden;
        }

        .container {
            background: rgba(255, 255, 255, 0.6);
            padding: 30px;
            border-radius: 25px;
            backdrop-filter: blur(8px);
            box-shadow: 0 10px 30px rgba(214, 51, 108, 0.15);
            max-width: 85%;
            z-index: 10;
        }

        h1 { font-size: 2.2rem; margin-bottom: 10px; }
        
        #timer {
            font-size: 1.8rem;
            font-weight: bold;
            margin: 20px 0;
            color: #b02656;
        }

        .gift-box { font-size: 5rem; animation: pulse 1.5s infinite; }

        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }

        canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 5;
        }
    </style>
</head>
<body>

    <canvas id="confetti-canvas"></canvas>

    <div class="container" id="content-card">
        </div>

    <script>
        const targetDate = new Date('2026-03-08T12:00:00');
        let celebrated = false;

        // --- INTERNAL CONFETTI ENGINE ---
        const canvas = document.getElementById('confetti-canvas');
        const ctx = canvas.getContext('2d');
        let pieces = [];

        function initCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }

        function createPiece() {
            return {
                x: Math.random() * canvas.width,
                y: Math.random() * canvas.height - canvas.height,
                rotation: Math.random() * 360,
                color: ['#FF69B4', '#FFB6C1', '#D6336C', '#FFFFFF'][Math.floor(Math.random() * 4)],
                size: Math.random() * 10 + 5,
                speed: Math.random() * 3 + 2
            };
        }

        function drawConfetti() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            pieces.forEach((p, i) => {
                p.y += p.speed;
                p.rotation += p.speed;
                ctx.fillStyle = p.color;
                ctx.save();
                ctx.translate(p.x, p.y);
                ctx.rotate(p.rotation * Math.PI / 180);
                ctx.fillRect(-p.size/2, -p.size/2, p.size, p.size);
                ctx.restore();
                if (p.y > canvas.height) pieces[i] = createPiece();
            });
            requestAnimationFrame(drawConfetti);
        }

        function startConfetti() {
            for (let i = 0; i < 100; i++) pieces.push(createPiece());
            drawConfetti();
        }

        window.addEventListener('resize', initCanvas);
        initCanvas();

        // --- COUNTDOWN LOGIC ---
        function update() {
            const now = new Date();
            const diff = targetDate - now;
            const card = document.getElementById('content-card');

            if (diff <= 0) {
                card.innerHTML = `
                    <h1>🎉 Happy Women's Day!</h1>
                    <div class="gift-box">🌸🎁✨</div>
                    <p>Celebrate the strength, grace, and brilliance of women everywhere!</p>
                `;
                if (!celebrated) {
                    startConfetti();
                    celebrated = true;
                }
                return;
            }

            const d = Math.floor(diff / 86400000);
            const h = Math.floor((diff / 3600000) % 24);
            const m = Math.floor((diff / 60000) % 60);
            const s = Math.floor((diff / 1000) % 60);

            card.innerHTML = `
                <h1>✨ Something Special...</h1>
                <p>Your Women's Day surprise reveals in:</p>
                <div id="timer">${d}d ${h}h ${m}m ${s}s</div>
                <p>Check back at noon on March 8th!</p>
            `;
        }

        setInterval(update, 1000);
        update();
    </script>
</body>
</html>
