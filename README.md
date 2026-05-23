<html lang="en">
<head>
    <style>
        body { background: #000; color: #0f0; font-family: 'Courier New', Courier, monospace; padding: 15px; margin: 0; overflow-x: hidden; }
        h1 { color: #f00; text-align: center; animation: blink 0.5s infinite; }
        @keyframes blink { 50% { opacity: 0; } }
        .box { border: 1px solid #0f0; padding: 10px; margin-bottom: 10px; }
        .progress-bar { width: 100%; background: #222; height: 15px; margin: 5px 0; }
        .fill { height: 100%; background: #0f0; width: 0%; transition: width 0.5s; }
        #logs { font-size: 12px; height: 150px; overflow: hidden; border: 1px solid #333; padding: 5px; }
    </style>
</head>
<body>
    <h1>!!! SYSTEM SECURITY BREACH !!!</h1>
    
    <div class="box">
        <div>Target: FACEBOOK_DB_ACCESS</div>
        <div class="progress-bar"><div class="fill" id="bar1"></div></div>
        
        <div>Target: WHATSAPP_ENCRYPTION</div>
        <div class="progress-bar"><div class="fill" id="bar2"></div></div>
        
        <div>Target: SNAPCHAT_DATA_SYNC</div>
        <div class="progress-bar"><div class="fill" id="bar3"></div></div>
    </div>

    <div id="logs"></div>

    <script>
        // Progress Bars
        function startBar(id, speed) {
            let width = 0;
            let bar = document.getElementById(id);
            let interval = setInterval(() => {
                if (width >= 100) clearInterval(interval);
                else { width++; bar.style.width = width + '%'; }
            }, speed);
        }
        startBar('bar1', 150); startBar('bar2', 250); startBar('bar3', 350);

        // Scrolling Logs
        const logs = document.getElementById('logs');
        const lines = ["Connecting to proxy...", "Bypassing firewall...", "Deciphering AES-256...", "Accessing user sessions...", "Uploading files...", "Connection stable."];
        setInterval(() => {
            logs.innerHTML += "> " + lines[Math.floor(Math.random() * lines.length)] + "<br>";
            logs.scrollTop = logs.scrollHeight;
        }, 800);
    </script>
</body>
</html>
