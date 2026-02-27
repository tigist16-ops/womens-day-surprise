# womens-day-surprise
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Women's Day Surprise 🎉</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      background: linear-gradient(135deg, #FFE5EC, #FFD6F0);
      color: #D6336C;
      height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      margin: 0;
    }
    h1 {
      font-size: 2.5em;
      margin-bottom: 20px;
    }
    p {
      font-size: 1.2em;
    }
    .gift {
      font-size: 3em;
      margin-top: 20px;
    }
  </style>
</head>
<body>
<script>
  const now = new Date();
  const eventTime = new Date('2026-03-08T12:00:00'); // Set your event date & time here

  if (now >= eventTime) {
      document.write("<h1>🎉 Happy Women's Day! 🎁</h1>");
      document.write("<p>We hope you enjoy your special surprise during the event!</p>");
      document.write("<div class='gift'>🌸🎀🍫</div>");
  } else {
      document.write("<h1>✨ Patience! Your surprise is coming soon 😉</h1>");
      document.write("<p>Scan this QR again during the event to reveal your gift!</p>");
  }
</script>
</body>
</html>
