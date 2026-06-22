<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OlympTrade Fully Functional Real-Time Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .custom-scrollbar::-webkit-scrollbar { width: 4px; height: 4px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #11141a; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #222933; border-radius: 4px; }
        body { background-color: #11141a; color: #e2e8f0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        .neon-green-btn { background-color: #00e676; color: #000000; font-weight: 700; }
        .neon-green-btn:hover { background-color: #00c853; }
        .trading-down-btn { background-color: #f14343; }
        .trading-up-btn { background-color: #26a69a; }
        .app-bg-dark { background-color: #1c222c; }
        .app-bg-card { background-color: #161b22; }
    </style>
</head>
<body class="custom-scrollbar min-h-screen flex flex-col justify-between select-none pb-14">

    <!-- TOP HEADER NAVIGATION BAR -->
    <nav class="bg-[#161b22] border-b border-gray-800/60 px-4 h-14 flex items-center justify-between sticky top-0 z-40">
        <div class="flex items-center space-x-3">
            <div onclick="switchMainTabView('profile')" class="w-8 h-8 rounded-full bg-gray-700/60 flex items-center justify-center border border-gray-600/40 cursor-pointer">
                <i class="fa-solid fa-user text-sm text-gray-300"></i>
            </div>
            <div class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></div>
        </div>

        <div onclick="openAccountsModal()" class="flex flex-col items-center justify-center cursor-pointer group">
            <div class="flex items-center space-x-1">
                <span id="navActiveAccountBalance" class="font-mono font-bold text-sm tracking-wide text-white">PKR 0.00</span>
                <i class="fa-solid fa-chevron-down text-[10px] text-gray-400 group-hover:text-white transition"></i>
            </div>
            <span id="navActiveAccountLabel" class="text-[9px] text-gray-400 font-medium">PKR Account</span>
        </div>

        <button onclick="openPaymentsModal()" class="w-9 h-8 rounded-lg neon-green-btn flex items-center justify-center shadow-lg active:scale-95 transition">
            <i class="fa-solid fa-wallet text-sm"></i>
        </button>
    </nav>

    <!-- DYNAMIC CORE CONTENT CONTAINER SHEETS -->
    <div class="w-full max-w-md mx-auto flex-grow flex flex-col px-3 pt-2">
        
        <!-- SECTION 1: TRADING VIEW DECK (DEFAULT ACTIVE CHANNELS) -->
        <div id="coreTabSheetTrading" class="flex-grow flex flex-col justify-between space-y-2">
            <!-- Asset Selection Header Array -->
            <div class="flex items-center justify-between bg-[#161b22] p-2 rounded-xl border border-gray-800/40">
                <div onclick="openAssetsSelectionModal()" class="flex items-center space-x-2 bg-gray-800/40 px-3 py-1 rounded-lg cursor-pointer hover:bg-gray-800/80">
                    <div class="w-4 h-4 bg-amber-500 rounded flex items-center justify-center text-[10px] font-black text-black">A</div>
                    <span id="currentActiveAssetLabelText" class="text-xs font-bold text-white tracking-wide">Asia Composite Index</span>
                    <span id="currentActiveAssetYieldLabel" class="text-[11px] font-mono font-bold text-emerald-400">85%</span>
                    <i class="fa-solid fa-chevron-down text-[9px] text-gray-400"></i>
                </div>
                <div class="flex items-center space-x-2">
                    <button class="w-7 h-7 bg-gray-800/60 text-gray-400 rounded-lg text-xs flex items-center justify-center"><i class="fa-solid fa-compass"></i></button>
                    <button class="px-2 h-7 bg-gray-800/60 text-white font-mono font-bold rounded-lg text-[11px] flex items-center justify-center">5s</button>
                    <button onclick="toggleChartTypeStructureStyle()" class="w-7 h-7 bg-gray-800/60 text-emerald-400 rounded-lg text-xs flex items-center justify-center"><i class="fa-solid fa-chart-simple"></i></button>
                </div>
            </div>

            <!-- CORE GRAPH INTERACTIVE LIVE MONITOR -->
            <div class="flex-grow bg-[#11141a] border border-gray-900 rounded-2xl relative p-1 flex flex-col justify-center min-h-[290px]">
                <div id="mainChartContainer" class="w-full h-full"></div>
                <div class="absolute right-2 top-1/2 -translate-y-1/2 bg-slate-900 border border-gray-700/80 rounded-l pl-2 pr-1 py-0.5 text-[11px] font-mono font-bold text-white flex items-center space-x-1.5 z-20 shadow-xl">
                    <span id="chartCountdownTracker" class="text-gray-400 text-[10px] bg-gray-800 px-1 rounded">00:03</span>
                    <span id="chartFloatingAssetPrice" class="text-emerald-400">5984.13</span>
                </div>
            </div>

            <div class="flex items-center justify-between text-[11px] px-1 text-gray-400 font-medium">
                <span>Fixed Time mode</span>
                <span class="font-mono text-emerald-400 font-semibold" id="potentialYieldLabel">Profit: +PKR 238</span>
            </div>

            <!-- CONTROL DECKS RENDER BLOCK -->
            <div class="bg-[#161b22] border border-gray-800/60 rounded-2xl p-3 space-y-3 shadow-2xl">
                <div class="grid grid-cols-2 gap-2.5">
                    <div class="bg-[#1c222c] border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                        <button onclick="adjustNumericInput('timer', -1)" class="w-8 h-8 rounded-lg bg-gray-800/60 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                        <span id="displayExpiryWindowValue" class="text-xs font-mono font-bold text-white">1 min</span>
                        <button onclick="adjustNumericInput('timer', 1)" class="w-8 h-8 rounded-lg bg-gray-800/60 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                    </div>
                    <div class="bg-[#1c222c] border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                        <button onclick="adjustNumericInput('amount', -50)" class="w-8 h-8 rounded-lg bg-gray-800/60 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                        <span id="displayAllocationValue" class="text-xs font-mono font-bold text-white">PKR 280</span>
                        <button onclick="adjustNumericInput('amount', 50)" class="w-8 h-8 rounded-lg bg-gray-800/60 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                    </div>
                </div>

                <div class="flex items-center space-x-2">
                    <button onclick="dispatchBinaryContract('PUT')" class="flex-1 h-12 rounded-xl trading-down-btn text-white font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg">
                        <span class="text-xs uppercase font-extrabold">Down</span>
                        <i class="fa-solid fa-arrow-down text-sm"></i>
                    </button>
                    <button class="w-12 h-12 rounded-xl bg-gray-800/60 text-gray-300 flex items-center justify-center border border-gray-700/40"><i class="fa-solid fa-clock text-sm"></i></button>
                    <button onclick="dispatchBinaryContract('CALL')" class="flex-1 h-12 rounded-xl trading-up-btn text-white font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg">
                        <span class="text-xs uppercase font-extrabold">Up</span>
                        <i class="fa-solid fa-arrow-up text-sm"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- SECTION 2: DYNAMIC REWARDS / TASKS VIEW -->
        <div id="coreTabSheetRewards" class="hidden flex-grow space-y-4 pt-2">
            <div class="bg-gradient-to-r from-amber-600 to-orange-700 p-4 rounded-2xl relative overflow-hidden shadow-xl">
                <span class="absolute right-3 top-3 text-[9px] bg-black/30 px-2 py-0.5 rounded-full text-white tracking-widest uppercase font-bold">Active</span>
                <h3 class="text-lg font-black text-white tracking-wide">Football Sense Campaign</h3>
                <p class="text-xs text-orange-100/80 mt-1">Ends on July 20</p>
                <div class="mt-4 bg-black/20 p-2.5 rounded-xl border border-white/10 flex items-center justify-between text-xs">
                    <span>Use TOPUP with > 20$ for up to 100% bonus execution matrix values.</span>
                    <button onclick="openPaymentsModal('deposit')" class="px-3 py-1.5 bg-white text-orange-900 rounded-lg font-bold shadow-sm">Apply</button>
                </div>
            </div>
            <div class="bg-[#161b22] border border-gray-800 rounded-xl p-4 space-y-3">
                <h4 class="text-xs font-bold text-gray-400 uppercase tracking-wider">Platform Leaderboards</h4>
                <div class="grid grid-cols-3 gap-2 text-center text-xs">
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Best Trade</p><p class="font-mono font-bold text-emerald-400 mt-1">$4,920</p></div>
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Profit Sum</p><p class="font-mono font-bold text-emerald-400 mt-1">$12,851</p></div>
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Total Vol</p><p class="font-mono font-bold text-white mt-1">21.8K</p></div>
                </div>
            </div>
        </div>

        <!-- SECTION 3: OPEN ORDERS / ACTIVE TRADES PANEL DECK -->
        <div id="coreTabSheetTrades" class="hidden flex-grow space-y-3 pt-2">
            <div class="flex bg-[#161b22] rounded-xl p-1 text-xs border border-gray-800/40">
                <button class="flex-1 py-1.5 font-bold text-white bg-gray-800 rounded-lg text-center">Fixed Time</button>
                <button class="flex-1 py-1.5 font-bold text-gray-500 text-center opacity-50 cursor-not-allowed">Forex</button>
                <button class="flex-1 py-1.5 font-bold text-gray-500 text-center opacity-50 cursor-not-allowed">Stocks</button>
            </div>
            <div id="emptyTradesFallbackArea" class="bg-[#161b22] border border-gray-800/60 rounded-2xl p-6 text-center space-y-4">
                <div class="w-16 h-16 bg-gray-800/40 rounded-full flex items-center justify-center mx-auto text-gray-600 text-xl"><i class="fa-solid fa-box-open"></i></div>
                <div>
                    <h4 class="text-sm font-bold text-white">No Active Positions Logged</h4>
                    <p class="text-xs text-gray-500 mt-1">Deploy automated structural buy/sell derivative triggers to track orders.</p>
                </div>
                <button onclick="switchMainTabView('trading')" class="px-4 py-2 bg-gray-800 hover:bg-gray-700 text-xs font-bold rounded-xl text-white transition">Explore Assets</button>
            </div>
            <div id="activeTradesRunningListStack" class="space-y-2 hidden"></div>
        </div>

        <!-- SECTION 4: MARKET / STORE TERMINALS PACK -->
        <div id="coreTabSheetMarket" class="hidden flex-grow space-y-3 pt-2">
            <div class="bg-[#161b22] border border-gray-800 rounded-xl p-4 flex items-center justify-between text-xs">
                <div><h4 class="font-bold text-white">Forex Extended Packs</h4><p class="text-gray-500 mt-0.5">Professional analysis predictive indicator kits.</p></div>
                <i class="fa-solid fa-chevron-right text-gray-600"></i>
            </div>
            <div class="bg-gradient-to-br from-[#1c222c] to-[#161b22] border border-gray-800 rounded-xl p-4 text-center space-y-3">
                <div class="w-10 h-10 bg-emerald-500/10 text-emerald-400 rounded-xl flex items-center justify-center mx-auto text-base"><i class="fa-solid fa-shield-halved"></i></div>
                <h4 class="text-xs font-bold text-white">Advanced Trading Conditions</h4>
                <p class="text-[11px] text-gray-500">Unlock higher return percentage layers up to 92% profit payout matrix indices.</p>
            </div>
        </div>

        <!-- SECTION 5: PROFILE INFRASTRUCTURE DATA INDEX -->
        <div id="coreTabSheetProfile" class="hidden flex-grow space-y-3 pt-2">
            <div class="bg-[#161b22] border border-gray-800 rounded-2xl p-4 flex items-center space-x-4">
                <div class="w-12 h-12 rounded-full bg-emerald-500/20 border border-emerald-500/40 flex items-center justify-center text-xl text-emerald-400 font-bold">M</div>
                <div>
                    <h3 class="text-sm font-bold text-white">Muhammad Nazim</h3>
                    <p class="text-xs font-mono text-gray-500 mt-0.5 flex items-center space-x-1"><span>ID 121542844</span> <i class="fa-solid fa-copy text-[10px] text-gray-600 cursor-pointer hover:text-white"></i></p>
                </div>
            </div>
            <div class="bg-gradient-to-br from-indigo-950 via-[#161b22] to-slate-900 border border-indigo-500/20 rounded-2xl p-4 space-y-2">
                <h4 class="text-xs font-bold text-indigo-400 uppercase tracking-wide">Account Verification Level</h4>
                <div class="w-full bg-gray-900 h-1.5 rounded-full overflow-hidden mt-2"><div class="bg-indigo-500 h-full w-1/3"></div></div>
                <p class="text-[11px] text-gray-400 pt-1">Deposit USD 100 to get Smart status permissions tier matrices.</p>
            </div>
        </div>
    </div>

    <!-- BOTTOM APP NAVIGATION DECK CORE RIBBON BAR -->
    <div class="fixed bottom-0 left-0 right-0 h-14 bg-[#161b22] border-t border-gray-800/80 flex items-center justify-around z-30 max-w-md mx-auto px-2 shadow-2xl">
        <button id="navTabBtnTrading" onclick="switchMainTabView('trading')" class="flex flex-col items-center justify-center text-[#00e676] transition"><i class="fa-solid fa-chart-line text-base"></i></button>
        <button id="navTabBtnTrades" onclick="switchMainTabView('trades')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition relative"><i class="fa-solid fa-arrow-right-arrows-left text-base"></i><span id="activeTradesBadgeCount" class="absolute -top-1 -right-1.5 w-3.5 h-3.5 bg-rose-500 text-white text-[8px] font-black rounded-full flex items-center justify-center hidden">0</span></button>
        <button id="navTabBtnRewards" onclick="switchMainTabView('rewards')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition relative"><i class="fa-solid fa-trophy text-base"></i><span class="absolute -top-1 -right-1.5 w-3.5 h-3.5 bg-emerald-500 text-black text-[8px] font-black rounded-full flex items-center justify-center border border-black">1</span></button>
        <button id="navTabBtnMarket" onclick="switchMainTabView('market')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition"><i class="fa-solid fa-bag-shopping text-base"></i></button>
        <button id="navTabBtnProfile" onclick="switchMainTabView('profile')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition"><i class="fa-solid fa-user-gear text-base"></i></button>
    </div>

    <!-- SYSTEM SUB MODALS POPUP OVERLAYS ENGINE CANVAS LAYER -->
    <!-- OVERLAY 1: ACCOUNTS MULTI-TIER SWITCHING CONSOLE LAYOUT (VIDEO FRAME ACTION 00:01) -->
    <div id="accountsModalLayout" class="fixed inset-0 bg-black/70 z-50 hidden flex items-end justify-center transition-all backdrop-blur-sm">
        <div class="bg-[#161b22] w-full max-w-md rounded-t-3xl border-t border-gray-800 p-5 space-y-5 shadow-2xl relative">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white tracking-wide">Accounts</h2>
                <button onclick="closeAccountsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>
            <div class="space-y-3">
                <div onclick="selectPlatformAccountEnvironment('DEMO')" class="p-3.5 rounded-xl bg-gray-800/30 border border-gray-700/30 flex items-center justify-between cursor-pointer hover:bg-gray-800/60 transition relative">
                    <div class="flex items-center space-x-3">
                        <div class="w-7 h-7 bg-amber-500/20 rounded-lg text-amber-500 font-bold text-xs flex items-center justify-center font-mono">Ð</div>
                        <div><p class="text-xs font-bold text-gray-400">Demo account</p><p id="modalDemoBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">Ð58,766.67</p></div>
                    </div>
                    <i id="checkIconDemo" class="fa-solid fa-circle-check text-emerald-400 text-sm hidden"></i>
                </div>

                <div onclick="selectPlatformAccountEnvironment('PKR')" class="p-3.5 rounded-xl bg-gray-800/40 border border-gray-700/30 flex flex-col space-y-2 cursor-pointer transition relative group">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center space-x-3">
                            <div class="w-7 h-5 bg-emerald-800 rounded flex items-center justify-center text-[9px] text-white font-bold border border-emerald-600">PK</div>
                            <div><p class="text-xs font-bold text-gray-300">PKR Account</p><p id="modalPkrBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">PKR 0.00</p></div>
                        </div>
                        <div class="flex items-center space-x-3">
                            <div onclick="event.stopPropagation(); toggleAccountSettingsContextMenu();" class="p-2 text-gray-400 hover:text-white cursor-pointer"><i class="fa-solid fa-ellipsis-vertical text-xs"></i></div>
                            <i id="checkIconPkr" class="fa-solid fa-circle-check text-emerald-400 text-sm hidden"></i>
                        </div>
                    </div>
                    
                    <!-- CONTEXT FLYOUT MENU SUB ELEMENTS ACTIONS (VIDEO FRAME ACTION 00:49) -->
                    <div id="accountSettingsContextMenuPanel" class="hidden bg-[#1c222c] border border-gray-800 rounded-xl p-2 grid grid-cols-2 gap-1.5 text-[11px] font-medium text-gray-300">
                        <button onclick="event.stopPropagation(); openPaymentsModal('deposit')" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg text-emerald-400"><i class="fa-solid fa-circle-arrow-down w-4"></i><span>Deposit</span></button>
                        <button onclick="event.stopPropagation(); openPaymentsModal('withdraw')" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg text-rose-400"><i class="fa-solid fa-circle-arrow-up w-4"></i><span>Withdraw</span></button>
                        <button onclick="event.stopPropagation(); alert('Context Action Routing Verified.');" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg"><i class="fa-solid fa-pen-to-square w-4"></i><span>Rename</span></button>
                        <button onclick="event.stopPropagation(); alert('Pipeline Archived Successfully.');" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg text-gray-500"><i class="fa-solid fa-box-                        archive w-4"></i><span>Archive</span></button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- OVERLAY 2: ASSETS SELECTION MODAL LAYER -->
    <div id="assetsSelectionModalLayout" class="fixed inset-0 bg-black/70 z-50 hidden flex items-end justify-center backdrop-blur-sm">
        <div class="bg-[#161b22] w-full max-w-md h-[80vh] rounded-t-3xl border-t border-gray-800 p-5 flex flex-col space-y-4 shadow-2xl">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white tracking-wide">Assets</h2>
                <button onclick="closeAssetsSelectionModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>
            
            <div class="bg-gray-900/50 rounded-xl px-3 h-10 flex items-center space-x-2 border border-gray-800">
                <i class="fa-solid fa-magnifying-glass text-gray-500 text-xs"></i>
                <input type="text" placeholder="Search asset..." class="bg-transparent border-none outline-none text-xs text-white w-full placeholder-gray-600">
            </div>

            <div class="flex-grow overflow-y-auto custom-scrollbar space-y-2 pr-1" id="assetsModalListStack">
                <!-- Assets injection array loop handled dynamically via JS -->
            </div>
        </div>
    </div>

    <!-- OVERLAY 3: PAYMENTS MATRIX MODAL DECK -->
    <div id="paymentsModalLayout" class="fixed inset-0 bg-black/70 z-50 hidden flex items-end justify-center backdrop-blur-sm">
        <div class="bg-[#161b22] w-full max-w-md rounded-t-3xl border-t border-gray-800 p-5 space-y-4 shadow-2xl">
            <div class="flex justify-between items-center">
                <h2 id="paymentsModalHeaderTitle" class="text-lg font-bold text-white tracking-wide">Payments Window</h2>
                <button onclick="closePaymentsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>

            <div class="flex bg-gray-900 rounded-xl p-1 text-xs border border-gray-800">
                <button id="payTabBtnDeposit" onclick="switchPaymentsModalTab('deposit')" class="flex-1 py-2 font-bold rounded-lg text-center transition">Deposit</button>
                <button id="payTabBtnWithdraw" onclick="switchPaymentsModalTab('withdraw')" class="flex-1 py-2 font-bold rounded-lg text-center transition">Withdraw</button>
            </div>

            <div id="paymentTabContentArea" class="space-y-4 pt-1">
                <!-- Dynamic injection point for inner fields -->
            </div>
        </div>
    </div>

    <!-- CORE LOGIC APPLICATION HANDLER SCRIPT MODULE -->
    <script>
        // CONFIGURATIONS MATRIX INDEXES
        const ASSETS_COLLECTION_DATA = [
            { id: 'asia_comp', label: 'Asia Composite Index', yield: 85, price: 5984.13, type: 'A' },
            { id: 'commodity_comp', label: 'Commodity Composite Index', yield: 82, price: 2144.60, type: 'C' },
            { id: 'europe_comp', label: 'Europe Composite Index', yield: 78, price: 3412.85, type: 'E' },
            { id: 'crypto_idx', label: 'Crypto Index', yield: 90, price: 84150.20, type: '₿' }
        ];

        let stateGlobalApplication = {
            activeEnvironment: 'DEMO', // 'DEMO' | 'PKR'
            balances: { DEMO: 58766.67, PKR: 0.00 },
            currentAssetIndex: 0,
            chartObjectRef: null,
            chartDataSeries: [],
            activeTradingPositions: [],
            currentChartTypeStyle: 'AREA', // 'AREA' | 'CANDLE'
            inputs: { timer: 1, amount: 280 }
        };

        // LIFECYCLE INITIALIZER ONLOAD RUN
        window.addEventListener('DOMContentLoaded', () => {
            initializeApplicationEngineLayers();
        });

        function initializeApplicationEngineLayers() {
            renderDynamicInterfaceElements();
            constructApexChartCanvas();
            renderAssetsModalStackDom();
            startGlobalTickIntervalEngines();
            switchMainTabView('trading');
            selectPlatformAccountEnvironment('DEMO');
        }

        function renderDynamicInterfaceElements() {
            document.getElementById('displayExpiryWindowValue').innerText = stateGlobalApplication.inputs.timer + " min";
            document.getElementById('displayAllocationValue').innerText = "PKR " + stateGlobalApplication.inputs.amount;
            
            const currentAsset = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex];
            document.getElementById('currentActiveAssetLabelText').innerText = currentAsset.label;
            document.getElementById('currentActiveAssetYieldLabel').innerText = currentAsset.yield + "%";
            
            const localProfitCalculated = Math.floor(stateGlobalApplication.inputs.amount * (currentAsset.yield / 100));
            document.getElementById('potentialYieldLabel').innerText = `Profit: +PKR ${localProfitCalculated}`;

            document.getElementById('navActiveAccountBalance').innerText = (stateGlobalApplication.activeEnvironment === 'DEMO' ? 'Ð ' : 'PKR ') + stateGlobalApplication.balances[stateGlobalApplication.activeEnvironment].toFixed(2);
            document.getElementById('navActiveAccountLabel').innerText = stateGlobalApplication.activeEnvironment === 'DEMO' ? 'Demo Account' : 'PKR Account';
            
            document.getElementById('modalDemoBalanceDisplay').innerText = "Ð " + stateGlobalApplication.balances.DEMO.toFixed(2);
            document.getElementById('modalPkrBalanceDisplay').innerText = "PKR " + stateGlobalApplication.balances.PKR.toFixed(2);
        }

        function constructApexChartCanvas() {
            const chartNode = document.getElementById("mainChartContainer");
            if(!chartNode) return;

            let seedPrice = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex].price;
            for(let i = 0; i < 40; i++) {
                seedPrice += (Math.random() - 0.5) * 4;
                stateGlobalApplication.chartDataSeries.push({ x: new Date(Date.now() - (40 - i) * 1000), y: parseFloat(seedPrice.toFixed(2)) });
            }

            const chartLayoutOptions = {
                chart: {
                    type: 'area',
                    height: '100%',
                    sparklines: { enabled: true },
                    animations: { enabled: true, easing: 'linear', dynamicAnimation: { speed: 1000 } },
                    toolbar: { show: false }
                },
                colors: ['#00e676'],
                stroke: { curve: 'smooth', width: 2 },
                fill: {
                    type: 'gradient',
                    gradient: { shadeIntensity: 1, opacityFrom: 0.4, opacityTo: 0.02, stops: [0, 90, 100] }
                },
                series: [{ name: 'Price', data: stateGlobalApplication.chartDataSeries.slice() }],
                xaxis: { type: 'datetime' },
                yaxis: { opposite: true, labels: { show: false } },
                tooltip: { enabled: false }
            };

            stateGlobalApplication.chartObjectRef = new ApexCharts(chartNode, chartLayoutOptions);
            stateGlobalApplication.chartObjectRef.render();
        }

        function renderAssetsModalStackDom() {
            const targetedContainer = document.getElementById('assetsModalListStack');
            if(!targetedContainer) return;
            targetedContainer.innerHTML = '';

            ASSETS_COLLECTION_DATA.forEach((assetItem, loopIndex) => {
                const domNode = document.createElement('div');
                domNode.className = "flex items-center justify-between p-3 bg-gray-800/20 hover:bg-gray-800/60 rounded-xl cursor-pointer border border-transparent hover:border-gray-700/50 transition";
                domNode.onclick = () => { selectActiveTradingAssetIndexPointer(loopIndex); };
                
                domNode.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <div class="w-6 h-6 bg-gray-800 rounded flex items-center justify-center text-[10px] font-black text-amber-500">${assetItem.type}</div>
                        <div>
                            <p class="text-xs font-bold text-white tracking-wide">${assetItem.label}</p>
                            <p class="text-[10px] font-mono text-gray-500 mt-0.5">${assetItem.price.toFixed(2)}</p>
                        </div>
                    </div>
                    <span class="text-xs font-mono font-bold text-emerald-400">${assetItem.yield}%</span>
                `;
                targetedContainer.appendChild(domNode);
            });
        }

        function startGlobalTickIntervalEngines() {
            setInterval(() => {
                const currentAsset = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex];
                const shiftValue = (Math.random() - 0.5) * 3;
                let currentLatestPrice = stateGlobalApplication.chartDataSeries[stateGlobalApplication.chartDataSeries.length - 1].y + shiftValue;
                currentLatestPrice = parseFloat(currentLatestPrice.toFixed(2));

                document.getElementById('chartFloatingAssetPrice').innerText = currentLatestPrice.toFixed(2);
                
                const elementFloatingPrice = document.getElementById('chartFloatingAssetPrice');
                if (shiftValue >= 0) {
                    elementFloatingPrice.className = 'text-emerald-400';
                } else {
                    elementFloatingPrice.className = 'text-rose-400';
                }

                const updatedTimestampNode = { x: new Date(), y: currentLatestPrice };
                stateGlobalApplication.chartDataSeries.push(updatedTimestampNode);
                if(stateGlobalApplication.chartDataSeries.length > 50) stateGlobalApplication.chartDataSeries.shift();

                if(stateGlobalApplication.chartObjectRef) {
                    stateGlobalApplication.chartObjectRef.updateSeries([{ data: stateGlobalApplication.chartDataSeries }]);
                }

                processActiveOrderTickMatrices(currentLatestPrice);
            }, 1000);

            setInterval(() => {
                const totalSecondsLeft = Math.floor(Math.random() * 5) + 1;
                document.getElementById('chartCountdownTracker').innerText = `00:0${totalSecondsLeft}`;
            }, 3000);
        }

        function switchMainTabView(targetedTabTokenString) {
            const arrayTabsMapping = ['trading', 'rewards', 'trades', 'market', 'profile'];
            arrayTabsMapping.forEach(tabLoopToken => {
                const sheetDomRef = document.getElementById(`coreTabSheet${tabLoopToken.charAt(0).toUpperCase() + tabLoopToken.slice(1)}`);
                const ribbonBtnDomRef = document.getElementById(`navTabBtn${tabLoopToken.charAt(0).toUpperCase() + tabLoopToken.slice(1)}`);
                
                if(sheetDomRef) sheetDomRef.classList.add('hidden');
                if(ribbonBtnDomRef) ribbonBtnDomRef.className = "flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition";
            });

            const activeSheetNode = document.getElementById(`coreTabSheet${targetedTabTokenString.charAt(0).toUpperCase() + targetedTabTokenString.slice(1)}`);
            if(activeSheetNode) activeSheetNode.classList.remove('hidden');

            const activeRibbonBtnNode = document.getElementById(`navTabBtn${targetedTabTokenString.charAt(0).toUpperCase() + targetedTabTokenString.slice(1)}`);
            if(activeRibbonBtnNode) {
                activeRibbonBtnNode.className = "flex flex-col items-center justify-center text-[#00e676] transition";
            }
        }

        function openAccountsModal() { document.getElementById('accountsModalLayout').classList.remove('hidden'); }
        function closeAccountsModal() { 
            document.getElementById('accountsModalLayout').classList.add('hidden'); 
            document.getElementById('accountSettingsContextMenuPanel').classList.add('hidden');
        }
        function toggleAccountSettingsContextMenu() { document.getElementById('accountSettingsContextMenuPanel').classList.toggle('hidden'); }

        function selectPlatformAccountEnvironment(targetEnvironmentToken) {
            stateGlobalApplication.activeEnvironment = targetEnvironmentToken;
            if(targetEnvironmentToken === 'DEMO') {
                document.getElementById('checkIconDemo').classList.remove('hidden');
                document.getElementById('checkIconPkr').classList.add('hidden');
            } else {
                document.getElementById('checkIconDemo').classList.add('hidden');
                document.getElementById('checkIconPkr').classList.remove('hidden');
            }
            renderDynamicInterfaceElements();
            closeAccountsModal();
        }

        function openAssetsSelectionModal() { document.getElementById('assetsSelectionModalLayout').classList.remove('hidden'); }
        function closeAssetsSelectionModal() { document.getElementById('assetsSelectionModalLayout').classList.add('hidden'); }

        function selectActiveTradingAssetIndexPointer(indexPointer) {
            stateGlobalApplication.currentAssetIndex = indexPointer;
            stateGlobalApplication.chartDataSeries = [];
            
            let seedPrice = ASSETS_COLLECTION_DATA[indexPointer].price;
            for(let i = 0; i < 40; i++) {
                seedPrice += (Math.random() - 0.5) * 4;
                stateGlobalApplication.chartDataSeries.push({ x: new Date(Date.now() - (40 - i) * 1000), y: parseFloat(seedPrice.toFixed(2)) });
            }
            
            renderDynamicInterfaceElements();
            closeAssetsSelectionModal();
        }

        function adjustNumericInput(inputFieldToken, modifierValue) {
            if(inputFieldToken === 'timer') {
                stateGlobalApplication.inputs.timer = Math.max(1, stateGlobalApplication.inputs.timer + modifierValue);
            } else if(inputFieldToken === 'amount') {
                stateGlobalApplication.inputs.amount = Math.max(50, stateGlobalApplication.inputs.amount + modifierValue);
            }
            renderDynamicInterfaceElements();
        }

        function toggleChartTypeStructureStyle() {
            stateGlobalApplication.currentChartTypeStyle = stateGlobalApplication.currentChartTypeStyle === 'AREA' ? 'CANDLE' : 'AREA';
            alert(`Chart View Mode Switched to: ${stateGlobalApplication.currentChartTypeStyle}`);
        }

        function dispatchBinaryContract(directionTypeString) {
            const allocationValue = stateGlobalApplication.inputs.amount;
            const liveBalance = stateGlobalApplication.balances[stateGlobalApplication.activeEnvironment];

            if(liveBalance < allocationValue) {
                alert("Insufficient Account Balances to dispatch contract pipeline layers.");
                return;
            }

            stateGlobalApplication.balances[stateGlobalApplication.activeEnvironment] -= allocationValue;
            
            const currentAsset = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex];
            const strikePrice = stateGlobalApplication.chartDataSeries[stateGlobalApplication.chartDataSeries.length - 1].y;
            
            const createdContractPayload = {
                id: Math.floor(Math.random() * 89999) + 10000,
                assetLabel: currentAsset.label,
                direction: directionTypeString,
                amountAllocated: allocationValue,
                strikePrice: strikePrice,
                yieldPercentage: currentAsset.yield,
                secondsRemaining: stateGlobalApplication.inputs.timer * 60,
                accountEnvironment: stateGlobalApplication.activeEnvironment
            };

            stateGlobalApplication.activeTradingPositions.push(createdContractPayload);
            syncActivePositionsViewStack();
            renderDynamicInterfaceElements();
        }

        function syncActivePositionsViewStack() {
            const fallBackDomNode = document.getElementById('emptyTradesFallbackArea');
            const collectionStackNode = document.getElementById('activeTradesRunningListStack');
            const badgeCountNode = document.getElementById('activeTradesBadgeCount');

            if(stateGlobalApplication.activeTradingPositions.length === 0) {
                fallBackDomNode.classList.remove('hidden');
                collectionStackNode.classList.add('hidden');
                badgeCountNode.classList.add('hidden');
                return;
            }

            fallBackDomNode.classList.add('hidden');
            collectionStackNode.classList.remove('hidden');
            badgeCountNode.classList.remove('hidden');
            badgeCountNode.innerText = stateGlobalApplication.activeTradingPositions.length;

            collectionStackNode.innerHTML = '';
            stateGlobalApplication.activeTradingPositions.forEach((positionObject) => {
                const positionWrapperNode = document.createElement('div');
                positionWrapperNode.className = "bg-[#161b22] border border-gray-800 rounded-xl p-3 flex items-center justify-between";
                
                const pathIconDirection = positionObject.direction === 'CALL' ? 'fa-arrow-up text-emerald-400' : 'fa-arrow-down text-rose-400';
                const outputPrefixEnvironment = positionObject.accountEnvironment === 'DEMO' ? 'Ð' : 'PKR';

                positionWrapperNode.innerHTML = `
                    <div class="flex items-center space-x-3 text-xs">
                        <div class="w-7 h-7 rounded-lg bg-gray-900 flex items-center justify-center"><i class="fa-solid ${pathIconDirection}"></i></div>
                        <div>
                            <p class="font-bold text-white">${positionObject.assetLabel}</p>
                            <p class="text-[10px] text-gray-500 font-mono mt-0.5">Strike: ${positionObject.strikePrice.toFixed(2)} | Alloc: ${outputPrefixEnvironment} ${positionObject.amountAllocated}</p>
                        </div>
                    </div>
                    <div class="text-right">
                        <span class="text-xs font-mono font-bold text-white bg-gray-900 px-2 py-1 rounded-md border border-gray-800">${positionObject.secondsRemaining}s</span>
                    </div>
                `;
                collectionStackNode.appendChild(positionWrapperNode);
            });
        }

        function processActiveOrderTickMatrices(liveAssetPriceUpdate) {
            if(stateGlobalApplication.activeTradingPositions.length === 0) return;

            for(let i = stateGlobalApplication.activeTradingPositions.length - 1; i >= 0; i--) {
                stateGlobalApplication.activeTradingPositions[i].secondsRemaining--;

                if(stateGlobalApplication.activeTradingPositions[i].secondsRemaining <= 0) {
                    const trackingPosition = stateGlobalApplication.activeTradingPositions[i];
                    let positionIsWinning = false;

                    if(trackingPosition.direction === 'CALL' && liveAssetPriceUpdate > trackingPosition.strikePrice) {
                        positionIsWinning = true;
                    } else if(trackingPosition.direction === 'PUT' && liveAssetPriceUpdate < trackingPosition.strikePrice) {
                        positionIsWinning = true;
                    }

                    if(positionIsWinning) {
                        const payoutReturns = trackingPosition.amountAllocated + Math.floor(trackingPosition.amountAllocated * (trackingPosition.yieldPercentage / 100));
                        stateGlobalApplication.balances[trackingPosition.accountEnvironment] += payoutReturns;
                        alert(`Trade Settlement Won! Retained total: ${trackingPosition.accountEnvironment === 'DEMO' ? 'Ð' : 'PKR'} ${payoutReturns}`);
                    } else {
                        alert(`Trade Settlement Expired OTM (Loss). Contract amount debited.`);
                    }

                    stateGlobalApplication.activeTradingPositions.splice(i, 1);
                }
            }
            syncActivePositionsViewStack();
            renderDynamicInterfaceElements();
        }

        function openPaymentsModal(forcedViewMode = 'deposit') {
            document.getElementById('paymentsModalLayout').classList.remove('hidden');
            switchPaymentsModalTab(forcedViewMode);
        }

        function closePaymentsModal() { document.getElementById('paymentsModalLayout').classList.add('hidden'); }

        function switchPaymentsModalTab(tabModeTokenString) {
            const btnDepositNode = document.getElementById('payTabBtnDeposit');
            const btnWithdrawNode = document.getElementById('payTabBtnWithdraw');
            const injectedContentContainerNode = document.getElementById('paymentTabContentArea');

            if(tabModeTokenString === 'deposit') {
                btnDepositNode.className = "flex-1 py-2 font-bold rounded-lg text-center bg-gray-800 text-emerald-400";
                btnWithdrawNode.className = "flex-1 py-2 font-bold rounded-lg text-center text-gray-500 hover:text-gray-400";
                
                injectedContentContainerNode.innerHTML = `
                    <div class="space-y-3">
                        <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Select Gateway</label>
                        <div class="grid grid-cols-2 gap-2">
                            <div class="p-3 bg-gray-900 border border-emerald-500/30 rounded-xl flex items-center justify-between cursor-pointer"><span class="text-xs font-bold text-white">EasyPaisa</span><i class="fa-solid fa-circle-check text-emerald-400 text-xs"></i></div>
                            <div class="p-3 bg-gray-900 border border-gray-800 rounded-xl flex items-center justify-between cursor-pointer opacity-60"><span class="text-xs font-bold text-white">JazzCash</span></div>
                        </div>
                        <div class="space-y-1.5 pt-1">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Deposit Volume Amount</label>
                            <input type="number" id="depositAmountFieldInputElement" value="1000" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-emerald-500 outline-none">
                        </div>
                        <button onclick="executePaymentGatewayPipeline('DEPOSIT')" class="w-full h-11 rounded-xl neon-green-btn text-xs font-black uppercase tracking-wider shadow-lg pt-0.5 mt-2 active:scale-95 transition">Authorize Funding Channel</button>
                    </div>
                `;
            } else {
                btnDepositNode.className = "flex-1 py-2 font-bold rounded-lg text-center text-gray-500 hover:text-gray-400";
                btnWithdrawNode.className = "flex-1 py-2 font-bold rounded-lg text-center bg-gray-800 text-rose-400";

                injectedContentContainerNode.innerHTML = `
                    <div class="space-y-3">
                        <div class="space-y-1.5">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Withdrawal Value (PKR)</label>
                            <input type="number" id="withdrawAmountFieldInputElement" placeholder="Min 500" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-rose-500 outline-none">
                        </div>
                        <div class="space-y-1.5">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Destination Account Identifier Number</label>
                            <input type="text" placeholder="03XXXXXXXXX" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-rose-500 outline-none">
                        </div>
                        <button onclick="executePaymentGatewayPipeline('WITHDRAW')" class="w-full h-11 rounded-xl bg-rose-500 text-white text-xs font-black uppercase tracking-wider shadow-lg pt-0.5 mt-2 active:scale-95 transition">Process Withdrawal Outflux</button>
                    </div>
                `;
            }
        }

        function executePaymentGatewayPipeline(actionTypeToken) {
            if(actionTypeToken === 'DEPOSIT') {
                const depositValueInput = parseFloat(document.getElementById('depositAmountFieldInputElement').value) || 0;
                if(depositValueInput <= 0) {
                    alert("Invalid transaction balance value specified.");
                    return;
                }
                stateGlobalApplication.balances.PKR += depositValueInput;
                alert(`Gateway Simulation Approved. Real-Time account updated with: PKR ${depositValueInput.toFixed(2)}`);
            } else {
                const withdrawValueInput = parseFloat(document.getElementById('withdrawAmountFieldInputElement').value) || 0;
                if(withdrawValueInput <= 0 || stateGlobalApplication.balances.PKR < withdrawValueInput) {
                    alert("Insufficient clear account asset balances or invalid bounds.");
                    return;
                }
                stateGlobalApplication.balances.PKR -= withdrawValueInput;
                alert(`Withdrawal Request Layer Logged. PKR ${withdrawValueInput.toFixed(2)} passed into verification buffer.`);
            }
            renderDynamicInterfaceElements();
            closePaymentsModal();
        }
    </script>
</body>
</html>
