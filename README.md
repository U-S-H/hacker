<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>TradeX - Paper Trading</title>
<style>
  :root { --bg: #0d1117; --card: #161b22; --border: #30363d; --green: #2ea043; --red: #f85149; --text: #c9d1d9; }
    * { margin: 0; padding: 0; box-sizing: border-box; }
  body { background: var(--bg); color: var(--text); font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; }
  header { background: var(--card); border-bottom: 1px solid var(--border); padding: 16px 24px; display: flex; justify-content: space-between; align-items: center; }
  .logo { font-size: 1.5rem; font-weight: 700; color: #58a6ff; }
  .balance { font-size: 1.2rem; }
  .balance span { color: var(--green); font-weight: 700; }
  .wrap { max-width: 1200px; margin: 24px auto; padding: 0 16px; display: grid; grid-template-columns: 2fr 1fr; gap: 20px; }
  @media(max-width: 900px) { .wrap { grid-template-columns: 1fr; } }
  .card { background: var(--card); border: 1px solid var(--border); border-radius: 8px; padding: 20px; }
  .tabs { display: flex; gap: 8px; margin-bottom: 16px; }
  .tab { padding: 8px 16px; background: transparent; border: 1px solid var(--border); color: var(--text); border-radius: 6px; cursor: pointer; }
  .tab.active { background: #1f6feb; border-color: #1f6feb; }
  #chart { width: 100%; height: 300px; background: #010409; border-radius: 6px; }
  .stock-list { display: flex; flex-direction: column; gap: 12px; }
  .stock-row { display: flex; justify-content: space-between; align-items: center; padding: 12px; border: 1px solid var(--border); border-radius: 6px; }
  .price.up { color: var(--green); }
  .price.down { color: var(--red); }
  input[type="number"] { background: var(--bg); border: 1px solid var(--border); color: var(--text); padding: 8px; width: 80px; border-radius: 6px; }
  .btn { padding: 8px 16px; border: none; border-radius: 6px; font-weight: 600; cursor: pointer; }
  .btn-buy { background: var(--green); color: #fff; }
  .btn-sell { background: var(--red); color: #fff; }
  .portfolio-item { display: flex; justify-content: space-between; padding: 10px 0; border-bottom: 1px solid var(--border); }
  .note { margin-top: 16px; font-size: 0.85rem; color: #8b949e; text-align: center; }
</style>
</head>
<body>

<header>
  <div class="logo">TradeX Demo</div>
  <div class="balance">Balance: $<span id="bal">10000.00</span></div>
</header>

<div class="wrap">
  <div class="card">
    <div class="tabs">
      <button class="tab active" onclick="switchStock('AAPL')">AAPL</button>
      <button class="tab" onclick="switchStock('TSLA')">TSLA</button>
      <button class="tab" onclick="switchStock('BTC')">BTC</button>
    </div>
    <canvas id="chart"></canvas>
    <div id="orderBox" style="margin-top: 20px;"></div>
  </div>

  <div class="card">
    <h3 style="margin-bottom: 16px;">Portfolio</h3>
    <div id="portfolio"></div>
    <h3 style="margin: 24px 0 16px;">Market</h3>
    <div class="stock-list" id="market"></div>
  </div>
</div>

<p class="note">⚠️ Demo Only. No real money. Educational purpose.</p>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import { getDatabase, ref, set, onValue, update } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";

const firebaseConfig = {
  apiKey: "AIzaSyCsgXPW-h2NzAHMrDBIL_HjlU8wSpcgzvI",
  authDomain: "course-3cc77.firebaseapp.com",
  databaseURL: "https://course-3cc77-default-rtdb.firebaseio.com",
  projectId: "course-3cc77",
  storageBucket: "course-3cc77.firebasestorage.app",
  messagingSenderId: "136140432667",
  appId: "1:136140432667:web:9f543dc3db8683944ddfbe"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app);
const uid = "user1";

let balance = 10000;
let portfolio = {};
let currentStock = 'AAPL';
let prices = { AAPL: [], TSLA: [], BTC: [] };
let lastPrice = { AAPL: 150, TSLA: 250, BTC: 60000 };

// Load user data
onValue(ref(db, 'users/' + uid), snap => {
  const data = snap.val();
  if (data) {
    balance = data.balance || 10000;
    portfolio = data.portfolio || {};
  } else {
    set(ref(db, 'users/' + uid), { balance, portfolio });
  }
  renderAll();
});

// Generate price history
function genPrice(base) {
  let p = base + (Math.random() - 0.5) * 5;
  return Math.max(1, p);
}

setInterval(() => {
  for (let s in lastPrice) {
    lastPrice[s] = genPrice(lastPrice[s]);
    prices[s].push(lastPrice[s]);
    if (prices[s].length > 60) prices[s].shift();
  }
  drawChart();
  renderMarket();
  renderPortfolio();
}, 2000);

function switchStock(s) {
  currentStock = s;
  document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
  event.target.classList.add('active');
  drawChart();
  renderOrderBox();
}

function buy() {
  const qty = parseInt(document.getElementById('qty').value);
  const cost = lastPrice[currentStock] * qty;
  if (cost > balance) return alert('Insufficient balance');
  balance -= cost;
  portfolio[currentStock] = (portfolio[currentStock] || 0) + qty;
  save();
}

function sell() {
  const qty = parseInt(document.getElementById('qty').value);
  if (!portfolio[currentStock] || portfolio[currentStock] < qty) return alert('Not enough shares');
  balance += lastPrice[currentStock] * qty;
  portfolio[currentStock] -= qty;
  if (portfolio[currentStock] === 0) delete portfolio[currentStock];
  save();
}

function save() {
  update(ref(db, 'users/' + uid), { balance, portfolio });
}

function drawChart() {
  const canvas = document.getElementById('chart');
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth;
  canvas.height = 300;
  const data = prices[currentStock];
  if (data.length < 2) return;
  
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.strokeStyle = '#58a6ff';
  ctx.lineWidth = 2;
  ctx.beginPath();
  
  const min = Math.min(...data), max = Math.max(...data);
  data.forEach((p, i) => {
    const x = (i / (data.length - 1)) * canvas.width;
    const y = canvas.height - ((p - min) / (max - min || 1)) * canvas.height;
    i === 0 ? ctx.moveTo(x, y) : ctx.lineTo(x, y);
  });
  ctx.stroke();
}

function renderOrderBox() {
  document.getElementById('orderBox').innerHTML = `
    <h4>Trade ${currentStock} - $${lastPrice[currentStock].toFixed(2)}</h4>
    <div style="margin-top: 12px; display: flex; gap: 10px; align-items: center;">
      <input type="number" id="qty" value="1" min="1">
      <button class="btn btn-buy" onclick="buy()">Buy</button>
      <button class="btn btn-sell" onclick="sell()">Sell</button>
    </div>
  `;
}

function renderMarket() {
  let html = '';
  for (let s in lastPrice) {
    const change = ((lastPrice[s] - prices[s][0] || lastPrice[s]) / lastPrice[s] * 100).toFixed(2);
    const cls = change >= 0 ? 'up' : 'down';
    html += `
      <div class="stock-row">
        <div><b>${s}</b></div>
        <div class="price ${cls}">$${lastPrice[s].toFixed(2)} ${change}%</div>
      </div>
    `;
  }
  document.getElementById('market').innerHTML = html;
}

function renderPortfolio() {
  document.getElementById('bal').textContent = balance.toFixed(2);
  let html = '';
  for (let s in portfolio) {
    const val = portfolio[s] * lastPrice[s];
    const pl = val - (portfolio[s] * 150); // dummy avg buy price
    html += `<div class="portfolio-item"><span>${s} x${portfolio[s]}</span><span>$${val.toFixed(2)}</span></div>`;
  }
  document.getElementById('portfolio').innerHTML = html || '<p>No holdings</p>';
}

function renderAll() {
  renderOrderBox();
  renderMarket();
  renderPortfolio();
  drawChart();
}

window.buy = buy;
window.sell = sell;
window.switchStock = switchStock;
</script>
</body>
</html>
