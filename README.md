<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MegaWin Club - Premium Live Casino Terminal</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .custom-scrollbar::-webkit-scrollbar { width: 4px; height: 4px; }
        .custom-scrollbar::-webkit-scrollbar-track { background: #0b0d13; }
        .custom-scrollbar::-webkit-scrollbar-thumb { background: #1f2330; border-radius: 4px; }
        body { background-color: #0b0d13; color: #e2e8f0; font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif; }
        .neon-gold-btn { background-color: #ffd700; color: #000000; font-weight: 800; }
        .neon-gold-btn:hover { background-color: #ffc400; }
        .bet-low-btn { background-color: #de3333; }
        .bet-low-btn:hover { background-color: #c22525; }
        .bet-high-btn { background-color: #00b0ff; }
        .bet-high-btn:hover { background-color: #0091ea; }
    </style>
</head>
<body class="custom-scrollbar min-h-screen flex flex-col justify-between pb-14">

    <!-- TOP HEADER NAVIGATION BAR -->
    <nav class="bg-[#121620] border-b border-yellow-600/20 px-4 h-14 flex items-center justify-between sticky top-0 z-40">
        <div class="flex items-center space-x-3">
            <div onclick="switchMainTabView('profile')" class="w-8 h-8 rounded-full bg-yellow-600/10 flex items-center justify-center border border-yellow-600/30 cursor-pointer">
                <i class="fa-solid fa-crown text-sm text-amber-400"></i>
            </div>
            <div class="w-2 h-2 rounded-full bg-red-500 animate-ping"></div>
        </div>

        <div onclick="openAccountsModal()" class="flex flex-col items-center justify-center cursor-pointer group">
            <div class="flex items-center space-x-1">
                <span id="navActiveAccountBalance" class="font-mono font-bold text-sm tracking-wide text-yellow-400">PKR 0.00</span>
                <i class="fa-solid fa-chevron-down text-[10px] text-gray-400 group-hover:text-yellow-400 transition"></i>
            </div>
            <span id="navActiveAccountLabel" class="text-[9px] text-gray-400 font-medium">Casino Wallet</span>
        </div>

        <button onclick="openPaymentsModal()" class="w-9 h-8 rounded-lg neon-gold-btn flex items-center justify-center shadow-lg active:scale-95 transition">
            <i class="fa-solid fa-coins text-sm"></i>
        </button>
    </nav>

    <!-- DYNAMIC CORE CONTENT CONTAINER SHEETS -->
    <div class="w-full max-w-md mx-auto flex-grow flex flex-col px-3 pt-2">
        
        <!-- SECTION 1: CASINO LIVE BETTING STAGE -->
        <div id="coreTabSheetTrading" class="flex-grow flex flex-col justify-between space-y-2">
            <!-- Game Selection Header Array -->
            <div class="flex items-center justify-between bg-[#121620] p-2 rounded-xl border border-yellow-600/20">
                <div onclick="openAssetsSelectionModal()" class="flex items-center space-x-2 bg-gray-900 px-3 py-1 rounded-lg cursor-pointer hover:bg-gray-800">
                    <span id="currentActiveAssetType" class="text-sm">🎰</span>
                    <span id="currentActiveAssetLabelText" class="text-xs font-bold text-white tracking-wide">777 Golden Slots Wheel</span>
                    <span id="currentActiveAssetYieldLabel" class="text-[11px] font-mono font-bold text-yellow-400">x1.95</span>
                    <i class="fa-solid fa-chevron-down text-[9px] text-gray-400"></i>
                </div>
                <div class="flex items-center space-x-2">
                    <button class="px-2 h-7 bg-gray-900 text-yellow-400 font-mono font-bold rounded-lg text-[11px] flex items-center justify-center border border-yellow-600/20">LIVE</button>
                </div>
            </div>

            <!-- INTERACTIVE MULTIPLIER MULTI-GRAPH -->
            <div class="flex-grow bg-[#0b0d13] border border-gray-900 rounded-2xl relative p-1 flex flex-col justify-center min-h-[290px]">
                <div id="mainChartContainer" class="w-full h-full"></div>
                <div class="absolute right-2 top-1/2 -translate-y-1/2 bg-slate-950 border border-yellow-600/30 rounded-l pl-2 pr-1 py-0.5 text-[11px] font-mono font-bold text-white flex items-center space-x-1.5 z-20 shadow-xl">
                    <span id="chartCountdownTracker" class="text-yellow-400 text-[10px] bg-yellow-950/40 px-1 rounded">SPINNING</span>
                    <span id="chartFloatingAssetPrice" class="text-yellow-400">1.00x</span>
                </div>
            </div>

            <div class="flex items-center justify-between text-[11px] px-1 text-gray-400 font-medium">
                <span>Multi-odds House Multiplier</span>
                <span class="font-mono text-yellow-400 font-semibold" id="potentialYieldLabel">Potential Win: PKR 546</span>
            </div>

            <!-- BETTING CONTROL PANEL -->
            <div class="bg-[#121620] border border-yellow-600/10 rounded-2xl p-3 space-y-3 shadow-2xl">
                <div class="grid grid-cols-2 gap-2.5">
                    <div class="bg-gray-900 border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                        <button onclick="adjustNumericInput('timer', -1)" class="w-8 h-8 rounded-lg bg-gray-800 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                        <span id="displayExpiryWindowValue" class="text-xs font-mono font-bold text-white">10 Sec</span>
                        <button onclick="adjustNumericInput('timer', 1)" class="w-8 h-8 rounded-lg bg-gray-800 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                    </div>
                    <div class="bg-gray-900 border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                        <button onclick="adjustNumericInput('amount', -50)" class="w-8 h-8 rounded-lg bg-gray-800 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                        <span id="displayAllocationValue" class="text-xs font-mono font-bold text-white">PKR 280</span>
                        <button onclick="adjustNumericInput('amount', 50)" class="w-8 h-8 rounded-lg bg-gray-800 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                    </div>
                </div>

                <div class="flex items-center space-x-2">
                    <button onclick="dispatchBinaryContract('PUT')" class="flex-1 h-12 rounded-xl bet-low-btn text-white font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg">
                        <span class="text-xs uppercase font-extrabold tracking-wider">Bet Low</span>
                        <i class="fa-solid fa-dice-one text-base"></i>
                    </button>
                    <button class="w-12 h-12 rounded-xl bg-gray-900 text-yellow-400 flex items-center justify-center border border-yellow-600/20"><i class="fa-solid fa-dice text-sm animate-spin"></i></button>
                    <button onclick="dispatchBinaryContract('CALL')" class="flex-1 h-12 rounded-xl bet-high-btn text-white font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg">
                        <span class="text-xs uppercase font-extrabold tracking-wider">Bet High</span>
                        <i class="fa-solid fa-dice-six text-base"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- SECTION 2: CASINO REWARDS / DAILY WHEEL -->
        <div id="coreTabSheetRewards" class="hidden flex-grow space-y-4 pt-2">
            <div class="bg-gradient-to-r from-purple-900 to-indigo-950 p-4 rounded-2xl relative overflow-hidden shadow-xl border border-purple-500/30">
                <span class="absolute right-3 top-3 text-[9px] bg-yellow-500 text-black px-2 py-0.5 rounded-full tracking-widest uppercase font-bold">VIP BONUS</span>
                <h3 class="text-lg font-black text-yellow-400 tracking-wide">Jackpot Multiplier Week</h3>
                <p class="text-xs text-purple-200/80 mt-1">Get up to 200% on EasyPaisa / JazzCash Transfers</p>
                <div class="mt-4 bg-black/40 p-2.5 rounded-xl border border-white/10 flex items-center justify-between text-xs">
                    <span>Use Code: LUCKY777 on checkout nodes.</span>
                    <button onclick="openPaymentsModal('deposit')" class="px-3 py-1.5 bg-yellow-400 text-black rounded-lg font-black shadow-sm">Claim</button>
                </div>
            </div>
            <div class="bg-[#121620] border border-gray-800 rounded-xl p-4 space-y-3">
                <h4 class="text-xs font-bold text-yellow-500 uppercase tracking-wider">Live Winners Board</h4>
                <div class="grid grid-cols-3 gap-2 text-center text-xs">
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Ali_78</p><p class="font-mono font-bold text-emerald-400 mt-1">+PKR 45,000</p></div>
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Zain_King</p><p class="font-mono font-bold text-emerald-400 mt-1">+PKR 12,500</p></div>
                    <div class="bg-slate-950 p-2 rounded-lg border border-gray-900"><p class="text-gray-500 font-medium">Sana_Xx</p><p class="font-mono font-bold text-emerald-400 mt-1">+PKR 98,200</p></div>
                </div>
            </div>
        </div>

        <!-- SECTION 3: OPEN BETS / HISTORY -->
        <div id="coreTabSheetTrades" class="hidden flex-grow space-y-3 pt-2">
            <div class="flex bg-[#121620] rounded-xl p-1 text-xs border border-gray-800">
                <button class="flex-1 py-1.5 font-bold text-yellow-400 bg-gray-900 rounded-lg text-center">Active Bets</button>
                <button class="flex-1 py-1.5 font-bold text-gray-500 text-center opacity-50 cursor-not-allowed">History</button>
            </div>
            <div id="emptyTradesFallbackArea" class="bg-[#121620] border border-gray-800 rounded-2xl p-6 text-center space-y-4">
                <div class="w-16 h-16 bg-gray-900 rounded-full flex items-center justify-center mx-auto text-yellow-500 text-xl"><i class="fa-solid fa-circle-dollar-to-slot"></i></div>
                <div>
                    <h4 class="text-sm font-bold text-white">No Active Bets Placed</h4>
                    <p class="text-xs text-gray-500 mt-1">Choose high or low limits to start your live predictions pool.</p>
                </div>
                <button onclick="switchMainTabView('trading')" class="px-4 py-2 bg-gray-900 border border-yellow-600/20 text-xs font-bold rounded-xl text-white transition">Choose Game</button>
            </div>
            <div id="activeTradesRunningListStack" class="space-y-2 hidden"></div>
        </div>

        <!-- SECTION 4: CASINO CASHOUT TIER MARKET -->
        <div id="coreTabSheetMarket" class="hidden flex-grow space-y-3 pt-2">
            <div class="bg-[#121620] border border-gray-800 rounded-xl p-4 flex items-center justify-between text-xs">
                <div><h4 class="font-bold text-white">VIP Club Pass</h4><p class="text-gray-500 mt-0.5">Increases bet return scales up to x2.5 payouts.</p></div>
                <i class="fa-solid fa-chevron-right text-yellow-500"></i>
            </div>
        </div>

        <!-- SECTION 5: PROFILE HUB -->
        <div id="coreTabSheetProfile" class="hidden flex-grow space-y-3 pt-2">
            <div class="bg-[#121620] border border-gray-800 rounded-2xl p-4 flex items-center space-x-4">
                <div class="w-12 h-12 rounded-full bg-yellow-500/20 border border-yellow-500/40 flex items-center justify-center text-xl text-yellow-400 font-bold">M</div>
                <div>
                    <h3 class="text-sm font-bold text-white">Muhammad Nazim</h3>
                    <p class="text-xs font-mono text-gray-500 mt-0.5 flex items-center space-x-1"><span>ID 121542844</span> <i class="fa-solid fa-copy text-[10px] text-gray-600 cursor-pointer hover:text-white"></i></p>
                </div>
            </div>
        </div>
    </div>

    <!-- BOTTOM APP NAVIGATION RIBBON -->
    <div class="fixed bottom-0 left-0 right-0 h-14 bg-[#121620] border-t border-yellow-600/10 flex items-center justify-around z-30 max-w-md mx-auto px-2 shadow-2xl">
        <button id="navTabBtnTrading" onclick="switchMainTabView('trading')" class="flex flex-col items-center justify-center text-yellow-400 transition"><i class="fa-solid fa-gamepad text-base"></i></button>
        <button id="navTabBtnTrades" onclick="switchMainTabView('trades')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition relative"><i class="fa-solid fa-receipt text-base"></i><span id="activeTradesBadgeCount" class="absolute -top-1 -right-1.5 w-3.5 h-3.5 bg-red-500 text-white text-[8px] font-black rounded-full flex items-center justify-center hidden">0</span></button>
        <button id="navTabBtnRewards" onclick="switchMainTabView('rewards')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition relative"><i class="fa-solid fa-clover text-base"></i><span class="absolute -top-1 -right-1.5 w-3.5 h-3.5 bg-yellow-400 text-black text-[8px] font-black rounded-full flex items-center justify-center border border-black">1</span></button>
        <button id="navTabBtnMarket" onclick="switchMainTabView('market')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition"><i class="fa-solid fa-shop text-base"></i></button>
        <button id="navTabBtnProfile" onclick="switchMainTabView('profile')" class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 transition"><i class="fa-solid fa-user-ninja text-base"></i></button>
    </div>

    <!-- MODAL OVERLAYS ENGINE -->
    <!-- OVERLAY 1: WALLETS SWITCHER -->
    <div id="accountsModalLayout" class="fixed inset-0 bg-black/80 z-50 hidden flex items-end justify-center backdrop-blur-sm">
        <div class="bg-[#121620] w-full max-w-md rounded-t-3xl border-t border-yellow-600/20 p-5 space-y-5 shadow-2xl relative">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white tracking-wide">Select Wallet</h2>
                <button onclick="closeAccountsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>
            <div class="space-y-3">
                <div onclick="selectPlatformAccountEnvironment('DEMO')" class="p-3.5 rounded-xl bg-gray-900 border border-gray-800 flex items-center justify-between cursor-pointer hover:bg-gray-800/60 transition">
                    <div class="flex items-center space-x-3">
                        <div class="w-7 h-7 bg-amber-500/20 rounded-lg text-amber-500 font-bold text-xs flex items-center justify-center font-mono">Ð</div>
                        <div><p class="text-xs font-bold text-gray-400">Demo Play Balance</p><p id="modalDemoBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">Ð58,766.67</p></div>
                    </div>
                    <i id="checkIconDemo" class="fa-solid fa-circle-check text-yellow-400 text-sm hidden"></i>
                </div>

                <div onclick="selectPlatformAccountEnvironment('PKR')" class="p-3.5 rounded-xl bg-gray-900 border border-gray-800 flex flex-col space-y-2 cursor-pointer transition">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center space-x-3">
                            <div class="w-7 h-5 bg-emerald-800 rounded flex items-center justify-center text-[9px] text-white font-bold">PK</div>
                            <div><p class="text-xs font-bold text-gray-300">Real PKR Wallet</p><p id="modalPkrBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">PKR 0.00</p></div>
                        </div>
                        <div class="flex items-center space-x-3">
                            <div onclick="event.stopPropagation(); toggleAccountSettingsContextMenu();" class="p-2 text-gray-400 hover:text-white cursor-pointer"><i class="fa-solid fa-ellipsis-vertical text-xs"></i></div>
                            <i id="checkIconPkr" class="fa-solid fa-circle-check text-yellow-400 text-sm hidden"></i>
                        </div>
                    </div>
                    <div id="accountSettingsContextMenuPanel" class="hidden bg-[#1c222c] border border-gray-800 rounded-xl p-2 grid grid-cols-2 gap-1.5 text-[11px] font-medium text-gray-300">
                        <button onclick="event.stopPropagation(); openPaymentsModal('deposit')" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg text-emerald-400"><i class="fa-solid fa-circle-arrow-down w-4"></i><span>Deposit</span></button>
                        <button onclick="event.stopPropagation(); openPaymentsModal('withdraw')" class="flex items-center space-x-2 p-2 hover:bg-slate-900 rounded-lg text-rose-400"><i class="fa-solid fa-circle-arrow-up w-4"></i><span>Withdraw</span></button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- OVERLAY 2: CASINO GAMES SELECTION -->
    <div id="assetsSelectionModalLayout" class="fixed inset-0 bg-black/80 z-50 hidden flex items-end justify-center backdrop-blur-sm">
        <div class="bg-[#121620] w-full max-w-md h-[80vh] rounded-t-3xl border-t border-yellow-600/20 p-5 flex flex-col space-y-4 shadow-2xl">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white tracking-wide">Casino Games Lobby</h2>
                <button onclick="closeAssetsSelectionModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>
            <div class="flex-grow overflow-y-auto custom-scrollbar space-y-2 pr-1" id="assetsModalListStack"></div>
        </div>
    </div>

    <!-- OVERLAY 3: EASYPAISA / JAZZCASH DEPOSIT GATEWAY -->
    <div id="paymentsModalLayout" class="fixed inset-0 bg-black/80 z-50 hidden flex items-end justify-center backdrop-blur-sm">
        <div class="bg-[#121620] w-full max-w-md rounded-t-3xl border-t border-yellow-600/20 p-5 space-y-4 shadow-2xl">
            <div class="flex justify-between items-center">
                <h2 id="paymentsModalHeaderTitle" class="text-lg font-bold text-white tracking-wide">Cashier Desk</h2>
                <button onclick="closePaymentsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-xs">✕</button>
            </div>
            <div class="flex bg-gray-900 rounded-xl p-1 text-xs border border-gray-800">
                <button id="payTabBtnDeposit" onclick="switchPaymentsModalTab('deposit')" class="flex-1 py-2 font-bold rounded-lg text-center transition">Add Money</button>
                <button id="payTabBtnWithdraw" onclick="switchPaymentsModalTab('withdraw')" class="flex-1 py-2 font-bold rounded-lg text-center transition">Cashout</button>
            </div>
            <div id="paymentTabContentArea" class="space-y-4 pt-1"></div>
        </div>
    </div>

    <!-- MAIN APP ENGINE MODULE -->
    <script>
        // CASINO CASHOUT MATRIX INDEXES
        const ASSETS_COLLECTION_DATA = [
            { id: 'slots_777', label: '777 Golden Slots Wheel', yield: 95, price: 777.00, type: '🎰' },
            { id: 'cyber_dice', label: 'Cyber Dice Multiplier', yield: 88, price: 12.50, type: '🎲' },
            { id: 'roulette_spin', label: 'Imperial Roulette Index', yield: 92, price: 360.00, type: '🎡' },
            { id: 'rocket_crash', label: 'Moon Rocket Crash Index', yield: 120, price: 420.69, type: '🚀' }
        ];

        let stateGlobalApplication = {
            activeEnvironment: 'DEMO',
            balances: { DEMO: 58766.67, PKR: 0.00 },
            currentAssetIndex: 0,
            chartObjectRef: null,
            chartDataSeries: [],
            activeTradingPositions: [],
            inputs: { timer: 10, amount: 280 } // Timer parsed as Seconds for fast betting rounds
        };

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
            document.getElementById('displayExpiryWindowValue').innerText = stateGlobalApplication.inputs.timer + " Sec";
            document.getElementById('displayAllocationValue').innerText = "PKR " + stateGlobalApplication.inputs.amount;
            
            const currentAsset = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex];
            document.getElementById('currentActiveAssetType').innerText = currentAsset.type;
            document.getElementById('currentActiveAssetLabelText').innerText = currentAsset.label;
            document.getElementById('currentActiveAssetYieldLabel').innerText = "x" + (1 + currentAsset.yield / 100).toFixed(2);
            
            const localProfitCalculated = Math.floor(stateGlobalApplication.inputs.amount * (1 + currentAsset.yield / 100));
            document.getElementById('potentialYieldLabel').innerText = `Potential Win: PKR ${localProfitCalculated}`;

            document.getElementById('navActiveAccountBalance').innerText = (stateGlobalApplication.activeEnvironment === 'DEMO' ? 'Ð ' : 'PKR ') + stateGlobalApplication.balances[stateGlobalApplication.activeEnvironment].toFixed(2);
            document.getElementById('navActiveAccountLabel').innerText = stateGlobalApplication.activeEnvironment === 'DEMO' ? 'Demo Account' : 'Casino Wallet';
            
            document.getElementById('modalDemoBalanceDisplay').innerText = "Ð " + stateGlobalApplication.balances.DEMO.toFixed(2);
            document.getElementById('modalPkrBalanceDisplay').innerText = "PKR " + stateGlobalApplication.balances.PKR.toFixed(2);
        }

        function constructApexChartCanvas() {
            const chartNode = document.getElementById("mainChartContainer");
            if(!chartNode) return;

            let seedPrice = ASSETS_COLLECTION_DATA[stateGlobalApplication.currentAssetIndex].price;
            for(let i = 0; i < 40; i++) {
                seedPrice += (Math.random() - 0.5) * 5;
                stateGlobalApplication.chartDataSeries.push({ x: new Date(Date.now() - (40 - i) * 1000), y: parseFloat(Math.abs(seedPrice).toFixed(2)) });
            }

            const chartLayoutOptions = {
                chart: {
                    type: 'area',
                    height: '100%',
                    sparklines: { enabled: true },
                    animations: { enabled: true, easing: 'linear', dynamicAnimation: { speed: 1000 } },
                    toolbar: { show: false }
                },
                colors: ['#ffd700'],
                stroke: { curve: 'smooth', width: 2 },
                fill: {
                    type: 'gradient',
                    gradient: { shadeIntensity: 1, opacityFrom: 0.5, opacityTo: 0.01, stops: [0, 90, 100] }
                },
                series: [{ name: 'Odds', data: stateGlobalApplication.chartDataSeries.slice() }],
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
                domNode.className = "flex items-center justify-between p-3 bg-gray-900 hover:bg-gray-800 rounded-xl cursor-pointer border border-transparent hover:border-yellow-600/30 transition";
                domNode.onclick = () => { selectActiveTradingAssetIndexPointer(loopIndex); };
                
                domNode.innerHTML = `
                    <div class="flex items-center space-x-3">
                        <div class="text-xl">${assetItem.type}</div>
                        <div>
                            <p class="text-xs font-bold text-white tracking-wide">${assetItem.label}</p>
                            <p class="text-[10px] font-mono text-gray-500 mt-0.5">Pool Pool Multipliers: Dynamic</p>
                        </div>
                    </div>
                    <span class="text-xs font-mono font-bold text-yellow-400">x${(1 + assetItem.yield/100).toFixed(2)}</span>
                `;
                targetedContainer.appendChild(domNode);
            });
        }

        function startGlobalTickIntervalEngines() {
            setInterval(() => {
                const shiftValue = (Math.random() - 0.5) * 4;
                let currentLatestPrice = stateGlobalApplication.chartDataSeries[stateGlobalApplication.chartDataSeries.length - 1].y + shiftValue;
                currentLatestPrice = parseFloat(Math.abs(currentLatestPrice).toFixed(2));

                const multiplierVisualFactor = (1 + (currentLatestPrice % 2) / 2).toFixed(2) + "x";
                document.getElementById('chartFloatingAssetPrice').innerText = multiplierVisualFactor;
                
                document.getElementById('chartFloatingAssetPrice').className = shiftValue >= 0 ? 'text-yellow-400' : 'text-red-400';

                const updatedTimestampNode = { x: new Date(), y: currentLatestPrice };
                stateGlobalApplication.chartDataSeries.push(updatedTimestampNode);
                if(stateGlobalApplication.chartDataSeries.length > 50) stateGlobalApplication.chartDataSeries.shift();

                if(stateGlobalApplication.chartObjectRef) {
                    stateGlobalApplication.chartObjectRef.updateSeries([{ data: stateGlobalApplication.chartDataSeries }]);
                }

                processActiveOrderTickMatrices(currentLatestPrice);
            }, 1000);

            setInterval(() => {
                const indicators = ["ROLLING", "SPINNING", "NEXT ROUND", "BET OPEN"];
                const pick = indicators[Math.floor(Math.random() * indicators.length)];
                document.getElementById('chartCountdownTracker').innerText = pick;
            }, 4000);
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
                activeRibbonBtnNode.className = "flex flex-col items-center justify-center text-yellow-400 transition";
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
                seedPrice += (Math.random() - 0.5) * 5;
                stateGlobalApplication.chartDataSeries.push({ x: new Date(Date.now() - (40 - i) * 1000), y: parseFloat(Math.abs(seedPrice).toFixed(2)) });
            }
            
            renderDynamicInterfaceElements();
            closeAssetsSelectionModal();
        }

        function adjustNumericInput(inputFieldToken, modifierValue) {
            if(inputFieldToken === 'timer') {
                // Adjusting seconds interval rules
                stateGlobalApplication.inputs.timer = Math.max(5, stateGlobalApplication.inputs.timer + modifierValue);
            } else if(inputFieldToken === 'amount') {
                stateGlobalApplication.inputs.amount = Math.max(50, stateGlobalApplication.inputs.amount + modifierValue);
            }
            renderDynamicInterfaceElements();
        }

        function dispatchBinaryContract(directionTypeString) {
            const allocationValue = stateGlobalApplication.inputs.amount;
            const liveBalance = stateGlobalApplication.balances[stateGlobalApplication.activeEnvironment];

            if(liveBalance < allocationValue) {
                alert("Insufficient wallet balance to match this house bet.");
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
                secondsRemaining: stateGlobalApplication.inputs.timer,
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
                positionWrapperNode.className = "bg-gray-900 border border-gray-800 rounded-xl p-3 flex items-center justify-between";
                
                const pathIconDirection = positionObject.direction === 'CALL' ? 'fa-arrow-turn-up text-blue-400' : 'fa-arrow-turn-down text-red-400';
                const outputPrefixEnvironment = positionObject.accountEnvironment === 'DEMO' ? 'Ð' : 'PKR';

                positionWrapperNode.innerHTML = `
                    <div class="flex items-center space-x-3 text-xs">
                        <div class="w-7 h-7 rounded-lg bg-black flex items-center justify-center"><i class="fa-solid ${pathIconDirection}"></i></div>
                        <div>
                            <p class="font-bold text-white">${positionObject.assetLabel}</p>
                            <p class="text-[10px] text-gray-500 font-mono mt-0.5">Pool Mark: ${positionObject.strikePrice.toFixed(2)} | Risk: ${outputPrefixEnvironment} ${positionObject.amountAllocated}</p>
                        </div>
                    </div>
                    <div class="text-right">
                        <span class="text-xs font-mono font-bold text-yellow-400 bg-black px-2 py-1 rounded-md border border-gray-800">${positionObject.secondsRemaining}s</span>
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
                        const payoutReturns = Math.floor(trackingPosition.amountAllocated * (1 + trackingPosition.yieldPercentage / 100));
                        stateGlobalApplication.balances[trackingPosition.accountEnvironment] += payoutReturns;
                        alert(`🎉 JACKPOT WIN! Multiplier hit successfully. Payout Added: ${trackingPosition.accountEnvironment === 'DEMO' ? 'Ð' : 'PKR'} ${payoutReturns}`);
                    } else {
                        alert(`💸 HOUSE WINS! Prediction went off-bounds. Try your luck next spin!`);
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
                btnDepositNode.className = "flex-1 py-2 font-bold rounded-lg text-center bg-gray-800 text-yellow-400";
                btnWithdrawNode.className = "flex-1 py-2 font-bold rounded-lg text-center text-gray-500 hover:text-gray-400";
                
                injectedContentContainerNode.innerHTML = `
                    <div class="space-y-3">
                        <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Local Super Channels</label>
                        <div class="grid grid-cols-2 gap-2">
                            <div class="p-3 bg-gray-900 border border-yellow-500/30 rounded-xl flex items-center justify-between cursor-pointer"><span class="text-xs font-bold text-white">EasyPaisa</span><i class="fa-solid fa-circle-check text-yellow-400 text-xs"></i></div>
                            <div class="p-3 bg-gray-900 border border-gray-800 rounded-xl flex items-center justify-between cursor-pointer opacity-60"><span class="text-xs font-bold text-white">JazzCash</span></div>
                        </div>
                        <div class="space-y-1.5 pt-1">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Topup Chips (PKR)</label>
                            <input type="number" id="depositAmountFieldInputElement" value="1000" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-yellow-400 outline-none">
                        </div>
                        <button onclick="executePaymentGatewayPipeline('DEPOSIT')" class="w-full h-11 rounded-xl neon-gold-btn text-xs font-black uppercase tracking-wider shadow-lg pt-0.5 mt-2 active:scale-95 transition">Secure Gateway Loading</button>
                    </div>
                `;
            } else {
                btnDepositNode.className = "flex-1 py-2 font-bold rounded-lg text-center text-gray-500 hover:text-gray-400";
                btnWithdrawNode.className = "flex-1 py-2 font-bold rounded-lg text-center bg-gray-800 text-red-400";

                injectedContentContainerNode.innerHTML = `
                    <div class="space-y-3">
                        <div class="space-y-1.5">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">Cashout Amount (PKR)</label>
                            <input type="number" id="withdrawAmountFieldInputElement" placeholder="Min 500" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-red-500 outline-none">
                        </div>
                        <div class="space-y-1.5">
                            <label class="text-[11px] font-bold text-gray-400 uppercase tracking-wider block">EasyPaisa Mobile Number</label>
                            <input type="text" placeholder="03XXXXXXXXX" class="w-full h-11 bg-gray-900 border border-gray-800 rounded-xl px-3 font-mono text-sm text-white focus:border-red-500 outline-none">
                        </div>
                        <button onclick="executePaymentGatewayPipeline('WITHDRAW')" class="w-full h-11 rounded-xl bg-red-600 text-white text-xs font-black uppercase tracking-wider shadow-lg pt-0.5 mt-2 active:scale-95 transition">Request Fast Payout</button>
                    </div>
                `;
            }
        }

        function executePaymentGatewayPipeline(actionTypeToken) {
            if(actionTypeToken === 'DEPOSIT') {
                const depositValueInput = parseFloat(document.getElementById('depositAmountFieldInputElement').value) || 0;
                if(depositValueInput <= 0) return;
                stateGlobalApplication.balances.PKR += depositValueInput;
                alert(`Chips Approved! Wallet Updated: PKR ${depositValueInput.toFixed(2)}`);
            } else {
                const withdrawValueInput = parseFloat(document.getElementById('withdrawAmountFieldInputElement').value) || 0;
                if(withdrawValueInput <= 0 || stateGlobalApplication.balances.PKR < withdrawValueInput) {
                    alert("Insufficient payout balance limits.");
                    return;
                }
                stateGlobalApplication.balances.PKR -= withdrawValueInput;
                alert(`Cashout Requested: PKR ${withdrawValueInput.toFixed(2)} processing queue running.`);
            }
            renderDynamicInterfaceElements();
            closePaymentsModal();
        }
    </script>
</body>
</html>
