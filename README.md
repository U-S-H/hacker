<html lang="ur">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Paper Trading Demo</title>
<style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'Segoe UI', sans-serif; background: #0a0e27; color: #fff; padding: 20px; }
 .container { max-width: 1000px; margin: auto; }
  h1 { text-align: center; margin-bottom: 20px; color: #00d4aa; }
 .balance { background: #1e2340; padding: 20px; border-radius: 12px; text-align: center; margin-bottom: 20px; }
 .balance h2 { font-size: 2rem; color: #00d4aa; }
 .grid { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
  @media(max-width: 768px) {.grid { grid-template-columns: 1fr; } }
 .card { background: #1e2340; padding: 20px; border-radius: 12px; }
 .stock { display: flex; justify-content: space-between; align-items: center; padding: 12px; margin: 8px 0; background: #2a3150; border-radius: 8px; }
 .price { font-weight: bold; font-size: 1.2rem; }
 .up { color: #00d4aa; }
 .down { color: #ff4d4d; }
  button { background: #00d4aa; color: #0a0e27; border: none; padding: 8px 16px; border-radius: 6px; cursor: pointer; font-weight: bold; }
  button.sell { background: #ff4d4d; color: #fff; }
  input { width: 60px; padding: 6px; border-radius: 6px; border: none; background: #0a0e27; color: #fff; margin: 0 5px; }
 .note { text-align: center; margin-top: 20px; font-size: 0.9rem; color: #888; }
</style>
</head>
<body>
<div class="container">
  <h1>📈 Paper Trading Demo</h1>

  <div class="balance">
    <p>Balance</p>
    <h2 id="balance">$10,000.00</h2>
  </div>

  <div class="grid">
    <div class="card">
      <h3>Market</h3>
      <div id="market"></div>
    </div>
    <div class="card">
      <h3>Mera Portfolio</h3>
      <div id="portfolio">Koi share nahi khareeda abhi</div>
    </div>
  </div>

  <p class="note">⚠️ Ye sirf demo hai. Real trading nahi hai. Prices random update hoti hain.</p>
</div>

<script type="module">
import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";
import { getDatabase, ref, set, onValue, update } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-app.js";

// Tumhara Firebase config
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
import { getDatabase } from "https://www.gstatic.com/firebasejs/10.12.2/firebase-database.js";
const db = getDatabase(app);

const userId = "demo-user"; // Baad me auth add kar sakte ho
const stocks = { AAPL: 150, TSLA: 250, GOOGL: 2800, BTC: 60000 };

let balance = 10000;
let portfolio = {};

// Load data
onValue(ref(db, 'users/' + userId), (snap) => {
  const data = snap.val();
  if (data) {
    balance = data.balance || 10000;
    portfolio = data.portfolio || {};
  } else {
    set(ref(db, 'users/' + userId), { balance: 10000, portfolio: {} });
  }
  updateUI();
});

// Prices har 3 sec me update
setInterval(() => {
  for (let s in stocks) {
    let change = (Math.random() - 0.5) * 10;
    stocks[s] = Math.max(1, stocks[s] + change);
  }
  updateUI();
}, 3000);

function buy(symbol) {
  let qty = parseInt(document.getElementById('qty-' + symbol).value);
  let cost = stocks[symbol] * qty;
  if (cost > balance) return alert("Balance kam hai!");
  balance -= cost;
  portfolio[symbol] = (portfolio[symbol] || 0) + qty;
  saveData();
}

function sell(symbol) {
  let qty = parseInt(document.getElementById('qty-' + symbol).value);
  if (!portfolio[symbol] || portfolio[symbol] < qty) return alert("Itne share nahi hain!");
  balance += stocks[symbol] * qty;
  portfolio[symbol] -= qty;
  if (portfolio[symbol] === 0) delete portfolio[symbol];
  saveData();
}

function saveData() {
  update(ref(db, 'users/' + userId), { balance, portfolio });
}

function updateUI() {
  document.getElementById('balance').textContent = '$' + balance.toFixed(2);

  let marketHTML = '';
  for (let s in stocks) {
    let prev = stocks[s] - ((Math.random() - 0.5) * 10);
    let cls = stocks[s] > prev? 'up' : 'down';
    marketHTML += `
      <div class="stock">
        <div>
          <b>${s}</b><br>
          <span class="price ${cls}">$${stocks[s].toFixed(2)}</span>
        </div>
        <div>
          <input type="number" id="qty-${s}" value="1" min="1">
          <button onclick="buy('${s}')">Buy</button>
          <button class="sell" onclick="sell('${s}')">Sell</button>
        </div>
      </div>
    `;
  }
  document.getElementById('market').innerHTML = marketHTML;

  let portHTML = '';
  for (let s in portfolio) {
    portHTML += `<div class="stock"><b>${s}</b> <span>${portfolio[s]} shares</span></div>`;
  }
  document.getElementById('portfolio').innerHTML = portHTML || 'Koi share nahi khareeda abhi';
}

window.buy = buy;
window.sell = sell;
</script>
</body>
</html>
