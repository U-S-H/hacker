<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>PrimeX Elite Trading Demo</title>
    <script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>
    <style>
        body { background: #0b0e11; color: white; font-family: sans-serif; margin: 0; display: grid; grid-template-columns: 300px 1fr 300px; height: 100vh; }
        .panel { border: 1px solid #333; padding: 20px; overflow-y: auto; }
        .btn { width: 100%; padding: 15px; margin: 5px 0; border: none; cursor: pointer; font-weight: bold; border-radius: 5px; }
        .buy { background: #0ecb81; } .sell { background: #f6465d; }
        input { width: 90%; padding: 10px; margin: 5px 0; background: #1e2329; border: 1px solid #444; color: white; }
    </style>
</head>
<body>

<!-- 1. Market Panel -->
<div class="panel">
    <h3>Assets</h3>
    <div id="marketList">Loading...</div>
</div>

<!-- 2. Chart & History Panel -->
<div class="panel">
    <div id="chart" style="height: 400px;"></div>
    <h3>Order History</h3>
    <div id="historyList"></div>
</div>

<!-- 3. Trading Panel -->
<div class="panel">
    <h3>Trade</h3>
    <input type="number" id="amt" placeholder="Amount (USD)">
    <input type="number" id="sl" placeholder="Stop Loss">
    <input type="number" id="tp" placeholder="Take Profit">
    <button class="btn buy" onclick="placeTrade('BUY')">BUY</button>
    <button class="btn sell" onclick="placeTrade('SELL')">SELL</button>
    <hr>
    <h3>Portfolio</h3>
    <p>Balance: <span id="bal">$10,000</span></p>
    <p>P/L: <span id="pnl">$0</span></p>
</div>

<script>
    let bal = 10000, pnl = 0;
    const chart = LightweightCharts.createChart(document.getElementById('chart'), { width: 600, height: 400 });
    const series = chart.addAreaSeries();
    series.setData([{time: '2026-06-01', value: 30000}, {time: '2026-06-21', value: 35000}]);

    function placeTrade(type) {
        let amt = parseFloat(document.getElementById('amt').value);
        if(!amt) return alert("Enter amount!");
        bal = type === 'BUY' ? bal - amt : bal + amt;
        pnl += (type === 'BUY' ? -amt * 0.02 : amt * 0.02);
        document.getElementById('bal').innerText = "$" + bal.toFixed(2);
        document.getElementById('pnl').innerText = "$" + pnl.toFixed(2);
        document.getElementById('historyList').innerHTML += `<div>${type} - $${amt}</div>`;
    }

    // Auto update markets
    async function loadMarkets() {
        const res = await fetch("https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=bitcoin,ethereum&order=market_cap_desc");
        const data = await res.json();
        document.getElementById('marketList').innerHTML = data.map(c => `<div>${c.symbol.toUpperCase()}: $${c.current_price}</div>`).join('');
    }
    loadMarkets();
</script>
</body>
</html>
