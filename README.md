# Atrapa-el-Cuadrado
Atrapa el Cuadrado es un juego diseñado para paginas web donde la gente se aburre leyendo

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Juego: Atrapa el Cuadrado</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            font-family: Arial, sans-serif;
            text-align: center;
        }
        canvas {
            display: block;
            margin: auto;
            background-color: #f0f0f0;
        }
        #score {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 24px;
            font-weight: bold;
            color: #333;
        }
    </style>
</head>
<body>
    <div id="score">Puntuación: 0</div>
    <canvas id="gameCanvas"></canvas>
    <script>
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // Configuración del juego
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let score = 0;
        let squareSize = 50;
        let squareX = Math.random() * (canvas.width - squareSize);
        let squareY = Math.random() * (canvas.height - squareSize);

        // Dibujar cuadrado
        function drawSquare() {
            ctx.fillStyle = "red";
            ctx.fillRect(squareX, squareY, squareSize, squareSize);
        }

        // Actualizar puntuación
        function updateScore() {
            document.getElementById("score").innerText = `Puntuación: ${score}`;
        }

        // Detectar clic en el cuadrado
        canvas.addEventListener("click", (event) => {
            const rect = canvas.getBoundingClientRect();
            const clickX = event.clientX - rect.left;
            const clickY = event.clientY - rect.top;

            if (
                clickX >= squareX &&
                clickX <= squareX + squareSize &&
                clickY >= squareY &&
                clickY <= squareY + squareSize
            ) {
                score++;
                squareX = Math.random() * (canvas.width - squareSize);
                squareY = Math.random() * (canvas.height - squareSize);
                updateScore();
            }
        });

        // Bucle principal del juego
        function gameLoop() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            drawSquare();
            requestAnimationFrame(gameLoop);
        }

        updateScore();
        gameLoop();
    </script>
</body>
</html>
