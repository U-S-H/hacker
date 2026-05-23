<html lang="en">
<head>
    <style>
        body { background: #000; color: #00FF41; font-family: 'Courier New', monospace; margin: 0; overflow: hidden; }
        .terminal { padding: 20px; }
        .glitch { animation: glitch 1s linear infinite; }
        @keyframes glitch { 0% { opacity: 1; } 50% { opacity: 0.5; } 100% { opacity: 1; } }
        .data-stream { color: #008F11; font-size: 12px; }
    </style>
</head>
<body>
    <div class="terminal">
        <h1 class="glitch">> ROOT ACCESS GRANTED</h1>
        <div id="system-info">
            <p>> STATUS: SYSTEM OPERATIONAL</p>
            <p>> NETWORK: ENCRYPTED</p>
            <p>> TARGET: [UNDEFINED]</p>
        </div>
        <div class="data-stream" id="logs"></div>
    </div>

    <script>
        const logs = document.getElementById('logs');
        setInterval(() => {
            const entry = document.createElement('p');
            entry.innerText = "> Running packet sniff: " + Math.random().toString(36).substring(7);
            logs.appendChild(entry);
        }, 1000);
    </script>
</body>
</html>
