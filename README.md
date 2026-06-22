<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vestify Pro - Live Trading Simulator</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: { darkBg: '#0b0f19', cardBg: '#111827', accentGreen: '#10b981', accentRed: '#ef4444' }
                }
            }
        }
    </script>
</head>
<body class="bg-darkBg text-gray-100 font-sans antialiased">

    <!-- Navbar -->
    <nav class="border-b border-gray-800 bg-darkBg/50 backdrop-blur-md sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-2">
                <div class="w-8 h-8 bg-accentGreen rounded-lg flex items-center justify-center font-bold text-darkBg">V</div>
                <span class="text-xl font-bold tracking-wider text-white">Vestify<span class="text-accentGreen">Pro</span></span>
            </div>
            <span class="bg-gray-800 text-xs text-accentGreen font-mono px-3 py-1 rounded-full border border-gray-700">Live Trading Engine V1</span>
        </div>
    </nav>

    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        
        <!-- Live Market Ticker -->
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-8">
            <div class="bg-cardBg border border-gray-800 p-4 rounded-xl flex justify-between items-center">
                <div>
                    <p class="text-xs text-gray-400 font-semibold uppercase">Bitcoin (BTC/USD)</p>
                    <p id="btcPrice" class="text-2xl font-mono font-bold text-accentGreen mt-1">$65,000.00</p>
                </div>
                <span id="btcBadge" class="text-xs font-bold text-accentGreen bg-emerald-500/10 px-2 py-1 rounded">Stable</span>
            </div>
            <div class="bg-cardBg border border-gray-800 p-4 rounded-xl flex justify-between items-center">
                <div>
                    <p class="text-xs text-gray-400 font-semibold uppercase">Ethereum (ETH/USD)</p>
                    <p id="ethPrice" class="text-2xl font-mono font-bold text-accentGreen mt-1">$3,400.00</p>
                </div>
                <span id="ethBadge" class="text-xs font-bold text-accentGreen bg-emerald-500/10 px-2 py-1 rounded">Stable</span>
            </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
            
            <!-- Trading Terminal (Order Form) -->
            <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                <h2 class="text-lg font-semibold text-white mb-4">Place Trade</h2>
                
                <div class="space-y-4">
                    <div>
                        <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Select Asset</label>
                        <select id="tradeAsset" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white focus:outline-none focus:border-accentGreen">
                            <option value="BTC">Bitcoin (BTC)</option>
                            <option value="ETH">Ethereum (ETH)</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Amount (Tokens)</label>
                        <input type="number" id="tradeAmount" value="0.1" step="0.01" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white font-mono focus:outline-none focus:border-accentGreen">
                    </div>

                    <div class="grid grid-cols-2 gap-2">
                        <div>
                            <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Take Profit ($)</label>
                            <input type="number" id="tradeTP" placeholder="Optional Target" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white text-sm font-mono focus:outline-none focus:border-accentGreen">
                        </div>
                        <div>
                            <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Stop Loss ($)</label>
                            <input type="number" id="tradeSL" placeholder="Optional Floor" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white text-sm font-mono focus:outline-none focus:border-accentRed">
                        </div>
                    </div>

                    <div class="grid grid-cols-2 gap-4 pt-4">
                        <button onclick="executeTrade('BUY')" class="bg-accentGreen hover:bg-emerald-600 text-darkBg font-bold py-3 rounded-xl transition uppercase tracking-wider text-sm shadow-md">Buy / Long</button>
                        <button onclick="executeTrade('SELL')" class="bg-accentRed hover:bg-red-600 text-white font-bold py-3 rounded-xl transition uppercase tracking-wider text-sm shadow-md">Sell / Short</button>
                    </div>
                </div>
            </div>

            <!-- Active Positions Monitor (Stop/Close Interface) -->
            <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl lg:col-span-2 flex flex-col justify-between">
                <div>
                    <div class="flex justify-between items-center mb-4">
                        <h2 class="text-lg font-semibold text-white">Active Open Positions</h2>
                        <span class="text-xs text-gray-400">Auto-triggers active</span>
                    </div>
                    
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead>
                                <tr class="border-b border-gray-800 text-xs font-semibold uppercase text-gray-400">
                                    <th class="pb-3">Asset</th>
                                    <th class="pb-3">Type</th>
                                    <th class="pb-3">Entry</th>
                                    <th class="pb-3">Current</th>
                                    <th class="pb-3">TP / SL</th>
                                    <th class="pb-3 text-right">Action</th>
                                </tr>
                            </thead>
                            <tbody id="positionsTable" class="divide-y divide-gray-800/50">
                                <!-- Dynamic rows inserted here -->
                                <tr id="emptyRow"><td colspan="6" class="py-8 text-center text-gray-500">No open positions. Place a trade to start!</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <script>
        // Live Price State
        let prices = { BTC: 65000.00, ETH: 3400.00 };
        let positions = [];

        // 1. Simulate Market Volatility (Up / Down)
        setInterval(() => {
            ['BTC', 'ETH'].forEach(asset => {
                const changePercent = (Math.random() * 0.4 - 0.2) / 100; // -0.2% to +0.2%
                const oldPrice = prices[asset];
                prices[asset] = oldPrice * (1 + changePercent);

                // Update UI Price Text
                const el = document.getElementById(`${asset.toLowerCase()}Price`);
                const badge = document.getElementById(`${asset.toLowerCase()}Badge`);
                el.innerText = `$${prices[asset].toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;

                if (prices[asset] > oldPrice) {
                    el.className = "text-2xl font-mono font-bold text-accentGreen mt-1";
                    badge.innerText = "▲ UP";
                    badge.className = "text-xs font-bold text-accentGreen bg-emerald-500/10 px-2 py-1 rounded";
                } else {
                    el.className = "text-2xl font-mono font-bold text-accentRed mt-1";
                    badge.innerText = "▼ DOWN";
                    badge.className = "text-xs font-bold text-accentRed bg-red-500/10 px-2 py-1 rounded";
                }
            });

            // Check triggers (Stop Loss / Take Profit)
            checkOrderTriggers();
            renderPositions();
        }, 2000);

        // 2. Execute Trade (Add to open positions)
        function executeTrade(type) {
            const asset = document.getElementById('tradeAsset').value;
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            const tp = parseFloat(document.getElementById('tradeTP').value) || null;
            const sl = parseFloat(document.getElementById('tradeSL').value) || null;
            
            if (amount <= 0) return alert("Please enter a valid amount!");

            const newPosition = {
                id: Date.now(),
                asset: asset,
                type: type,
                entryPrice: prices[asset],
                amount: amount,
                tp: tp,
                sl: sl
            };

            positions.push(newPosition);
            
            // Clear Form inputs
            document.getElementById('tradeTP').value = '';
            document.getElementById('tradeSL').value = '';
            renderPositions();
        }

        // 3. Manual Close Position (Stop/Close Button)
        function closePosition(id) {
            positions = positions.filter(pos => pos.id !== id);
            renderPositions();
        }

        // 4. Automated Triggers (TP/SL Core Logic)
        function checkOrderTriggers() {
            positions.forEach((pos, index) => {
                const currentPrice = prices[pos.asset];
                let shouldClose = false;

                if (pos.type === 'BUY') {
                    if (pos.tp && currentPrice >= pos.tp) shouldClose = true; // Take Profit hit
                    if (pos.sl && currentPrice <= pos.sl) shouldClose = true; // Stop Loss hit
                } else if (pos.type === 'SELL') {
                    if (pos.tp && currentPrice <= pos.tp) shouldClose = true; // Take Profit hit
                    if (pos.sl && currentPrice >= pos.sl) shouldClose = true; // Stop Loss hit
                }

                if (shouldClose) {
                    positions.splice(index, 1);
                    alert(`Order automated trigger executed! Position closed for ${pos.asset}.`);
                }
            });
        }

        // 5. Render Positions Table
        function renderPositions() {
            const tbody = document.getElementById('positionsTable');
            if (positions.length === 0) {
                tbody.innerHTML = `<tr id="emptyRow"><td colspan="6" class="py-8 text-center text-gray-500">No open positions. Place a trade to start!</td></tr>`;
                return;
            }

            tbody.innerHTML = '';
            positions.forEach(pos => {
                const currentPrice = prices[pos.asset];
                const typeColor = pos.type === 'BUY' ? 'text-accentGreen bg-emerald-500/10' : 'text-accentRed bg-red-500/10';
                
                const row = document.createElement('tr');
                row.className = "hover:bg-gray-800/20 transition";
                row.innerHTML = `
                    <td class="py-3 font-semibold text-white">${pos.asset} (${pos.amount})</td>
                    <td class="py-3"><span class="px-2 py-0.5 text-xs font-bold rounded ${typeColor}">${pos.type}</span></td>
                    <td class="py-3 font-mono text-gray-400">$${pos.entryPrice.toFixed(2)}</td>
                    <td class="py-3 font-mono text-white">$${currentPrice.toFixed(2)}</td>
                    <td class="py-3 font-mono text-xs text-gray-400">
                        TP: ${pos.tp ? '$' + pos.tp : 'None'}<br>SL: ${pos.sl ? '$' + pos.sl : 'None'}
                    </td>
                    <td class="py-3 text-right">
                        <button onclick="closePosition(${pos.id})" class="bg-gray-800 hover:bg-accentRed text-gray-300 hover:text-white px-3 py-1 rounded text-xs font-medium transition">
                            Close
                        </button>
                    </td>
                `;
                tbody.appendChild(row);
            });
        }
    </script>
</body>
</html>
