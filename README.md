<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Virtual Lucky Slots (Fun Only)</title>
    <style>
        body {
            margin: 0;
            background: #1a1a2e;
            color: #fff;
            font-family: 'Arial', sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            text-align: center;
            background: #162447;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
        }
        .slots {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 20px 0;
        }
        .slot {
            width: 80px;
            height: 80px;
            background: #e43f5a;
            font-size: 40px;
            line-height: 80px;
            text-align: center;
            border-radius: 10px;
            border: 3px solid #fff;
        }
        button {
            padding: 12px 30px;
            font-size: 18px;
            background: #1f4068;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
        }
        button:hover {
            background: #e43f5a;
        }
        .score-board {
            font-size: 20px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Virtual Lucky Slots</h2>
    <p style="color: #bbb;">Purely for Entertainment - No Real Money Involved</p>
    
    <div class="score-board">Virtual Credits: <span id="credits">100</span></div>
    
    <div class="slots">
        <div class="slot" id="slot1">🍒</div>
        <div class="slot" id="slot2">🍋</div>
        <div class="slot" id="slot3">🍇</div>
    </div>
    
    <button onclick="spin()">SPIN (Cost: 10 Credits)</button>
    <p id="message" style="font-weight: bold; margin-top: 15px;"></p>
</div>

<script>
    const items = ['🍒', '🍋', '🍇', '💎', '7️⃣'];
    let credits = 100;

    function spin() {
        if (credits < 10) {
            document.getElementById('message').innerText = "Game Over! Refresh to restart with full credits.";
            return;
        }

        // Deduct cost
        credits -= 10;
        document.getElementById('credits').innerText = credits;
        document.getElementById('message').innerText = "Spinning...";

        // Logic for Random Generation
        const res1 = items[Math.floor(Math.random() * items.length)];
        const res2 = items[Math.floor(Math.random() * items.length)];
        const res3 = items[Math.floor(Math.random() * items.length)];

        // Update UI
        document.getElementById('slot1').innerText = res1;
        document.getElementById('slot2').innerText = res2;
        document.getElementById('slot3').innerText = res3;

        // Check Win Status
        if (res1 === res2 && res2 === res3) {
            let winAmount = 50;
            if (res1 === '💎' || res1 === '7️⃣') winAmount = 100; // Jackpot elements
            credits += winAmount;
            document.getElementById('message').innerText = `🎉 JACKPOT! You won ${winAmount} Virtual Credits!`;
        } else if (res1 === res2 || res2 === res3 || res1 === res3) {
            credits += 15;
            document.getElementById('message').innerText = "Match 2! You got 15 Virtual Credits back.";
        } else {
            document.getElementById('message').innerText = "No luck this time. Try again!";
        }

        document.getElementById('credits').innerText = credits;
    }
</script>

</body>
</html>
