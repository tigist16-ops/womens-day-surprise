<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Women's Day Surprise</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: #f8c8dc;
        color: #c2185b;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        text-align: center;
    }

    main.container {
        background: #ffffff;
        padding: 40px;
        border-radius: 15px;
        box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        max-width: 420px;
        width: 90vw;
    }

    h1 {
        margin-bottom: 10px;
    }

    .countdown {
        font-size: 28px;
        font-weight: bold;
        margin: 20px 0;
        min-height: 44px;
        letter-spacing: 2px;
        transition: color 0.4s;
        animation: pulse 1s infinite;
    }

    @keyframes pulse {
        0% { color: #c2185b; text-shadow: 0 0 0 #f06292; }
        50% { color: #8e004d; text-shadow: 0 2px 12px #f06292; }
        100% { color: #c2185b; text-shadow: 0 0 0 #f06292; }
    }

    .hidden {
        display: none;
    }

    .gift {
        font-size: 22px;
        color: #8e004d;
        margin-top: 20px;
        font-weight: bold;
    }

    /* Surprise animation */
    #surprise {
        opacity: 0;
        transform: translateY(40px) scale(0.98);
        transition: opacity 1s cubic-bezier(.45,.05,.55,.95), transform 1s cubic-bezier(.45,.05,.55,.95);
        will-change: opacity, transform;
    }
    #surprise.show {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
</style>
</head>

<body>

<main class="container" aria-label="Women's Day Celebration">
    <h1>🌸 Happy Women's Day! 🌸</h1>
    <p>Today we celebrate your strength, kindness, and the amazing energy you bring every day.</p>
    <p>Your special surprise will be revealed soon!</p>

    <div id="countdown" class="countdown" aria-live="polite"></div>

    <div id="surprise" class="hidden">
        <p class="gift">🎁 It's Surprise Time!</p>
        <p>Please see the event host to receive your gift.</p>
    </div>
</main>

<script>
    // Automatically find the next March 7 at 10:00 AM
    function getNextWomensDayDate() {
        var now = new Date();
        var year = now.getFullYear();

        // March is month 2 (0-based), day 7, 10:00 AM
        var eventDate = new Date(year, 2, 7, 10, 0, 0);

        // If today is past March 7, 10:00 AM this year, use next year
        if (now > eventDate) {
            eventDate = new Date(year + 1, 2, 7, 10, 0, 0);
        }
        return eventDate.getTime();
    }

    var eventDate = getNextWomensDayDate();
    var lastCountdown = "";

    var countdownFunction = setInterval(function() {
        var now = new Date().getTime();
        var distance = eventDate - now;

        var countdownElem = document.getElementById("countdown");
        var surpriseElem = document.getElementById("surprise");

        if (distance <= 0) {
            clearInterval(countdownFunction);
            countdownElem.style.display = "none";
            // Animate reveal
            surpriseElem.classList.remove("hidden");
            setTimeout(function() {
                surpriseElem.classList.add("show");
            }, 30); // Allow rendering .hidden removed before adding .show
            return;
        }

        var days = Math.floor(distance / (1000 * 60 * 60 * 24));
        var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
        var seconds = Math.floor((distance % (1000 * 60)) / 1000);

        var countdownStr =
            days + "d " + hours + "h " + minutes + "m " + seconds + "s";

        // Only update innerHTML if changed, for a subtle pop (if you want digit animation, you could enhance here)
        if (lastCountdown !== countdownStr) {
            countdownElem.innerHTML = countdownStr;
            lastCountdown = countdownStr;
        }

        countdownElem.setAttribute("aria-label",
            days + " days, " + hours + " hours, " + minutes + " minutes, " + seconds + " seconds remaining.");

    }, 1000);
</script>

</body>
</html>              
