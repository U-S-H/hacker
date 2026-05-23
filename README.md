<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>SYSTEM CRITICAL</title>
    <style>
        body { background: #000; color: #f00; font-family: 'Courier New', monospace; margin: 0; overflow: hidden; height: 100vh; display: flex; flex-direction: column; justify-content: center; align-items: center; cursor: none; transition: background 0.1s; }
        #timer { font-size: 8rem; font-weight: bold; }
        .alert { border: 4px solid #f00; padding: 40px; background: rgba(255,0,0,0.2); text-align: center; }
        @keyframes flash { 0% { background: #000; } 50% { background: #300; } 100% { background: #000; } }
        .flash-active { animation: flash 0.2s infinite; }
        @keyframes shake { 0% { transform: translate(1px, 1px); } 100% { transform: translate(-1px, -1px); } }
        .shake-active { animation: shake 0.1s infinite; }
    </style>
</head>
<body onclick="makeFullScreen()" class="flash-active shake-active">

    <div class="alert">
        <h1>SYSTEM HACKED!</h1>
        <div id="timer">10</div>
        <p id="status">INTRUDER DETECTED IN LOCAL NETWORK...</p>
    </div>

    <script>
        function makeFullScreen() { document.documentElement.requestFullscreen(); }

        let count = 10;
        const timerDisplay = document.getElementById('timer');
        const statusText = document.getElementById('status');
        
        const interval = setInterval(() => {
            count--;
            timerDisplay.innerText = count;
            
            // Random terminal messages
            const msgs = ["ACCESSING DATA...", "BYPASSING FIREWALL...", "SYSTEM CORRUPTION 45%...", "TARGET LOCKED..."];
            statusText.innerText = msgs[Math.floor(Math.random() * msgs.length)];

            if (count % 2 === 0) { alert("SECURITY BREACH ALERT!"); }

            if (count <= 0) {
                clearInterval(interval);
                alert("Prank complete, sweetie! Everything is secure again. 😄");
                location.reload();
            }
        }, 1000);

        document.addEventListener('contextmenu', event => event.preventDefault());
    </script>
</body>
</html>
