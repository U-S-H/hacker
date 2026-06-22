<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vestify Pro - Live Trading Engine</title>
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

                <button id="mainAuthBtn" class="w-full bg-accentGreen hover:bg-emerald-600 text-darkBg font-bold py-2.5 rounded-lg transition tracking-wider text-sm mt-2">
                    Login
                </button>

                <div class="relative flex py-2 items-center">
                    <div class="flex-grow border-t border-gray-800"></div>
                    <span class="flex-shrink mx-4 text-gray-500 text-xs uppercase">Or continue with</span>
                    <div class="flex-grow border-t border-gray-800"></div>
                </div>

                <button id="googleAuthBtn" class="w-full bg-gray-800 hover:bg-gray-700 text-white font-medium py-2.5 rounded-lg transition text-sm flex items-center justify-center space-x-2 border border-gray-700">
                    <svg class="w-4 h-4" viewBox="0 0 24 24">
                        <path fill="currentColor" d="M22.56 12.25c0-.78-.07-1.53-.2-2.25H12v4.26h5.92c-.26 1.37-1.04 2.53-2.21 3.31v2.77h3.57c2.08-1.92 3.28-4.74 3.28-8.09z"/>
                        <path fill="currentColor" d="M12 23c2.97 0 5.46-.98 7.28-2.66l-3.57-2.77c-.98.66-2.23 1.06-3.71 1.06-2.86 0-5.29-1.93-6.16-4.53H2.18v2.84C3.99 20.53 7.7 23 12 23z"/>
                        <path fill="currentColor" d="M5.84 14.09c-.22-.66-.35-1.36-.35-2.09s.13-1.43.35-2.09V7.06H2.18C1.43 8.55 1 10.22 1 12s.43 3.45 1.18 4.94l2.85-2.22.81-.63z"/>
                        <path fill="currentColor" d="M12 5.38c1.62 0 3.06.56 4.21 1.64l3.15-3.15C17.45 2.09 14.97 1 12 1 7.7 1 3.99 3.47 2.18 7.06l3.66 2.84c.87-2.6 3.3-4.53 6.16-4.53z"/>
                    </svg>
                    <span>Google Account</span>
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
                    <button id="logoutBtn" class="text-xs font-semibold bg-gray-800 hover:bg-red-900 text-gray-300 hover:text-white px-3 py-1.5 rounded-lg transition border border-gray-700">
                        Logout
                    </button>
                </div>
            </div>
        </nav>

        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            
            <!-- Quick Stats / Wallet Header -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
                <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl border-l-4 border-accentGreen">
                    <p class="text-sm font-medium text-gray-400">Available Wallet Balance</p>
                    <p id="walletBalanceDisplay" class="text-3xl font-mono font-bold text-white mt-2">$10,000.00</p>
                    <button id="resetBalanceBtn" class="text-xs text-accentGreen hover:underline mt-2 inline-block">Reset Demo Cash ($10k)</button>
                </div>
                <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                    <p class="text-sm font-medium text-gray-400">Total Account Value</p>
                    <p id="totalAccountDisplay" class="text-3xl font-mono font-bold text-white mt-2">$10,000.00</p>
                    <span class="text-xs text-gray-500">Wallet + Live Open PNL</span>
                </div>
                <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                    <p class="text-sm font-medium text-gray-400">Bitcoin / USD</p>
                    <div class="flex items-center justify-between mt-2">
                        <p id="btcPrice" class="text-2xl font-mono font-bold text-accentGreen">$65,000.00</p>
                        <span id="btcBadge" class="text-xs font-bold text-accentGreen bg-emerald-500/10 px-2 py-0.5 rounded">▲ UP</span>
                    </div>
                    <span class="text-xs text-gray-500">Ethereum (ETH): <span id="ethPrice" class="font-mono text-white">$3,400.00</span> <span id="ethBadge" class="text-accentGreen">▲</span></span>
                </div>
            </div>

            <!-- Terminal Row -->
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                
                <!-- Trade Execution Panel -->
                <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl h-fit">
                    <h2 class="text-lg font-semibold text-white mb-4">Place Order</h2>
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
                            <p id="estimatedCost" class="text-xs text-gray-500 mt-1">Est. Cost: $6,500.00</p>
                        </div>
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Take Profit ($)</label>
                                <input type="number" id="tradeTP" placeholder="Target Price" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white text-sm font-mono focus:outline-none focus:border-accentGreen">
                            </div>
                            <div>
                                <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Stop Loss ($)</label>
                                <input type="number" id="tradeSL" placeholder="Floor Price" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white text-sm font-mono focus:outline-none focus:border-accentRed">
                            </div>
                        </div>
                        <div class="grid grid-cols-2 gap-4 pt-4">
                            <button id="buyBtn" class="bg-accentGreen hover:bg-emerald-600 text-darkBg font-bold py-3 rounded-xl transition uppercase tracking-wider text-sm shadow-md">Buy / Long</button>
                            <button id="sellBtn" class="bg-accentRed hover:bg-red-600 text-white font-bold py-3 rounded-xl transition uppercase tracking-wider text-sm shadow-md">Sell / Short</button>
                        </div>
                    </div>
                </div>

                <!-- Table Monitor with Live PNL Tracking -->
                <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl lg:col-span-2">
                    <h2 class="text-lg font-semibold text-white mb-4">Active Open Positions</h2>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead>
                                <tr class="border-b border-gray-800 text-xs font-semibold uppercase text-gray-400">
                                    <th class="pb-3">Asset</th>
                                    <th class="pb-3">Type</th>
                                    <th class="pb-3">Entry / Current</th>
                                    <th class="pb-3">Live P&L</th>
                                    <th class="pb-3">TP / SL</th>
                                    <th class="pb-3 text-right">Action</th>
                                </tr>
                            </thead>
                            <tbody id="positionsTable" class="divide-y divide-gray-800/50">
                                <tr id="emptyRow"><td colspan="6" class="py-8 text-center text-gray-500">No open positions. Place a trade to start!</td></tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- CORE PLATFORM ENGINE -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-app.js";
        import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signInWithPopup, GoogleAuthProvider, onAuthStateChanged, signOut } from "https://www.gstatic.com/firebasejs/10.7.1/firebase-auth.js";

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
        const auth = getAuth(app);
        const googleProvider = new GoogleAuthProvider();

        let isSignUpMode = false;
        const authScreen = document.getElementById('authScreen');
        const dashboardScreen = document.getElementById('dashboardScreen');
        const authTitle = document.getElementById('authTitle');
        const mainAuthBtn = document.getElementById('mainAuthBtn');
        const authToggleBtn = document.getElementById('authToggleBtn');
        const authToggleText = document.getElementById('authToggleText');
        const userEmailDisplay = document.getElementById('userEmailDisplay');

        // State Engine Data Memory
        let walletBalance = 10000.00; 
        let prices = { BTC: 65000.00, ETH: 3400.00 };
        let positions = [];

        // Auth Logic Controls
        authToggleBtn.addEventListener('click', () => {
            isSignUpMode = !isSignUpMode;
            authTitle.innerText = isSignUpMode ? "Create Your Account" : "Login to your account";
            mainAuthBtn.innerText = isSignUpMode ? "Register Account" : "Login";
            authToggleText.innerText = isSignUpMode ? "Already have an account?" : "Don't have an account?";
            authToggleBtn.innerText = isSignUpMode ? "Login" : "Sign Up";
        });

        mainAuthBtn.addEventListener('click', async () => {
            const email = document.getElementById('authEmail').value.trim();
            const password = document.getElementById('authPassword').value;
            if(!email || !password) return alert("Please fill details.");
            try {
                if (isSignUpMode) {
                    await createUserWithEmailAndPassword(auth, email, password);
                    alert("Registered successfully!");
                } else {
                    await signInWithEmailAndPassword(auth, email, password);
                }
            } catch (error) { alert(error.message); }
        });

        document.getElementById('googleAuthBtn').addEventListener('click', async () => {
            try { await signInWithPopup(auth, googleProvider); } catch (error) { alert(error.message); }
        });

        document.getElementById('logoutBtn').addEventListener('click', () => signOut(auth));

        onAuthStateChanged(auth, (user) => {
            if (user) {
                authScreen.classList.add('hidden');
                dashboardScreen.classList.remove('hidden');
                userEmailDisplay.innerText = user.email || "Investor";
                updateBalancesUI();
            } else {
                authScreen.classList.remove('hidden');
                dashboardScreen.classList.add('hidden');
            }
        });

        // Live Cost Estimate Updater
        const updateEstimate = () => {
            const asset = document.getElementById('tradeAsset').value;
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            document.getElementById('estimatedCost').innerText = `Est. Value: $${(prices[asset] * amount).toFixed(2)}`;
        };
        document.getElementById('tradeAsset').addEventListener('change', updateEstimate);
        document.getElementById('tradeAmount').addEventListener('input', updateEstimate);

        // Reset Balance Button
        document.getElementById('resetBalanceBtn').addEventListener('click', () => {
            walletBalance = 10000.00;
            updateBalancesUI();
        });

        // 2 Second Ticker Market Simulation Core Loop
        setInterval(() => {
            ['BTC', 'ETH'].forEach(asset => {
                const changePercent = (Math.random() * 0.6 - 0.3) / 100; // Volatility factor
                const oldPrice = prices[asset];
                prices[asset] = oldPrice * (1 + changePercent);

                const el = document.getElementById(`${asset.toLowerCase()}Price`);
                const badge = document.getElementById(`${asset.toLowerCase()}Badge`);
                if(!el) return;

                el.innerText = `$${prices[asset].toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
                if (prices[asset] > oldPrice) {
                    el.className = "text-2xl font-mono font-bold text-accentGreen";
                    if(badge) { badge.innerText = "▲ UP"; badge.className = "text-xs font-bold text-accentGreen bg-emerald-500/10 px-2 py-0.5 rounded"; }
                } else {
                    el.className = "text-2xl font-mono font-bold text-accentRed";
                    if(badge) { badge.innerText = "▼ DOWN"; badge.className = "text-xs font-bold text-accentRed bg-red-500/10 px-2 py-0.5 rounded"; }
                }
            });

            updateEstimate();
            checkOrderTriggers();
            renderPositions();
            updateBalancesUI();
        }, 2000);

        // Core Calculation Function for Live PNL
        function calculatePNL(pos) {
            const currentPrice = prices[pos.asset];
            let diff = currentPrice - pos.entryPrice;
            if (pos.type === 'SELL') diff = pos.entryPrice - currentPrice; // Short invert
            
            const pnlAmount = diff * pos.amount;
            const pnlPercent = (diff / pos.entryPrice) * 100;
            return { amount: pnlAmount, percent: pnlPercent };
        }

        function updateBalancesUI() {
            let totalOpenPNL = 0;
            positions.forEach(pos => { totalOpenPNL += calculatePNL(pos).amount; });

            document.getElementById('walletBalanceDisplay').innerText = `$${walletBalance.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
            const totalAccountVal = walletBalance + totalOpenPNL;
            document.getElementById('totalAccountDisplay').innerText = `$${totalAccountVal.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: 2})}`;
        }

        // Execute Order Logic (Validation + Capital Margin Reserve Check)
        function executeTrade(type) {
            const asset = document.getElementById('tradeAsset').value;
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            const tp = parseFloat(document.getElementById('tradeTP').value) || null;
            const sl = parseFloat(document.getElementById('tradeSL').value) || null;
            
            if (amount <= 0) return alert("Please enter a valid amount!");
            
            const orderValue = prices[asset] * amount;
            if (orderValue > walletBalance) {
                return alert(`Insufficient Funds! Required: $${orderValue.toFixed(2)}, Available: $${walletBalance.toFixed(2)}`);
            }

            // Deduct funds from available capital to hold dynamic margin
            walletBalance -= orderValue;

            positions.push({
                id: Date.now(),
                asset: asset,
                type: type,
                entryPrice: prices[asset],
                amount: amount,
                orderValue: orderValue, // Saved configuration cost
                tp: tp,
                sl: sl
            });
            
            document.getElementById('tradeTP').value = '';
            document.getElementById('tradeSL').value = '';
            renderPositions();
            updateBalancesUI();
        }

        // Close Position Settlement Action
        function settleAndClose(id) {
            const targetPos = positions.find(pos => pos.id === id);
            if (!targetPos) return;

            const finalPnl = calculatePNL(targetPos).amount;
            // Return base allocation capital + added performance matrix profit/loss
            walletBalance += (targetPos.orderValue + finalPnl);

            positions = positions.filter(pos => pos.id !== id);
            renderPositions();
            updateBalancesUI();
        }

        function checkOrderTriggers() {
            positions.forEach((pos) => {
                const currentPrice = prices[pos.asset];
                let shouldClose = false;

                if (pos.type === 'BUY') {
                    if (pos.tp && currentPrice >= pos.tp) shouldClose = true;
                    if (pos.sl && currentPrice <= pos.sl) shouldClose = true;
                } else if (pos.type === 'SELL') {
                    if (pos.tp && currentPrice <= pos.tp) shouldClose = true;
                    if (pos.sl && currentPrice >= pos.sl) shouldClose = true;
                }

                if (shouldClose) { settleAndClose(pos.id); }
            });
        }

        function renderPositions() {
            const tbody = document.getElementById('positionsTable');
            if(!tbody) return;
            if (positions.length === 0) {
                tbody.innerHTML = `<tr id="emptyRow"><td colspan="6" class="py-8 text-center text-gray-500">No open positions. Place a trade to start!</td></tr>`;
                return;
            }

            tbody.innerHTML = '';
            positions.forEach(pos => {
                const currentPrice = prices[pos.asset];
                const pnl = calculatePNL(pos);
                
                const typeColor = pos.type === 'BUY' ? 'text-accentGreen bg-emerald-500/10' : 'text-accentRed bg-red-500/10';
                const pnlColor = pnl.amount >= 0 ? 'text-accentGreen' : 'text-accentRed';
                const sign = pnl.amount >= 0 ? '+' : '';

                const row = document.createElement('tr');
                row.className = "hover:bg-gray-800/20 transition border-b border-gray-800/40 text-xs md:text-sm";
                row.innerHTML = `
                    <td class="py-3 font-semibold text-white">${pos.asset} (${pos.amount})</td>
                    <td class="py-3"><span class="px-2 py-0.5 text-xs font-bold rounded ${typeColor}">${pos.type}</span></td>
                    <td class="py-3 font-mono text-gray-400">$${pos.entryPrice.toFixed(2)}<br><span class="text-white">$${currentPrice.toFixed(2)}</span></td>
                    <td class="py-3 font-mono font-bold ${pnlColor}">${sign}$${pnl.amount.toFixed(2)}<br><span class="text-xs font-medium">${sign}${pnl.percent.toFixed(2)}%</span></td>
                    <td class="py-3 font-mono text-xs text-gray-400">TP: ${pos.tp ? '$' + pos.tp : 'None'}<br>SL: ${pos.sl ? '$' + pos.sl : 'None'}</td>
                    <td class="py-3 text-right">
                        <button data-id="${pos.id}" class="close-btn bg-gray-800 hover:bg-accentRed text-gray-300 hover:text-white px-3 py-1.5 rounded-lg text-xs font-medium transition border border-gray-700">Close</button>
                    </td>
                `;
                tbody.appendChild(row);
            });

            document.querySelectorAll('.close-btn').forEach(btn => {
                btn.addEventListener('click', (e) => {
                    const id = parseInt(e.target.getAttribute('data-id'));
                    settleAndClose(id);
                });
            });
        }

        document.getElementById('buyBtn').addEventListener('click', () => executeTrade('BUY'));
        document.getElementById('sellBtn').addEventListener('click', () => executeTrade('SELL'));
    </script>
</body>
</html>
