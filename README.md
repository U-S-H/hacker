<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SYSTEM CRITICAL</title>
    <style>
        body { background: #000; color: #ff0000; font-family: 'Courier New', monospace; margin: 0; overflow: hidden; height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; cursor: none; }
        #timer { font-size: 5rem; font-weight: bold; }
        .alert { border: 2px solid #f00; padding: 20px; background: rgba(255,0,0,0.1); }
    </style>
</head>
<body onclick="makeFullScreen()">

    <div class="alert">
        <h1>WARNING: SYSTEM COMPROMISED</h1>
        <div id="timer">10</div>
        <p>DO NOT REFRESH OR DATA WILL BE ERASED</p>
    </div>

    <script>
        // Feature: Auto Fullscreen on click
        function makeFullScreen() {
            document.documentElement.requestFullscreen();
        }

        // Feature: Countdown Timer
        let count = 10;
        const timerDisplay = document.getElementById('timer');
        const interval = setInterval(() => {
            count--;
            timerDisplay.innerText = count;
            
            // Feature: Random Popups
            if (count % 3 === 0) {
                alert("SYSTEM BREACH DETECTED!");
            }

            if (count <= 0) {
                clearInterval(interval);
                alert("Prank complete, sweetie! Everything is safe! 😄");
                location.reload();
            }
        }, 1000);

        // Feature: Disable right click
        document.addEventListener('contextmenu', event => event.preventDefault());
    </script>
</body>
</html>
