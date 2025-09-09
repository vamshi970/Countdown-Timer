<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Countdown Timer</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f2f2f2;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }

    .container {
      text-align: center;
      background: white;
      padding: 40px;
      border-radius: 15px;
      box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
    }

    input, button {
      padding: 10px;
      margin: 10px;
      font-size: 1rem;
    }

    .timer {
      font-size: 2rem;
      margin-top: 20px;
      color: #333;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Countdown to Exam</h1>
    <input type="datetime-local" id="event-date" />
    <button onclick="startCountdown()">Start Countdown</button>
    <div id="countdown" class="timer"></div>
  </div>

  <script>
    let countdownInterval;

    function startCountdown() {
      clearInterval(countdownInterval);
      const eventDateInput = document.getElementById("event-date").value;
      const countdownElement = document.getElementById("countdown");

      if (!eventDateInput) {
        countdownElement.textContent = "Please select a date and time.";
        return;
      }

      const eventDate = new Date(eventDateInput).getTime();

      countdownInterval = setInterval(() => {
        const now = new Date().getTime();
        const distance = eventDate - now;

        if (distance <= 0) {
          clearInterval(countdownInterval);
          countdownElement.textContent = "The event has started!";
          return;
        }

        const days = Math.floor(distance / (1000 * 60 * 60 * 24));
        const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
        const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
        const seconds = Math.floor((distance % (1000 * 60)) / 1000);

        countdownElement.textContent = ${days}d ${hours}h ${minutes}m ${seconds}s;
      }, 1000);
    }
  </script>
</body>
</html>
