<html lang="ur" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>Pro Trade App Terminal</title>
    <style>
        :root { --bg: #0b0e11; --card: #1e2329; --green: #00c087; --red: #ff5252; --text: #fff; --hover: #2b3139; }
        body { margin: 0; background: var(--bg); color: var(--text); font-family: 'Segoe UI', sans-serif; transition: 0.5s; overflow: hidden; }
        .app-grid { display: grid; grid-template-rows: 60px 1fr; height: 100vh; }
        .nav { background: var(--card); padding: 0 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #333; z-index: 10; }
        .main-content { display: grid; grid-template-columns: 3fr 1.2fr; flex: 1; overflow: hidden; }
        .chart-container { background: #000; position: relative; }
        .trade-panel { background: var(--card); padding: 20px; display: flex; flex-direction: column; gap: 15px; border-right: 1px solid #333; }
        .card { background: var(--hover); padding: 15px; border-radius: 12px; transition: transform 0.2s; }
        .card:hover { transform: translateY(-3px); }
        input, select { width: 90%; padding: 12px; background: var(--bg); border: 1px solid #444; color: var(--text); border-radius: 8px; font-size: 1rem; }
        .btn { width: 100%; padding: 15px; border: none; border-radius: 8px; cursor: pointer; font-weight: bold; font-size: 1.1rem; transition: 0.2s; color: white; }
        .buy { background: var(--green); } .sell { background: var(--red); }
        .btn:active { transform: scale(0.98); }
        .hidden { display: none; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
        .animated { animation: fadeIn 0.5s ease-in; }
    </style>
</head>
<body>

<div class="app-grid animated">
    <div class="nav">
        <h2 onclick="handleAdminTap()" style="cursor: pointer; animation: pulse 2s infinite;">PRO TRADE</h2>
        <div class="card" style="padding: 10px 20px;">Balance: $<span id="balance">0.00</span></div>
    </div>

    <div class="main-content">
        <div class="chart-container" id="tv_chart"></div>
        <div class="trade-panel">
            <div class="card">
                <h3>Trade Actions</h3>
                <div style="display:flex; gap:10px;">
                    <button onclick="openTab('deposit')" style="background:#4a90e2; padding:10px 15px;">Deposit</button>
                    <button onclick="openTab('withdraw')" style="background:#f39c12; padding:10px 15px;">Withdraw</button>
                </div>
            </div>

            <div class="card">
                <h3>Fixed-Time Trade</h3>
                <label>Amount ($)</label>
                <input type="number" id="tradeAmt" placeholder="100">
                <label style="margin-top:10px;">Duration</label>
                <select id="tradeDuration">
                    <option value="60">1 Min</option>
                    <option value="120">2 Mins</option>
                    <option value="300">5 Mins</option>
                    <option value="900">15 Mins</option>
                </select>
                <div style="display:flex; gap:10px; margin-top:15px;">
                    <button class="btn buy" onclick="executeTrade('BUY')">UP / CALL</button>
                    <button class="btn sell" onclick="executeTrade('SELL')">DOWN / PUT</button>
                </div>
            </div>

            <div class="card">
                <h3>Current Positions</h3>
                <div id="activeTrades" style="font-size:0.9rem;">No active trades.</div>
            </div>

            <div id="admin-panel" class="card hidden" style="border: 1px solid red;">
                <h3>Admin Panel</h3>
                <p>Pending database requests log.</p>
            </div>
        </div>
    </div>
</div>

<script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
    import { getFirestore, doc, onSnapshot, updateDoc, increment, addDoc, collection, query, where, getDocs } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

    const config = { /* Apni Configuration Yahan Rakhein */ };
    const db = getFirestore(initializeApp(config));
    const uid = "test_user_id";

    // 1. Professional Trading Logic (Fixed-Time)
    window.executeTrade = async (type) => {
        const amt = parseFloat(document.getElementById('tradeAmt').value);
        const duration = parseInt(document.getElementById('tradeDuration').value);
        const startTime = new Date();
        const endTime = new Date(startTime.getTime() + duration * 1000);

        await addDoc(collection(db, "activeTrades"), { uid, type, amount: amt, startTime, endTime, status: 'OPEN' });
        alert(type + " Trade initialized for " + duration/60 + " min!");
        updateActiveTrades();
    };

    // 2. Real-time Database for Trades and Balance
    onSnapshot(doc(db, "users", uid), (snap) => {
        document.getElementById("balance").innerText = snap.data().balance.toFixed(2);
    });

    // 3. User Wallet Flow (Integrated)
    window.openTab = async (type) => {
        const amt = prompt(type.toUpperCase() + " Amount ($):");
        await addDoc(collection(db, "walletRequests"), { uid, amount: parseFloat(amt), type, status: "PENDING", time: new Date() });
        alert(type + " Request submitted!");
    };

    // 4. Admin
    let tCount = 0;
    window.handleAdminTap = () => {
        tCount++;
        if(tCount === 5) {
            if(prompt("Secret Key:") === "5426224") document.getElementById('admin-panel').classList.remove('hidden');
            tCount = 0;
        }
    };
</script>

<script src="https://s3.tradingview.com/tv.js"></script>
<script>
    new TradingView.widget({"container_id": "tv_chart", "symbol": "BINANCE:BTCUSDT", "theme": "dark", "autosize": true});
</script>

</body>
</html>
