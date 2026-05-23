<html lang="en">
<head>
    <style>
        body { background: #000; color: #ff0000; font-family: 'Courier New', monospace; padding: 20px; }
        .alert { border: 2px solid #ff0000; padding: 20px; animation: blink 1s infinite; }
        @keyframes blink { 0% { opacity: 1; } 50% { opacity: 0; } }
        .data { color: #fff; font-size: 14px; margin-top: 20px; }
    </style>
</head>
<body>
    <div class="alert">
        <h1>WARNING: SYSTEM COMPROMISED</h1>
        <p>Your IP Address is being tracked...</p>
    </div>
    <div class="data" id="stream"></div>

    <script>
        const stream = document.getElementById('stream');
        const lines = [
            "Accessing root directory...",
            "Stealing local storage...",
            "Decrypting user passwords...",
            "Establishing connection to remote server...",
            "Uploading files: [DCIM/Photos/Private]..."
        ];
        
        let i = 0;
        setInterval(() => {
            stream.innerHTML += "<p>> " + lines[i % lines.length] + "</p>";
            i++;
        }, 800);
    </script>
</body>
</html>
