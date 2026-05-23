<html>
<head>
    <style>
        body { background: #000; color: #0f0; font-family: 'Courier New', monospace; padding: 20px; }
        .panel { border: 2px solid #0f0; padding: 20px; margin-top: 20px; }
        button { background: #0f0; border: none; padding: 10px; cursor: pointer; font-weight: bold; margin: 5px; }
        #monitor { height: 300px; overflow-y: scroll; border: 1px solid #333; margin-top: 20px; padding: 10px; }
        .red { color: red; }
    </style>
</head>
<body>
    <h1>[ CYBER-STRIKE COMMAND CENTER ]</h1>
    <div class="panel">
        <button onclick="log('Initiating WhatsApp Breach...')">BREACH WA</button>
        <button onclick="log('Accessing Gallery Files...')">STEAL PHOTOS</button>
        <button onclick="log('Decrypting Password Database...')">CRACK PASS</button>
        <button onclick="triggerAlarm()">EMERGENCY OVERRIDE</button>
    </div>
    <div id="monitor"></div>

    <script>
        function log(msg) {
            const m = document.getElementById('monitor');
            m.innerHTML += "> " + msg + "<br>";
            m.scrollTop = m.scrollHeight;
        }
        function triggerAlarm() {
            document.body.style.backgroundColor = "red";
            log('<span class="red">!!! SYSTEM ALERT: KERNEL PANIC !!!</span>');
            setTimeout(() => { document.body.style.backgroundColor = "black"; }, 500);
        }
    </script>
</body>
</html>
