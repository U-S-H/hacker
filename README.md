<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <title>AKBAR GROUPS | Builders & Real Estate - Premium Demo</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Inter:wght@300;400;600&display=swap');
        
        body { font-family: 'Inter', sans-serif; background: #fafafa; color: #1a1a1a; scroll-behavior: smooth; }
        .font-luxury { font-family: 'Cinzel', serif; }
        
        .hero-section {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1582407947304-fd86f028f716?q=80&w=1596&auto=format&fit=crop');
            background-size: cover; background-position: center;
            height: 90vh;
        }
        
        .gold-gradient {
            background: linear-gradient(135deg, #c5a059 0%, #947231 100%);
        }
        
        .nav-glass {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid rgba(0,0,0,0.05);
        }

        .card-hover:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        .transition-all-300 { transition: all 0.3s ease; }
    </style>
</head>
<body>

    <a href="https://wa.me/YOUR_NUMBER" target="_blank" class="fixed bottom-10 right-10 z-[100] bg-[#25D366] text-white p-4 rounded-full shadow-2xl hover:scale-110 transition-all-300 flex items-center justify-center">
        <i class="fa-brands fa-whatsapp text-3xl"></i>
    </a>

    <nav class="fixed w-full z-50 px-6 md:px-10 py-5 flex justify-between items-center nav-glass">
        <div class="flex flex-col">
            <h1 class="font-luxury text-xl md:text-2xl font-bold tracking-widest text-[#947231]">AKBAR GROUPS</h1>
            <span class="text-[9px] uppercase tracking-[0.3em] font-bold opacity-70">Builders & Real Estate</span>
        </div>
        <div class="hidden lg:flex gap-10 text-[11px] font-bold uppercase tracking-wider">
            <a href="#" class="hover:text-[#947231] transition-all-300">Home</a>
            <a href="#projects" class="hover:text-[#947231] transition-all-300">Projects</a>
            <a href="#calculator" class="hover:text-[#947231] transition-all-300">ROI Tool</a>
            <a href="#contact" class="hover:text-[#947231] transition-all-300">Contact Us</a>
        </div>
        <button class="gold-gradient text-white px-6 py-2 md:px-8 md:py-3 rounded-sm text-[10px] font-bold uppercase tracking-widest shadow-lg">Inquire Now</button>
    </nav>

    <section class="hero-section flex items-center px-10 md:px-24">
        <div class="max-w-3xl">
            <h2 class="text-white text-[10px] md:text-[12px] uppercase tracking-[0.5em] font-bold mb-6">Redefining Luxury Living</h2>
            <h3 class="font-luxury text-white text-4xl md:text-7xl mb-8 leading-tight">Crafting Legacies <br> <span class="text-[#c5a059]">Since Decades</span></h3>
            <p class="text-gray-300 text-base md:text-lg mb-10 font-light leading-relaxed max-w-xl">From premium residential plots to state-of-the-art commercial hubs in Rawalpindi & Islamabad.</p>
            <div class="flex flex-wrap gap-4">
                <button class="gold-gradient text-white px-8 py-4 font-bold uppercase text-[10px] tracking-widest">Explore Projects</button>
                <button class="border border-white/30 text-white px-8 py-4 font-bold uppercase text-[10px] tracking-widest hover:bg-white hover:text-black transition-all-300">Download Brochure</button>
            </div>
        </div>
    </section>

    <section class="py-16 px-10 grid grid-cols-2 md:grid-cols-4 gap-10 text-center bg-white border-b">
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">5.0</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Star Rating</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">88+</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Verified Reviews</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">500+</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Projects Delivered</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">40+</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Years Excellence</p>
        </div>
    </section>

    <section id="projects" class="py-24 px-10 md:px-24 bg-[#f4f4f4]">
        <div class="flex flex-col md:flex-row justify-between items-end mb-16">
            <div>
                <span class="text-[#947231] font-bold uppercase tracking-widest text-xs">Portfolio</span>
                <h2 class="font-luxury text-3xl md:text-4xl mt-4">Featured Developments</h2>
            </div>
            <button class="text-[11px] font-bold border-b-2 border-[#947231] pb-1 uppercase tracking-widest mt-4">View Full Catalog</button>
        </div>

        <div class="grid md:grid-cols-3 gap-8">
            <div class="bg-white rounded-lg overflow-hidden card-hover transition-all-300">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?q=80&w=1470&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[9px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Commercial</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">Modern Business Hub</h5>
                    <p class="text-gray-500 text-sm mb-6">Prime location in Bahria Town Phase 7, Islamabad.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 25M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-lg overflow-hidden card-hover transition-all-300 border-t-4 border-[#c5a059]">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1600596542815-ffad4c1539a9?q=80&w=1475&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[9px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Residential</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">The Royal Villa</h5>
                    <p class="text-gray-500 text-sm mb-6">Luxury Mansion in DHA with bespoke interiors.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 150M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-lg overflow-hidden card-hover transition-all-300">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1512917774080-9991f1c4c750?q=80&w=1470&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[9px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Apartment</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">Skyline Residency</h5>
                    <p class="text-gray-500 text-sm mb-6">Penthouse with panoramic views of Margalla Hills.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 45M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section id="calculator" class="py-24 px-6 md:px-10 bg-white">
        <div class="max-w-4xl mx-auto p-8 md:p-12 rounded-[2rem] border border-[#947231]/20 shadow-2xl bg-gray-50">
            <div class="text-center mb-10">
                <span class="text-[#947231] font-bold uppercase tracking-widest text-xs">Investors Corner</span>
                <h2 class="font-luxury text-3xl mt-2 text-gray-800">Projected ROI Calculator</h2>
                <p class="text-gray-500 text-sm mt-3">Estimate your future property value with Akbar Groups 15% annual growth model.</p>
            </div>

            <div class="grid md:grid-cols-2 gap-8">
                <div>
                    <label class="block text-[10px] font-bold uppercase tracking-widest mb-2 text-gray-500">Investment Amount (PKR)</label>
                    <input id="investAmount" type="number" placeholder="Enter amount..." class="w-full bg-white border border-gray-200 p-4 rounded-xl outline-none focus:border-[#947231] transition-all-300 shadow-sm">
                </div>
                <div>
                    <label class="block text-[10px] font-bold uppercase tracking-widest mb-2 text-gray-500">Growth Duration</label>
                    <select id="years" class="w-full bg-white border border-gray-200 p-4 rounded-xl outline-none focus:border-[#947231] transition-all-300 shadow-sm">
                        <option value="1">1 Year Plan</option>
                        <option value="3">3 Year Plan</option>
                        <option value="5">5 Year Plan</option>
                        <option value="10">10 Year Plan</option>
                    </select>
                </div>
            </div>

            <button onclick="calculateROI()" class="gold-gradient w-full text-white py-5 rounded-xl font-bold uppercase tracking-widest text-[11px] mt-8 shadow-xl hover:scale-[1.01] transition-all-300">Calculate Projected Value</button>
            
            <div id="roiResult" class="mt-10 text-center hidden p-6 bg-white border border-[#947231]/10 rounded-2xl">
                <p class="text-gray-500 text-[10px] uppercase tracking-widest font-bold">Estimated Future Market Value</p>
                <h4 id="futureValue" class="text-4xl font-luxury text-[#947231] mt-2"></h4>
                <p class="text-gray-400 text-[9px] mt-2 uppercase">*Based on premium development market trends.</p>
            </div>
        </div>
    </section>

    <section id="contact" class="py-24 text-center bg-[#111] px-10">
        <h2 class="font-luxury text-white text-3xl md:text-4xl mb-6">Ready to Build Your Legacy?</h2>
        <p class="text-gray-400 mb-10 max-w-2xl mx-auto italic font-light">"Four decades of unmatched construction quality and transparent real estate solutions."</p>
        <div class="flex flex-wrap justify-center gap-6">
            <button class="gold-gradient text-white px-10 py-5 font-bold uppercase text-[10px] tracking-widest shadow-2xl">Book Consultation</button>
            <button class="bg-transparent border border-gray-600 text-white px-10 py-5 font-bold uppercase text-[10px] tracking-widest hover:bg-white hover:text-black transition-all-300">View Office Locations</button>
        </div>
    </section>

    <footer class="bg-black py-10 px-10 text-white/40 border-t border-white/5">
        <div class="flex flex-col md:flex-row justify-between items-center">
            <div class="flex flex-col items-center md:items-start">
                <h1 class="font-luxury text-lg tracking-widest text-white/60">AKBAR GROUPS</h1>
                <p class="text-[8px] uppercase tracking-[0.2em] mt-1">Builders & Real Estate</p>
            </div>
            <p class="text-[9px] uppercase tracking-widest mt-6 md:mt-0">© 2026 Developed for Akbar Groups | High-End Digital Solutions</p>
        </div>
    </footer>

    <script>
        function calculateROI() {
            const amount = parseFloat(document.getElementById('investAmount').value);
            const years = parseInt(document.getElementById('years').value);
            
            if(amount > 0) {
                const rate = 0.15;
                const futureValue = amount * Math.pow((1 + rate), years);
                
                const resultDiv = document.getElementById('roiResult');
                const futureValueText = document.getElementById('futureValue');
                
                resultDiv.classList.remove('hidden');
                futureValueText.innerText = "PKR " + Math.round(futureValue).toLocaleString();
                
                resultDiv.scrollIntoView({ behavior: 'smooth', block: 'center' });
            } else {
                alert("Please enter a valid investment amount.");
            }
        }
    </script>
</body>
</html>
