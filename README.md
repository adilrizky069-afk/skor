<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <title>Karate Scoreboard WKF 2025</title>
    <style>
        body { background: #1a1a1a; color: white; font-family: sans-serif; text-align: center; margin: 0; }
        .container { display: flex; height: 80vh; }
        .side { flex: 1; padding: 20px; display: flex; flex-direction: column; justify-content: center; }
        .aka { background: #d32f2f; } /* Merah */
        .ao { background: #1976d2; }   /* Biru */
        .score { font-size: 150px; font-weight: bold; margin: 0; }
        .controls button { padding: 10px 20px; font-size: 20px; cursor: pointer; margin: 5px; }
        #timer { font-size: 100px; background: #000; padding: 20px; }
        .senshu { width: 30px; height: 30px; border-radius: 50%; background: gray; margin: 10px auto; }
        .senshu.active { background: yellow; box-shadow: 0 0 15px yellow; }
    </style>
</head>
<body>

    <div id="timer">03:00</div>
    <button onclick="startTimer()">START/STOP</button>
    <button onclick="resetAll()">RESET</button>

    <div class="container">
        <div class="side aka">
            <h2>AKA</h2>
            <div id="senshu-aka" class="senshu"></div>
            <p id="score-aka" class="score">0</p>
            <div class="controls">
                <button onclick="addScore('aka', 1)">Yuko</button>
                <button onclick="addScore('aka', 2)">Waza-Ari</button>
                <button onclick="addScore('aka', 3)">Ippon</button>
            </div>
        </div>

        <div class="side ao">
            <h2>AO</h2>
            <div id="senshu-ao" class="senshu"></div>
            <p id="score-ao" class="score">0</p>
            <div class="controls">
                <button onclick="addScore('ao', 1)">Yuko</button>
                <button onclick="addScore('ao', 2)">Waza-Ari</button>
                <button onclick="addScore('ao', 3)">Ippon</button>
            </div>
        </div>
    </div>

    <script>
        let scoreAka = 0, scoreAo = 0, timerVal = 180, interval, isRunning = false, senshu = null;

        function addScore(player, pts) {
            if (player === 'aka') scoreAka += pts;
            else scoreAo += pts;
            
            // Logika Senshu WKF
            if (senshu === null && (scoreAka > 0 || scoreAo > 0)) {
                senshu = player;
                document.getElementById(`senshu-${player}`).classList.add('active');
            }
            updateDisplay();
        }

        function updateDisplay() {
            document.getElementById('score-aka').innerText = scoreAka;
            document.getElementById('score-ao').innerText = scoreAo;
        }

        function startTimer() {
            if (isRunning) { clearInterval(interval); isRunning = false; }
            else {
                isRunning = true;
                interval = setInterval(() => {
                    if (timerVal <= 0) { clearInterval(interval); alert("Waktu Habis!"); return; }
                    timerVal--;
                    let m = Math.floor(timerVal / 60), s = timerVal % 60;
                    document.getElementById('timer').innerText = `${m}:${s < 10 ? '0' : ''}${s}`;
                }, 1000);
            }
        }

        function resetAll() {
            location.reload();
        }
    </script>
</body>
</html>
