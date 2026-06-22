<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trading1 - Institutional Multi-Asset & Settlement Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
    <style>
        .custom-scrollbar::-webkit-scrollbar { width: 4px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #111827; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #1b2537; border-radius: 2px; }
    </style>
</head>
<body class="bg-[#0b0f19] text-gray-100 font-sans antialiased custom-scrollbar">

    <!-- Auth Gateway Screen -->
    <div id="authScreen" class="fixed inset-0 bg-[#0b0f19] z-50 flex items-center justify-center p-4">
        <div class="bg-[#111827] border border-gray-800 p-8 rounded-2xl shadow-2xl w-full max-w-md">
            <div class="flex items-center space-x-2 justify-center mb-6">
                <div class="w-8 h-8 bg-[#10b981] rounded-lg flex items-center justify-center font-bold text-[#0b0f19]">T1</div>
                <span class="text-2xl font-bold tracking-wider text-white">Trading<span class="text-[#10b981]">1</span></span>
            </div>
            <h2 id="authTitle" class="text-xl font-semibold text-center text-white mb-6">Access Trading Floor</h2>
            <div class="space-y-4">
                <div>
                    <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Email Address</label>
                    <input type="email" id="authEmail" placeholder="trader@trading1.com" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white focus:outline-none focus:border-[#10b981]">
                </div>
                <div>
                    <label class="block text-xs font-medium text-gray-400 uppercase mb-1">Security Password</label>
                    <input type="password" id="authPassword" placeholder="••••••••" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-white focus:outline-none focus:border-[#10b981]">
                </div>
                <button id="mainAuthBtn" class="w-full bg-[#10b981] hover:bg-emerald-600 text-[#0b0f19] font-bold py-2.5 rounded-lg transition tracking-wider text-sm mt-2">Sign In</button>
                <div class="relative flex py-2 items-center">
                    <div class="flex-grow border-t border-gray-800"></div>
                    <span class="flex-shrink mx-4 text-gray-500 text-xs uppercase">Or</span>
                    <div class="flex-grow border-t border-gray-800"></div>
                </div>
                <button id="googleAuthBtn" class="w-full bg-gray-800 hover:bg-gray-700 text-white font-medium py-2.5 rounded-lg transition text-sm flex items-center justify-center space-x-2 border border-gray-700">
                    <span>Sign in with Google Account</span>
                </button>
            </div>
            <p class="text-xs text-center text-gray-400 mt-6">
                <span id="authToggleText">First time at Trading1?</span> 
                <button id="authToggleBtn" class="text-[#10b981] hover:underline font-medium ml-1">Open Account</button>
            </p>
        </div>
    </div>

    <!-- Main Platform Framework Dashboard -->
    <div id="dashboardScreen" class="hidden min-h-screen flex flex-col">
        
        <!-- Header Navigation Bar -->
        <nav class="border-b border-gray-800 bg-[#0b0f19]/50 backdrop-blur-md sticky top-0 z-40">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
                <!-- Secret Tap Target Box Logo -->
                <div id="logoTapTarget" class="flex items-center space-x-2 cursor-pointer select-none group">
                    <div class="w-8 h-8 bg-[#10b981] rounded-lg flex items-center justify-center font-bold text-[#0b0f19] group-hover:scale-105 transition">T1</div>
                    <span class="text-xl font-bold tracking-wider text-white">Trading<span class="text-[#10b981]">1</span></span>
                </div>

                <!-- Center Multi Currency Global Scale Controls -->
                <div class="bg-gray-900 border border-gray-800 p-1 rounded-xl flex items-center space-x-1">
                    <button id="currencyUsdBtn" class="px-3 py-1 text-xs font-bold rounded-lg bg-[#10b981] text-[#0b0f19] transition">USD ($)</button>
                    <button id="currencyPkrBtn" class="px-3 py-1 text-xs font-bold rounded-lg text-gray-400 hover:text-white transition">PKR (Rs)</button>
                </div>

                <div class="flex items-center space-x-4">
                    <span id="userEmailDisplay" class="text-xs text-gray-400 bg-gray-900 border border-gray-800 px-3 py-1.5 rounded-lg font-mono"></span>
                    <button id="logoutBtn" class="text-xs font-semibold bg-gray-800 hover:bg-red-900 text-gray-300 hover:text-white px-3 py-1.5 rounded-lg transition border border-gray-700">Logout</button>
                </div>
            </div>
        </nav>

        <!-- Dynamic Content Engine Area -->
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow w-full space-y-6">
            
            <!-- Financial Core Dashboard Statistics Tickers -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                <div class="bg-[#111827] border border-gray-800 p-5 rounded-xl border-l-4 border-[#10b981]">
                    <p class="text-xs font-medium text-gray-400 uppercase tracking-wider">Available Capital Balance</p>
                    <p id="valWalletBalance" class="text-2xl font-mono font-bold text-white mt-1" data-usd="10000.00">$10,000.00</p>
                    <div class="flex space-x-4 mt-2">
                        <button onclick="toggleFundingModal('deposit')" class="text-xs text-[#10b981] font-bold hover:underline">↑ Instant Deposit</button>
                        <button onclick="toggleFundingModal('withdraw')" class="text-xs text-gray-400 font-bold hover:underline">↓ Request Cashout</button>
                    </div>
                </div>
                <div class="bg-[#111827] border border-gray-800 p-5 rounded-xl">
                    <p class="text-xs font-medium text-gray-400 uppercase tracking-wider">Net Account Equity</p>
                    <p id="valTotalEquity" class="text-2xl font-mono font-bold text-white mt-1">$10,000.00</p>
                    <span class="text-[10px] text-gray-500">Real-time margin value valuation</span>
                </div>
                <div class="bg-[#111827] border border-gray-800 p-5 rounded-xl flex justify-between items-center">
                    <div>
                        <p class="text-xs font-medium text-gray-400 uppercase tracking-wider">Selected Asset Focus</p>
                        <p id="activeAssetTitle" class="text-xl font-bold text-white mt-1">BTC/USD</p>
                    </div>
                    <div class="text-right">
                        <p id="activeAssetPrice" class="text-xl font-mono font-bold text-[#10b981]">$65,000.00</p>
                        <span id="activeAssetBadge" class="text-[10px] font-bold text-[#10b981] bg-emerald-500/10 px-1.5 py-0.5 rounded">▲ UP</span>
                    </div>
                </div>
            </div>

            <!-- Terminal Row Section Dashboard Core -->
            <div id="mainTradingTerminal" class="grid grid-cols-1 lg:grid-cols-4 gap-6">
                <!-- Left Column: Asset Discovery Hub -->
                <div class="bg-[#111827] border border-gray-800 p-4 rounded-xl h-[560px] flex flex-col">
                    <h3 class="text-xs font-bold text-gray-400 mb-3 uppercase tracking-wider">Asset Discovery Hub</h3>
                    <input type="text" id="assetSearchInput" placeholder="Filter crypto, stocks, forex..." class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs text-white focus:outline-none focus:border-[#10b981] mb-3">
                    <div id="assetDiscoveryList" class="flex-grow overflow-y-auto space-y-1 pr-1 custom-scrollbar"></div>
                </div>

                <!-- Center Columns: Charts & Positions Matrix -->
                <div class="lg:col-span-2 flex flex-col space-y-6">
                    <div class="bg-[#111827] border border-gray-800 p-4 rounded-xl">
                        <div class="flex items-center justify-between mb-2">
                            <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider">Interactive Live Trend Monitor</h3>
                            <span class="w-2 h-2 rounded-full bg-[#10b981] animate-pulse"></span>
                        </div>
                        <div id="chartContainer" class="w-full h-[240px]"></div>
                    </div>

                    <div class="bg-[#111827] border border-gray-800 p-4 rounded-xl flex-grow overflow-hidden flex flex-col">
                        <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-3">Active Operational Positions</h3>
                        <div class="overflow-x-auto flex-grow max-h-[180px] custom-scrollbar">
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
                                    <tr id="emptyRow"><td colspan="5" class="py-6 text-center text-gray-500">No open risk operations detected.</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>

                <!-- Right Column: Order Execution Board -->
                <div class="bg-[#111827] border border-gray-800 p-4 rounded-xl h-fit">
                    <h3 class="text-xs font-bold text-gray-400 mb-4 uppercase tracking-wider">Execution Panel</h3>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Target Asset Asset</label>
                            <input type="text" id="displayActiveAsset" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs font-bold text-[#10b981] focus:outline-none" readonly>
                        </div>
                        <div>
                            <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Volume Allocation (Units)</label>
                            <input type="number" id="tradeAmount" value="1" step="0.01" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-2 text-xs text-white font-mono focus:outline-none focus:border-[#10b981]">
                            <p id="estimatedCost" class="text-[10px] text-gray-500 mt-1">Est. Exposure: $0.00</p>
                        </div>
                        <div class="grid grid-cols-2 gap-2">
                            <div>
                                <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Take Profit</label>
                                <input type="number" id="tradeTP" placeholder="Target" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-1.5 text-xs text-white font-mono focus:outline-none focus:border-[#10b981]">
                            </div>
                            <div>
                                <label class="block text-[10px] font-medium text-gray-400 uppercase mb-1">Stop Loss</label>
                                <input type="number" id="tradeSL" placeholder="Floor" class="w-full bg-gray-900 border border-gray-800 rounded-lg px-3 py-1.5 text-xs text-white font-mono focus:outline-none focus:border-[#ef4444]">
                            </div>
                        </div>
                        <div class="grid grid-cols-2 gap-3 pt-2">
                            <button id="buyBtn" class="bg-[#10b981] hover:bg-emerald-600 text-[#0b0f19] font-bold py-2.5 rounded-lg transition uppercase tracking-wider text-xs">Buy / Long</button>
                            <button id="sellBtn" class="bg-[#ef4444] hover:bg-red-600 text-white font-bold py-2.5 rounded-lg transition uppercase tracking-wider text-xs">Sell / Short</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Funding Transactions History Logs Section -->
            <div class="bg-[#111827] border border-gray-800 p-5 rounded-xl">
                <h3 class="text-xs font-bold text-gray-400 uppercase tracking-wider mb-4">Capital Ledger Funding History</h3>
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs">
                        <thead>
                            <tr class="border-b border-gray-800 font-semibold uppercase text-gray-400">
                                <th class="pb-2">Timestamp</th>
                                <th class="pb-2">Operation Type</th>
                                <th class="pb-2">Method Channel</th>
                                <th class="pb-2">Amount Requested</th>
                                <th class="pb-2">Verification ID / TID</th>
                                <th class="pb-2">Status Flag</th>
                            </tr>
                        </thead>
                        <tbody id="fundingLogsTable" class="divide-y divide-gray-800/50">
                            <tr><td colspan="6" class="py-4 text-center text-gray-500">No funding operations logged yet.</td></tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Corporate Transparency Footer Details Information -->
            <footer class="border-t border-gray-800 pt-8 mt-12 grid grid-cols-1 md:grid-cols-3 gap-8 text-xs text-gray-400">
                <div>
                    <h4 class="font-bold text-white uppercase tracking-wider mb-3">Trading1 Institutional Compliance</h4>
                    <p class="leading-relaxed">Trading1 is a premier global brokerage terminal regulated under multiple multi-asset derivative frameworks. Licensed registry validation number #5426224-BrokerCorp. Operations structured across institutional decentralized processing centers.</p>
                    <p class="mt-3 text-gray-500">&copy; 2026 Trading1 Corp. All rights reserved.</p>
                </div>
                <div>
                    <h4 class="font-bold text-white uppercase tracking-wider mb-3">Frequently Asked Security Parameters (FAQ)</h4>
                    <div class="space-y-3">
                        <div>
                            <p class="text-white font-medium">What is the minimum requirement threshold?</p>
                            <p class="text-gray-500">Deposits initialize at $1 USD / Rs 278 PKR. Withdrawals require a minimum baseline parameter of $2 USD / Rs 556 PKR.</p>
                        </div>
                        <div>
                            <p class="text-white font-medium">What is the capital settlement schedule timeline?</p>
                            <p class="text-gray-500">All submissions pass through administrative secret key authorization ledgers within 1 to 24 hourly periods.</p>
                        </div>
                    </div>
                </div>
                <div>
                    <h4 class="font-bold text-white uppercase tracking-wider mb-3">Privacy Framework & Risk Protocols</h4>
                    <p class="leading-relaxed">All transaction receipts, upload validation buffers, and dynamic profile signatures undergo local sandboxed encryption logic pipelines. Margin derivative operations involve structural risk exposures.</p>
                    <p class="mt-2 text-white font-semibold">Location: <span class="text-gray-400 font-normal">Global Hub Alpha, Commercial Zone 1, Gilgit Financial District.</span></p>
                </div>
            </footer>
        </main>

        <!-- SECRET ADMIN OVERLAY INTERACTIVE TERMINAL HUB -->
        <main id="secretAdminTerminal" class="hidden max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-6 flex-grow w-full space-y-6">
            <div class="bg-gray-900 border border-yellow-600/40 p-6 rounded-xl">
                <div class="flex justify-between items-center border-b border-gray-800 pb-3 mb-4">
                    <div class="flex items-center space-x-2">
                        <span class="w-2 h-2 rounded-full bg-yellow-500 animate-ping"></span>
                        <h2 class="text-lg font-bold text-yellow-500 uppercase font-mono tracking-widest">Trading1 Secret Registry Override Panel</h2>
                    </div>
                    <button onclick="deactivateAdminTerminal()" class="bg-gray-800 hover:bg-gray-700 text-xs text-white px-3 py-1 rounded-lg">Return to Trading Floor</button>
                </div>
                
                <div class="overflow-x-auto">
                    <table class="w-full text-left text-xs font-mono">
                        <thead>
                            <tr class="border-b border-gray-800 uppercase text-gray-400">
                                <th class="pb-2">ID/Time</th>
                                <th class="pb-2">User/Legal Scope</th>
                                <th class="pb-2">Method & Details</th>
                                <th class="pb-2">Amount Requested</th>
                                <th class="pb-2">Proof Upload File</th>
                                <th class="pb-2 text-right">Operational Judgement</th>
                            </tr>
                        </thead>
                        <tbody id="adminManagementTable" class="divide-y divide-gray-800/50">
                            <!-- Populated dynamically via state engine storage data -->
                        </tbody>
                    </table>
                </div>
            </div>
        </main>
    </div>

    <!-- CAPITAL COMPLIANCE INTERACTIVE FUNDING DIALOG MODAL -->
    <div id="fundingModal" class="fixed inset-0 bg-black/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
        <div class="bg-[#111827] border border-gray-800 p-6 rounded-2xl w-full max-w-lg shadow-2xl max-h-[90vh] overflow-y-auto custom-scrollbar">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3 mb-4">
                <h3 id="fundingModalTitle" class="text-base font-bold text-white uppercase tracking-wider">Gateway System</h3>
                <button onclick="toggleFundingModal()" class="text-gray-400 hover:text-white font-bold font-mono">✕</button>
            </div>

            <!-- MODAL INTERACTIVE FORM CONTAINER -->
            <div id="depositFormFields" class="space-y-4 hidden">
                <div class="bg-gray-900 border border-gray-800 p-3 rounded-xl space-y-2 text-xs">
                    <p class="text-yellow-500 font-bold uppercase">Official Receiving Node Addresses:</p>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-2 font-mono text-gray-300">
                        <div class="bg-[#0b0f19] p-2 rounded">
                            <span class="text-[#10b981] font-bold">JazzCash / value="SADApay">SADApay (03705519562)</option>
                            <option value="EasyPaisa">EasyPaisa (03379827882)</option>
                            <option value="Binance">Binance Merchant Pay Network</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Amount ($ USD Capital)</label>
                        <input type="number" id="depAmount" value="10" min="1" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs font-mono focus:outline-none focus:border-[#10b981]">
                        <p id="depPkrCalc" class="text-[10px] text-gray-500 mt-1">Est: Rs 2,780 PKR</p>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Legal Name</label>
                        <input type="text" id="depLegalName" placeholder="John Doe" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs focus:outline-none focus:border-[#10b981]">
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Transaction ID / TID Proof</label>
                        <input type="text" id="depTid" placeholder="TID88471264" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs font-mono focus:outline-none focus:border-[#10b981]">
                    </div>
                </div>
                <div>
                    <label class="block text-[10px] uppercase text-gray-400 mb-1">Upload Receipt Proof (Image Document Screenshot)</label>
                    <input type="file" id="depFile" accept="image/*" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-1.5 text-xs text-gray-400 focus:outline-none">
                </div>
                <button onclick="processSubmitDeposit()" class="w-full bg-[#10b981] text-[#0b0f19] font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider">Transmit Deposit Wire</button>
            </div>

            <!-- WITHDRAWAL SUBMISSION FORM FIELDS -->
            <div id="withdrawFormFields" class="space-y-4 hidden">
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Target Account Method</label>
                        <select id="wdMethod" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs focus:outline-none">
                            <option value="JazzCash">JazzCash Routing Profile</option>
                            <option value="SADApay">SADApay Settlement Wallet</option>
                            <option value="EasyPaisa">EasyPaisa Mobile Banking</option>
                            <option value="Binance">Binance Pay (UID String Link)</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Cashout Volume ($ USD)</label>
                        <input type="number" id="wdAmount" value="20" min="2" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs font-mono focus:outline-none">
                        <p id="wdPkrCalc" class="text-[10px] text-gray-500 mt-1">Est Receive: Rs 5,560 PKR</p>
                    </div>
                </div>
                <div class="grid grid-cols-2 gap-3">
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Profile Username Reference</label>
                        <input type="text" id="wdUser" placeholder="trader123" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs focus:outline-none">
                    </div>
                    <div>
                        <label class="block text-[10px] uppercase text-gray-400 mb-1">Account Holder Legal Title Name</label>
                        <input type="text" id="wdLegal" placeholder="Asif Khan" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs focus:outline-none">
                    </div>
                </div>
                <div>
                    <label class="block text-[10px] uppercase text-gray-400 mb-1">Target Destination Account Number / Binance UID</label>
                    <input type="text" id="wdNumber" placeholder="03XXXXXXXXX or UID" class="w-full bg-gray-900 border border-gray-800 rounded-lg p-2 text-xs font-mono focus:outline-none">
                </div>
                <button onclick="processSubmitWithdrawal()" class="w-full bg-[#ef4444] text-white font-bold py-2.5 rounded-xl text-xs uppercase tracking-wider">Commit Liquidation Dispatch</button>
            </div>

            <!-- DIGITAL RECEIPT INVOICE RENDER VIEW SCREEN -->
            <div id="receiptRenderBlock" class="hidden space-y-4 pt-2">
                <div class="bg-white text-gray-900 p-5 rounded-xl font-mono text-xs border-2 border-dashed border-gray-300 space-y-2">
                    <div class="text-center border-b border-gray-300 pb-2">
                        <h4 class="font-bold text-sm uppercase tracking-widest">Trading1 Wire Voucher</h4>
                        <p class="text-[10px] text-gray-500">Secured Crypto-Fiat Pipeline Settlement Node</p>
                    </div>
                    <p><strong>Invoice Type:</strong> <span id="recType">DEPOSIT</span></p>
                    <p><strong>Legal Identity:</strong> <span id="recLegal">-</span></p>
                    <p><strong>Channel Node:</strong> <span id="recMethod">-</span></p>
                    <p><strong>Identifier Target:</strong> <span id="recTarget">-</span></p>
                    <p><strong>Settlement Vol:</strong> <span class="text-sm font-bold" id="recVal">-</span></p>
                    <p class="border-t border-gray-200 pt-2 text-[10px] text-center text-gray-400 font-sans">Verification tracking payload committed to memory index matrix. Awaiting admin clearance authorization code.</p>
                </div>
                <button onclick="toggleFundingModal()" class="w-full bg-gray-800 hover:bg-gray-700 text-xs py-2 rounded-lg text-white font-bold uppercase">Acknowledge Ledger Broadcast</button>
            </div>

        </div>
    </div>

    <!-- SYSTEM MODULE ARCHITECTURE -->
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

        // Core State Values Structures Memory Bank
        let activeCurrency = 'USD'; // Alternate Mode Configuration: PKR
        const FX_RATE = 278.00; // 1 USD = 278 PKR Conversion Coefficient

        let walletBalance = parseFloat(localStorage.getItem('t1_wallet') || '10000.00');
        let selectedAsset = 'BTC';
        let positions = [];
        let chartInstance = null;
        let logoTaps = 0;
        let logoTapTimer = null;

        // Initialize Funding Registry Ledger array from local memory strings cache matrix
        let fundingLedger = JSON.parse(localStorage.getItem('t1_funding_ledger') || '[]');

        const assetsDatabase = {};
        const categories = ['BTC', 'ETH', 'SOL', 'BNB', 'XRP', 'ADA', 'DOT', 'DOGE', 'AVAX', 'LINK', 'AAPL', 'TSLA', 'NVDA', 'AMZN', 'MSFT', 'EURUSD', 'GBPUSD', 'USDJPY', 'GOLD', 'CRUDE'];
        
        categories.forEach((name) => {
            let basePrice = 1.20;
            if(name.includes('USD')) basePrice = 1.15;
            if(['BTC','GOLD'].includes(name)) basePrice = name==='BTC' ? 65000 : 2300;
            if(['AAPL','TSLA','NVDA','MSFT'].includes(name)) basePrice = Math.random() * 300 + 100;
            if(['ETH','SOL'].includes(name)) basePrice = name==='ETH' ? 3400 : 140;

            assetsDatabase[name] = {
                symbol: name, price: basePrice,
                history: Array.from({length: 15}, () => basePrice * (1 + (Math.random() * 0.04 - 0.02)))
            };
        });

        // Event Handling Matrix Wireframe Connections
        authToggleBtn.addEventListener('click', () => {
            isSignUpMode = !isSignUpMode;
            authTitle.innerText = isSignUpMode ? "Open Account Profile" : "Access Trading Floor";
            mainAuthBtn.innerText = isSignUpMode ? "Register Account" : "Sign In";
        });

        mainAuthBtn.addEventListener('click', async () => {
            const email = document.getElementById('authEmail').value.trim();
            const password = document.getElementById('authPassword').value;
            try {
                if (isSignUpMode) { await createUserWithEmailAndPassword(auth, email, password); alert("Trading1 Profile Provisioned!"); }
                else { await signInWithEmailAndPassword(auth, email, password); }
            } catch (e) { alert(e.message); }
        });

        document.getElementById('googleAuthBtn').addEventListener('click', async () => { try { await signInWithPopup(auth, googleProvider); } catch(e) { alert(e.message); } });
        document.getElementById('logoutBtn').addEventListener('click', () => signOut(auth));

        onAuthStateChanged(auth, (user) => {
            if (user) {
                authScreen.classList.add('hidden');
                dashboardScreen.classList.remove('hidden');
                userEmailDisplay.innerText = user.email || "Institutional Account";
                initializeChart();
                buildAssetDiscoveryUI();
                switchAsset(selectedAsset);
                updateBalancesUI();
                renderFundingLogs();
            } else { authScreen.classList.remove('hidden'); dashboardScreen.classList.add('hidden'); }
        });

        // Global Currency Interface Format Interceptors
        function formatValue(amount, isAssetPrice = false) {
            if (activeCurrency === 'USD') {
                return `$${amount.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: isAssetPrice ? 4 : 2})}`;
            } else {
                const pkrAmount = amount * FX_RATE;
                return `Rs ${pkrAmount.toLocaleString(undefined, {minimumFractionDigits: 2, maximumFractionDigits: isAssetPrice ? 2 : 2})}`;
            }
        }

        document.getElementById('currencyUsdBtn').addEventListener('click', () => {
            activeCurrency = 'USD';
            toggleCurrencyUIStyle('currencyUsdBtn', 'currencyPkrBtn');
            forceGlobalUIRefresh();
        });

        document.getElementById('currencyPkrBtn').addEventListener('click', () => {
            activeCurrency = 'PKR';
            toggleCurrencyUIStyle('currencyPkrBtn', 'currencyUsdBtn');
            forceGlobalUIRefresh();
        });

        function toggleCurrencyUIStyle(activeId, inactiveId) {
            document.getElementById(activeId).className = "px-3 py-1 text-xs font-bold rounded-lg bg-[#10b981] text-[#0b0f19] transition";
            document.getElementById(inactiveId).className = "px-3 py-1 text-xs font-bold rounded-lg text-gray-400 hover:text-white transition";
        }

        function forceGlobalUIRefresh() {
            updateBalancesUI();
            switchAsset(selectedAsset);
            renderPositions();
            renderFundingLogs();
        }

        // Live Cost Estimate Updater
        const updateEstimate = () => {
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            const expUsd = assetsDatabase[selectedAsset].price * amount;
            document.getElementById('estimatedCost').innerText = `Est. Exposure: ${formatValue(expUsd)}`;
        };
        document.getElementById('tradeAmount').addEventListener('input', updateEstimate);

        // Core Balance Update Functions
        function updateBalancesUI() {
            let openPnl = 0;
            positions.forEach(pos => { openPnl += calculatePNL(pos).amount; });
            
            document.getElementById('valWalletBalance').innerText = formatValue(walletBalance);
            document.getElementById('valTotalEquity').innerText = formatValue(walletBalance + openPnl);
            localStorage.setItem('t1_wallet', walletBalance.toString());
        }

        // Build Asset Selection Panel Grid
        function buildAssetDiscoveryUI(filter = '') {
            const list = document.getElementById('assetDiscoveryList');
            if(!list) return; list.innerHTML = '';
            
            Object.keys(assetsDatabase).forEach(sym => {
                if(filter && !sym.toLowerCase().includes(filter.toLowerCase())) return;
                const item = assetsDatabase[sym];
                const div = document.createElement('div');
                div.className = `flex justify-between items-center p-2 rounded-lg text-xs cursor-pointer transition border border-transparent ${selectedAsset === sym ? 'bg-gray-800 border-[#10b981]/40' : 'hover:bg-gray-900'}`;
                div.innerHTML = `
                    <div><p class="font-bold text-white">${sym}/USD</p><p class="text-[10px] text-gray-500">Derivative Feed</p></div>
                    <div class="text-right"><p id="feed-p-${sym}" class="font-mono font-bold">${formatValue(item.price, true)}</p></div>
                `;
                div.addEventListener('click', () => switchAsset(sym));
                list.appendChild(div);
            });
        }

        function switchAsset(symbol) {
            selectedAsset = symbol;
            document.getElementById('activeAssetTitle').innerText = `${symbol} / USD`;
            document.getElementById('displayActiveAsset').value = `${symbol} / USD`;
            buildAssetDiscoveryUI(document.getElementById('assetSearchInput').value);
            updateEstimate();
            updateChartData();
        }

        document.getElementById('assetSearchInput').addEventListener('input', (e) => {
            const query = e.target.value.toUpperCase().trim();
            if(query && !assetsDatabase[query] && query.length <= 6) {
                assetsDatabase[query] = { symbol: query, price: Math.random() * 400 + 5, history: Array.from({length:15}, () => Math.random()*400+5) };
            }
            buildAssetDiscoveryUI(e.target.value);
        });

        // High Frequency Global Clock Ticker Pipeline Loop
        setInterval(() => {
            Object.keys(assetsDatabase).forEach(sym => {
                const asset = assetsDatabase[sym];
                const change = (Math.random() * 0.6 - 0.3) / 100;
                const oldPrice = asset.price;
                asset.price = oldPrice * (1 + change);
                asset.history.push(asset.price); if(asset.history.length > 20) asset.history.shift();

                const feedEl = document.getElementById(`feed-p-${sym}`);
                if(feedEl) {
                    feedEl.innerText = formatValue(asset.price, true);
                    feedEl.className = asset.price >= oldPrice ? 'font-mono text-[#10b981]' : 'font-mono text-[#ef4444]';
                }

                if(sym === selectedAsset) {
                    const priceEl = document.getElementById('activeAssetPrice');
                    const badge = document.getElementById('activeAssetBadge');
                    priceEl.innerText = formatValue(asset.price, true);
                    if(asset.price >= oldPrice) {
                        priceEl.className = "text-xl font-mono font-bold text-[#10b981]";
                        badge.innerText = "▲ UP"; badge.className = "text-[10px] font-bold text-[#10b981] bg-emerald-500/10 px-1.5 py-0.5 rounded";
                    } else {
                        priceEl.className = "text-xl font-mono font-bold text-[#ef4444]";
                        badge.innerText = "▼ DOWN"; badge.className = "text-[10px] font-bold text-[#ef4444] bg-red-500/10 px-1.5 py-0.5 rounded";
                    }
                }
            });

            updateEstimate(); checkOrderTriggers(); renderPositions(); updateBalancesUI();
            if(chartInstance) updateChartData();
        }, 2000);

        function calculatePNL(pos) {
            const currentPrice = assetsDatabase[pos.asset].price;
            let diff = currentPrice - pos.entryPrice;
            if (pos.type === 'SELL') diff = pos.entryPrice - currentPrice;
            return { amount: diff * pos.amount, percent: (diff / pos.entryPrice) * 100 };
        }

        function executeTrade(type) {
            const amount = parseFloat(document.getElementById('tradeAmount').value) || 0;
            const tp = parseFloat(document.getElementById('tradeTP').value) || null;
            const sl = parseFloat(document.getElementById('tradeSL').value) || null;
            if(amount <= 0) return alert("Invalid allocation size volume.");

            const cost = assetsDatabase[selectedAsset].price * amount;
            if(cost > walletBalance) return alert("Insufficient Capital Funds Reservoir.");

            walletBalance -= cost;
            positions.push({ id: Date.now(), asset: selectedAsset, type: type, entryPrice: assetsDatabase[selectedAsset].price, amount: amount, orderValue: cost, tp: tp, sl: sl });
            
            document.getElementById('tradeTP').value = ''; document.getElementById('tradeSL').value = '';
            renderPositions(); updateBalancesUI();
        }

        function settleAndClose(id) {
            const p = positions.find(x => x.id === id); if(!p) return;
            walletBalance += (p.orderValue + calculatePNL(p).amount);
            positions = positions.filter(x => x.id !== id);
            renderPositions(); updateBalancesUI();
        }

        function checkOrderTriggers() {
            positions.forEach(pos => {
                const cur = assetsDatabase[pos.asset].price; let close = false;
                if(pos.type === 'BUY') { if((pos.tp && cur >= pos.tp) || (pos.sl && cur <= pos.sl)) close = true; }
                else { if((pos.tp && cur <= pos.tp) || (pos.sl && cur >= pos.sl)) close = true; }
                if(close) settleAndClose(pos.id);
            });
        }

        function renderPositions() {
            const tbody = document.getElementById('positionsTable'); if(!tbody) return;
            if(positions.length === 0) { tbody.innerHTML = `<tr id="emptyRow"><td colspan="5" class="py-6 text-center text-gray-500">No open risk operations detected.</td></tr>`; return; }
            tbody.innerHTML = '';
            positions.forEach(pos => {
                const cur = assetsDatabase[pos.asset].price; const pnl = calculatePNL(pos);
                const row = document.createElement('tr');
                row.className = "hover:bg-gray-800/10 text-xs border-b border-gray-800/30";
                row.innerHTML = `
                    <td class="py-2 font-bold">${pos.asset}</td>
                    <td class="py-2"><span class="px-1 py-0.5 rounded font-bold text-[10px] ${pos.type==='BUY'?'text-[#10b981] bg-emerald-500/10':'text-[#ef4444] bg-red-500/10'}">${pos.type}</span></td>
                    <td class="py-2 font-mono text-gray-400">${formatValue(pos.entryPrice)} → <span class="text-white">${formatValue(cur)}</span></td>
                    <td class="py-2 font-mono font-bold ${pnl.amount>=0?'text-[#10b981]':'text-[#ef4444]'}">${pnl.amount>=0?'+':''}${formatValue(pnl.amount)}</td>
                    <td class="py-2 text-right"><button data-id="${pos.id}" class="close-p-btn bg-gray-900 border border-gray-800 hover:bg-[#ef4444] px-2 py-1 rounded text-gray-300 hover:text-white transition">Close</button></td>
                `;
                tbody.appendChild(row);
            });
            document.querySelectorAll('.close-p-btn').forEach(b => b.addEventListener('click', (e) => settleAndClose(parseInt(e.target.getAttribute('data-id')))));
        }

        // Render Public Client Ledger Funding History Logs UI Grid Table
        function renderFundingLogs() {
            const tbody = document.getElementById('fundingLogsTable');
            if(!tbody) return;
            if(fundingLedger.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="py-4 text-center text-gray-500">No funding operations logged yet.</td></tr>`;
                return;
            }
            tbody.innerHTML = '';
            fundingLedger.forEach(log => {
                let badgeClass = 'text-yellow-500 bg-yellow-500/10';
                if(log.status === 'Approved') badgeClass = 'text-[#10b981] bg-emerald-500/10';
                if(log.status === 'Rejected') badgeClass = 'text-[#ef4444] bg-red-500/10';

                const row = document.createElement('tr');
                row.className = "border-b border-gray-800/40 hover:bg-gray-900/40 text-xs";
                row.innerHTML = `
                    <td class="py-2.5 font-mono text-gray-500">${log.date}</td>
                    <td class="py-2.5 font-bold uppercase ${log.type==='deposit'?'text-[#10b981]':'text-blue-400'}">${log.type}</td>
                    <td class="py-2.5 font-medium">${log.method}</td>
                    <td class="py-2.5 font-mono font-bold text-white">${formatValue(log.amount)}</td>
                    <td class="py-2.5 font-mono text-gray-400">${log.tid || 'N/A'}</td>
                    <td class="py-2.5"><span class="px-2 py-0.5 rounded-full text-[10px] font-bold ${badgeClass}">${log.status}</span></td>
                `;
                tbody.appendChild(row);
            });
        }

        // --- SECRET COGNITIVE LOGO TAP SEQUENCING CONTROLLER ---
        document.getElementById('logoTapTarget').addEventListener('click', () => {
            logoTaps++;
            clearTimeout(logoTapTimer);
            logoTapTimer = setTimeout(() => { logoTaps = 0; }, 3000); // 3 Second vector horizon boundary

            if (logoTaps >= 5) {
                logoTaps = 0;
                const adminKey = prompt("⚠️ Trading1 Critical Core Security Clearance Intercept.\nEnter Secret Admin Passcode Pattern Key:");
                if(adminKey === "5426224") {
                    alert("Access Granted. Transitioning operational interface dashboard architecture grid...");
                    activateAdminTerminal();
                } else {
                    alert("Unauthorized Authentication Vector Target Signature. Alert logged.");
                }
            }
        });

        function activateAdminTerminal() {
            document.getElementById('mainTradingTerminal').classList.add('hidden');
            document.getElementById('secretAdminTerminal').classList.remove('hidden');
            renderAdminManagementDashboard();
        }

        window.deactivateAdminTerminal = function() {
            document.getElementById('secretAdminTerminal').classList.add('hidden');
            document.getElementById('mainTradingTerminal').classList.remove('hidden');
        };

        // Render Secret Registry Dashboard View
        function renderAdminManagementDashboard() {
            const tbody = document.getElementById('adminManagementTable');
            if(!tbody) return;
            if(fundingLedger.length === 0) {
                tbody.innerHTML = `<tr><td colspan="6" class="py-4 text-center text-gray-500">No operational ledger rows found to process.</td></tr>`;
                return;
            }
            tbody.innerHTML = '';
            fundingLedger.forEach((log) => {
                const proofRender = log.proof ? `<img src="${log.proof}" class="w-12 h-12 rounded border border-gray-700 object-cover cursor-zoom-in" onclick="window.open(this.src)">` : '<span class="text-gray-600">No File</span>';
                
                const actionControls = log.status === 'Pending' ? `
                    <div class="flex space-x-1 justify-end">
                        <button onclick="adminActionOverride('${log.id}', 'Approved')" class="bg-[#10b981] hover:bg-emerald-600 text-[#0b0f19] px-2 py-1 rounded text-[10px] font-bold">Approve</button>
                        <button onclick="adminActionOverride('${log.id}', 'Rejected')" class="bg-[#ef4444] hover:bg-red-600 text-white px-2 py-1 rounded text-[10px] font-bold">Reject</button>
                    </div>
                ` : `<span class="text-gray-500 text-[10px] font-bold uppercase">Settled (${log.status})</span>`;

                const row = document.createElement('tr');
                row.className = "border-b border-gray-800 text-xs hover:bg-gray-900/60";
                row.innerHTML = `
                    <td class="py-3 text-gray-500">${log.date}<br><span class="text-[9px] text-gray-600">ID:${log.id}</span></td>
                    <td class="py-3 font-bold text-white uppercase">${log.type}<br><span class="text-[10px] text-gray-400 font-normal capitalize">Name: ${log.legalName || 'N/A'}</span></td>
                    <td class="py-3 text-gray-300 font-medium">${log.method}<br><span class="text-[10px] text-gray-500 font-mono">Node: ${log.accountNumber || log.tid || 'N/A'}</span></td>
                    <td class="py-3 text-yellow-500 font-bold font-mono">${formatValue(log.amount)}</td>
                    <td class="py-3">${proofRender}</td>
                    <td class="py-3 text-right">${actionControls}</td>
                `;
                tbody.appendChild(row);
            });
        }

        // Global Window Scope Admin Override Intercept Logic Execution Matrix
        window.adminActionOverride = function(id, finalStatus) {
            const targetIndex = fundingLedger.findIndex(x => x.id === id);
            if(targetIndex === -1) return;

            const targetLog = fundingLedger[targetIndex];
            targetLog.status = finalStatus;

            // If action parameter equals deposit approval, credit capital reserves directly
            if(targetLog.type === 'deposit' && finalStatus === 'Approved') {
                walletBalance += targetLog.amount;
            }
            // If action parameter equals withdrawal rejection, re-credit user capital margin reserves
            if(targetLog.type === 'withdraw' && finalStatus === 'Rejected') {
                walletBalance += targetLog.amount;
            }

            localStorage.setItem('t1_funding_ledger', JSON.stringify(fundingLedger));
            localStorage.setItem('t1_wallet', walletBalance.toString());
            
            updateBalancesUI();
            renderFundingLogs();
            renderAdminManagementDashboard();
        };

        // --- APEXCHARTS ENGINE VECTOR FLOW ---
        function initializeChart() {
            const options = {
                chart: { type: 'line', height: 220, toolbar: { show: false }, animations: { enabled: false }, background: 'transparent' },
                series: [{ name: 'Price Feed Feed', data: [] }],
                colors: ['#10b981'], stroke: { width: 3, curve: 'smooth' }, theme: { mode: 'dark' },
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

        // Binding Actions Event Callbacks
        document.getElementById('buyBtn').addEventListener('click', () => executeTrade('BUY'));
        document.getElementById('sellBtn').addEventListener('click', () => executeTrade('SELL'));
    </script>

    <!-- INTERACTIVE FUNDING CONTROLS AND BASE64 CORE RECEPTACLE LOGIC FUNCTIONS -->
    <script>
        const EXCHANGE_CONSTANT_VAL = 278.00;
        let currentModalViewMode = '';
        let base64ImageStringPayload = '';

        // Realtime Local Currency Live Label Cost Listeners
        document.getElementById('depAmount').addEventListener('input', (e) => {
            const val = parseFloat(e.target.value) || 0;
            document.getElementById('depPkrCalc').innerText = `Est: Rs ${(val * EXCHANGE_CONSTANT_VAL).toLocaleString(undefined, {minimumFractionDigits:2})} PKR`;
        });
        document.getElementById('wdAmount').addEventListener('input', (e) => {
            const val = parseFloat(e.target.value) || 0;
            document.getElementById('wdPkrCalc').innerText = `Est Receive: Rs ${(val * EXCHANGE_CONSTANT_VAL).toLocaleString(undefined, {minimumFractionDigits:2})} PKR`;
        });

        // Image Base64 Stream Interceptor Pipeline Loader
        document.getElementById('depFile').addEventListener('change', function(e) {
            const file = e.target.files[0];
            if(!file) return;
            const reader = new FileReader();
            reader.onloadend = function() { base64ImageStringPayload = reader.result; };
            reader.readAsDataURL(file);
        });

        function toggleFundingModal(mode = '') {
            const modal = document.getElementById('fundingModal');
            const depFields = document.getElementById('depositFormFields');
            const wdFields = document.getElementById('withdrawFormFields');
            const receiptView = document.getElementById('receiptRenderBlock');

            if(!mode) { modal.classList.add('hidden'); return; }

            currentModalViewMode = mode;
            modal.classList.remove('hidden');
            receiptView.classList.add('hidden');

            if(mode === 'deposit') {
                document.getElementById('fundingModalTitle').innerText = 'Institutional Capital Deposit Node';
                depFields.classList.remove('hidden'); wdFields.classList.add('hidden');
            } else if (mode === 'withdraw') {
                document.getElementById('fundingModalTitle').innerText = 'Asset Dispersal Cashout Gateway';
                wdFields.classList.remove('hidden'); depFields.classList.add('hidden');
            }
        }

        function processSubmitDeposit() {
            const amount = parseFloat(document.getElementById('depAmount').value) || 0;
            const method = document.getElementById('depMethod').value;
            const legalName = document.getElementById('depLegalName').value.trim();
            const tid = document.getElementById('depTid').value.trim();

            if(amount < 1) return alert("Minimum required investment threshold equals $1 USD.");
            if(!legalName || !tid || !base64ImageStringPayload) return alert("Please fill all identity criteria data points and embed verification receipt file.");

            const itemPayload = {
                id: 'DEP-' + Date.now(),
                type: 'deposit',
                date: new Date().toLocaleTimeString() + ' ' + new Date().toLocaleDateString(),
                amount: amount, method: method, legalName: legalName, tid: tid, proof: base64ImageStringPayload, status: 'Pending'
            };

            saveFundingObjectToLocalStorage(itemPayload);
            triggerDigitalReceiptView(itemPayload);
        }

        function processSubmitWithdrawal() {
            const amount = parseFloat(document.getElementById('wdAmount').value) || 0;
            const method = document.getElementById('wdMethod').value;
            const legalName = document.getElementById('wdLegal').value.trim();
            const accNum = document.getElementById('wdNumber').value.trim();
            const username = document.getElementById('wdUser').value.trim();

            if(amount < 2) return alert("Minimum compliance withdrawal dispersal parameters require $2 USD threshold.");
            if(!legalName || !accNum || !username) return alert("Please map destination routing account parameters precisely.");

            // Validation step against current client cash capital reserves balances
            let walletBalance = parseFloat(localStorage.getItem('t1_wallet') || '10000.00');
            if(amount > walletBalance) return alert("Requested volume matrix breaches current available capital lines.");

            // Instant deduction to hold margin capital allocations securely
            walletBalance -= amount;
            localStorage.setItem('t1_wallet', walletBalance.toString());

            const itemPayload = {
                id: 'WTH-' + Date.now(),
                type: 'withdraw',
                date: new Date().toLocaleTimeString() + ' ' + new Date().toLocaleDateString(),
                amount: amount, method: method, legalName: legalName, accountNumber: accNum, username: username, status: 'Pending'
            };

            saveFundingObjectToLocalStorage(itemPayload);
            triggerDigitalReceiptView(itemPayload);

            // Dispatch global event execution pipeline notify trigger loop hook
            const event = new Event('storage'); window.dispatchEvent(event);
        }

        function saveFundingObjectToLocalStorage(obj) {
            let currentList = JSON.parse(localStorage.getItem('t1_funding_ledger') || '[]');
            currentList.unshift(obj);
            localStorage.setItem('t1_funding_ledger', JSON.stringify(currentList));
            base64ImageStringPayload = ''; document.getElementById('depFile').value = '';
        }

        function triggerDigitalReceiptView(obj) {
            document.getElementById('depositFormFields').classNames = 'hidden';
            document.getElementById('depositFormFields').classList.add('hidden');
            document.getElementById('withdrawFormFields').classList.add('hidden');
            
            const block = document.getElementById('receiptRenderBlock');
            block.classList.remove('hidden');

            document.getElementById('recType').innerText = obj.type.toUpperCase();
            document.getElementById('recLegal').innerText = obj.legalName;
            document.getElementById('recMethod').innerText = obj.method;
            document.getElementById('recTarget').innerText = obj.accountNumber || obj.tid;
            document.getElementById('recVal').innerText = `$${obj.amount.toFixed(2)} USD (Rs ${(obj.amount * EXCHANGE_CONSTANT_VAL).toLocaleString()} PKR)`;
        }
    </script>
</body>
</html>
