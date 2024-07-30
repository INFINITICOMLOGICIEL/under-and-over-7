<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UNDER AND OVER 7 BY INFINITI COM LOGICIEL</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 10px;
        }
        #dice {
            display: flex;
            justify-content: center;
            margin: 100px;
        }
        .die {
            width: 60px;
            height: 60px;
            margin: 20px;
            background-color: #f1f500;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 8em; /* Augmenté pour une taille de symbole plus grande */
            border: 2px solid #eed70b;
            border-radius: 5px;
        }
        #result {
            margin-top: 20px;
            font-size: 1.5em;
        }
        #countdown {
            margin-top: 20px;
            font-size: 1.2em;
            color: #c92424;
        }
    </style>
</head>
<body>
    <h1>UNDER AND OVER 7 BY INFINITI COM LOGICIEL</h1>
    <div id="dice">
        <div class="die" id="die1">⚅</div>
        <div class="die" id="die2">⚅</div>
    </div>
    <button id="nextGameButton" onclick="startGame()">Prochain Jeu</button>
    <div id="result"></div>
    <div id="countdown"></div>

    <script>
        let countdownTimer;
        let isCountdownActive = false;
        const diceSymbols = ['⚀', '⚁', '⚂', '⚃', '⚄', '⚅'];
        const rollInterval = 50; // Temps entre les changements de symboles en millisecondes
        const rollDuration = 1000; // Durée totale de l'animation de rotation en millisecondes

        function rollDice() {
            return Math.floor(Math.random() * 6);
        }

        function startGame() {
            if (isCountdownActive) return;

            isCountdownActive = true;
            document.getElementById('result').textContent = ''; // Effacer le résultat précédent

            // Démarrer l'animation de rotation
            let rollingTime = 0;
            const rollAnimation = setInterval(() => {
                const die1 = rollDice();
                const die2 = rollDice();
                document.getElementById('die1').textContent = diceSymbols[die1];
                document.getElementById('die2').textContent = diceSymbols[die2];
                rollingTime += rollInterval;

                if (rollingTime >= rollDuration) {
                    clearInterval(rollAnimation);
                    displayFinalResult(die1, die2);
                }
            }, rollInterval);
        }

        function displayFinalResult(die1, die2) {
            const total = die1 + 1 + die2 + 1; // Ajustement pour les indices des dés
            let resultText;

            if (total > 7) {
                resultText = `Le numéro gagnant est ${total} (plus de 7)`;
            } else if (total < 7) {
                resultText = `Le numéro gagnant est ${total} (moins de 7)`;
            } else {
                resultText = `Le numéro gagnant est ${total} (égal à 7)`;
            }
            document.getElementById('result').textContent = resultText;

            startCountdown(3 * 60); // Démarrer le compte à rebours pour le prochain jeu
        }

        function startCountdown(seconds) {
            let remainingTime = seconds;
            document.getElementById('countdown').textContent = `Prochain tirage dans ${remainingTime} secondes`;
            countdownTimer = setInterval(() => {
                remainingTime--;
                document.getElementById('countdown').textContent = `Prochain tirage dans ${remainingTime} secondes`;
                if (remainingTime <= 0) {
                    clearInterval(countdownTimer);
                    document.getElementById('countdown').textContent = '';
                    isCountdownActive = false;
                }
            }, 1000);
        }
    </script>
</body>
</html>
