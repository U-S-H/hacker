<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vestify Pro - Institutional Multi-Asset Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
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

    <!-- Auth Screen -->
    <div id="authScreen" class="fixed inset-0 bg-darkBg z-50 flex items-center justify-center p-4">
        <div class="bg-cardBg border border-gray-800 p-8 rounded-2xl shadow-2xl w-full max-w-md">
            <div class="flex items-center space-x-2 justify-center mb-6">
                <div class="w-8 h-8 bg-accentGreen rounded-lg flex items-center justify-center font-bold text-darkBg">V</div>
                <span class="text-2xl font-bold tracking-wider text-white">Vestify<span class="text-accentGreen">Pro</span></span>
            </div>
            <h2 id="authTitle" class="text-xl font-semibold text-center text-white mb-6">Login to your account</h2>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Email Address</label>
                    <input type="email" id="authEmail" placeholder="name@example.com" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white focus:outline-none focus:border-accentGreen">
                </div>
                <div>
                    <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Password</label>
                    <input type="password" id="authPassword" placeholder="••••••••" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white focus:outline-none focus:border-accentGreen">
                </div>
                <button id="mainAuthBtn" class="w-full bg-accentGreen hover:bg-emerald-600 text-darkBg font-bold py-2.5 rounded-lg transition tracking-wider text-sm mt-2">Login</button>
                <div class="relative flex py-2 items-center">
                    <div class="flex-grow border-t border-gray-800"></div>
                    <span class="flex-shrink mx-4 text-gray-500 text-xs uppercase">Or</span>
                    <div class="flex-grow border-t border-gray-800"></div>
                </div>
                <button id="googleAuthBtn" class="w-full bg-gray-800 hover:bg-gray-700 text-white font-medium py-2.5 rounded-lg transition text-sm flex items-center justify-center space-x-2 border border-gray-700">
                    <span>Sign in with Google</span>
                </button>
            </div>
            <p class="text-xs text-center text-gray-400 mt-6">
                <span id="authToggleText">Don't have an account?</span> 
                <button id="authToggleBtn" class="text-accentGreen hover:underline font-medium ml-1">Sign Up</button>
            </p>
        </div>
    </div>

    <!-- Main Platform App Dashboard -->
    <div id="dashboardScreen" class="hidden">
        <nav class="border-b border-gray-800 bg-darkBg/50 backdrop-blur-md sticky top-0 z-50">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
                <div class="flex items-center space-x-2">
                    <div class="w-8 h-8 bg-accentGreen rounded-lg flex items-center justify-center font-bold text-darkBg">V</div>
                    <span class="text-xl font-bold tracking-wider text-white">Vestify<span class="text-accentGreen">Pro</span></span>
                </div>
                <div class="flex items-center space-x-4">
                    <span id="userEmailDisplay" class="text-xs text-gray-400 bg-gray-900 border border-gray-800 px-3 py-1.5 rounded-lg font-mono"></span>
                    <button id="logoutBtn" class="text-xs font-semibold bg-gray-800 hover:bg-red-900 text-gray-300 hover:text-white px-3 py-1.5 rounded-lg transition border border-gray-700">Logout</button>
                </div>
            </div>
        </nav>

        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6">
            
            <!-- Financial Metric Tickers -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4 mb-6">
                <div class="bg-cardBg border border-gray-800 p-4 rounded-xl border-l-4 border-accentGreen">
                    <p class="text-xs font-medium text-gray-400 uppercase">Available Capital</p>
                    <p id="walletBalanceDisplay" class="text-2xl font-mono font-bold text-white mt-1">$10,000.00</p>
                    <button id="resetBalanceBtn" class="text-[10px] text-accentGreen hover:underline mt-1 block">Reset Simulation Cash</button>
                </div>
                <div class="bg-cardBg border border-gray-800 p-4 rounded-xl">
                    <p class="text-xs font-medium text-gray-400 uppercase">Net Account Equity</p>
                    <p id="totalAccountDisplay" class="text-2xl font-mono font-bold text-white mt-1">$10,000.00</p>
                    <span class="text-[10px] text-gray-500">Includes live unrealized performance matrix</span>
                </div>
                <div class="bg-cardBg border border-gray-800 p-4 rounded-xl flex justify-between items-center">
                    <div>
                        <p class="text-xs font-medium text-gray-400 uppercase">Selected Asset Focus</p>
                        <p id="activeAssetTitle" class="text-xl font-bold text-white mt-1">BTC/USD</p>
                    </div>
                    <div class="text-right">
                        <p id="activeAssetPrice" class="text-xl font-mono font-bold text-accentGreen">$65,000.00</p>
                        <span id="activeAssetBadge" class="text-[10px] font-bold text-accentGreen bg-emerald-500/10 px-1.5 py-0.5 rounded">▲ UP</span>
                    </div>
                </div>
            </div>

            <!-- Terminal Row Dashboard Layout -->
            <div class="grid grid-cols-1 lg:grid-cols-4 gap-6">
                
                <!-- COLUMN 1: Infinite Asset Discovery Hub -->
                <div class="bg-cardBg border border-gray-800 p-4 rounded-xl h-[620px] flex flex-col">
                    <h3 class="text-sm font-semibold text-white mb-3 uppercase tracking-wider text-gray-400">Asset Discovery</h3>
                    <input type="text" id="assetSearchInput" placeholder="Search thousands of assets... (e.g., AAPL, EURUSD, SOL)" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-accentGreen mb-3">
                    
                    <div id="assetDiscoveryList" class="flex-grow overflow-y-auto space-y-1 pr-1 custom-scrollbar">
                        <!-- Dynamic assets load here -->
                    </div>
                </div>

                <!-- COLUMN 2 & 3: Realtime Charts & Positions -->
                <div class="lg:col-span-2 flex flex-col space-y-6">
                    <!-- Chart Core Box -->
                    <div class="bg-cardBg border border-gray-800 p-4 rounded-xl">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider">Advanced Trend Feed Monitor</h3>
                            <span class="w-2 h-2 rounded-full bg-accentGreen animate-pulse"></span>
                        </div>
                        <div id="chartContainer" class="w-full h-[280px]"></div>
                    </div>

                    <!-- Active Monitor Positions Table -->
                    <div class="bg-cardBg border border-gray-800 p-4 rounded-xl flex-grow overflow-hidden flex flex-col">
                        <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-3">Active Corporate Positions</h3>
                        <div class="overflow-x-auto flex-grow max-h-[220px]">
                            <table class="w-full text-left text-xs">
                                <thead>
                                    <tr class="border-b border-gray-800 font-semibold uppercase text-gray-400">
                                        <th class="pb-2">Asset</th>
                                        <th class="pb-2">Side</th>
                                        <th class="pb-2">Entry / Current</th>
                                        <th class="pb-2">Live P&L</th>
                                        <th class="pb-2 text-right">Action</th>
                                    </tr>
                                </thead>
                                <tbody id="positionsTable" class="divide-y divide-gray-800/50">
                                    <tr id="emptyRow"><td colspan="5" class="py-6 text-center text-gray-500">No open operations detected.</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- COLUMN 4: Tactical Orders Board -->
                <div class="bg-cardBg border border-gray-800 p-4 rounded-xl h-fit">
                    <h3 class="text-sm font-semibold text-white mb-4 uppercase tracking-wider text-gray-400">Execution Panel</h3>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Target Asset Pair</label>
                            <input type="text" id="displayActiveAsset" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs font-bold text-accentGreen focus:outline-none" readonly>
                        </div>
                        <div>
                            <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Volume Allocation (Units / Tokens)</label>
                            <input type="number" id="tradeAmount" value="1" step="0.01" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs text-white font-mono focus:outline-none focus:border-accentGreen">
                            <p id="estimatedCost" class="text-[10px] text-gray-500 mt-1">Est. Exposure: $0.00</p>
                        </div>
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Take Profit ($)</label>
                                <input type="number" id="tradeTP" placeholder="Target" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-1.5 text-xs text-white font-mono focus:outline-none focus:border-accentGreen">
                            </div>
                            <div>
                                <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Stop Loss ($)</label>
                                <input type="number" id="tradeSL" placeholder="Floor" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-1.5 text-xs text-white font-mono focus:outline-none focus:border-accentRed">
                            </div>
                        </div>
                        <div class="grid grid-cols-2 gap-3 pt-2">
                            <button id="buyBtn" class="bg-accentGreen hover:bg-emerald-600 text-darkBg font-bold py-2.5 rounded-lg transition uppercase tracking-wider text-xs shadow-md">Buy / Long</button>
                            <button id="sellBtn" class="bg-accentRed hover:bg-red-600 text-white font-bold py-2.5 rounded-lg transition uppercase tracking-wider text-xs shadow-md">Sell / Short</button>
                        </div>
                    </div>
                </div>

            </div>
        </main>
    </div>

    <!-- SYSTEM CORE BACKEND EMULATION ENGINE -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

        const firebaseConfig = {
            apiKey: "AIzaSyCsgXPW-h2NzAHMrDBIL_HjlU8wSpcgzvI",
            authDomain: "course-3cc77.firebaseapp.com",
            projectId: "course-3cc77",
            appId: "1:136140432667:web:9f543dc3db8683944ddfbe"
        };

        const app = initializeApp(firebaseConfig);
        const auth = getAuth(app);
        const googleProvider = new GoogleAuthProvider();

        let isSignUpMode = false;
        const authScreen = document.getElementById('authScreen');
        const dashboardScreen = document.getElementById('dashboardScreen');
        const authTitle = document.getElementById('authTitle');
        const mainAuthBtn = document.getElementById('mainAuthBtn');
        const authToggleBtn = document.getElementById('authToggleBtn');
        const userEmailDisplay = document.getElementById('userEmailDisplay');

        // Main Ledger State Architecture
        let walletBalance = 10000.00; 
        let selectedAsset = 'BTC';
        let positions = [];
        let chartInstance = null;

        // Massive Global Dynamic Asset Engine Library Map (Hazaron Assets Simulate Karne K Liye Matrix Map)
        const assetsDatabase = {};
        const categories = ['BTC', 'ETH', 'SOL', 'BNB', 'XRP', 'ADA', 'DOT', 'DOGE', 'AVAX', 'LINK', 'AAPL', 'TSLA', 'NVDA', 'AMZN', 'MSFT', 'EURUSD', 'GBPUSD', 'USDJPY', 'GOLD', 'CRUDE'];
        
        // Dynamic Seed Generation initialization vector loop
        categories.forEach((name) => {
            let basePrice = 1.20;
            if(name.includes('USD')) basePrice = 1.15;
            if(['BTC','GOLD','BRUSH'].includes(name)) basePrice = name==='BTC' ? 65000 : 2300;
            if(['AAPL','TSLA','NVDA','MSFT'].includes(name)) basePrice = Math.random() * 300 + 100;
            if(['ETH','SOL','AVAX'].includes(name)) basePrice = name==='ETH' ? 3400 : 140;

            assetsDatabase[name] = {
                symbol: name,
                price: basePrice,
                history: Array.from({length: 15}, () => basePrice * (1 + (Math.random() * 0.04 - 0.02)))
            };
        });

        // Auth Framework Handlers
        authToggleBtn.addEventListener('click', () => {
            isSignUpMode = !isSignUpMode;
            authTitle.innerText = isSignUpMode ? "Create Your Account" : "Login to your account";
            mainAuthBtn.innerText = isSignUpMode ? "Register Account" : "Login";
        });

        mainAuthBtn.addEventListener('click', async () => {
            const email = document.getElementById('authEmail').value.trim();
            const password = document.getElementById('authPassword').value;
            try {
                if (isSignUpMode) { await createUserWithEmailAndPassword(auth, email, password); alert("Success!"); }
                else { await signInWithEmailAndPassword(auth, email, password); }
            } catch (e) { alert(e.message); }
        });

        document.getElementById('googleAuthBtn').addEventListener('click', async () => { try { await signInWithPopup(auth, googleProvider); } catch(e) { alert(e.message); } });
        document.getElementById('logoutBtn').addEventListener('click', () => signOut(auth));

        onAuthStateChanged(auth, (user) => {
            if (user) {
                authScreen.classList.add('hidden');
                dashboardScreen.classList.remove('hidden');
                userEmailDisplay.innerText = user.email || "Trader Account";
                initializeChart();
                buildAssetDiscoveryUI();
                switchAsset(selectedAsset);
            } else { authScreen.classList.remove('hidden'); dashboardScreen.classList.add('hidden'); }
        });

        // Build Asset UI Feed Grid
        function buildAssetDiscoveryUI(filter = '') {
            const list = document.getElementById('assetDiscoveryList');
            if(!list) return;
            list.innerHTML = '';
            
            Object.keys(assetsDatabase).forEach(sym => {
                if(filter && !sym.toLowerCase().includes(filter.toLowerCase())) return;
                
                const item = assetsDatabase[sym];
                const div = document.createElement('div');
                div.className = `flex justify-between items-center p-2 rounded-lg text-xs cursor-pointer transition border border-transparent ${selectedAsset === sym ? 'bg-gray-800 border-accentGreen/40' : 'hover:bg-gray-900'}`;
                div.innerHTML = `
                    <div><p class="font-bold text-white">${sym}/USD</p><p class="text-[10px] text-gray-500">Global Feed</p></div>
                    <div class="text-right"><p id="feed-p-${sym}" class="font-mono font-bold">${item.price.toFixed(2)}</p></div>
                `;
                div.addEventListener('click', () => switchAsset(sym));
                list.appendChild(div);
            });
        }

        // Active Asset Vector Switcher
        function switchAsset(symbol) {
            selectedAsset = symbol;
            document.getElementById('activeAssetTitle').innerText = `${symbol} / USD`;
            document.getElementById('displayActiveAsset').value = `${symbol} / USD`;
            buildAssetDiscoveryUI(document.getElementById('assetSearchInput').value);
            updateEstimate();
            updateChartData();
        }

        document.getElementById('assetSearchInput').addEventListener('input', (e) => {
            // Dynamic Generator logic if asset not found in database arrays matrix scale
            const query = e.target.value.toUpperCase().trim();
            if(query && !assetsDatabase[query] && query.length <= 6) {
                assetsDatabase[query] = {
                    symbol: query,
                    price: Math.random() * 500 + 10,
                    history: Array.from({length: 15}, () => (Math.random() * 500 + 10))
                };
            }
            buildAssetDiscoveryUI(e.target.value);
        });

        const updateEstimate = () => {
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            document.getElementById('estimatedCost').innerText = `Est. Exposure: $${(assetsDatabase[selectedAsset].price * amount).toFixed(2)}`;
        };
        document.getElementById('tradeAmount').addEventListener('input', updateEstimate);

        document.getElementById('resetBalanceBtn').addEventListener('click', () => { walletBalance = 10000.00; updateBalancesUI(); });

        // High Frequency Core Pricing Ticker simulation pipeline loop
        setInterval(() => {
            Object.keys(assetsDatabase).forEach(sym => {
                const asset = assetsDatabase[sym];
                const change = (Math.random() * 0.8 - 0.4) / 100;
                const oldPrice = asset.price;
                asset.price = oldPrice * (1 + change);
                asset.history.push(asset.price);
                if(asset.history.length > 20) asset.history.shift();

                const feedEl = document.getElementById(`feed-p-${sym}`);
                if(feedEl) {
                    feedEl.innerText = asset.price.toFixed(2);
                    feedEl.className = asset.price >= oldPrice ? 'font-mono text-accentGreen' : 'font-mono text-accentRed';
                }

                if(sym === selectedAsset) {
                    const priceEl = document.getElementById('activeAssetPrice');
                    const badge = document.getElementById('activeAssetBadge');
                    priceEl.innerText = `$${asset.price.toLocaleString(undefined, {minimumFractionDigits:2, maximumFractionDigits:2})}`;
                    if(asset.price >= oldPrice) {
                        priceEl.className = "text-xl font-mono font-bold text-accentGreen";
                        badge.innerText = "▲ UP"; badge.className = "text-[10px] font-bold text-accentGreen bg-emerald-500/10 px-1.5 py-0.5 rounded";
                    } else {
                        priceEl.className = "text-xl font-mono font-bold text-accentRed";
                        badge.innerText = "▼ DOWN"; badge.className = "text-[10px] font-bold text-accentRed bg-red-500/10 px-1.5 py-0.5 rounded";
                    }
                }
            });

            updateEstimate();
            checkOrderTriggers();
            renderPositions();
            updateBalancesUI();
            if(chartInstance) updateChartData();
        }, 2000);

        function calculatePNL(pos) {
            const currentPrice = assetsDatabase[pos.asset].price;
            let diff = currentPrice - pos.entryPrice;
            if (pos.type === 'SELL') diff = pos.entryPrice - currentPrice;
            return { amount: diff * pos.amount, percent: (diff / pos.entryPrice) * 100 };
        }

        function updateBalancesUI() {
            let openPnl = 0;
            positions.forEach(pos => { openPnl += calculatePNL(pos).amount; });
            document.getElementById('walletBalanceDisplay').innerText = `$${walletBalance.toLocaleString(undefined, {minimumFractionDigits:2})}`;
            document.getElementById('totalAccountDisplay').innerText = `$${(walletBalance + openPnl).toLocaleString(undefined, {minimumFractionDigits:2})}`;
        }

        function executeTrade(type) {
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            const tp = parseFloat(document.getElementById('tradeTP').value) || null;
            const sl = parseFloat(document.getElementById('tradeSL').value) || null;
            if(amount <= 0) return alert("Invalid amount.");

            const cost = assetsDatabase[selectedAsset].price * amount;
            if(cost > walletBalance) return alert("Insufficient Capital.");

            walletBalance -= cost;
            positions.push({ id: Date.now(), asset: selectedAsset, type: type, entryPrice: assetsDatabase[selectedAsset].price, amount: amount, orderValue: cost, tp: tp, sl: sl });
            
            document.getElementById('tradeTP').value = ''; document.getElementById('tradeSL').value = '';
            renderPositions(); updateBalancesUI();
        }

        function settleAndClose(id) {
            const p = positions.find(x => x.id === id);
            if(!p) return;
            walletBalance += (p.orderValue + calculatePNL(p).amount);
            positions = positions.filter(x => x.id !== id);
            renderPositions(); updateBalancesUI();
        }

        function checkOrderTriggers() {
            positions.forEach(pos => {
                const cur = assetsDatabase[pos.asset].price;
                let close = false;
                if(pos.type === 'BUY') { if((pos.tp && cur >= pos.tp) || (pos.sl && cur <= pos.sl)) close = true; }
                else { if((pos.tp && cur <= pos.tp) || (pos.sl && cur >= pos.sl)) close = true; }
                if(close) settleAndClose(pos.id);
            });
        }

        function renderPositions() {
            const tbody = document.getElementById('positionsTable');
            if(!tbody) return;
            if(positions.length === 0) { tbody.innerHTML = `<tr id="emptyRow"><td colspan="5" class="py-6 text-center text-gray-500">No open operations detected.</td></tr>`; return; }
            tbody.innerHTML = '';
            positions.forEach(pos => {
                const cur = assetsDatabase[pos.asset].price;
                const pnl = calculatePNL(pos);
                const row = document.createElement('tr');
                row.className = "hover:bg-gray-800/10 text-xs border-b border-gray-800/30";
                row.innerHTML = `
                    <td class="py-2 font-bold">${pos.asset}</td>
                    <td class="py-2"><span class="px-1 py-0.5 rounded font-bold text-[10px] ${pos.type==='BUY'?'text-accentGreen bg-emerald-500/10':'text-accentRed bg-red-500/10'}">${pos.type}</span></td>
                    <td class="py-2 font-mono text-gray-400">$${pos.entryPrice.toFixed(2)} → <span class="text-white">$${cur.toFixed(2)}</span></td>
                    <td class="py-2 font-mono font-bold ${pnl.amount>=0?'text-accentGreen':'text-accentRed'}">${pnl.amount>=0?'+':''}$${pnl.amount.toFixed(2)}</td>
                    <td class="py-2 text-right"><button data-id="${pos.id}" class="close-p-btn bg-gray-900 border border-gray-800 hover:bg-accentRed px-2 py-1 rounded text-gray-300 hover:text-white transition">Close</button></td>
                `;
                tbody.appendChild(row);
            });
            document.querySelectorAll('.close-p-btn').forEach(b => b.addEventListener('click', (e) => settleAndClose(parseInt(e.target.getAttribute('data-id')))));
        }

        // --- APEXCHARTS VISUAL VECTOR PIPELINE ---
        function initializeChart() {
            const options = {
                chart: { type: 'line', height: 260, toolbar: { show: false }, animations: { enabled: false }, background: 'transparent' },
                series: [{ name: 'Price Feed', data: [] }],
                colors: ['#10b981'],
                stroke: { width: 3, curve: 'smooth' },
                theme: { mode: 'dark' },
                grid: { borderColor: '#1f2937', strokeDashArray: 3 },
                xaxis: { labels: { show: false }, axisBorder: { show: false } },
                yaxis: { labels: { style: { colors: '#9ca3af', fontFamily: 'monospace' } } }
            };
            chartInstance = new ApexCharts(document.getElementById("chartContainer"), options);
            chartInstance.render();
        }

        function updateChartData() {
            if(!chartInstance || !assetsDatabase[selectedAsset]) return;
            chartInstance.updateSeries([{ data: assetsDatabase[selectedAsset].history }]);
        }

        document.getElementById('buyBtn').addEventListener('click', () => executeTrade('BUY'));
        document.getElementById('sellBtn').addEventListener('click', () => executeTrade('SELL'));
    </script>
</body>
</html>
