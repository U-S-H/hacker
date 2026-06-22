<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OlympTrade Replicated Pro Platform Terminal</title>
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
        .trading-down-btn:hover { background-color: #d32f2f; }
        .trading-up-btn { background-color: #26a69a; }
        .trading-up-btn:hover { background-color: #00897b; }
        .app-bg-dark { background-color: #1c222c; }
        .app-bg-card { background-color: #161b22; }
    </style>
</head>
<body class="custom-scrollbar min-h-screen flex flex-col justify-between select-none pb-20 md:pb-0">

    <!-- TOP HEADER NAVIGATION BAR (Replicating Screenshot _28-39) -->
    <nav class="bg-[#161b22] border-b border-gray-800/60 px-4 h-14 flex items-center justify-between sticky top-0 z-40">
        <div class="flex items-center space-x-3">
            <div id="profileDropdownBtn" class="w-8 h-8 rounded-full bg-gray-700/60 flex items-center justify-center border border-gray-600/40 cursor-pointer">
                <i class="fa-solid fa-user text-sm text-gray-300"></i>
            </div>
            <div class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></div>
        </div>

        <!-- Center Accounts Switch Context Trigger -->
        <div onclick="openAccountsModal()" class="flex flex-col items-center justify-center cursor-pointer group">
            <div class="flex items-center space-x-1">
                <span id="navActiveAccountBalance" class="font-mono font-bold text-sm tracking-wide text-white">PKR 0.00</span>
                <i class="fa-solid fa-chevron-down text-[10px] text-gray-400 group-hover:text-white transition"></i>
            </div>
            <span id="navActiveAccountLabel" class="text-[9px] text-gray-400 font-medium">PKR Account</span>
        </div>

        <!-- Right Hand Neon Wallet Action Trigger Button -->
        <button onclick="openPaymentsModal()" class="w-9 h-8 rounded-lg neon-green-btn flex items-center justify-center shadow-lg shadow-emerald-500/10 active:scale-95 transition">
            <i class="fa-solid fa-wallet text-sm"></i>
        </button>
    </nav>

    <!-- MAIN DASHBOARD CONTENT AREA DECK FRAME -->
    <main class="max-w-md mx-auto w-full flex-grow flex flex-col justify-between px-3 pt-2 space-y-2">
        
        <!-- Asset Setup Info Dropdown Array Line -->
        <div class="flex items-center justify-between bg-[#161b22] p-2 rounded-xl border border-gray-800/40">
            <div id="logoTapTarget" class="flex items-center space-x-2 bg-gray-800/40 px-3 py-1 rounded-lg cursor-pointer">
                <div class="w-4 h-4 bg-amber-500 rounded flex items-center justify-center text-[10px] font-black text-black">A</div>
                <span class="text-xs font-bold text-white tracking-wide">Asia Composite Index</span>
                <span class="text-[11px] font-mono font-bold text-emerald-400">85%</span>
                <i class="fa-solid fa-chevron-down text-[9px] text-gray-400"></i>
            </div>
            <div class="flex items-center space-x-2">
                <button class="w-7 h-7 bg-gray-800/60 text-gray-400 rounded-lg text-xs flex items-center justify-center"><i class="fa-solid fa-compass"></i></button>
                <button class="px-2 h-7 bg-gray-800/60 text-white font-mono font-bold rounded-lg text-[11px] flex items-center justify-center">5s</button>
                <button class="w-7 h-7 bg-gray-800/60 text-gray-400 rounded-lg text-xs flex items-center justify-center"><i class="fa-solid fa-wave-square"></i></button>
            </div>
        </div>

        <!-- MAIN GRAPH INTERACTIVE ENGINE SCREEN CANVAS BLOCK -->
        <div class="flex-grow bg-[#11141a] border border-gray-900 rounded-2xl relative p-1 flex flex-col justify-center min-h-[280px]">
            <div id="mainChartContainer" class="w-full h-full"></div>
            
            <!-- Real Time Floating Strike Coordinate Tag Floating Label -->
            <div class="absolute right-2 top-1/2 -translate-y-1/2 bg-slate-900 border border-gray-700/80 rounded-l pl-2 pr-1 py-0.5 text-[11px] font-mono font-bold text-white flex items-center space-x-1.5 shadow-xl z-20">
                <span id="chartCountdownTracker" class="text-gray-400 text-[10px] bg-gray-800 px-1 rounded">00:03</span>
                <span id="chartFloatingAssetPrice" class="text-emerald-400">5984.13</span>
            </div>
        </div>

        <!-- SYSTEM OPERATIONAL PARAMS METRICS INFO BAR (Fixed Time Indicators) -->
        <div class="flex items-center justify-between text-[11px] px-1 text-gray-400 font-medium">
            <span>Fixed Time mode</span>
            <span class="font-mono text-emerald-400 font-semibold" id="potentialYieldLabel">Profit: +PKR 238</span>
        </div>

        <!-- INTERACTIVE BOTTOM ALLOCATION AND CONTROL TRANSMISSION PANEL SHEETS (Screenshot _28-39 Layout) -->
        <div class="bg-[#161b22] border border-gray-800/60 rounded-2xl p-3 space-y-3 shadow-2xl">
            
            <!-- Amount & Timer Horizontal Stepper Pickers Inputs Matrix Grid -->
            <div class="grid grid-cols-2 gap-2.5">
                <div class="bg-[#1c222c] border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                    <button onclick="adjustNumericInput('timer', -1)" class="w-8 h-8 rounded-lg bg-gray-800/60 hover:bg-gray-700 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                    <div class="flex flex-col">
                        <span id="displayExpiryWindowValue" class="text-xs font-mono font-bold text-white">1 min</span>
                    </div>
                    <button onclick="adjustNumericInput('timer', 1)" class="w-8 h-8 rounded-lg bg-gray-800/60 hover:bg-gray-700 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                </div>

                <div class="bg-[#1c222c] border border-gray-800 rounded-xl p-1.5 flex items-center justify-between text-center">
                    <button onclick="adjustNumericInput('amount', -50)" class="w-8 h-8 rounded-lg bg-gray-800/60 hover:bg-gray-700 text-gray-300 font-bold flex items-center justify-center text-sm">-</button>
                    <div class="flex flex-col">
                        <span id="displayAllocationValue" class="text-xs font-mono font-bold text-white">PKR 280</span>
                    </div>
                    <button onclick="adjustNumericInput('amount', 50)" class="w-8 h-8 rounded-lg bg-gray-800/60 hover:bg-gray-700 text-gray-300 font-bold flex items-center justify-center text-sm">+</button>
                </div>
            </div>

            <!-- Double Launch High/Low Action Blocks Channels Trigger Deck -->
            <div class="flex items-center space-x-2">
                <button onclick="dispatchBinaryContract('PUT')" class="flex-1 h-12 rounded-xl trading-down-btn text-white font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg shadow-rose-500/10">
                    <span class="text-xs uppercase tracking-wider font-extrabold">Down</span>
                    <i class="fa-solid fa-arrow-down text-sm"></i>
                </button>
                
                <button class="w-12 h-12 rounded-xl bg-gray-800/60 hover:bg-gray-700 text-gray-300 flex items-center justify-center border border-gray-700/40">
                    <i class="fa-solid fa-clock text-sm"></i>
                </button>

                <button onclick="dispatchBinaryContract('CALL')" class="flex-1 h-12 rounded-xl trading-up-btn text-slate-950 font-bold flex items-center justify-between px-4 transition active:scale-95 shadow-lg shadow-emerald-500/10">
                    <span class="text-xs uppercase tracking-wider font-extrabold text-white">Up</span>
                    <i class="fa-solid fa-arrow-up text-sm text-white"></i>
                </button>
            </div>
        </div>

    </main>

    <!-- NATIVE APP BAR MENU FOOTER NAVIGATION OVERLAYS TABS (Visible Bottom Elements) -->
    <div class="fixed bottom-0 left-0 right-0 h-14 bg-[#161b22] border-t border-gray-800/80 flex items-center justify-around z-30 max-w-md mx-auto px-2 shadow-2xl">
        <button class="flex flex-col items-center justify-center text-[#00e676]"><i class="fa-solid fa-chart-line text-base"></i></button>
        <button class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300"><i class="fa-solid fa-arrow-right-arrows-left text-base"></i></button>
        <button class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300 relative"><i class="fa-solid fa-trophy text-base"></i><span class="absolute -top-1.5 -right-2 w-3.5 h-3.5 bg-emerald-500 text-black text-[8px] font-black rounded-full flex items-center justify-center border border-black">1</span></button>
        <button class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300"><i class="fa-solid fa-bag-shopping text-base"></i></button>
        <button class="flex flex-col items-center justify-center text-gray-500 hover:text-gray-300"><i class="fa-solid fa-circle-question text-base"></i></button>
    </div>

    <!-- OVERLAY SLIDE MODAL WINDOW 1: ACCOUNTS PANEL COMPONENT (Screenshot _51-35) -->
    <div id="accountsModalLayout" class="fixed inset-0 bg-black/70 z-50 hidden flex items-end justify-center transition-all duration-300 backdrop-blur-sm">
        <div class="bg-[#161b22] w-full max-w-md rounded-t-3xl border-t border-gray-800 p-5 space-y-5 animate-slide-up shadow-2xl">
            <div class="flex justify-between items-center">
                <h2 class="text-lg font-bold text-white tracking-wide">Accounts</h2>
                <button onclick="closeAccountsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-sm">✕</button>
            </div>

            <!-- Interactive Currency Balances List Stack Block Frame -->
            <div class="space-y-3">
                
                <!-- Demo Account Option Wrapper Frame Block -->
                <div onclick="selectPlatformAccountEnvironment('DEMO')" class="p-3.5 rounded-xl bg-gray-800/30 border border-gray-700/30 flex items-center justify-between cursor-pointer hover:bg-gray-800/60 transition">
                    <div class="flex items-center space-x-3">
                        <div class="w-7 h-7 bg-amber-500/20 rounded-lg text-amber-500 font-bold text-xs flex items-center justify-center font-mono">Ð</div>
                        <div>
                            <p class="text-xs font-bold text-gray-300">Demo account</p>
                            <p id="modalDemoBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">Ð58,766.67</p>
                        </div>
                    </div>
                    <i id="checkIconDemo" class="fa-solid fa-circle-check text-emerald-400 text-sm hidden"></i>
                </div>

                <!-- PKR Real Cash Account Option Wrapper Frame Block -->
                <div onclick="selectPlatformAccountEnvironment('PKR')" class="p-3.5 rounded-xl bg-gray-800/80 border-2 border-emerald-500/60 flex flex-col space-y-3 cursor-pointer transition">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center space-x-3">
                            <div class="w-7 h-5 bg-emerald-800 rounded flex items-center justify-center text-[9px] text-white font-bold tracking-tighter border border-emerald-600">PK</div>
                            <div>
                                <p class="text-xs font-bold text-gray-100">PKR Account</p>
                                <p id="modalPkrBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">PKR 0.00</p>
                            </div>
                        </div>
                        <div class="flex items-center space-x-2">
                            <i class="fa-solid fa-ellipsis-vertical text-gray-400 text-xs px-1"></i>
                            <i id="checkIconPkr" class="fa-solid fa-circle-check text-emerald-400 text-sm"></i>
                        </div>
                    </div>
                    <!-- Sub Actions Shortcut Ribbon Array Links -->
                    <div class="grid grid-cols-2 gap-2 pt-1.5">
                        <button onclick="event.stopPropagation(); openPaymentsModal('withdraw')" class="py-2 rounded-xl bg-gray-700/60 hover:bg-gray-700 text-xs text-white font-bold transition">Withdraw</button>
                        <button onclick="event.stopPropagation(); openPaymentsModal('deposit')" class="py-2 rounded-xl neon-green-btn text-xs transition">Deposit</button>
                    </div>
                </div>

                <!-- USDT Crypto Corporate Asset Holding Wrapper Frame Block -->
                <div onclick="selectPlatformAccountEnvironment('USDT')" class="p-3.5 rounded-xl bg-gray-800/30 border border-gray-700/30 flex items-center justify-between cursor-pointer hover:bg-gray-800/60 transition">
                    <div class="flex items-center space-x-3">
                        <div class="w-7 h-7 bg-teal-500/10 rounded-lg text-teal-400 font-bold text-xs flex items-center justify-center"><i class="fa-brands fa-ethereum"></i></div>
                        <div>
                            <p class="text-xs font-bold text-gray-300">USDT Account</p>
                            <p id="modalUsdtBalanceDisplay" class="text-sm font-mono font-black text-white mt-0.5">USDT 0.00</p>
                        </div>
                    </div>
                    <div class="flex items-center space-x-2">
                        <i class="fa-solid fa-ellipsis-vertical text-gray-400 text-xs px-1"></i>
                        <i id="checkIconUsdt" class="fa-solid fa-circle-check text-emerald-400 text-sm hidden"></i>
                    </div>
                </div>

                <!-- Add Extra Sandbox Environment Configuration Trigger Area -->
                <button class="w-full py-3 border border-dashed border-gray-700 rounded-xl text-xs font-bold text-gray-400 hover:text-white transition flex items-center justify-center space-x-2">
                    <i class="fa-solid fa-plus text-[10px]"></i> <span>Add Account</span>
                </button>
            </div>
        </div>
    </div>

    <!-- OVERLAY SLIDE MODAL WINDOW 2: PAYMENTS INTERFACE MATRIX DECK PANEL (Screenshot _51-42 Layout) -->
    <div id="paymentsModalLayout" class="fixed inset-0 bg-black/70 z-50 hidden flex items-end justify-center transition-all duration-300 backdrop-blur-sm">
        <div class="bg-[#161b22] w-full max-w-md rounded-t-3xl border-t border-gray-800 p-5 space-y-5 shadow-2xl">
            <div class="flex justify-between items-center border-b border-gray-800 pb-3">
                <h2 class="text-lg font-bold text-white tracking-wide">Payments</h2>
                <button onclick="closePaymentsModal()" class="w-8 h-8 rounded-full bg-gray-800 text-gray-400 flex items-center justify-center font-bold text-sm">✕</button>
            </div>

            <!-- Big Stacked Uniform Grid Panel Items List Menu Options Columns -->
            <div id="paymentsMenuStackList" class="space-y-2.5">
                <button onclick="switchPaymentsViewSubForm('deposit')" class="w-full py-3.5 px-4 rounded-xl neon-green-btn flex items-center space-x-3 transition active:scale-[0.99]">
                    <i class="fa-solid fa-wallet text-sm"></i> <span class="text-xs uppercase font-black tracking-wider">Deposit</span>
                </button>
                <button onclick="switchPaymentsViewSubForm('withdraw')" class="w-full py-3.5 px-4 rounded-xl bg-gray-800 text-gray-200 hover:text-white flex items-center space-x-3 transition active:scale-[0.99]">
                    <i class="fa-solid fa-money-bill-transfer text-sm text-gray-400"></i> <span class="text-xs uppercase font-bold tracking-wider">Withdraw</span>
                </button>
                <button class="w-full py-3.5 px-4 rounded-xl bg-gray-800 text-gray-200 hover:text-white flex items-center space-x-3 transition opacity-50 cursor-not-allowed">
                    <i class="fa-solid fa-right-left text-sm text-gray-400"></i> <span class="text-xs uppercase font-bold tracking-wider">Transfer</span>
                </button>
                <button onclick="switchPaymentsViewSubForm('history')" class="w-full py-3.5 px-4 rounded-xl bg-gray-800 text-gray-200 hover:text-white flex items-center space-x-3 transition active:scale-[0.99]">
                    <i class="fa-solid fa-clock-rotate-left text-sm text-gray-400"></i> <span class="text-xs uppercase font-bold tracking-wider">Transactions</span>
                </button>
            </div>

            <!-- Dynamic Sub-Forms Inputs Field Sets Container Context -->
            <div id="paymentsActionSubInterfaceBox" class="hidden space-y-4">
                <div class="flex items-center space-x-2 text-xs text-amber-400 font-bold bg-amber-500/10 p-2.5 rounded-xl border border-amber-500/20">
                    <i class="fa-solid fa-circle-exclamation text-sm"></i>
                    <span>Authorized Core Routing Terminal Node Operations Channels:</span>
                </div>
                
                <!-- Inner Deposit Setup Wire Fields Layout Elements Box -->
                <div id="subFormFieldsDeposit" class="hidden space-y-3 text-xs">
                    <div class="bg-slate-950 p-3 rounded-xl border border-gray-800 space-y-1.5 font-mono text-gray-400">
                        <p><span class="text-emerald-400 font-bold">JazzCash Node Pool:</span> 03705519562</p>
                        <p><span class="text-emerald-400 font-bold">EasyPaisa Distribution:</span> 03379827882</p>
                    </div>
                    <input type="number" id="inputDepositAmountVal" value="280" class="w-full bg-slate-950 border border-gray-800 rounded-xl p-3 text-white font-mono font-bold focus:outline-none focus:border-emerald-500" placeholder="Amount Capacity (PKR)">
                    <input type="text" id="inputDepositTIDVal" class="w-full bg-slate-950 border border-gray-800 rounded-xl p-3 text-white font-mono focus:outline-none focus:border-emerald-500" placeholder="Verification TID String Key">
                    <button onclick="commitFundingFormTransmission('DEP')" class="w-full py-3 neon-green-btn rounded-xl uppercase text-xs font-black tracking-wider">Submit Deposit Invoice</button>
                </div>

                <!-- Inner Cashout Settlement Fields Layout Box -->
                <div id="subFormFieldsWithdraw" class="hidden space-y-3 text-xs">
                    <input type="number" id="inputWithdrawAmountVal" value="500" class="w-full bg-slate-950 border border-gray-800 rounded-xl p-3 text-white font-mono font-bold focus:outline-none focus:border-rose-500" placeholder="Withdrawal Allocation (PKR)">
                    <input type="text" id="inputWithdrawTargetNumber" class="w-full bg-slate-950 border border-gray-800 rounded-xl p-3 text-white font-mono focus:outline-none focus:border-rose-500" placeholder="Receiver Mobile Account Number (03XXXXXXXXX)">
                    <button onclick="commitFundingFormTransmission('WTH')" class="w-full py-3 bg-rose-500 text-white rounded-xl uppercase text-xs font-black tracking-wider">Request Liquidation Wire</button>
                </div>

                <!-- Inner Transactional History Logs List Deck Canvas -->
                <div id="subFormFieldsHistory" class="hidden max-h-[220px] overflow-y-auto custom-scrollbar space-y-2">
                    <p class="text-center text-gray-500 text-xs py-4" id="emptyLogsTextFallback">No recorded clear funding vectors tracked in local buffer.</p>
                    <div id="innerLogsOutputStackArea" class="space-y-1.5"></div>
                </div>

                <button onclick="revertToPaymentsMenuMainHome()" class="w-full py-2 bg-gray-800 text-gray-400 rounded-xl font-bold text-xs uppercase tracking-wide transition">Back to Payment Center</button>
            </div>
        </div>
    </div>

    <!-- SECRET CONTROL ADM OVERLAY PLATFORM MATRIX FRAME (Triggered via 5 rapid taps on Asset box) -->
    <div id="backOfficeAdminConsolePanel" class="fixed inset-0 bg-[#0f1217] z-50 hidden p-4 flex flex-col font-mono text-xs">
        <div class="flex justify-between items-center border-b border-gray-800 pb-2 mb-3">
            <h3 class="text-amber-500 font-black tracking-widest uppercase">Trading1 Secret Back-Office Terminal Authorization Index</h3>
            <button onclick="deactivateAdminInterfaceConsole()" class="bg-gray-800 text-white px-2.5 py-1 rounded text-[10px]">Exit Overlay</button>
        </div>
        <div class="flex-grow overflow-y-auto custom-scrollbar">
            <table class="w-full text-left border-collapse">
                <thead>
                    <tr class="border-b border-gray-800 text-gray-500 text-[10px] uppercase">
                        <th class="pb-1">ID Node String</th>
                        <th class="pb-1">Dimension</th>
                        <th class="pb-1">Capacity Amount</th>
                        <th class="pb-1 text-right">Judgement Action Act</th>
                    </tr>
                </thead>
                <tbody id="adminManagementTableBodyRows" class="divide-y divide-gray-900"></tbody>
            </table>
        </div>
    </div>

    <!-- MAIN CORE PLATFORM ARCHITECTURE DATA SCRIPT ENGINE CONTROL -->
    <script>
        // Internal Global Environment Management State Arrays Matrix
        let platformActiveEnvironmentMode = 'DEMO'; // Switch options items: 'PKR', 'USDT'
        let demoAccountCapitalBalanceSum = parseFloat(localStorage.getItem('ot_demo_bal') || '58766.67');
        let pkrAccountCapitalBalanceSum = parseFloat(localStorage.getItem('ot_pkr_bal') || '0.00');
        let usdtAccountCapitalBalanceSum = parseFloat(localStorage.getItem('ot_usdt_bal') || '0.00');

        let allocationInputAmountStepValue = 280;
        let selectedTimeExpirySecondsLength = 60;

        let internalLiveGlobalApexChartInstance = null;
        let runningActiveRealTimeContractsBufferList = [];
        let globalCorporateFundingLedgerArray = JSON.parse(localStorage.getItem('ot_funding_ledger') || '[]');

        let logoConsecutiveTapsClickCounter = 0;
        let logoTapsTimerContextTimeoutRef = null;

        const assetHistoryFeedsLiveDatabase = {
            basePrice: 5984.10,
            currentPrice: 5984.13,
            historyArray: Array.from({length: 25}, () => 5984.10 + (Math.random() * 2 - 1))
        };

        // Window UI Initializer Matrix Core Hooks
        window.onload = function() {
            renderActiveInterfaceMainDisplayValues();
            initializeHighFrequencyLiveChart();
            processActiveContractsLedgerTickingLoops();
        };

        function renderActiveInterfaceMainDisplayValues() {
            // Update Top Header Context Displays Anchors points
            const navBalLabel = document.getElementById('navActiveAccountBalance');
            const navTitleLabel = document.getElementById('navActiveAccountLabel');

            if(platformActiveEnvironmentMode === 'DEMO') {
                navBalLabel.innerText = `Ð${demoAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2, maximumFractionDigits:2})}`;
                navTitleLabel.innerText = "Demo account";
            } else if(platformActiveEnvironmentMode === 'PKR') {
                navBalLabel.innerText = `PKR ${pkrAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2, maximumFractionDigits:2})}`;
                navTitleLabel.innerText = "PKR Account";
            } else {
                navBalLabel.innerText = `USDT ${usdtAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2, maximumFractionDigits:2})}`;
                navTitleLabel.innerText = "USDT Account";
            }

            // Sync Slider Inside Elements Boxes Models Text Strings
            document.getElementById('modalDemoBalanceDisplay').innerText = `Ð${demoAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2})}`;
            document.getElementById('modalPkrBalanceDisplay').innerText = `PKR ${pkrAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2})}`;
            document.getElementById('modalUsdtBalanceDisplay').innerText = `USDT ${usdtAccountCapitalBalanceSum.toLocaleString(undefined, {minimumFractionDigits:2})}`;

            // Save Structural Framework State Profiles Local Variables Storage Pools
            localStorage.setItem('ot_demo_bal', demoAccountCapitalBalanceSum.toString());
            localStorage.setItem('ot_pkr_bal', pkrAccountCapitalBalanceSum.toString());
            localStorage.setItem('ot_usdt_bal', usdtAccountCapitalBalanceSum.toString());

            document.getElementById('displayAllocationValue').innerText = `${platformActiveEnvironmentMode === 'DEMO' ? 'Ð' : (platformActiveEnvironmentMode === 'USDT' ? 'USDT' : 'PKR')} ${allocationInputAmountStepValue}`;
            document.getElementById('potentialYieldLabel').innerText = `Profit: +${platformActiveEnvironmentMode === 'DEMO' ? 'Ð' : (platformActiveEnvironmentMode === 'USDT' ? 'USDT' : 'PKR')} ${Math.floor(allocationInputAmountStepValue * 0.85)}`;
        }

        // Stepper Selector Modifiers Actions Methods Controllers Links
        window.adjustNumericInput = function(dimensionType, incrementCoefficientDelta) {
            if(dimensionType === 'amount') {
                allocationInputAmountStepValue = Math.max(10, allocationInputAmountStepValue + incrementCoefficientDelta);
            } else {
                selectedTimeExpirySecondsLength = Math.max(5, selectedTimeExpirySecondsLength + (incrementCoefficientDelta * 5));
                document.getElementById('displayExpiryWindowValue').innerText = selectedTimeExpirySecondsLength >= 60 ? `${selectedTimeExpirySecondsLength/60} min` : `${selectedTimeExpirySecondsLength} sec`;
            }
            renderActiveInterfaceMainDisplayValues();
        };

        // Account Environment Slider Layer Switches Triggers Layout Bindings Connects
        window.openAccountsModal = function() { document.getElementById('accountsModalLayout').classList.remove('hidden'); syncCheckedIconsCheckmarks(); };
        window.closeAccountsModal = function() { document.getElementById('accountsModalLayout').classList.add('hidden'); };

        window.selectPlatformAccountEnvironment = function(targetEnvKeyString) {
            platformActiveEnvironmentMode = targetEnvKeyString;
            renderActiveInterfaceMainDisplayValues();
            syncCheckedIconsCheckmarks();
            setTimeout(closeAccountsModal, 200);
        };

        function syncCheckedIconsCheckmarks() {
            ['Demo', 'Pkr', 'Usdt'].forEach(k => {
                document.getElementById(`checkIcon${k}`).classList.add('hidden');
            });
            if(platformActiveEnvironmentMode === 'DEMO') document.getElementById('checkIconDemo').classList.remove('hidden');
            if(platformActiveEnvironmentMode === 'PKR') document.getElementById('checkIconPkr').classList.remove('hidden');
            if(platformActiveEnvironmentMode === 'USDT') document.getElementById('checkIconUsdt').classList.remove('hidden');
        }

        // Payments Layer Sub Modules Triggers Channels Actions Interfaces
        window.openPaymentsModal = function(directRouteSubViewMode = '') {
            document.getElementById('paymentsModalLayout').classList.remove('hidden');
            if(directRouteSubViewMode) { switchPaymentsViewSubForm(directRouteSubViewMode); }
            else { revertToPaymentsMenuMainHome(); }
        };
        window.closePaymentsModal = function() { document.getElementById('paymentsModalLayout').classList.add('hidden'); };

        window.switchPaymentsViewSubForm = function(subTargetKeyString) {
            document.getElementById('paymentsMenuStackList').classList.add('hidden');
            const box = document.getElementById('paymentsActionSubInterfaceBox'); box.classList.remove('hidden');

            ['deposit', 'withdraw', 'history'].forEach(f => document.getElementById(`subFormFields${f.charAt(0).toUpperCase() + f.slice(1)}`).classList.add('hidden'));
            
            if(subTargetKeyString === 'deposit') document.getElementById('subFormFieldsDeposit').classList.remove('hidden');
            if(subTargetKeyString === 'withdraw') document.getElementById('subFormFieldsWithdraw').classList.remove('hidden');
            if(subTargetKeyString === 'history') { document.getElementById('subFormFieldsHistory').classList.remove('hidden'); syncUIRenderedHistoryLogsItems(); }
        };

        window.revertToPaymentsMenuMainHome = function() {
            document.getElementById('paymentsActionSubInterfaceBox').classList.add('hidden');
            document.getElementById('paymentsMenuStackList').classList.remove('hidden');
        };

        // Appending Wire Invoices Payload Matrix Units Array
        window.commitFundingFormTransmission = function(typeSignatureKey) {
            const calculatedTimestampNodeId = 'INV-' + Math.floor(Math.random()*90000 + 10000);
            let inputtedVolumeValue = 0;
            let transactionNoteCoordinateString = '';

            if(typeSignatureKey === 'DEP') {
                inputtedVolumeValue = parseFloat(document.getElementById('inputDepositAmountVal').value) || 0;
                transactionNoteCoordinateString = document.getElementById('inputDepositTIDVal').value.trim();
                if(inputtedVolumeValue < 10 || !transactionNoteCoordinateString) return alert("All billing transaction identification numbers fields are mandatory inputs.");
            } else {
                inputtedVolumeValue = parseFloat(document.getElementById('inputWithdrawAmountVal').value) || 0;
                transactionNoteCoordinateString = document.getElementById('inputWithdrawTargetNumber').value.trim();
                
                let activeDeductionSourceWalletLevelValue = platformActiveEnvironmentMode === 'DEMO' ? demoAccountCapitalBalanceSum : (platformActiveEnvironmentMode === 'USDT' ? usdtAccountCapitalBalanceSum : pkrAccountCapitalBalanceSum);
                if(inputtedVolumeValue > activeDeductionSourceWalletLevelValue) return alert("System Risk Breach. Clearance limit failure from capital holdings balance pool.");

                // Hold balance assets immediately inside internal pipeline array balance limits checks
                if(platformActiveEnvironmentMode === 'DEMO') demoAccountCapitalBalanceSum -= inputtedVolumeValue;
                else if(platformActiveEnvironmentMode === 'USDT') usdtAccountCapitalBalanceSum -= inputtedVolumeValue;
                else pkrAccountCapitalBalanceSum -= inputtedVolumeValue;
            }

            const billingTransactionPayloadLogItem = {
                id: calculatedTimestampNodeId,
                type: typeSignatureKey === 'DEP' ? 'deposit' : 'withdraw',
                amount: inputtedVolumeValue,
                coordinate: transactionNoteCoordinateString,
                status: 'Pending',
                env: platformActiveEnvironmentMode,
                dateString: new Date().toLocaleTimeString()
            };

            globalCorporateFundingLedgerArray.unshift(billingTransactionPayloadLogItem);
            localStorage.setItem('ot_funding_ledger', JSON.stringify(globalCorporateFundingLedgerArray));
            renderActiveInterfaceMainDisplayValues();
            alert(`Broadcasting Settlement Sequence Token Key: ${calculatedTimestampNodeId}. Awaiting corporate validation framework clearance check rows.`);
            revertToPaymentsMenuMainHome();
        };

        function syncUIRenderedHistoryLogsItems() {
            const listArea = document.getElementById('innerLogsOutputStackArea');
            const textFallback = document.getElementById('emptyLogsTextFallback');
            if(globalCorporateFundingLedgerArray.length === 0) { listArea.innerHTML = ''; textFallback.classList.remove('hidden'); return; }

            textFallback.classList.add('hidden'); listArea.innerHTML = '';
            globalCorporateFundingLedgerArray.forEach(log => {
                const badgeStyleColorClass = log.status === 'Approved' ? 'text-emerald-400' : (log.status === 'Rejected' ? 'text-rose-500' : 'text-amber-400 animate-pulse');
                const row = document.createElement('div');
                row.className = "bg-slate-950 p-2 rounded-xl border border-gray-900 flex justify-between items-center text-[11px] font-mono";
                row.innerHTML = `
                    <div>
                        <p class="font-bold text-white uppercase">${log.type} (${log.env})</p>
                        <p class="text-gray-500 text-[10px]">${log.dateString} | Ref:${log.coordinate}</p>
                    </div>
                    <div class="text-right">
                        <p class="font-black text-gray-200">${log.amount} ${log.env === 'DEMO'?'Ð':'PKR'}</p>
                        <span class="font-bold uppercase ${badgeStyleColorClass}">${log.status}</span>
                    </div>
                `;
                listArea.appendChild(row);
            });
        }

        // Modern Candlestick/Line Hybrid ApexCharts High-Frequency Interactive Rendering Engine
        function initializeHighFrequencyLiveChart() {
            const initialDataPointsListPayload = assetHistoryFeedsLiveDatabase.historyArray;
            const options = {
                chart: { type: 'area', height: '100%', width: '100%', toolbar: { show: false }, sparkline: { enabled: false }, animations: { enabled: true, easing: 'linear', speed: 100 }, background: 'transparent' },
                series: [{ name: 'Price Feed Index Index', data: initialDataPointsListPayload }],
                colors: ['#00e676'],
                stroke: { width: 2.5, curve: 'smooth' },
                fill: { type: 'gradient', gradient: { shadeIntensity: 1, opacityFrom: 0.25, opacityTo: 0.0, stopOnAllowed: true } },
                grid: { show: true, borderColor: '#161b22', strokeDashArray: 3, padding: { right: 50, left: 10 } },
                theme: { mode: 'dark' },
                xaxis: { labels: { show: false }, axisBorder: { show: false }, axisTicks: { show: false } },
                yaxis: { show: true, labels: { style: { colors: '#4b5563', fontFamily: 'monospace' } }, side: 'right', opposite: true }
            };
            if(internalLiveGlobalApexChartInstance) internalLiveGlobalApexChartInstance.destroy();
            internalLiveGlobalApexChartInstance = new ApexCharts(document.getElementById("mainChartContainer"), options);
            internalLiveGlobalApexChartInstance.render();
        }

        // Continuous High Frequency Intermittent Pricing Engine Broadcast Ticking Task Loops
        setInterval(() => {
            const originalBasePriceIndexValue = assetHistoryFeedsLiveDatabase.currentPrice;
            const microPriceOscillationDeltaValue = (Math.random() * 0.16 - 0.08);
            
            assetHistoryFeedsLiveDatabase.currentPrice = originalBasePriceIndexValue + microPriceOscillationDeltaValue;
            assetHistoryFeedsLiveDatabase.historyArray.push(assetHistoryFeedsLiveDatabase.currentPrice);
            if(assetHistoryFeedsLiveDatabase.historyArray.length > 30) assetHistoryFeedsLiveDatabase.historyArray.shift();

            // Refresh Anchors Targets elements items blocks labels
            document.getElementById('chartFloatingAssetPrice').innerText = assetHistoryFeedsLiveDatabase.currentPrice.toFixed(2);
            document.getElementById('chartFloatingAssetPrice').className = assetHistoryFeedsLiveDatabase.currentPrice >= originalBasePriceIndexValue ? "text-emerald-400":"text-rose-500";

            if(internalLiveGlobalApexChartInstance) {
                internalLiveGlobalApexChartInstance.updateSeries([{ data: assetHistoryFeedsLiveDatabase.historyArray }]);
            }

            // Continuous Evaluation Processes on Operating Live Option Positions Positions
            processActiveContractsLedgerTickingLoops();
        }, 1000);

        // Binary Derivatives Trading Operation Action Logic Handles (Includes Dynamic Broker Node Balance Mitigation Risk Shield)
        window.dispatchBinaryContract = function(vectorDirectionKeyString) {
            let activeWalletBalanceLevelValue = platformActiveEnvironmentMode === 'DEMO' ? demoAccountCapitalBalanceSum : (platformActiveEnvironmentMode === 'USDT' ? usdtAccountCapitalBalanceSum : pkrAccountCapitalBalanceSum);
            
            if(allocationInputAmountStepValue <= 0) return alert("Invalid contract entry configuration range values.");
            if(allocationInputAmountStepValue > activeWalletBalanceLevelValue) return alert("Declined entry operation lines. Account balances limits exhaustion boundaries met.");

            if(platformActiveEnvironmentMode === 'DEMO') demoAccountCapitalBalanceSum -= allocationInputAmountStepValue;
            else if(platformActiveEnvironmentMode === 'USDT') usdtAccountCapitalBalanceSum -= allocationInputAmountStepValue;
            else pkrAccountCapitalBalanceSum -= allocationInputAmountStepValue;

            const lockedEntryIndexStrikePoint = assetHistoryFeedsLiveDatabase.currentPrice;
            const singleContractOptionPositionRowItemPayload = {
                id: 'TXN-' + Math.floor(Math.random()*90000 + 10000),
                direction: vectorDirectionKeyString,
                strikePrice: lockedEntryIndexStrikePoint,
                amount: allocationInputAmountStepValue,
                timeRemainingSeconds: selectedTimeExpirySecondsLength,
                env: platformActiveEnvironmentMode
            };

            runningActiveRealTimeContractsBufferList.push(singleContractOptionPositionRowItemPayload);
            renderActiveInterfaceMainDisplayValues();
        };

        function processActiveContractsLedgerTickingLoops() {
            if(runningActiveRealTimeContractsBufferList.length === 0) {
                document.getElementById('chartCountdownTracker').innerText = "00:03";
                return;
            }

            const currentLivePriceSnapshotIndexValue = assetHistoryFeedsLiveDatabase.currentPrice;

            runningActiveRealTimeContractsBufferList.forEach(c => {
                c.timeRemainingSeconds--;
                document.getElementById('chartCountdownTracker').innerText = `00:${c.timeRemainingSeconds < 10 ? '0' + c.timeRemainingSeconds : c.timeRemainingSeconds}`;

                // --- BROKER PROTECTION SYSTEM RISK MANAGEMENT FORMULA (LOSS GENERATOR LOGIC LAYER) ---
                // If a user registers trades with significant financial volume (> PKR 200 / > 200 units) inside Real live environments channels,
                // the platform intercepts values inside terminal loops inside execution nodes at final countdown tick limits to adjust market momentum.
                if(c.env !== 'DEMO' && c.amount >= 200 && c.timeRemainingSeconds === 1) {
                    if(c.direction === 'CALL' && currentLivePriceSnapshotIndexValue >= c.strikePrice) {
                        assetHistoryFeedsLiveDatabase.currentPrice = c.strikePrice - 0.05; // Force micro correction beneath strike index tag bounds
                    } else if(c.direction === 'PUT' && currentLivePriceSnapshotIndexValue <= c.strikePrice) {
                        assetHistoryFeedsLiveDatabase.currentPrice = c.strikePrice + 0.05; // Force dynamic push over position boundaries
                    }
                }
            });

            const stillActiveRunningPositionsList = runningActiveRealTimeContractsBufferList.filter(x => x.timeRemainingSeconds > 0);
            const expiredPositionsToSettleList = runningActiveRealTimeContractsBufferList.filter(x => x.timeRemainingSeconds <= 0);

            runningActiveRealTimeContractsBufferList = stillActiveRunningPositionsList;

            expiredPositionsToSettleList.forEach(c => {
                const settlementPriceEndpointVal = assetHistoryFeedsLiveDatabase.currentPrice;
                let outcomeWinFlagStatus = false;

                if(c.direction === 'CALL' && settlementPriceEndpointVal > c.strikePrice) outcomeWinFlagStatus = true;
                if(c.direction === 'PUT' && settlementPriceEndpointVal < c.strikePrice) outcomeWinFlagStatus = true;

                if(outcomeWinFlagStatus) {
                    const financialReturnCreditedYieldSum = c.amount * 1.85;
                    if(c.env === 'DEMO') demoAccountCapitalBalanceSum += financialReturnCreditedYieldSum;
                    else if(c.env === 'USDT') usdtAccountCapitalBalanceSum += financialReturnCreditedYieldSum;
                    else pkrAccountCapitalBalanceSum += financialReturnCreditedYieldSum;
                    
                    alert(`🎉 Option Position Closed in Profit! Settlement yield processed: +${c.env==='DEMO'?'Ð':'PKR'} ${financialReturnCreditedYieldSum.toFixed(2)}`);
                } else {
                    alert(`📉 Option Position Settled Out-of-the-Money. Market index momentum crossed opposite to your chosen position vector.`);
                }
            });

            renderActiveInterfaceMainDisplayValues();
        }

        // --- ADMINISTRATIVE OFFICE INTERFACE INTERCEPTORS GATES CONNECTORS ---
        document.getElementById('logoTapTarget').addEventListener('click', () => {
            logoConsecutiveTapsClickCounter++;
            clearTimeout(logoTapsTimerContextTimeoutRef);
            logoTapsTimerContextTimeoutRef = setTimeout(() => logoConsecutiveTapsClickCounter = 0, 3000);

            if(logoConsecutiveTapsClickCounter >= 5) {
                logoConsecutiveTapsClickCounter = 0;
                const passcode = prompt("Enter Secret Admin Passcode Pattern Key:");
                if(passcode === "5426224") { activateAdminInterfaceConsoleOverlayRows(); }
                else { alert("Access Denied. Signature verification error."); }
            }
        });

        function activateAdminInterfaceConsoleOverlayRows() {
            document.getElementById('backOfficeAdminConsolePanel').classList.remove('hidden');
            const tbody = document.getElementById('adminManagementTableBodyRows'); tbody.innerHTML = '';

            if(globalCorporateFundingLedgerArray.length === 0) {
                tbody.innerHTML = `<tr><td colspan="4" class="py-4 text-center text-gray-600">No available transaction vectors needing review inside local memory.</td></tr>`;
                return;
            }

            globalCorporateFundingLedgerArray.forEach(log => {
                const actionButtonRibbon = log.status === 'Pending' ? `
                    <div class="flex space-x-1 justify-end">
                        <button onclick="adminActionOverrideJudgement('${log.id}', 'Approved')" class="bg-emerald-500 text-black px-2 py-0.5 rounded text-[10px] font-bold uppercase">Approve</button>
                        <button onclick="adminActionOverrideJudgement('${log.id}', 'Rejected')" class="bg-rose-500 text-white px-2 py-0.5 rounded text-[10px] font-bold uppercase">Reject</button>
                    </div>
                ` : `<span class="text-gray-600 uppercase tracking-wide text-[10px]">${log.status}</span>`;

                const row = document.createElement('tr');
                row.className = "border-b border-gray-900 text-gray-300";
                row.innerHTML = `
                    <td class="py-2 text-gray-500">${log.id}</td>
                    <td class="py-2 uppercase text-white font-bold">${log.type} (${log.env})</td>
                    <td class="py-2 text-amber-400 font-bold">${log.amount}</td>
                    <td class="py-2 text-right">${actionButtonRibbon}</td>
                `;
                tbody.appendChild(row);
            });
        }

        window.adminActionOverrideJudgement = function(targetLogIdString, finalSettledStatusKey) {
            const index = globalCorporateFundingLedgerArray.findIndex(x => x.id === targetLogIdString);
            if(index === -1) return;

            const targetPayloadItemObject = globalCorporateFundingLedgerArray[index];
            targetPayloadItemObject.status = finalSettledStatusKey;

            if(targetPayloadItemObject.type === 'deposit' && finalSettledStatusKey === 'Approved') {
                if(targetPayloadItemObject.env === 'DEMO') demoAccountCapitalBalanceSum += targetPayloadItemObject.amount;
                else if(targetPayloadItemObject.env === 'USDT') usdtAccountCapitalBalanceSum += targetPayloadItemObject.amount;
                else pkrAccountCapitalBalanceSum += targetPayloadItemObject.amount;
            }
            if(targetPayloadItemObject.type === 'withdraw' && finalSettledStatusKey === 'Rejected') {
                if(targetPayloadItemObject.env === 'DEMO') demoAccountCapitalBalanceSum += targetPayloadItemObject.amount;
                else if(targetPayloadItemObject.env === 'USDT') usdtAccountCapitalBalanceSum += targetPayloadItemObject.amount;
                else pkrAccountCapitalBalanceSum += targetPayloadItemObject.amount;
            }

            localStorage.setItem('ot_funding_ledger', JSON.stringify(globalCorporateFundingLedgerArray));
            renderActiveInterfaceMainDisplayValues();
            activateAdminInterfaceConsoleOverlayRows();
        };

        window.deactivateAdminInterfaceConsole = function() { document.getElementById('backOfficeAdminConsolePanel').classList.add('hidden'); };
    </script>
</body>
</html>
