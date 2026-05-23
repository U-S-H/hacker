<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CYBER_COMMANDER_PRO</title>
    <style>
        body { background: #000; color: #00FF41; font-family: 'Courier New', monospace; margin: 0; overflow: hidden; }
        canvas { position: absolute; top: 0; left: 0; z-index: 1; }
        #overlay { position: relative; z-index: 2; padding: 30px; text-align: center; }
        #logs { text-align: left; background: rgba(0,0,0,0.85); padding: 15px; height: 350px; overflow-y: hidden; border: 1px solid #0f0; margin-top: 20px; font-size: 16px; }
        .red-flash { color: #ff0000; font-weight: bold; animation: blink 0.4s infinite; }
        @keyframes blink { 50% { opacity: 0; } }
        button { background: #00FF41; border: none; padding: 15px 30px; font-weight: bold; cursor: pointer; font-size: 18px; margin-top: 20px; }
    </style>
</head>
<body>

    <canvas id="matrix"></canvas>
    
    <div id="overlay">
        <h1>SYSTEM OVERRIDE INITIATED</h1>
        <button onclick="startPrank()">INITIALIZE HACK SEQUENCE</button>
        <div id="logs"></div>
    </div>

    <script>
        // Matrix Background
        const c = document.getElementById("matrix");
        const ctx = c.getContext("2d");
        c.height = window.innerHeight; c.width = window.innerWidth;
        const drops = Array(Math.floor(c.width/20)).fill(1);
        setInterval(() => {
            ctx.fillStyle = "rgba(0,0,0,0.05)"; ctx.fillRect(0,0,c.width,c.height);
            ctx.fillStyle = "#0f0";
            drops.map((y, i) => {
                ctx.fillText(String.fromCharCode(65+Math.random()*20), i*20, y*20);
                drops[i] = y*20 > c.height ? 0 : y + 1;
            });
        }, 33);

        // Hacking Logic
        const logBox = document.getElementById('logs');
        const tasks = [
            "SCANNING NETWORK_PERIMETER...",
            "DEVICE ID DETECTED: " + navigator.platform,
            "ESTABLISHING SECURE PROXY...",
            "BYPASSING FIREWALLS [..........] 40%",
            "CRACKING WHATSAPP_SESSION_TOKENS...",
            "ACCESSING SOCIAL_MEDIA_DATABASE...",
            "DOWNLOADING BANK_FINANCIAL_LOGS...",
            "<span class='red-flash'>!!! WARNING: PASSWORD BREACH DETECTED !!!</span>",
            "PASSWORD FOUND: Admin@2026_Secure",
            "UPLOADING DATA TO SERVER: 99%...",
            "SUCCESS: FULL SYSTEM CONTROL ACQUIRED"
        ];

        function startPrank() {
            let i = 0;
            let int = setInterval(() => {
                if(i < tasks.length) {
                    logBox.innerHTML += "> " + tasks[i] + "<br>";
                    logBox.scrollTop = logBox.scrollHeight;
                    i++;
                } else {
                    clearInterval(int);
                    setTimeout(() => { 
                        alert("PRANK HACKED! Relax sweetie, sab mazak tha!");
                        window.location.href = "https://github.com"; 
                    }, 2000);
                }
            }, 1000);
        }
    </script>
</body>
</html>
