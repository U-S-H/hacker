<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Pro Trade Platform</title>
    <style>
        body { background: #0f172a; color: #f8fafc; font-family: 'Segoe UI', sans-serif; padding: 20px; }
        .dashboard { display: grid; grid-template-columns: 250px 1fr; gap: 20px; }
        .card { background: #1e293b; padding: 15px; border-radius: 10px; margin-bottom: 10px; }
        .btn { padding: 10px; cursor: pointer; border: none; border-radius: 5px; width: 45%; margin: 5px; font-weight: bold; }
        .buy { background: #22c55e; color: white; }
        .sell { background: #ef4444; color: white; }
        #admin-trigger { cursor: pointer; text-align: center; padding: 10px; border-bottom: 1px solid #334155; }
    </style>
</head>
<body>

<div class="dashboard">
    <aside class="card">
        <h2 id="admin-trigger">Trade Dashboard</h2>
        <h3>Wallet Balance</h3>
        <p style="font-size: 24px;">$<span id="balance">1000.00</span></p>
        <h3>Trade History</h3>
        <ul id="history-list" style="font-size: 12px;"></ul>
    </aside>
    
    <main id="market-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
        <!-- Market cards will appear here -->
    </main>
</div>

<script>
    let balance = parseFloat(localStorage.getItem('balance')) || 1000.00;
    let history = JSON.parse(localStorage.getItem('history')) || [];
    let tapCount = 0;

    // Secret Admin Trigger
    document.getElementById('admin-trigger').addEventListener('click', () => {
        tapCount++;
        if (tapCount === 5) {
            alert("Admin Panel Unlocked! (Simulation Active)");
            tapCount = 0;
        }
    });

    function updateUI() {
        document.getElementById('balance').innerText = balance.toFixed(2);
        localStorage.setItem('balance', balance);
        const list = document.getElementById('history-list');
        list.innerHTML = history.slice(-8).map(item => `<li>${item}</li>`).join('');
    }

    async function fetchMarkets() {
        try {
            const res = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&per_page=6');
            const data = await res.json();
            const grid = document.getElementById('market-grid');
            grid.innerHTML = data.map(coin => `
                <div class="card">
                    <h3>${coin.symbol.toUpperCase()}</h3>
                    <p>Price: $${coin.current_price.toLocaleString()}</p>
                    <button class="btn buy" onclick="trade('${coin.symbol}', ${coin.current_price}, 'buy')">Buy</button>
                    <button class="btn sell" onclick="trade('${coin.symbol}', ${coin.current_price}, 'sell')">Sell</button>
                </div>
            `).join('');
        } catch (e) { console.error(e); }
    }

    function trade(symbol, price, type) {
        if (type === 'buy') {
            if (balance >= price) {
                balance -= price;
                history.push(`Bought ${symbol.toUpperCase()} @ $${price}`);
            } else { alert("Insufficient funds, sweetie!"); return; }
        } else {
            balance += price;
            history.push(`Sold ${symbol.toUpperCase()} @ $${price}`);
        }
        localStorage.setItem('history', JSON.stringify(history));
        updateUI();
    }

    updateUI();
    fetchMarkets();
    setInterval(fetchMarkets, 60000); // Auto-update prices every minute
</script>
</body>
</html>
