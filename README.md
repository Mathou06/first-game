<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Jeu de Clic</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
            font-family: Arial, sans-serif;
        }

        .container {
            text-align: center;
        }

        #gameArea {
            position: relative;
            width: 400px;
            height: 400px;
            background-color: #ddd;
            margin: 20px auto;
            border: 2px solid #333;
        }

        #target {
            position: absolute;
            width: 50px;
            height: 50px;
            background-color: red;
            border-radius: 50%;
            display: none;
            cursor: pointer;
        }

        .info {
            display: flex;
            justify-content: space-around;
            margin-bottom: 10px;
        }

        button {
            padding: 10px 20px;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Jeu de Clic</h1>
        <div class="info">
            <p>Temps restant: <span id="time">30</span>s</p>
            <p>Score: <span id="score">0</span></p>
        </div>
        <div id="gameArea">
            <div id="target"></div>
        </div>
        <button id="startButton">Démarrer le jeu</button>
    </div>
    <script>
        let score = 0;
        let time = 30;
        let gameInterval;
        let target = document.getElementById('target');
        let timeDisplay = document.getElementById('time');
        let scoreDisplay = document.getElementById('score');
        let startButton = document.getElementById('startButton');

        function startGame() {
            score = 0;
            time = 30;
            scoreDisplay.textContent = score;
            timeDisplay.textContent = time;
            target.style.display = 'block';
            moveTarget();
            gameInterval = setInterval(updateGame, 1000);
            startButton.disabled = true;
        }

        function updateGame() {
            time--;
            timeDisplay.textContent = time;
            if (time <= 0) {
                endGame();
            }
        }

        function endGame() {
            clearInterval(gameInterval);
            target.style.display = 'none';
            alert('Temps écoulé ! Votre score est : ' + score);
            startButton.disabled = false;
        }

        function moveTarget() {
            const gameArea = document.getElementById('gameArea');
            const x = Math.floor(Math.random() * (gameArea.clientWidth - target.clientWidth));
            const y = Math.floor(Math.random() * (gameArea.clientHeight - target.clientHeight));
            target.style.left = `${x}px`;
            target.style.top = `${y}px`;
        }

        target.addEventListener('click', () => {
            score++;
            scoreDisplay.textContent = score;
            moveTarget();
        });

        startButton.addEventListener('click', startGame);
    </script>
</body>
</html>
