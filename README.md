<!DOCTYPE html>
<html>
<head>
    <title>Dinosaur Game</title>
    <style>
        canvas {
            border: 1px solid black;
        }
    </style>
</head>
<body>
    <canvas id="gameCanvas" width="800" height="400"></canvas>

    <script>
        // Get the canvas element
        const canvas = document.getElementById("gameCanvas");
        const ctx = canvas.getContext("2d");

        // Dinosaur object
        const dinosaur = {
            x: 50,
            y: canvas.height - 50,
            width: 50,
            height: 50,
            speed: 5,
            jumping: false,
            jumpHeight: 150,
            jumpCount: 0
        };

        // Game loop
        function gameLoop() {
            // Clear canvas
            ctx.clearRect(0, 0, canvas.width, canvas.height);

            // Draw dinosaur
            ctx.fillStyle = "green";
            ctx.fillRect(dinosaur.x, dinosaur.y - dinosaur.height, dinosaur.width, dinosaur.height);

            // Update dinosaur position
            if (dinosaur.jumping) {
                dinosaur.y -= dinosaur.speed;
                dinosaur.jumpCount += dinosaur.speed;
                if (dinosaur.jumpCount >= dinosaur.jumpHeight) {
                    dinosaur.jumping = false;
                    dinosaur.jumpCount = 0;
                }
            } else {
                dinosaur.y += dinosaur.speed;
            }

            // Request next frame
            requestAnimationFrame(gameLoop);
        }

        // Handle key events
        document.addEventListener("keydown", function (event) {
            if (event.code === "Space" && !dinosaur.jumping) {
                dinosaur.jumping = true;
            }
        });

        // Start the game loop
        gameLoop();
    </script>
</body>
</html>
