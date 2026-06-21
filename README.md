<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PrimeX Premium</title>
    <style>
        :root {
            --bg: #050505;
            --card: rgba(255, 255, 255, 0.05);
            --accent: #00f2ff;
            --text: #ffffff;
            --green: #0ecb81;
            --red: #f6465d;
        }

        body {
            background: var(--bg);
            color: var(--text);
            font-family: 'Segoe UI', sans-serif;
            margin: 0;
            padding: 20px;
            padding-bottom: 80px;
        }

        .premium-card {
            background: var(--card);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            padding: 20px;
            border-radius: 25px;
            margin-bottom: 20px;
        }

        .btn-premium {
            background: linear-gradient(45deg, #00f2ff, #7000ff);
            border: none;
            padding: 15px;
            border-radius: 15px;
            color: white;
            font-weight: bold;
            cursor: pointer;
            width: 100%;
            margin-top: 10px;
        }

        input {
            width: 100%;
            padding: 15px;
            background: rgba(255,255,255,0.1);
            border: none;
            border-radius: 15px;
            color: white;
            margin-bottom: 10px;
            box-sizing: border-box;
        }

        .hidden { display: none; }
        .green { color: var(--green); }
        .red { color: var(--red); }
    </style>
</head>
<body>

<div id="loginScreen" class="premium-card">
    <h1 style="text-align:center; color: var(--accent);">PrimeX PRO</h1>
    <input type="text" id="username" placeholder="Username">
    <input type="password" id="password" placeholder="Password">
    <button class="btn-premium" onclick="loginUser()">ENTER PLATFORM</button>
</div>

<div id="app" class="hidden">
    <div class="premium-card">
        <h2>Balance: $<span id="balance">10000</span></h2>
        <button class="btn-premium" onclick="demoDeposit()">Add $1000</button>
    </div>

    <div class="premium-card">
        <h3>Market Overview</h3>
        <div id="marketList">Loading...</div>
    </div>
</div>

<script>
    // Integration of logic from README (57).md[span_1](start_span)[span_1](end_span)
    let balance = 10000;
    let portfolio = {};
    let history = [];
    let marketData = [];

    function loginUser() {
        if(document.getElementById("username").value) {
            document.getElementById("loginScreen").classList.add("hidden");
            document.getElementById("app").classList.remove("hidden");
        }
    }

    async function loadMarkets() {
        try {
            const res = await fetch("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=bitcoin,ethereum,binancecoin,solana,ripple&order=market_cap_desc");
            marketData = await res.json();
            renderMarkets();
        } catch(err) { console.log(err); }
    }

    function renderMarkets() {
        const list = document.getElementById("marketList");
        list.innerHTML = "";
        marketData.forEach(c => {
            list.innerHTML += `
                <div style="background:rgba(255,255,255,0.05); padding:10px; border-radius:10px; margin-bottom:10px; display:flex; justify-content:space-between;">
                    <div><b>${c.name}</b><br>$${c.current_price}</div>
                    <button onclick="alert('Trade ${c.symbol}')" style="background:var(--accent); border:none; padding:5px 15px; border-radius:8px;">Trade</button>
                </div>
            `;
        });
    }

    function demoDeposit() {
        balance += 1000;
        document.getElementById("balance").innerText = balance;
    }

    loadMarkets();
</script>

</body>
</html>
