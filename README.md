<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Women's Day Surprise 🎉</title>
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
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
            background: rgba(255, 255, 255, 0.4);
            padding: 2rem;
            border-radius: 20px;
            backdrop-filter: blur(10px);
            box-shadow: 0 10px 30px rgba(214, 51, 108, 0.1);
            max-width: 90%;
        }

        h1 { font-size: 2.5rem; margin-bottom: 10px; }
        p { font-size: 1.2rem; margin-bottom: 20px; }

        #timer {
            font-family: monospace;
            font-size: 2rem;
            font-weight: bold;
            background: #D6336C;
            color: white;
            padding: 10px 20px;
            border-radius: 10px;
            display: inline-block;
        }

        .gift { font-size: 5rem; animation: bounce 2s infinite; }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
    </style>
</head>
<body>

    <div class="container" id="main-card">
        </div>

    <script>
        const targetDate = new Date('2026-03-08T12:00:00');
        let hasCelebrated = false;

        function fireConfetti() {
            const duration = 5 * 1000;
            const animationEnd = Date.now() + duration;
            const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 };

            const interval = setInterval(function() {
                const timeLeft = animationEnd - Date.now();
                if (timeLeft <= 0) return clearInterval(interval);

                const particleCount = 50 * (timeLeft / duration);
                confetti({...defaults, particleCount, origin: { x: Math.random(), y: Math.random() - 0.2 }});
            }, 250);
        }

        function update() {
            const now = new Date();
            const diff = targetDate - now;
            const card = document.getElementById('main-card');

            if (diff <= 0) {
                // THE REVEAL
                card.innerHTML = `
                    <h1>🎉 Happy Women's Day!</h1>
                    <p>You deserve all the flowers today!</p>
                    <div class="gift">🌸🎀🎁</div>
                    <p style="margin-top:20px;">Enjoy your special surprise!</p>
                `;
                
                if (!hasCelebrated) {
                    fireConfetti();
                    hasCelebrated = true;
                }
                return;
            }

            // THE COUNTDOWN
            const d = Math.floor(diff / (1000 * 60 * 60 * 24));
            const h = Math.floor((diff / (1000 * 60 * 60)) % 24);
            const m = Math.floor((diff / 1000 / 60) % 60);
            const s = Math.floor((diff / 1000) % 60);

            card.innerHTML = `
                <h1>✨ Almost There...</h1>
                <p>Your Women's Day surprise reveals in:</p>
                <div id="timer">${d}d ${h}h ${m}m ${s}s</div>
                <p style="margin-top:20px; font-size: 0.9em; opacity: 0.8;">
                    Keep this tab open or scan the QR code again at noon!
                </p>
            `;
        }

        // Run the clock
        setInterval(update, 1000);
        update();
    </script>
</body>
</html>
