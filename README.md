<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>EliteTrade | Neo-Dashboard</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;600&display=swap');
        
        body { 
            background: radial-gradient(circle at top right, #1e293b, #0f172a); 
            color: white; font-family: 'Inter', sans-serif; margin: 0; padding: 20px; 
            min-height: 100vh;
        }
        .glass { 
            background: rgba(255, 255, 255, 0.05); backdrop-filter: blur(10px); 
            border: 1px solid rgba(255, 255, 255, 0.1); border-radius: 20px; padding: 20px;
        }
        .grid { display: grid; grid-template-columns: 300px 1fr; gap: 20px; }
        .coin-card { 
            background: rgba(255, 255, 255, 0.03); padding: 15px; border-radius: 15px;
            transition: transform 0.3s, border 0.3s; cursor: pointer;
        }
        .coin-card:hover { transform: translateY(-5px); border: 1px solid #3b82f6; }
        .btn { 
            width: 48%; padding: 10px; border-radius: 10px; border: none; 
            font-weight: 600; cursor: pointer; transition: 0.2s;
        }
        .buy { background: #10b981; color: white; }
        .sell { background: #ef4444; color: white; }
        .buy:hover { box-shadow: 0 0 15px #10b981; }
        .sell:hover { box-shadow: 0 0 15px #ef4444; }
    </style>
</head>
<body>

<div class="grid">
    <aside class="glass">
        <h2 id="admin-trigger">EliteTrade Pro</h2>
        <p style="opacity: 0.6;">Total Equity</p>
        <h1 id="balance-display">$1000.00</h1>
        <hr style="border: 0.1px solid #334155;">
        <h3>Activity Feed</h3>
        <ul id="history-list" style="list-style: none; padding: 0;"></ul>
    </aside>
    
    <main>
        <div id="market-grid" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;"></div>
    </main>
</div>

<script>
    let balance = parseFloat(localStorage.getItem('balance')) || 1000.00;
    let history = JSON.parse(localStorage.getItem('history')) || [];

    function updateUI() {
        document.getElementById('balance-display').innerText = `$${balance.toLocaleString(undefined, {minimumFractionDigits: 2})}`;
        localStorage.setItem('balance', balance);
        const list = document.getElementById('history-list');
        list.innerHTML = history.slice(-6).reverse().map(item => `<li>✅ ${item}</li>`).join('');
    }

    async function fetchMarkets() {
        const res = await fetch('https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&per_page=6');
        const data = await res.json();
        document.getElementById('market-grid').innerHTML = data.map(coin => `
            <div class="glass coin-card">
                <img src="${coin.image}" width="30">
                <h3>${coin.name}</h3>
                <p>Price: <strong>$${coin.current_price.toLocaleString()}</strong></p>
                <button class="btn buy" onclick="trade('${coin.symbol}', ${coin.current_price}, 'buy')">Buy</button>
                <button class="btn sell" onclick="trade('${coin.symbol}', ${coin.current_price}, 'sell')">Sell</button>
            </div>
        `).join('');
    }

    function trade(symbol, price, type) {
        if (type === 'buy') {
            if (balance >= price) {
                balance -= price;
                history.push(`Bought ${symbol.toUpperCase()}`);
            } else { alert("Insufficient funds, sweetie!"); return; }
        } else {
            balance += price;
            history.push(`Sold ${symbol.toUpperCase()}`);
        }
        localStorage.setItem('history', JSON.stringify(history));
        updateUI();
    }

    updateUI();
    fetchMarkets();
    setInterval(fetchMarkets, 30000);
</script>
</body>
</html>
