<div id="final-surprise-overlay">
    <canvas id="confetti-canvas"></canvas>
    <div class="main-container" id="content-card">
        </div>

    <style>
        /* This ID selector covers the entire screen from (0,0) 
           to hide the 'DOCTYPE' and filename text behind it */
        #final-surprise-overlay {
            font-family: 'Segoe UI', Arial, sans-serif;
            text-align: center;
            background: #FFD6F0;
            background: linear-gradient(135deg, #FFE5EC, #FFD6F0);
            color: #D6336C;
            position: fixed; 
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            z-index: 999999;
            margin: 0;
            overflow: hidden;
        }

        .main-container {
            background: #ffffff;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            max-width: 420px;
            width: 90vw;
            z-index: 1000000;
            position: relative;
        }

        h1 { margin-bottom: 10px; color: #D6336C; font-size: 2rem; }

        .countdown {
            font-size: 28px;
            font-weight: bold;
            margin: 20px 0;
            min-height: 44px;
            letter-spacing: 2px;
            animation: pulse 1s infinite;
        }

        @keyframes pulse {
            0% { color: #c2185b; text-shadow: 0 0 0 #f06292; }
            50% { color: #8e004d; text-shadow: 0 2px 12px #f06292; }
            100% { color: #c2185b; text-shadow: 0 0 0 #f06292; }
        }

        .gift {
            font-size: 5rem;
            margin-top: 20px;
            animation: bounce 2s infinite;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-15px); }
        }

        #confetti-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 5;
        }
    </style>

    <script>
        (function() {
            const targetDate = new Date('2026-03-08T12:00:00');
            let celebrated = false;
            const canvas = document.getElementById('confetti-canvas');
            const ctx = canvas.getContext('2d');
            let pieces = [];

            function init() {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            }

            function createPiece() {
                return {
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height - canvas.height,
                    rotation: Math.random() * 360,
                    color: ['#FF69B4', '#FFB6C1', '#D6336C', '#FFD700'][Math.floor(Math.random() * 4)],
                    size: Math.random() * 10 + 5,
                    speed: Math.random() * 3 + 2
                };
            }

            function draw() {
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
                requestAnimationFrame(draw);
            }

            window.addEventListener('resize', init);
            init();

            function update() {
                const now = new Date();
                const diff = targetDate - now;
                const card = document.getElementById('content-card');

                if (diff <= 0) {
                    card.innerHTML = `
                        <h1>🎉 Happy Women's Day!</h1>
                        <div class="gift">🌸🎁✨</div>
                        <p style="color: #8e004d; font-weight: bold; margin-top:20px;">Celebrating your strength and brilliance!</p>
                    `;
                    if (!celebrated) {
                        for (let i = 0; i < 100; i++) pieces.push(createPiece());
                        draw();
                        celebrated = true;
                    }
                    return;
                }

                const d = Math.floor(diff / 86400000);
                const h = Math.floor((diff / 3600000) % 24);
                const m = Math.floor((diff / 60000) % 60);
                const s = Math.floor((diff / 1000) % 60);

                card.innerHTML = `
                    <h1>✨ Almost There...</h1>
                    <p style="color: #666;">Your Women's Day surprise reveals in:</p>
                    <div class="countdown">${d}d ${h}h ${m}m ${s}s</div>
                    <p style="font-size: 0.8rem; opacity: 0.7;">Check back at noon on March 8th!</p>
                `;
            }

            setInterval(update, 1000);
            update();
        })();
    </script>
</div>
