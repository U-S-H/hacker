<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <title>AKBAR GROUPS | Builders & Real Estate</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;700&family=Inter:wght@300;400;600&display=swap');
        
        body { font-family: 'Inter', sans-serif; background: #fafafa; color: #1a1a1a; }
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
        transition { transition: all 0.3s ease; }
    </style>
</head>
<body>

    <nav class="fixed w-full z-50 px-10 py-5 flex justify-between items-center nav-glass">
        <div class="flex flex-col">
            <h1 class="font-luxury text-2xl font-bold tracking-widest text-[#947231]">AKBAR GROUPS</h1>
            <span class="text-[9px] uppercase tracking-[0.3em] font-bold opacity-70">Builders & Real Estate</span>
        </div>
        <div class="hidden lg:flex gap-10 text-[11px] font-bold uppercase tracking-wider">
            <a href="#" class="hover:text-[#947231] transition">Home</a>
            <a href="#" class="hover:text-[#947231] transition">Projects</a>
            <a href="#" class="hover:text-[#947231] transition">Developments</a>
            <a href="#" class="hover:text-[#947231] transition">About Us</a>
        </div>
        <button class="gold-gradient text-white px-8 py-3 rounded-sm text-[10px] font-bold uppercase tracking-widest shadow-lg">Contact Team</button>
    </nav>

    <section class="hero-section flex items-center px-10 md:px-24">
        <div class="max-w-3xl">
            <h2 class="text-white text-[12px] uppercase tracking-[0.5em] font-bold mb-6">Redefining Luxury Living</h2>
            <h3 class="font-luxury text-white text-5xl md:text-7xl mb-8 leading-tight">Crafting Legacies <br> <span class="text-[#c5a059]">Since Decades</span></h3>
            <p class="text-gray-300 text-lg mb-12 font-light leading-relaxed max-w-xl">From premium residential plots to state-of-the-art commercial hubs in Rawalpindi & Islamabad.</p>
            <div class="flex gap-6">
                <button class="gold-gradient text-white px-10 py-5 font-bold uppercase text-[11px] tracking-widest">Explore Projects</button>
                <button class="border border-white/30 text-white px-10 py-5 font-bold uppercase text-[11px] tracking-widest hover:bg-white hover:text-black transition">Our Profile</button>
            </div>
        </div>
    </section>

    <section class="py-20 px-10 grid grid-cols-2 md:grid-cols-4 gap-10 text-center bg-white border-b">
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">5.0</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Star Rating</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">88+</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Reviews</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">500+</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Projects Done</p>
        </div>
        <div>
            <h4 class="font-luxury text-3xl font-bold text-[#947231]">100%</h4>
            <p class="text-[10px] uppercase font-bold tracking-widest mt-2">Client Trust</p>
        </div>
    </section>

    <section class="py-24 px-10 md:px-24 bg-[#f4f4f4]">
        <div class="flex justify-between items-end mb-16">
            <div>
                <span class="text-[#947231] font-bold uppercase tracking-widest text-xs">Portfolio</span>
                <h2 class="font-luxury text-4xl mt-4">Featured Developments</h2>
            </div>
            <button class="text-[11px] font-bold border-b-2 border-[#947231] pb-1 uppercase tracking-widest">View All</button>
        </div>

        <div class="grid md:grid-cols-3 gap-8">
            <div class="bg-white rounded-lg overflow-hidden card-hover transition">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1600585154340-be6161a56a0c?q=80&w=1470&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[10px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Commercial</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">Modern Business Hub</h5>
                    <p class="text-gray-500 text-sm mb-6">Located in the heart of Bahria Town Phase 7.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 25M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-lg overflow-hidden card-hover transition">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1600596542815-ffad4c1539a9?q=80&w=1475&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[10px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Residential</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">The Royal Villa</h5>
                    <p class="text-gray-500 text-sm mb-6">5-Kanal Luxury Mansion in DHA Islamabad.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 150M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-lg overflow-hidden card-hover transition">
                <div class="h-64 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1512917774080-9991f1c4c750?q=80&w=1470&auto=format&fit=crop');"></div>
                <div class="p-8">
                    <span class="text-[10px] gold-gradient text-white px-3 py-1 rounded-full font-bold uppercase">Apartment</span>
                    <h5 class="font-luxury text-xl mt-4 mb-2">Skyline Residency</h5>
                    <p class="text-gray-500 text-sm mb-6">Penthouse with panoramic views of Margalla.</p>
                    <div class="flex justify-between items-center pt-6 border-t">
                        <span class="font-bold text-[#947231]">Starting PKR 45M</span>
                        <i class="fa-solid fa-arrow-right text-gray-300"></i>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <section class="py-24 text-center bg-white px-10">
        <h2 class="font-luxury text-4xl mb-6">Interested in Investing with Us?</h2>
        <p class="text-gray-500 mb-10 max-w-2xl mx-auto italic">"40 years of building trust, brick by brick. Let's build your future together."</p>
        <button class="gold-gradient text-white px-12 py-5 font-bold uppercase text-[12px] tracking-[0.2em] shadow-2xl">Talk to an Agent</button>
    </section>

    <footer class="bg-[#111] py-16 px-10 text-white">
        <div class="flex flex-col md:flex-row justify-between items-center opacity-60">
            <h1 class="font-luxury text-xl tracking-widest">AKBAR GROUPS</h1>
            <p class="text-[10px] uppercase tracking-widest mt-6 md:mt-0">© 2026 Developed by High-End Digital Solutions</p>
        </div>
    </footer>

</body>
</html>
