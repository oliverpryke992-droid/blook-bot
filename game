<!doctype html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>Eternity Stopwatch</title>

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      display: grid;
      place-items: center;
      padding: 24px;
      font-family: system-ui, sans-serif;
      background: radial-gradient(circle at top, #20254a, #080914 60%);
      color: white;
    }

    .game {
      width: min(900px, 100%);
      padding: 36px;
      border: 1px solid #ffffff22;
      border-radius: 28px;
      background: #14172add;
      box-shadow: 0 25px 80px #0008;
      text-align: center;
    }

    .title {
      font-size: 14px;
      letter-spacing: .3em;
      font-weight: 800;
      opacity: .65;
      margin-bottom: 22px;
    }

    #timer {
      font-size: clamp(32px, 7vw, 72px);
      font-weight: 900;
      font-variant-numeric: tabular-nums;
      overflow-wrap: anywhere;
    }

    #result {
      min-height: 34px;
      margin-top: 20px;
      font-size: 22px;
      font-weight: 800;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 14px;
      margin-top: 30px;
    }

    button {
      border: 0;
      min-height: 64px;
      border-radius: 18px;
      color: white;
      font-size: 17px;
      font-weight: 900;
      letter-spacing: .08em;
      cursor: pointer;
      transition: .12s;
    }

    button:hover:not(:disabled) {
      transform: translateY(-3px);
      filter: brightness(1.12);
    }

    button:active:not(:disabled) {
      transform: scale(.98);
    }

    button:disabled {
      opacity: .35;
      cursor: not-allowed;
    }

    #start {
      background: linear-gradient(135deg, #7c3aed, #4f46e5);
      box-shadow: 0 10px 30px #6366f155;
    }

    #stop {
      background: linear-gradient(135deg, #ef4444, #b91c1c);
      box-shadow: 0 10px 30px #ef444433;
    }

    #reset {
      background: linear-gradient(135deg, #374151, #1f2937);
    }

    .hint {
      margin-top: 22px;
      font-size: 13px;
      opacity: .45;
    }

    @media (max-width: 600px) {
      .game {
        padding: 24px 16px;
      }

      .buttons {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>

<body>

  <main class="game">

    <div class="title">ETERNITY STOPWATCH</div>

    <div id="timer">00:00:00.000</div>

    <div id="result">Ready?</div>

    <div class="buttons">
      <button id="start">▶ START</button>
      <button id="stop" disabled>■ STOP</button>
      <button id="reset">↻ RESET</button>
    </div>

    <div class="hint">
      Stop the timer as fast as you can.
    </div>

  </main>

  <script>
    (() => {

      const timer = document.getElementById("timer");
      const result = document.getElementById("result");

      const startButton = document.getElementById("start");
      const stopButton = document.getElementById("stop");
      const resetButton = document.getElementById("reset");

      // Hidden winning limit
      const LIMIT = 500;

      // Fake eternity timer
      const ETERNITY =
        "999999999999999:9999999999:99999999999:9999:999:24:59:58.999";

      let running = false;
      let finished = false;
      let startTime = 0;
      let animationFrame = 0;


      function formatTime(milliseconds) {

        let ms = Math.max(0, Math.floor(milliseconds));

        let hours = Math.floor(ms / 3600000);

        let minutes =
          Math.floor((ms % 3600000) / 60000);

        let seconds =
          Math.floor((ms % 60000) / 1000);

        let millis =
          ms % 1000;

        return (
          String(hours).padStart(2, "0") +
          ":" +
          String(minutes).padStart(2, "0") +
          ":" +
          String(seconds).padStart(2, "0") +
          "." +
          String(millis).padStart(3, "0")
        );
      }


      function updateTimer(currentTime) {

        if (!running) return;

        timer.textContent =
          formatTime(currentTime - startTime);

        animationFrame =
          requestAnimationFrame(updateTimer);
      }


      function finishGame() {

        running = false;
        finished = true;

        cancelAnimationFrame(animationFrame);

        startButton.disabled = true;
        stopButton.disabled = true;

        const elapsed =
          performance.now() - startTime;


        if (elapsed <= LIMIT) {

          timer.textContent =
            "00:00:00.000";

          result.textContent =
            "🎉 YOU WON!";

        } else {

          timer.textContent =
            ETERNITY;

          result.textContent =
            "⏳ 1 eternity later";
        }
      }


      startButton.onclick = () => {

        if (running || finished) return;

        running = true;
        finished = false;

        startTime = performance.now();

        timer.textContent =
          "00:00:00.000";

        result.textContent =
          "GO!";

        startButton.disabled = true;
        stopButton.disabled = false;

        animationFrame =
          requestAnimationFrame(updateTimer);
      };


      stopButton.onclick = () => {

        if (running) {
          finishGame();
        }
      };


      resetButton.onclick = () => {

        running = false;
        finished = false;

        cancelAnimationFrame(animationFrame);

        timer.textContent =
          "00:00:00.000";

        result.textContent =
          "Ready?";

        startButton.disabled = false;
        stopButton.disabled = true;
      };

    })();
  </script>

</body>
</html>
