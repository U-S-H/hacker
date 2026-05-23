<html>
<head>
    <style>
        body { background: #000; color: #00FF41; font-family: 'Courier New', monospace; overflow: hidden; }
        #canvas { display: block; }
        .overlay { position: absolute; top: 20%; left: 10%; font-size: 24px; text-shadow: 0 0 10px #00FF41; }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="overlay">
        <h1>ACCESSING REMOTE DEVICE...</h1>
        <p id="status">ESTABLISHING CONNECTION</p>
    </div>

    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth; canvas.height = window.innerHeight;
        const drops = Array(Math.floor(canvas.width/20)).fill(0);

        function draw() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = '#00FF41';
            drops.forEach((y, i) => {
                const text = String.fromCharCode(Math.random() * 128);
                ctx.fillText(text, i * 20, y * 20);
                drops[i] = y * 20 > canvas.height ? 0 : y + 1;
            });
        }
        setInterval(draw, 33);
        
        setTimeout(() => { document.getElementById('status').innerText = "SUCCESS: ROOT PRIVILEGES GRANTED!"; }, 3000);
    </script>
</body>
</html>
