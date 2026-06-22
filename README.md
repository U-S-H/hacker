<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vestify Pro - Investment Dashboard</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        darkBg: '#0b0f19',
                        cardBg: '#111827',
                        accentGreen: '#10b981',
                    }
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
            <div class="hidden md:flex space-x-8 text-sm font-medium text-gray-400">
                <a href="#" class="hover:text-accentGreen transition">Dashboard</a>
                <a href="#" class="hover:text-accentGreen transition">Analytics</a>
                <a href="#" class="hover:text-accentGreen transition">Markets</a>
                <a href="#" class="hover:text-accentGreen transition">Settings</a>
            </div>
            <div>
                <button class="bg-accentGreen hover:bg-emerald-600 text-darkBg font-semibold px-4 py-2 rounded-lg text-sm transition shadow-lg shadow-emerald-500/20">
                    Connect Wallet
                </button>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
        
        <!-- Hero / Welcome Section -->
        <div class="mb-10 flex flex-col md:flex-row md:items-center md:justify-between gap-4">
            <div>
                <h1 class="text-3xl font-bold text-white">Welcome Back, Investor</h1>
                <p class="text-gray-400 mt-1">Here is your investment portfolio overview for today.</p>
            </div>
            <div class="flex gap-3">
                <button class="bg-gray-800 hover:bg-gray-700 text-white px-4 py-2 rounded-lg text-sm font-medium transition">
                    Deposit
                </button>
                <button class="bg-accentGreen hover:bg-emerald-600 text-darkBg px-4 py-2 rounded-lg text-sm font-medium transition">
                    Invest Now
                </button>
            </div>
        </div>

        <!-- Quick Stats Grid -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-10">
            <!-- Stat 1 -->
            <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                <p class="text-sm font-medium text-gray-400">Total Balance</p>
                <p class="text-3xl font-bold text-white mt-2">$24,850.00</p>
                <span class="text-xs font-semibold text-accentGreen bg-emerald-500/10 px-2 py-1 rounded mt-3 inline-block">
                    +12.5% this month
                </span>
            </div>
            <!-- Stat 2 -->
            <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                <p class="text-sm font-medium text-gray-400">Total Profit</p>
                <p class="text-3xl font-bold text-accentGreen mt-2">+$3,120.45</p>
                <span class="text-xs font-semibold text-accentGreen bg-emerald-500/10 px-2 py-1 rounded mt-3 inline-block">
                    Live Tracking
                </span>
            </div>
            <!-- Stat 3 -->
            <div class="bg-cardBg border border-gray-800 p-6 rounded-2xl shadow-xl">
                <p class="text-sm font-medium text-gray-400">Active Investments</p>
                <p class="text-3xl font-bold text-white mt-2">4 Assets</p>
                <span class="text-xs font-semibold text-blue-400 bg-blue-500/10 px-2 py-1 rounded mt-3 inline-block">
                    Diversified
                </span>
            </div>
        </div>

        <!-- Portfolio Assets Table / List -->
        <div class="bg-cardBg border border-gray-800 rounded-2xl shadow-xl overflow-hidden">
            <div class="p-6 border-b border-gray-800 flex justify-between items-center">
                <h2 class="text-lg font-semibold text-white">Your Assets</h2>
                <a href="#" class="text-sm text-accentGreen hover:underline">View All</a>
            </div>
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="border-b border-gray-800 text-xs font-semibold uppercase tracking-wider text-gray-400 bg-gray-900/50">
                            <th class="p-4">Asset</th>
                            <th class="p-4">Amount</th>
                            <th class="p-4">Price</th>
                            <th class="p-4 text-right">Change</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-gray-800 text-sm">
                        <!-- Asset 1 -->
                        <tr class="hover:bg-gray-800/30 transition">
                            <td class="p-4 flex items-center space-x-3">
                                <span class="w-2 h-2 rounded-full bg-yellow-500"></span>
                                <span class="font-medium text-white">Bitcoin (BTC)</span>
                            </td>
                            <td class="p-4 text-gray-300">0.45 BTC</td>
                            <td class="p-4 text-gray-300">$65,200.00</td>
                            <td class="p-4 text-right text-accentGreen font-medium">+4.2%</td>
                        </tr>
                        <!-- Asset 2 -->
                        <tr class="hover:bg-gray-800/30 transition">
                            <td class="p-4 flex items-center space-x-3">
                                <span class="w-2 h-2 rounded-full bg-blue-500"></span>
                                <span class="font-medium text-white">Ethereum (ETH)</span>
                            </td>
                            <td class="p-4 text-gray-300">2.10 ETH</td>
                            <td class="p-4 text-gray-300">$3,450.00</td>
                            <td class="p-4 text-right text-accentGreen font-medium">+2.8%</td>
                        </tr>
                        <!-- Asset 3 -->
                        <tr class="hover:bg-gray-800/30 transition">
                            <td class="p-4 flex items-center space-x-3">
                                <span class="w-2 h-2 rounded-full bg-green-500"></span>
                                <span class="font-medium text-white">Tech Stocks Fund</span>
                            </td>
                            <td class="p-4 text-gray-300">15 Shares</td>
                            <td class="p-4 text-gray-300">$150.25</td>
                            <td class="p-4 text-right text-red-400 font-medium">-0.5%</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="border-t border-gray-800 mt-20 bg-gray-950 text-xs text-gray-500 py-6 text-center">
        <p>&copy; 2026 Vestify Pro. Built with clean code & security first approach.</p>
    </footer>

</body>
</html>
