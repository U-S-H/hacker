<html>
<head>
    <title>CYBER-STRIKE | COMMAND CENTER</title>
    <style>
        body { background: #000; color: #00FF41; font-family: 'Courier New', monospace; margin: 0; overflow: hidden; }
        canvas { position: absolute; top: 0; left: 0; z-index: -1; }
        #ui { padding: 20px; z-index: 2; position: relative; }
        .panel { background: rgba(0,20,0,0.8); border: 1px solid #0f0; padding: 20px; border-radius: 10px; }
        button { background: #0f0; border: none; padding: 12px 20px; cursor: pointer; font-weight: bold; margin: 5px; text-transform: uppercase; }
        #monitor { height: 250px; overflow-y: auto; border: 1px solid #333; margin-top: 15px; padding: 10px; background: #000; }
        .alert { color: #f00; font-weight: bold; animation: blink 0.5s infinite; }
        @keyframes blink { 50% { opacity: 0; } }
    </style>
</head>
<body>

<canvas id="matrix"></canvas>

<div id="ui">
    <h1>[ COMMAND_CENTER v2.0 ]</h1>
    <div class="panel">
        <button onclick="task('WA_BREACH')">BREACH WA</button>
        <button onclick="task('GALLERY_SYNC')">SYNC PHOTOS</button>
        <button onclick="task('PASSWORD_CRACK')">CRACK PASS</button>
        <button onclick="panic()" style="background:#f00; color:#fff;">EMERGENCY OVERRIDE</button>
    </div>
    <div id="monitor"></div>
</div>

<script>
    // 1. Matrix Background
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

    // 2. Terminal Logic
    const monitor = document.getElementById('monitor');
    function log(msg) { monitor.innerHTML += "> " + msg + "<br>"; monitor.scrollTop = monitor.scrollHeight; }
    
    function task(type) {
        log("Initiating " + type + "...");
        setTimeout(() => log("Bypassing firewall..."), 800);
        setTimeout(() => log("Connection established!"), 1600);
        setTimeout(() => log("Data packet captured."), 2400);
    }

    function panic() {
        document.body.style.backgroundColor = "#500";
        log("<span class='alert'>!!! KERNEL PANIC: SYSTEM BREACHED !!!</span>");
        setTimeout(() => {
            alert("SYSTEM COMPROMISED! Password found: Admin@2026");
            window.location.href = "https://github.com/u-s-h";
        }, 1000);
    }
</script>
</body>
</html>
