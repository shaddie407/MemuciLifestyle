<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Memuci Lifestyle | Live Beautifully. Live Intentionally.</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600&family=Playfair+Display:wght@400;500;600&display=swap" rel="stylesheet">
    <!-- Added Alpine.js for UI interactivity -->
    <script src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js" defer></script>
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: { 'sans': ['Inter', 'sans-serif'], 'serif': ['Playfair Display', 'serif'], },
                    colors: { 'brand-base': '#333333', 'brand-bg': '#F9F8F6', 'brand-secondary-bg': '#FFFFFF', 'brand-accent': '#C4A484', 'brand-gray': '#888888', 'brand-border': '#EAEAEA', 'brand-pink-bg': '#FCE7F3', 'brand-pink-text': '#DB2777', }
                }
            }
        }
    </script>
    <style>
        .cta-button { transition: all 0.3s ease-in-out; }
        .cta-button:hover { background-color: #333333; color: #FFFFFF; }
        .nav-link { position: relative; transition: color 0.3s; }
        .nav-link::after { content: ''; position: absolute; width: 0; height: 1px; bottom: -5px; left: 50%; transform: translateX(-50%); background-color: #333333; transition: width 0.3s ease-in-out; }
        .nav-link:hover::after { width: 100%; }
        .prose { max-width: 65ch; margin-left: auto; margin-right: auto; }
        .prose h1, .prose h2, .prose h3 { font-family: 'Playfair Display', serif; }
        .prose p, .prose li { font-family: 'Inter', sans-serif; line-height: 1.75; }
        .prose a { text-decoration: underline; color: #C4A484; }
        .prose a:hover { color: #333333; }
        .page { animation: fadeIn 0.5s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
        .color-swatch.active { box-shadow: 0 0 0 2px #333333; }
        .slider-dot.active { background-color: #333333; }
        
        #search-overlay, #popup-overlay, #sale-popup-overlay { transition: opacity 0.3s ease-in-out; }
        .trending-slide { transition: opacity 1s ease-in-out; }
        
        /* Custom scrollbar styles */
        .hide-scrollbar { -ms-overflow-style: none; scrollbar-width: none; }
        .hide-scrollbar::-webkit-scrollbar { display: none; }

        /* Hero Slider Styles */
        .hero-slide { position: absolute; inset: 0; opacity: 0; transition: opacity 1.2s ease-in-out; transform: scale(1.1); }
        .hero-slide.active { opacity: 1; transform: scale(1); }
        .hero-slide .hero-media { position: absolute; top: 50%; left: 50%; min-width: 100%; min-height: 100%; width: auto; height: auto; transform: translateX(-50%) translateY(-50%); z-index: 1; object-fit: cover; }
        .hero-slide .hero-content > * { transition: opacity 0.8s ease-in-out, transform 0.8s ease-in-out; }
        .hero-slide .hero-content h1 { transition-delay: 0.1s; }
        .hero-slide .hero-content p { transition-delay: 0.2s; }
        .hero-slide .hero-content a { transition-delay: 0.3s; }
        .hero-slide:not(.active) .hero-content > * { opacity: 0; transform: translateY(20px); }
        .hero-slide.active .hero-content > * { opacity: 1; transform: translateY(0); }

        [x-cloak] { display: none !important; }
        .gallery-tab.active { background-color: #333333; color: #FFFFFF; }
        
        #sale-popup-content { animation: slideInUp 0.5s ease-out forwards; }
        @keyframes slideInUp { from { transform: translateY(100%); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* Animation for sections */
        .animate-on-scroll {
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s ease-out, transform 0.6s ease-out;
        }
        .animate-on-scroll.is-visible {
            opacity: 1;
            transform: translateY(0);
        }
    </style>
</head>
<body class="bg-brand-bg text-brand-base font-sans antialiased">

    <!-- Header Section -->
    <header id="header" class="bg-brand-bg/80 backdrop-blur-sm sticky top-0 z-50">
        <div class="bg-brand-secondary-bg text-brand-base text-center py-2.5 text-xs border-b border-brand-border">
            <p>FREE SHIPPING ON ALL ORDERS OVER KSH 5,000. <a href="#" data-target="shop-page" class="page-link underline font-medium">SHOP NOW</a></p>
        </div>
        <nav class="container mx-auto px-6 py-5 flex justify-between items-center">
             <div class="flex-1">
                <div x-data="{ open: false }" class="relative hidden md:inline-block">
                    <button @click="open = !open" class="text-xs uppercase tracking-widest text-brand-gray hover:text-brand-base flex items-center gap-1">
                        Pillars
                        <svg class="w-3 h-3 transition-transform" :class="{'rotate-180': open}" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                    </button>
                    <div id="pillars-mega-menu" 
                         x-show="open" 
                         @click.away="open = false" 
                         x-cloak
                         x-transition:enter="transition ease-out duration-200"
                         x-transition:enter-start="opacity-0 transform -translate-y-2"
                         x-transition:enter-end="opacity-100 transform translate-y-0"
                         x-transition:leave="transition ease-in duration-150"
                         x-transition:leave-start="opacity-100 transform translate-y-0"
                         x-transition:leave-end="opacity-0 transform -translate-y-2"
                         class="absolute bg-white shadow-lg rounded-md mt-4 p-8 w-[800px] border border-brand-border z-10">
                    </div>
                </div>
            </div>
            <div class="flex-1 text-center">
                 <a href="#" data-target="home-page" class="page-link text-3xl font-serif font-medium text-brand-base">Memuci Lifestyle</a>
            </div>
            <div class="flex-1 flex items-center justify-end space-x-6">
                <a href="#" data-target="recipes-collection-page" class="page-link hidden md:block nav-link text-xs uppercase tracking-widest text-brand-gray hover:text-brand-base">Recipes</a>
                <a href="#" data-target="shop-page" class="page-link hidden md:block nav-link text-xs uppercase tracking-widest text-brand-gray hover:text-brand-base">Shop</a>
                <a href="#" id="search-button" class="hidden md:block">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-brand-base" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" /></svg>
                </a>
                <a href="#" id="cart-link" data-target="cart-page" class="page-link relative hidden md:block">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-brand-base" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
                    <span id="cart-counter" class="hidden absolute -top-2 -right-2 bg-brand-pink-text text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">0</span>
                </a>
                <button id="mobile-menu-button" class="md:hidden">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-brand-base" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M4 6h16M4 12h16m-16 6h16" /></svg>
                </button>
            </div>
        </nav>
        <div id="mobile-menu" class="hidden md:hidden bg-brand-secondary-bg">
             <a href="#" data-target="epicure-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Epicure & Entertaining</a>
             <a href="#" data-target="motherhood-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Modern Motherhood</a>
             <a href="#" data-target="style-beauty-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Style & Beauty</a>
             <a href="#" data-target="culture-escapes-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Culture & Escapes</a>
             <a href="#" data-target="power-purpose-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Power & Purpose</a>
             <a href="#" data-target="health-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Health</a>
             <a href="#" data-target="fitness-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Fitness</a>
             <a href="#" data-target="relationships-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Relationships</a>
             <a href="#" data-target="recipes-collection-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Recipes</a>
             <a href="#" data-target="shop-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg border-b border-brand-border">Shop</a>
             <a href="#" data-target="cart-page" class="page-link block py-3 px-6 text-sm hover:bg-brand-bg font-semibold">Cart</a>
        </div>
    </header>

    <!-- Search Overlay -->
    <div id="search-overlay" class="fixed inset-0 bg-black/50 z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-lg p-8 w-full max-w-2xl relative">
            <button id="close-search-button" class="absolute top-4 right-4 text-brand-gray hover:text-brand-base">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
            </button>
            <h2 class="text-2xl font-serif text-center mb-6">What are you looking for?</h2>
            <input type="text" id="search-input" class="w-full border border-brand-border rounded-md p-3 text-lg" placeholder="Search articles, recipes, products...">
            <div id="search-results" class="mt-6 max-h-96 overflow-y-auto"></div>
        </div>
    </div>
    
    <main id="app-router">
        <!-- Pages will be rendered here by JavaScript -->
        <div id="home-page" class="page"></div>
        <div id="epicure-page" class="page hidden"></div>
        <div id="motherhood-page" class="page hidden"></div>
        <div id="style-beauty-page" class="page hidden"></div>
        <div id="culture-escapes-page" class="page hidden"></div>
        <div id="power-purpose-page" class="page hidden"></div>
        <div id="health-page" class="page hidden"></div>
        <div id="fitness-page" class="page hidden"></div>
        <div id="relationships-page" class="page hidden"></div>
        <div id="explore-stories-page" class="page hidden"></div>
        <div id="shop-page" class="page hidden"></div>
        <div id="article-page" class="page hidden"></div>
        <div id="recipe-page" class="page hidden"></div>
        <div id="recipes-collection-page" class="page hidden"></div>
        <div id="product-page" class="page hidden"></div>
        <div id="about-page" class="page hidden"></div>
        <div id="contact-page" class="page hidden"></div>
        <div id="faq-page" class="page hidden"></div>
        <div id="terms-page" class="page hidden"></div>
        <div id="cart-page" class="page hidden"></div>
    </main>
    
    <footer class="bg-brand-secondary-bg border-t border-brand-border">
        <div class="container mx-auto px-6 pt-16 pb-12">
            <div class="grid grid-cols-1 md:grid-cols-3 gap-12 mb-12">
                <div>
                    <h3 class="font-serif text-lg mb-4">Follow Us</h3>
                    <p class="text-sm text-brand-gray mb-4">@memucilifestyle</p>
                    <div class="grid grid-cols-3 gap-2">
                        <img src="https://images.unsplash.com/photo-1542060748-10c28b62716f?q=80&w=2070&auto=format&fit=crop" class="w-full h-24 object-cover rounded-md">
                        <img src="https://images.unsplash.com/photo-1552346154-21d32810aba3?q=80&w=2070&auto=format&fit=crop" class="w-full h-24 object-cover rounded-md">
                        <img src="https://images.unsplash.com/photo-1524250502761-5ac9f2e501a3?q=80&w=1887&auto=format&fit=crop" class="w-full h-24 object-cover rounded-md">
                    </div>
                </div>
                 <div>
                    <h3 class="font-serif text-lg mb-4">Navigation</h3>
                    <ul class="space-y-2 text-sm text-brand-gray">
                        <li><a href="#" data-target="about-page" class="page-link hover:text-brand-base">About</a></li>
                        <li><a href="#" data-target="shop-page" class="page-link hover:text-brand-base">Shop</a></li>
                        <li><a href="#" data-target="explore-stories-page" class="page-link hover:text-brand-base">Stories</a></li>
                        <li><a href="#" data-target="contact-page" class="page-link hover:text-brand-base">Contact</a></li>
                    </ul>
                </div>
                 <div>
                    <h3 class="font-serif text-lg mb-4">Join The Community</h3>
                    <p class="text-sm text-brand-gray mb-4">Get exclusive content and updates delivered to your inbox.</p>
                     <form class="flex gap-2">
                        <input type="email" placeholder="Enter your email" class="flex-grow p-2 border border-brand-border rounded-md text-sm focus:outline-none focus:ring-2 focus:ring-brand-accent">
                        <button type="submit" class="bg-brand-base text-white py-2 px-4 text-sm font-semibold cta-button rounded-md">Subscribe</button>
                    </form>
                </div>
            </div>
            <div class="text-center border-t border-brand-border pt-8">
                 <p class="text-xs text-brand-gray">&copy; 2025 Memuci Lifestyle. All Rights Reserved. <a href="#" data-target="terms-page" class="page-link underline">Terms</a> & <a href="#" data-target="terms-page" class="page-link underline">Privacy</a>.</p>
            </div>
        </div>
    </footer>

    <!-- Newsletter Pop-up Modal -->
    <div id="popup-overlay" 
         class="fixed inset-0 bg-black/70 z-[60] flex items-center justify-center p-4"
         x-data="newsletterPopup()"
         x-show="show"
         x-transition:enter="transition ease-out duration-300"
         x-transition:enter-start="opacity-0"
         x-transition:enter-end="opacity-100"
         x-transition:leave="transition ease-in duration-200"
         x-transition:leave-start="opacity-100"
         x-transition:leave-end="opacity-0"
         @click.self="manualClose()"
         x-cloak
    >
        <div id="popup-modal" 
             class="bg-brand-base text-white rounded-lg p-8 w-full max-w-md relative text-center"
             x-show="show"
             x-transition:enter="transition ease-out duration-300"
             x-transition:enter-start="opacity-0 scale-95"
             x-transition:enter-end="opacity-100 scale-100"
             x-transition:leave="transition ease-in duration-200"
             x-transition:leave-start="opacity-100 scale-100"
             x-transition:leave-end="opacity-0 scale-95"
        >
            <button @click="manualClose()" class="absolute top-4 right-4 text-gray-400 hover:text-white">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
            </button>
            <h2 class="text-4xl font-serif">Get 10% off.</h2>
            <h3 class="text-3xl font-serif mt-1">It's on us.</h3>
            <p class="mt-4 text-sm text-gray-300">Become a member of the Memuci Club and get <strong>10% off your first order</strong>—plus early access to exclusive promos, product launches, and wellness content to make your life feel just a little bit better.</p>
            <form @submit.prevent="manualClose()" class="mt-6">
                <input type="email" placeholder="Email address" class="w-full p-3 bg-gray-700 border border-gray-600 rounded-md text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-brand-accent">
                <button type="submit" class="mt-4 w-full bg-white text-brand-base py-3 font-semibold rounded-md hover:bg-gray-200 transition-colors">CONTINUE</button>
            </form>
            <p class="text-xs text-gray-400 mt-4">By continuing, you agree to our <a href="#" data-target="terms-page" class="page-link underline">Terms & Conditions</a>.</p>
        </div>
    </div>


    <!-- Sale Pop-up Modal -->
    <div id="sale-popup-overlay" class="fixed inset-0 bg-black/70 z-[70] flex items-center justify-center hidden">
        <div id="sale-popup-content" class="relative w-full h-full flex items-center justify-center">
            <button id="close-sale-popup-btn" class="absolute top-6 right-6 text-white hover:opacity-75 z-10">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" /></svg>
            </button>
            <div class="absolute inset-0 bg-cover bg-center" style="background-image: url('https://images.unsplash.com/photo-1579546929518-9e396f3cc809?q=80&w=2070&auto=format&fit=crop'); opacity: 0.5;"></div>
            <div class="relative text-center text-white p-8">
                 <h2 class="text-6xl md:text-8xl font-serif font-light leading-none">50% OFF!</h2>
                 <p class="text-2xl md:text-3xl uppercase tracking-widest mt-2">Leather Bags Mega Sale</p>
                 <p class="mt-4 max-w-md">Our biggest sale of the season is here. Discover our collection of timeless leather bags, now at half the price.</p>
                 <a href="#" data-target="shop-page" class="page-link sale-popup-shop-now mt-8 inline-block bg-white text-brand-base py-4 px-12 text-base font-semibold cta-button uppercase tracking-wider rounded-md">Shop Now</a>
            </div>
        </div>
    </div>


    <script>
        document.addEventListener('alpine:init', () => {
            Alpine.data('newsletterPopup', () => ({
                show: false,
                popupTimer: null,
                reappearTimer: null,
                init() {
                    // This component initializes when it's in the DOM.
                    // Start the timer logic.
                    if (sessionStorage.getItem('popupManuallyClosed') !== 'true') {
                        this.reappearTimer = setTimeout(() => this.managePopupCycle(), 8000); // 8 seconds initial delay
                    }
                },
                managePopupCycle() {
                     if (sessionStorage.getItem('popupManuallyClosed') === 'true') return;
                    
                    this.show = true;
                    this.popupTimer = setTimeout(() => {
                        this.show = false;
                        
                        this.reappearTimer = setTimeout(() => {
                            this.managePopupCycle();
                        }, 120000); // 2 minutes (120000 ms)
                    }, 10000); // 10 seconds
                },
                manualClose() {
                    this.show = false;
                    sessionStorage.setItem('popupManuallyClosed', 'true');
                    clearTimeout(this.popupTimer);
                    clearTimeout(this.reappearTimer);
                }
            }));
        });

        document.addEventListener('DOMContentLoaded', () => {
            // --- DATA STORE ---
            let cart = [];
            const content = {
                teamMembers: [
                    { name: 'Carolyne', title: 'Founder & CEO', image: 'https://images.unsplash.com/photo-1494790108377-be9c29b29330?q=80&w=1887&auto=format&fit=crop' },
                    { name: 'Benjamin Carter', title: 'Creative Director', image: 'https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?q=80&w=1887&auto=format&fit=crop' },
                    { name: 'Sophia Rodriguez', title: 'Head of Content', image: 'https://images.unsplash.com/photo-1580489944761-15a19d654956?q=80&w=1961&auto=format&fit=crop' }
                ],
                articles: {
                    "Wine Culture – Pairings, Home Bar Curation, Wine Lifestyle": { image: "https://images.unsplash.com/photo-1553723622-957aa7d1a29a?q=80&w=1935&auto=format&fit=crop", category: "Epicure & Entertaining", subcategory: "Wine Culture", author: "Memuci Editorial", body: "<p>Wine is more than a drink; it’s a language of taste, place, and time. Each bottle holds a story — of sunlight, soil, and craftsmanship — waiting to be uncorked and shared. It’s a symbol of life’s slower rhythms, where conversation lingers and laughter fills the air.</p>" },
                    "Kitchen & Table – Recipes, Hosting Tips, Cooking Essentials": { image: "https://images.unsplash.com/photo-1617418295593-a9a3b6a9a3b0?q=80&w=1887&auto=format&fit=crop", category: "Epicure & Entertaining", subcategory: "Kitchen & Table", author: "Carolyne", body: "<p>Every home has a heart, and it beats in the kitchen. It’s where aromas mingle with laughter, where ingredients become memories, and where love takes the form of nourishment. The kitchen isn’t just a room — it’s the soul of hospitality, creativity, and connection.</p>" },
                    "Garden Notes – Balcony Gardens, Organic Living": { image: "https://images.unsplash.com/photo-1587329245145-5a57897216f1?q=80&w=1887&auto=format&fit=crop", category: "Epicure & Entertaining", subcategory: "Garden Notes", author: "Memuci Editorial", body: "<p>Even in the heart of a city, nature finds a way. A few pots of green can transform a balcony, a window ledge, or a courtyard into a living sanctuary. Gardening isn’t just about growing plants — it’s about cultivating peace.</p>" },
                    "Curated Finds – Tools, Books, and Lifestyle Picks": { image: "https://images.unsplash.com/photo-1594123293998-5a242f534808?q=80&w=1887&auto=format&fit=crop", category: "Epicure & Entertaining", subcategory: "Curated Finds", author: "Memuci Editorial", body: "<p>Curation is the art of choosing with intention. In a world overflowing with noise, choosing less — but better — becomes a form of elegance. A curated life is a mindful one.</p>" },
                    "The Art of the Dinner Party Playlist": { image: "https://images.unsplash.com/photo-1511379938547-c1f69419868d?q=80&w=2070&auto=format&fit=crop", category: "Epicure & Entertaining", author: "Memuci Editorial", body: "<p>Music is the unseen guest at every dinner party. The right playlist can elevate the mood, spark conversation, and turn a simple meal into a memorable experience. We explore how to curate a sonic journey that complements your menu and your company.</p>" },
                    "A Guide to Artisanal Kenyan Coffee": { image: "https://images.unsplash.com/photo-1559496417-e7f25cb247f3?q=80&w=1887&auto=format&fit=crop", category: "Epicure & Entertaining", author: "Carolyne", body: "<p>Kenya is home to some of the world's finest coffee beans. Move beyond your usual brew and explore the rich, complex world of single-origin artisanal coffee. We'll guide you through tasting notes, brewing methods, and the local roasters you need to know.</p>" },
                    "Childhood Journeys – Milestones, Growth Activities, Conscious Parenting": { image: "https://images.unsplash.com/photo-1503919545823-a9f7362f7d3d?q=80&w=1887&auto=format&fit=crop", category: "Modern Motherhood", subcategory: "Childhood Journeys", author: "Carolyne", body: "<p>Childhood is fleeting yet infinite — a collection of small moments that shape a lifetime. From first steps to first friendships, every milestone deserves to be witnessed with presence.</p>" },
                    "Mindful Living – Spirituality, Wellness, Family Rituals": { image: "https://images.unsplash.com/photo-1544321269-8d7c043f6283?q=80&w=2070&auto=format&fit=crop", category: "Modern Motherhood", subcategory: "Mindful Living", author: "Memuci Editorial", body: "<p>Modern life moves fast. Mindful living is a conscious decision to slow it down — to create space for reflection, gratitude, and togetherness.</p>" },
                    "Navigating Postpartum: A Guide for New Mothers": { image: "https://images.unsplash.com/photo-1566004100631-35d015d6a491?q=80&w=1887&auto=format&fit=crop", category: "Modern Motherhood", author: "Carolyne", body: "<p>The postpartum period is a time of immense change and adjustment. This guide offers gentle advice and practical tips for navigating the fourth trimester with grace, self-compassion, and support.</p>" },
                    "Screen Time Sanity: A Balanced Approach for Kids": { image: "https://images.unsplash.com/photo-1584697964190-7383c38b4a78?q=80&w=2070&auto=format&fit=crop", category: "Modern Motherhood", author: "Memuci Editorial", body: "<p>In a digital world, managing screen time is a major challenge for parents. We explore a balanced, mindful approach that focuses on quality over quantity and connection over control.</p>" },
                    "Creating Meaningful Family Traditions": { image: "https://images.unsplash.com/photo-1543340921-820f929f4c5e?q=80&w=1887&auto=format&fit=crop", category: "Modern Motherhood", author: "Memuci Editorial", body: "<p>Traditions are the threads that weave a family's story together. Discover simple yet powerful rituals you can start today to create lasting memories and a strong sense of belonging for your children.</p>" },
                    "The Working Mom's Guide to Beating Burnout": { image: "https://images.unsplash.com/photo-1517245386807-bb43f82c33c4?q=80&w=2070&auto=format&fit=crop", category: "Modern Motherhood", author: "Carolyne", body: "<p>Juggling a career and motherhood can be overwhelming. We share practical strategies for setting boundaries, managing your energy, and finding moments of rest to prevent burnout and thrive in both roles.</p>" },
                    "Beauty Rituals – Skincare, Wellness, Glow Guides": { image: "https://images.unsplash.com/photo-1564292288395-5a5b51b75c87?q=80&w=1887&auto=format&fit=crop", category: "Style & Beauty", subcategory: "Beauty Rituals", author: "Carolyne", body: "<p>Beauty begins with care, not cosmetics. A true glow is cultivated from within — through nourishment, sleep, and serenity.</p>" },
                    "The Wardrobe – Fashion Inspiration, Capsule Wardrobes, Trends": { image: "https://images.unsplash.com/photo-1558769132-cb1aea458c5e?q=80&w=1974&auto=format&fit=crop", category: "Style & Beauty", subcategory: "The Wardrobe", author: "Memuci Editorial", body: "<p>Fashion is storytelling. What you wear communicates who you are before you even speak.</p>" },
                    "15 California Clothing Brands For Casual Style (2025)": { image: "https://images.unsplash.com/photo-1552668693-2be72c866be4?q=80&w=1887&auto=format&fit=crop", category: "Style & Beauty", subcategory: "The Wardrobe", author: "Memuci Editorial", body: "<p>Embrace the laid-back, sun-kissed vibe of the West Coast with these top California-based clothing brands. From sustainable basics to bohemian-chic dresses, we've curated a list of brands that perfectly capture that effortless California style. Perfect for building a versatile and conscious wardrobe.</p>" },
                    "11 Sustainable Underwear And Lingerie Brands (2025)": { image: "https://images.unsplash.com/photo-1617038260897-41a1f1b03348?q=80&w=1887&auto=format&fit=crop", category: "Style & Beauty", subcategory: "The Wardrobe", author: "Memuci Editorial", body: "<p>What you wear closest to your skin matters. These sustainable underwear and lingerie brands prioritize eco-friendly materials, ethical production, and inclusive sizing. Feel good inside and out with our top picks for conscious intimates.</p>" },
                    "9 Sustainable Cashmere Sweaters (2025 Review)": { image: "https://images.unsplash.com/photo-1608675978491-a615a3b9347a?q=80&w=1887&auto=format&fit=crop", category: "Style & Beauty", subcategory: "The Wardrobe", author: "Memuci Editorial", body: "<p>Investing in a cashmere sweater is a luxury that can last a lifetime. We've found the best brands committed to sustainable and ethical cashmere sourcing. Stay warm, stylish, and eco-conscious this season with these beautiful, high-quality sweaters.</p>" },
                    "5-Minute Makeup for a Polished Look": { image: "https://images.unsplash.com/photo-1596495763242-263a45a16823?q=80&w=1887&auto=format&fit=crop", category: "Style & Beauty", author: "Memuci Editorial", body: "<p>Short on time but want to look put-together? Master the art of the 5-minute face. We'll show you the multi-tasking products and simple techniques to achieve a fresh, polished look in no time.</p>" },
                    "Travel Diaries – Weekend Getaways, Kenyan Gems, Destination Guides": { image: "https://images.unsplash.com/photo-1539635278303-d4002c07eae3?q=80&w=2070&auto=format&fit=crop", category: "Culture & Escapes", subcategory: "Travel Diaries", author: "Memuci Editorial", body: "<p>Travel expands perspective. Each journey reveals something — not just about new places, but about yourself.</p>" },
                    "Social Calendar – Events, Gatherings, Special Moments": { image: "https://images.unsplash.com/photo-1519167758481-83f550bb49b6?q=80&w=2098&auto=format&fit=crop", category: "Culture & Escapes", subcategory: "Social Calendar", author: "Memuci Editorial", body: "<p>Life’s beauty is magnified when shared. Attend art shows, wine tastings, and intimate dinners. Host gatherings that spark conversation and connection.</p>" },
                    "Screen & Stage – Shows, Reviews, Creative Culture": { image: "https://images.unsplash.com/photo-1542204165-65bf26472b9b?q=80&w=1974&auto=format&fit=crop", category: "Culture & Escapes", subcategory: "Screen & Stage", author: "Carolyne", body: "<p>Culture is the heartbeat of imagination. Whether film, theatre, or art, storytelling allows us to feel and reflect.</p>" },
                    "The Best Art Galleries to Visit in Nairobi": { image: "https://images.unsplash.com/photo-1549887552-cb1082d_5650?q=80&w=2070&auto=format&fit=crop", category: "Culture & Escapes", author: "Memuci Editorial", body: "<p>Nairobi's art scene is vibrant and booming. From contemporary African art to local craft, we've curated a list of the must-visit galleries that showcase the incredible talent and creative energy of the city.</p>" },
                    "A Weekend Guide to the Champagne Ridge": { image: "https://images.unsplash.com/photo-1621243765882-212e52ac7e12?q=80&w=2070&auto=format&fit=crop", category: "Culture & Escapes", author: "Carolyne", body: "<p>Escape the city and discover the breathtaking views of the Great Rift Valley from Champagne Ridge. Our guide covers the best places to stay, what to do, and how to make the most of a serene weekend getaway just a short drive from Nairobi.</p>" },
                    "Discovering Kenya's Hidden Waterfalls": { image: "https://images.unsplash.com/photo-1500322301132-8f4b7a1e5318?q=80&w=1887&auto=format&fit=crop", category: "Culture & Escapes", author: "Memuci Editorial", body: "<p>Beyond the savanna, Kenya is home to stunning, hidden waterfalls. We've mapped out a few of our favorites, from majestic cascades to secret swimming spots, perfect for your next adventure.</p>" },
                    "Business Playbook – Strategies, Entrepreneurial Tips, Money Talk": { image: "https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?q=80&w=2070&auto=format&fit=crop", category: "Power & Purpose", subcategory: "Business Playbook", author: "Memuci Editorial", body: "<p>Modern entrepreneurship blends ambition with intention. It’s about creating work that matters, not just work that pays.</p>" },
                    "Podcasts & Conversations – Real Talk, Interviews, Audio Diaries": { image: "https://images.unsplash.com/photo-1589903308904-1010c2294adc?q=80&w=1887&auto=format&fit=crop", category: "Power & Purpose", subcategory: "Podcasts & Conversations", author: "Memuci Editorial", body: "<p>In a world of noise, genuine voices matter. Podcasts have become modern storytelling — intimate, authentic, and raw.</p>" },
                    "Books & Brain Food – Reads, Reviews, Reflections": { image: "https://images.unsplash.com/photo-1524995767962-b6f7b11d957f?q=80&w=2070&auto=format&fit=crop", category: "Power & Purpose", subcategory: "Books & Brain Food", author: "Carolyne", body: "<p>Books expand consciousness. Read deeply — fiction for empathy, non-fiction for insight, poetry for soul.</p>" },
                    "Give Back – Philanthropy, Charity Stories, Impact Projects": { image: "https://images.unsplash.com/photo-1532629345422-7515f3d16bb6?q=80&w=2070&auto=format&fit=crop", category: "Power & Purpose", subcategory: "Give Back", author: "Memuci Editorial", body: "<p>True success extends beyond self. Giving back — whether through time, resources, or mentorship — amplifies your purpose.</p>" },
                    "Goal Setting for the Modern Woman": { image: "https://images.unsplash.com/photo-1521791136064-7986c2920216?q=80&w=2070&auto=format&fit=crop", category: "Power & Purpose", author: "Carolyne", body: "<p>Move beyond New Year's resolutions with a more intentional approach to goal setting. We share a framework for setting meaningful goals that align with your values and creating actionable steps to achieve them.</p>" },
                    "Building a Personal Brand with Authenticity": { image: "https://images.unsplash.com/photo-1522202176988-66273c2fd55f?q=80&w=2071&auto=format&fit=crop", category: "Power & Purpose", author: "Memuci Editorial", body: "<p>In today's world, a personal brand is essential. Learn how to cultivate a brand that is a true reflection of your skills, values, and personality, and how to communicate it with confidence and authenticity.</p>" },
                    "9 Best Nontoxic Period Underwear Without PFAS (2025)": { image: "https://images.unsplash.com/photo-1620023613689-3e248b92b6c3?q=80&w=1887&auto=format&fit=crop", category: "Health", subcategory: "Wellness", author: "Carolyne", body: "<p>Making the switch to period underwear is a game-changer for comfort and sustainability. But not all pairs are created equal. We've researched and tested to find the best nontoxic options free from harmful PFAS chemicals, so you can have a worry-free cycle.</p>" },
                    "How To Befriend The Dating Apps": { image: "https://placehold.co/500x600/F8D7DA/212529?text=Illustration", category: "Relationships", subcategory: "Dating", author: "Carolyne", body: "<p>Swiping can feel like a chore, but it doesn't have to. Learn how to craft a profile that truly represents you, write opening lines that actually get a response, and navigate the world of online dating with confidence and a sense of humor. It's time to make the apps work for you.</p>" },
                    "The Three Loves Theory": { image: "https://images.unsplash.com/photo-1563723821757-54202b9f393b?q=80&w=1887&auto=format&fit=crop", category: "Relationships", subcategory: "Theory", author: "Memuci Editorial", body: "<p>Have you heard of the theory that we each experience three great loves in our lifetime? The first is the idealistic love, the second is the hard love that teaches us lessons, and the third is the unexpected love that lasts. We dive deep into this fascinating concept and what it means for your own journey.</p>" },
                    "Flirting Techniques To Lock In Your Summer Fling": { image: "https://images.unsplash.com/photo-157470114821-236562404353?q=80&w=1887&auto=format&fit=crop", category: "Relationships", subcategory: "Dating", author: "Carolyne", body: "<p>Summer's heating up, and so is your love life. Whether you've got your eye on someone special or just want to be ready for a chance encounter, we've got the foolproof flirting tips to help you make a lasting impression. Confidence is key, and we'll show you how to use it.</p>" },
                    "How To Manifest The Relationship You Want": { image: "https://images.unsplash.com/photo-1554126807-6b10f6006702?q=80&w=1935&auto=format&fit=crop", category: "Relationships", subcategory: "Wellness", author: "Memuci Editorial", body: "<p>The law of attraction isn't just about wishful thinking. It's about aligning your energy, thoughts, and actions to attract the love you deserve. We'll guide you through the process of setting clear intentions, releasing limiting beliefs, and calling in the partner of your dreams.</p>" },
                     "Navigating Conflict: A Guide to Healthy Disagreements": { image: "https://images.unsplash.com/photo-1563903530908-afdd155d054a?q=80&w=1887&auto=format&fit=crop", category: "Relationships", subcategory: "Communication", author: "Memuci Editorial", body: "<p>Disagreements are a natural part of any relationship, but how you handle them makes all the difference. Learn to communicate effectively, listen with empathy, and find common ground. Healthy conflict can actually strengthen your bond.</p>" },
                     "The 5 Love Languages: A Summary": { image: "https://images.unsplash.com/photo-1577015412532-62032a13b639?q=80&w=1887&auto=format&fit=crop", category: "Relationships", subcategory: "Theory", author: "Carolyne", body: "<p>Understanding how you and your partner give and receive love is a game-changer. We break down Dr. Gary Chapman's five love languages—Words of Affirmation, Acts of Service, Receiving Gifts, Quality Time, and Physical Touch—and how to apply them to your relationship.</p>" },
                    "The Only 4 Moves You Need to TONE YOUR WHOLE BODY": { image: "https://images.unsplash.com/photo-1598140422479-9c595d7f1b7f?q=80&w=1887&auto=format&fit=crop", category: "Fitness", subcategory: "Workouts", author: "Memuci Editorial", body: "<p>Forget spending hours at the gym. These four compound exercises target multiple muscle groups at once, giving you a full-body workout in record time. From perfecting your squat to mastering the plank, we'll show you moves that deliver maximum results with minimal time commitment.</p>" },
                    "Tone And Tighten On The Go With These Travel-Friendly Pilates": { image: "https://images.unsplash.com/photo-1544367567-0f2fcb009e0b?q=80&w=1820&auto=format&fit=crop", category: "Fitness", subcategory: "Workouts", author: "Carolyne", body: "<p>Staying fit while traveling can be a challenge, but not with these Pilates-inspired moves. All you need is a little bit of floor space to get in a great workout that will lengthen, strengthen, and tone your muscles. No equipment necessary!</p>" },
                    "5 Energizing Morning Yoga Poses": { image: "https://images.unsplash.com/photo-1545346315-f4c47e3e1b55?q=80&w=1887&auto=format&fit=crop", category: "Fitness", subcategory: "Yoga", author: "Memuci Editorial", body: "<p>Start your day on the right foot with a gentle yoga flow. These five poses are designed to awaken your body, increase your energy levels, and set a positive tone for the day ahead. From a simple cat-cow stretch to an invigorating sun salutation, you'll feel ready to take on anything.</p>" },
                    "4 Exercises For a Snatched Waist": { image: "https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?q=80&w=1887&auto=format&fit=crop", category: "Fitness", subcategory: "Workouts", author: "Carolyne", body: "<p>Dreaming of a defined waistline? These four core-cinching exercises are designed to target your obliques and tighten your midsection. Incorporate moves like Russian twists and bicycle crunches into your routine to build a strong, sculpted core.</p>" },
                    "The Importance of Hydration: Are You Drinking Enough Water?": { image: "https://images.unsplash.com/photo-1563203369-694a7c067645?q=80&w=1887&auto=format&fit=crop", category: "Health", subcategory: "Wellness", author: "Memuci Editorial", body: "<p>Water is essential for nearly every bodily function, yet many of us don't drink enough. Learn how to calculate your ideal water intake, the surprising benefits of proper hydration (hello, glowing skin!), and easy ways to make drinking water a habit.</p>" },
                    "Beyond the Gym: Finding Joy in Movement": { image: "https://images.unsplash.com/photo-1517836357463-d25dfeac3438?q=80&w=2070&auto=format&fit=crop", category: "Fitness", subcategory: "Wellness", author: "Carolyne", body: "<p>Exercise doesn't have to be a chore. Discover fun and engaging ways to move your body that you'll actually look forward to, from dance classes and hiking to team sports and outdoor yoga.</p>" }
                },
                products: {
                    "Classic T-shirt": { price: 3200, image: "https://images.unsplash.com/photo-1583743814966-8936f5b7be1a?q=80&w=1887&auto=format&fit=crop", description: "<p>A timeless t-shirt made from a soft, breathable fabric. Its minimalist design makes it a versatile piece for any wardrobe.</p>" },
                    "Tote Bag": { price: 2600, image: "https://images.unsplash.com/photo-1544441893-675973e31985?q=80&w=2070&auto=format&fit=crop", description: "<p>Durable and stylish, our tote bag is your perfect companion for a day out. It's spacious enough to carry your essentials and more.</p>" },
                    "Branded Mug": { price: 1900, image: "https://images.unsplash.com/photo-1510972527921-ce157c70414b?q=80&w=1935&auto=format&fit=crop", description: "<p>Start your day with a cup of coffee or tea in our elegant branded mug. A simple yet powerful addition to your morning routine.</p>" },
                    "Lifestyle Journal": { price: 2850, image: "https://images.unsplash.com/photo-1533083168-b73898822558?q=80&w=1974&auto=format&fit=crop", description: "<p>Document your journey with our beautifully designed lifestyle journal. Its pages are an invitation to reflect, plan, and create.</p>" },
                    "Signature Cap": { price: 2300, image: "https://images.unsplash.com/photo-1521369909040-5549b3a01642?q=80&w=1974&auto=format&fit=crop", description: "<p>Complete your look with our signature cap. Made with quality materials and a classic design, it's a stylish accessory for any casual outing.</p>" },
                    "Gentle Gel Cleanser": { price: 3500, image: "https://images.unsplash.com/photo-1556228852-6d45a7ae2666?q=80&w=1887&auto=format&fit=crop", description: "<p>A pH-balanced gel cleanser that effectively removes impurities without stripping the skin's natural moisture barrier.</p>" },
                    "Hydrating Serum": { price: 4800, image: "https://images.unsplash.com/photo-1620916566398-35f1624a7e30?q=80&w=1887&auto=format&fit=crop", description: "<p>Packed with hyaluronic acid and vitamin B5, this serum delivers a powerful boost of hydration for plump, dewy skin.</p>" },
                    "Nourishing Face Oil": { price: 5200, image: "https://images.unsplash.com/photo-1608248579932-3aca12d8a3e7?q=80&w=1887&auto=format&fit=crop", description: "<p>A luxurious blend of botanical oils to nourish, soothe, and restore your skin's natural radiance. Perfect as the final step in your evening routine.</p>" },
                    "Vitamin C Serum": { price: 5500, image: "https://images.unsplash.com/photo-1600180730995-037a027310a2?q=80&w=1887&auto=format&fit=crop", description: "<p>Brighten, firm, and protect your skin with our potent Vitamin C serum. Helps to reduce the appearance of dark spots and promotes a radiant complexion.</p>" },
                    "Purifying Clay Mask": { price: 4200, image: "https://images.unsplash.com/photo-1620891738274-f252bcfd0c31?q=80&w=1887&auto=format&fit=crop", description: "<p>A detoxifying clay mask formulated to draw out impurities, refine pores, and leave your skin feeling smooth and refreshed.</p>" },
                    "Rosewater Facial Mist": { price: 2800, image: "https://images.unsplash.com/photo-1598453482223-1d3654f5451c?q=80&w=1887&auto=format&fit=crop", description: "<p>A refreshing and hydrating facial mist with pure rosewater to soothe and tone the skin. Use it to set makeup or for a quick pick-me-up throughout the day.</p>" },
                    "Restorative Night Cream": { price: 6200, image: "https://images.unsplash.com/photo-1620916666343-a74ddb9c058c?q=80&w=1887&auto=format&fit=crop", description: "<p>A rich, nourishing night cream that works while you sleep to repair, hydrate, and rejuvenate your skin for a visibly smoother, more youthful appearance by morning.</p>" },
                    "Scented Soy Candle": { price: 3400, image: "https://images.unsplash.com/photo-1614036132943-24754fd18e4e?q=80&w=1887&auto=format&fit=crop", description: "<p>Create a calming ambiance with our hand-poured soy wax candle, scented with natural essential oils. Perfect for moments of relaxation and mindfulness.</p>" },
                    "Linen Throw Blanket": { price: 7500, image: "https://images.unsplash.com/photo-1620625901193-e5f87b3b3a98?q=80&w=1887&auto=format&fit=crop", description: "<p>A beautifully soft and breathable linen throw blanket, perfect for adding a touch of cozy elegance to your living space or bedroom.</p>" },
                    "Ceramic Oil Diffuser": { price: 6800, image: "https://images.unsplash.com/photo-1627910303837-a1a7c452e698?q=80&w=1887&auto=format&fit=crop", description: "<p>Elevate your home's atmosphere with our minimalist ceramic essential oil diffuser. Its sculptural design doubles as a piece of art.</p>" },
                    "Minimalist Wall Art": { price: 4500, image: "https://images.unsplash.com/photo-1536237880829-dd44010468ec?q=80&w=1887&auto=format&fit=crop", description: "<p>A simple, elegant piece of line art to bring a sense of calm and sophistication to any room. Printed on high-quality archival paper.</p>" },
                    "Leather Notebook": { price: 3800, image: "https://images.unsplash.com/photo-1516414447565-b14be0adf13e?q=80&w=1887&auto=format&fit=crop", description: "<p>A high-quality leather-bound notebook for your thoughts, dreams, and plans. The perfect companion for a life of intention.</p>" },
                    "Yoga Mat": { price: 5500, image: "https://images.unsplash.com/photo-1599447379899-3b0484813936?q=80&w=1887&auto=format&fit=crop", description: "<p>A premium, non-slip yoga mat made from sustainable, eco-friendly materials. Designed to support your practice and your values.</p>" }
                },
                recipes: {
                    "Pilau": { prepTime: "20 mins", cookTime: "40 mins", servings: "4", calories: 650, tags: ['High protein'], image: "https://images.unsplash.com/photo-1589301760014-d929f39791e8?q=80&w=1887&auto=format&fit=crop", description: "A flavorful rice dish cooked with spices and meat.", ingredients: ["2 cups Basmati rice", "500g beef, cubed", "2 large onions", "4 cloves garlic", "1 tbsp Pilau Masala", "3 tbsp vegetable oil", "4 cups beef broth", "Salt to taste"], instructions: ["Caramelize sugar in oil, then sauté onions.", "Add beef, garlic, ginger, and all spices. Brown the meat.", "Pour in broth, season with salt, and simmer until meat is tender.", "Add rice, cover, and cook on low heat for 15-20 minutes until fluffy."] },
                    "Sukuma Wiki": { prepTime: "10 mins", cookTime: "10 mins", servings: "2", calories: 150, tags: [], image: "https://images.unsplash.com/photo-1586952518485-221f6c245236?q=80&w=1887&auto=format&fit=crop", description: "A popular Kenyan vegetable dish made from collard greens.", ingredients: ["1 large bunch of collard greens (Sukuma)", "1 large onion, chopped", "2 ripe tomatoes", "2 tbsp vegetable oil", "Salt to taste"], instructions: ["Heat oil and cook onions until soft.", "Add tomatoes and cook down.", "Add shredded sukuma and stir until just wilted (3-5 minutes).", "Season with salt and serve immediately."] },
                    "Kuku Choma": { prepTime: "15 mins", cookTime: "30 mins", servings: "4", calories: 550, tags: ['High protein'], image: "https://images.unsplash.com/photo-1598511654729-6b47816020a3?q=80&w=1964&auto=format&fit=crop", description: "Grilled chicken, often served with kachumbari and ugali.", ingredients: ["1 whole chicken, cut into pieces", "Juice of 2 lemons", "4 cloves garlic, minced", "1 inch ginger, grated", "1 tbsp salt", "1 tsp black pepper"], instructions: ["Mix all marinade ingredients in a bowl.", "Marinate the chicken for at least 1 hour.", "Grill over medium heat for 20-30 minutes, turning occasionally, until cooked through.", "Serve hot with kachumbari and ugali."] },
                    "Vitamin-Packed Carrot Juice": { prepTime: "5 mins", cookTime: "2 mins", servings: "1", calories: 120, tags: [], image: "https://images.unsplash.com/photo-1598824846423-43b9e4a3c10a?q=80&w=1964&auto=format&fit=crop", description: "A vibrant and refreshing juice to boost your immune system.", ingredients: ["5 large carrots", "2 oranges, peeled", "1-inch piece of ginger", "1/2 lemon, peeled"], instructions: ["Wash all produce thoroughly.", "Pass all ingredients through a juicer.", "Stir and serve immediately over ice for the best taste and nutritional value."] },
                    "Famous Layered Dip": { prepTime: "15 mins", cookTime: "0 mins", servings: "8", calories: 350, tags: [], image: "https://images.unsplash.com/photo-1625944026292-b43a9a15c8a4?q=80&w=1887&auto=format&fit=crop", description: "The ultimate crowd-pleasing dip, perfect for any gathering.", ingredients: ["1 can (16oz) refried beans", "1 cup guacamole", "1 cup sour cream", "1 cup salsa", "1 cup shredded cheddar cheese", "1/2 cup chopped tomatoes", "1/4 cup sliced black olives", "2 tbsp chopped green onions"], instructions: ["Spread refried beans on the bottom of a clear serving dish.", "Carefully layer guacamole, sour cream, and salsa on top.", "Sprinkle with cheese, tomatoes, olives, and green onions.", "Chill for at least 1 hour before serving with tortilla chips."] },
                    "Protein Smoothie Bowl": { prepTime: "10 mins", cookTime: "0 mins", servings: "1", calories: 450, tags: ['High protein'], image: "https://images.unsplash.com/photo-1505252585461-1b632da5468a?q=80&w=1887&auto=format&fit=crop", description: "A delicious and energizing smoothie bowl, perfect for a post-workout breakfast.", ingredients: ["1 frozen banana", "1/2 cup frozen berries", "1 scoop vanilla protein powder", "1/2 cup almond milk", "Toppings: granola, fresh fruit, chia seeds"], instructions: ["Combine frozen banana, berries, protein powder, and almond milk in a blender.", "Blend until smooth and creamy.", "Pour into a bowl and add your favorite toppings.", "Enjoy immediately!"] },
                    "Post-Workout Chicken Salad": { prepTime: "15 mins", cookTime: "0 mins", servings: "2", calories: 400, tags: ['High protein'], image: "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38?q=80&w=1981&auto=format&fit=crop", description: "A light yet satisfying salad packed with protein to refuel your muscles.", ingredients: ["2 cups cooked shredded chicken", "1/4 cup Greek yogurt", "1 tbsp lemon juice", "1/4 cup chopped celery", "1/4 cup halved grapes", "Salt and pepper to taste", "Lettuce wraps or whole-wheat bread"], instructions: ["In a medium bowl, combine shredded chicken, Greek yogurt, and lemon juice.", "Stir in celery and grapes.", "Season with salt and pepper to taste.", "Serve in lettuce wraps or on whole-wheat bread for a delicious and healthy meal."] },
                    "Kourt's Famous Zoodles Recipe": { prepTime: "15 mins", cookTime: "10 mins", servings: "2", calories: 350, tags: [], image: "https://images.unsplash.com/photo-1560035219-14f72aa2333b?q=80&w=1887&auto=format&fit=crop", description: "A light, healthy, and surprisingly delicious zucchini noodle dish that's a celebrity favorite.", ingredients: ["2 medium zucchinis, spiralized", "1/4 cup crispy bacon bits", "1 cup baby spinach", "1/4 cup shredded carrots", "2 tbsp olive oil", "Salt and pepper to taste"], instructions: ["Heat olive oil in a pan over medium heat.", "Add spinach and carrots, sautéing until spinach is wilted.", "Add the zoodles and cook for 2-3 minutes until just tender.", "Toss with bacon bits, season with salt and pepper, and serve immediately."] },
                    "A Debloating Salad to ADD TO YOUR ROTATION": { prepTime: "15 mins", cookTime: "10 mins", servings: "2", calories: 320, tags: [], image: "https://images.unsplash.com/photo-1540420773420-3366772f4999?q=80&w=1887&auto=format&fit=crop", description: "This delicious salad is packed with ingredients that help reduce bloating and support digestion.", ingredients: ["2 cups arugula", "1 cup roasted sweet potatoes, cubed", "1/2 cup cooked quinoa", "1/4 cup toasted walnuts", "Dressing: 2 tbsp olive oil, 1 tbsp lemon juice, 1 tsp maple syrup"], instructions: ["Roast sweet potato cubes at 400°F (200°C) for 10 minutes or until tender.", "In a large bowl, combine arugula, quinoa, and roasted sweet potatoes.", "Whisk together dressing ingredients and pour over the salad.", "Top with toasted walnuts and serve."] }
                }
            };

            // --- DOM ELEMENTS ---
            const cartCounter = document.getElementById('cart-counter');
            const mobileMenu = document.getElementById('mobile-menu');
            const searchOverlay = document.getElementById('search-overlay');
            const searchInput = document.getElementById('search-input');
            const searchResultsContainer = document.getElementById('search-results');
            const salePopupOverlay = document.getElementById('sale-popup-overlay');
            const closeSalePopupBtn = document.getElementById('close-sale-popup-btn');

            // --- HELPER FUNCTIONS ---
            const updateCartCount = () => { cartCounter.textContent = cart.reduce((acc, item) => acc + item.quantity, 0); cartCounter.classList.toggle('hidden', cart.length === 0); };
            
            const getPillarPageIdFromArticleTitle = (title) => {
                const article = content.articles[title];
                if (!article) return 'home-page';
                switch(article.category) {
                    case 'Epicure & Entertaining': return 'epicure-page';
                    case 'Modern Motherhood': return 'motherhood-page';
                    case 'Style & Beauty': return 'style-beauty-page';
                    case 'Culture & Escapes': return 'culture-escapes-page';
                    case 'Power & Purpose': return 'power-purpose-page';
                    default: return 'home-page';
                }
            };

            const addToCart = (productData) => {
                 const existingItem = cart.find(item => item.title === productData.title);
                 if(existingItem) {
                    existingItem.quantity++;
                 } else {
                    const cartItem = {
                        title: productData.title,
                        price: productData.price,
                        image: productData.image,
                        id: Date.now(),
                        quantity: 1
                    };
                    cart.push(cartItem);
                 }
                updateCartCount();
                showPage('cart-page');
            };
            
            const createRecipeTextForDownload = (recipeTitle) => {
                const recipe = content.recipes[recipeTitle];
                if (!recipe) return "";

                let text = ``;
                text += `${recipeTitle.toUpperCase()}\n`;
                text += `================================\n\n`;
                text += `${recipe.description}\n\n`;
                text += `Prep Time: ${recipe.prepTime}\n`;
                text += `Cook Time: ${recipe.cookTime}\n`;
                text += `Servings: ${recipe.servings}\n\n`;
                text += `INGREDIENTS\n`;
                text += `--------------------------------\n`;
                recipe.ingredients.forEach(i => text += `- ${i}\n`);
                text += `\nINSTRUCTIONS\n`;
                text += `--------------------------------\n`;
                recipe.instructions.forEach((step, index) => text += `${index + 1}. ${step}\n`);
                
                return encodeURIComponent(text);
            };
            
            const renderGridColumn = (title, articleTitles) => {
                return `
                    <div>
                        <h3 class="text-lg font-semibold uppercase tracking-wider border-b-2 border-brand-base pb-2 mb-4">${title}</h3>
                        <div class="space-y-6">
                            ${articleTitles.map(articleTitle => {
                                const article = content.articles[articleTitle];
                                if (!article) return '';
                                return `
                                <a href="#" class="page-link group block" data-target="article-page" data-title="${articleTitle}">
                                    <div class="overflow-hidden rounded-lg mb-3">
                                        <img src="${article.image}" alt="${articleTitle}" class="w-full h-40 object-cover group-hover:scale-105 transition-transform duration-300">
                                    </div>
                                    <h4 class="font-serif text-brand-base group-hover:text-brand-accent">${articleTitle.split('–')[0]}</h4>
                                    <span class="text-xs text-brand-accent font-semibold mt-1">Read More &rarr;</span>
                                </a>
                                `;
                            }).join('')}
                        </div>
                    </div>
                `;
            };

            const renderGridSection = (title, articles, pageTarget) => {
                // Modified: Removed specific grid class logic, now defaults to 3 columns on large screens
                // and 2 on small, which matches the other sections.
                return `
                <section class="py-20 bg-brand-bg px-6 animate-on-scroll">
                    <div class="container mx-auto">
                        <div class="text-center mb-12">
                            <h2 class="text-lg font-sans font-medium tracking-[0.2em] uppercase text-brand-base">${title}</h2>
                        </div>
                        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
                            ${articles.map(articleData => `
                                <a href="#" class="page-link group" data-target="article-page" data-title="${articleData.title}">
                                    <div class="overflow-hidden rounded-md"><img src="${articleData.image}" class="w-full h-96 object-cover group-hover:opacity-80 transition-opacity duration-300"></div>
                                    <div class="pt-4 text-center">
                                        <p class="text-xs uppercase tracking-widest text-brand-gray">${articleData.category}</p>
                                        <h3 class="text-base font-medium text-brand-base mt-1 group-hover:text-brand-accent">${articleData.shortTitle || articleData.title.split('–')[0]}</h3>
                                    </div>
                                </a>
                            `).join('')}
                        </div>
                    </div>
                </section>
                `;
            };

            // --- PAGE RENDERERS ---
            const renderHomePage = () => {
                const heroSlides = [
                    { type: 'video', src: 'https://videos.pexels.com/video-files/3254002/3254002-hd_1920_1080_30fps.mp4', title: 'Live Beautifully.', subtitle: 'Live Intentionally.' },
                    { type: 'image', src: 'https://images.unsplash.com/photo-1506126613408-4e05860f5c54?q=80&w=2070&auto=format&fit=crop', title: 'Nourish Your Soul.', subtitle: 'Find Your Balance.' },
                    { type: 'video', src: 'https://videos.pexels.com/video-files/4434249/4434249-hd_1920_1080_25fps.mp4', title: 'Embrace Your Strength.', subtitle: 'Move with Purpose.' },
                    { type: 'image', src: 'https://images.unsplash.com/photo-1498837167922-ddd27525d352?q=80&w=2070&auto=format&fit=crop', title: 'Savor The Moment.', subtitle: 'Create & Connect.' },
                    { type: 'image', src: 'https://images.unsplash.com/photo-1512436991641-6745cdb1723f?q=80&w=2070&auto=format&fit=crop', title: 'Define Your Style.', subtitle: 'Curate with Confidence.' }
                ];
                
                const trendingArticles = Object.entries(content.articles).slice(0, 6).map(([title, article]) => ({ ...article, title }));
                
                const pillars = [
                    { name: 'Epicure & Entertaining', target: 'epicure-page', image: 'https://images.unsplash.com/photo-1556911220-bff31c812dba?q=80&w=1935&auto=format&fit=crop'},
                    { name: 'Modern Motherhood', target: 'motherhood-page', image: 'https://images.unsplash.com/photo-1515488042361-ee00e0ddd4e4?q=80&w=1887&auto=format&fit=crop'},
                    { name: 'Style & Beauty', target: 'style-beauty-page', image: 'https://images.unsplash.com/photo-1483985988355-763728e1935b?q=80&w=2070&auto=format&fit=crop'},
                    { name: 'Culture & Escapes', target: 'culture-escapes-page', image: 'https://images.unsplash.com/photo-1530789253388-582c481c54b0?q=80&w=2070&auto=format&fit=crop'},
                    { name: 'Power & Purpose', target: 'power-purpose-page', image: 'https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?q=80&w=2070&auto=format&fit=crop'},
                ];
                
                const featuredProductTitles = ["Vitamin C Serum", "Purifying Clay Mask", "Rosewater Facial Mist", "Restorative Night Cream", "Scented Soy Candle", "Linen Throw Blanket"];
                const relationshipArticles = Object.entries(content.articles).filter(([_, a]) => a.category === 'Relationships').slice(0,6).map(([title, article]) => ({ ...article, title, shortTitle: title }));
                const fitnessArticles = Object.entries(content.articles).filter(([_, a]) => a.category === 'Fitness' || a.category === 'Health').slice(0,6).map(([title, article]) => ({ ...article, title, shortTitle: title }));
                
                const galleryImages = {
                    travels: [
                        "https://images.unsplash.com/photo-1501785888041-af3ef285b470", "https://images.unsplash.com/photo-1476514525535-07fb3b4ae5f1", "https://images.unsplash.com/photo-1488646953014-85cb44e25828", "https://images.unsplash.com/photo-1503220317375-aaad61436b1b",
                        "https://images.unsplash.com/photo-1530789253388-582c481c54b0", "https://images.unsplash.com/photo-1500835556837-99ac94a94552", "https://images.unsplash.com/photo-1469854523086-cc02fe5d8800", "https://images.unsplash.com/photo-1527631746610-bca00a040d60",
                        "https://images.unsplash.com/photo-1528543606781-2f6e6857f318", "https://images.unsplash.com/photo-1506197603052-3cc9c3a201bd", "https://images.unsplash.com/photo-1507525428034-b723a9ce6890", "https://images.unsplash.com/photo-1517760444937-f6397edcbbcd",
                        "https://images.unsplash.com/photo-1498307833015-e7b400441eb8", "https://images.unsplash.com/photo-1542051841857-5f90071e7989", "https://images.unsplash.com/photo-1505832018843-57151d383818", "https://images.unsplash.com/photo-1502602898657-3e91760c0341",
                        "https://images.unsplash.com/photo-1483729558449-99ef09a8c325", "https://images.unsplash.com/photo-1534430480872-3498386e7856", "https://images.unsplash.com/photo-1506744038136-46273834b3fb", "https://images.unsplash.com/photo-1539635278303-d4002c07eae3",
                        "https://images.unsplash.com/photo-1473625247510-8ceb1760943f", "https://images.unsplash.com/photo-1519922639102-1a221a7c881a", "https://images.unsplash.com/photo-1504275107627-0c2ba7a43dba", "https://images.unsplash.com/photo-1532976331682-a8eb5ade9f1d"
                    ],
                    tours: [
                        "https://images.unsplash.com/photo-1535358593892-127921447833", "https://images.unsplash.com/photo-1581489189913-0941855a153d", "https://images.unsplash.com/photo-1615638519442-42e77b6a1d4a", "https://images.unsplash.com/photo-1599557049-92f7062a4a2b",
                        "https://images.unsplash.com/photo-1525078964292-62886105a884", "https://images.unsplash.com/photo-1534710134446-b8a7b3b4d1b7", "https://images.unsplash.com/photo-1547471080-7cc2d_5d88e93", "https://images.unsplash.com/photo-1516426122078-c23e763199c0",
                        "https://images.unsplash.com/photo-1534341821434-1a35f2df1818", "https://images.unsplash.com/photo-1574717467657-618731b0587a", "https://images.unsplash.com/photo-1524314184646-60787e14889c", "https://images.unsplash.com/photo-1602416974033-285f25a952f4",
                        "https://images.unsplash.com/photo-1565538749452-f63451515283", "https://images.unsplash.com/photo-1566473952134-928d54ad010d", "https://images.unsplash.com/photo-1569488859353-93d3a7d51784", "https://images.unsplash.com/photo-1526485856403-910543685649",
                        "https://images.unsplash.com/photo-1594892417743-5778a8779133", "https://images.unsplash.com/photo-1563653123491-913a89a1a09d", "https://images.unsplash.com/photo-1569398322234-8c876f2f2187", "https://images.unsplash.com/photo-1550978939-5e9215003504",
                        "https://images.unsplash.com/photo-1549643462-8f1952a5e456", "https://images.unsplash.com/photo-1528702748617-c67d29f9c3fd", "https://images.unsplash.com/photo-1518544465-7562f854f738", "https://images.unsplash.com/photo-1564522237810-d54b8a562b26"
                    ],
                    "mom-diaries": [
                        "https://images.unsplash.com/photo-1515488042361-ee00e0ddd4e4", "https://images.unsplash.com/photo-1593108422119-a1b66511a8a2", "https://images.unsplash.com/photo-1527529482837-4698179dc6ce", "https://images.unsplash.com/photo-1484665754824-2d0963191873",
                        "https://images.unsplash.com/photo-1478479405421-ce83c92fb3ba", "https://images.unsplash.com/photo-1482235225574-c37692835cf3", "https://images.unsplash.com/photo-1507983936109-3a19e18b08c0", "https://images.unsplash.com/photo-1546015220-45d2d8959ed7",
                        "https://images.unsplash.com/photo-1616728079860-88abbf1a5f4d", "https://images.unsplash.com/photo-1485182708500-e8f1f3182e2e", "https://images.unsplash.com/photo-1508215886492-c889a721387d", "https://images.unsplash.com/photo-1595152772105-a7e692a8323a",
                        "https://images.unsplash.com/photo-1545239351-ef35f43d514b", "https://images.unsplash.com/photo-1566004100631-35d015d6a491", "https://images.unsplash.com/photo-1527814223023-e696352d3a33", "https://images.unsplash.com/photo-1530012270924-5b363afd11e4",
                        "https://images.unsplash.com/photo-1488114312323-5a0d3b6649f3", "https://images.unsplash.com/photo-1491841550275-5b462bf92929", "https://images.unsplash.com/photo-1519641471654-76ce0107ad1b", "https://images.unsplash.com/photo-1531185343486-973658455325",
                        "https://images.unsplash.com/photo-1484980972926-edee96e0960d", "https://images.unsplash.com/photo-1476492981352-f15562a045a2", "https://images.unsplash.com/photo-1506045353593-01004a187a53", "https://images.unsplash.com/photo-1560380894-26105f23512c"
                    ],
                    food: [
                        "https://images.unsplash.com/photo-1555939594-58d7cb561ad1", "https://images.unsplash.com/photo-1490645935967-10de6ba17025", "https://images.unsplash.com/photo-1607532941433-304659e8198a", "https://images.unsplash.com/photo-1540189549336-e6e99c3679fe",
                        "https://images.unsplash.com/photo-1484723050470-8bf10b643034", "https://images.unsplash.com/photo-1482049016688-2d3e1b311543", "https://images.unsplash.com/photo-1504674900247-0877df9cc836", "https://images.unsplash.com/photo-1498837167922-ddd27525d352",
                        "https://images.unsplash.com/photo-1565299624946-b28f40a0ae38", "https://images.unsplash.com/photo-1473093226795-af9932fe5856", "https://images.unsplash.com/photo-1512621776951-a57141f2eefd", "https://images.unsplash.com/photo-1467003909585-2f8a72700288",
                        "https://images.unsplash.com/photo-1478145046317-39f10e56b5e9", "https://images.unsplash.com/photo-1496116218417-1a764741a332", "https://images.unsplash.com/photo-1490818387583-1baba5e638af", "https://images.unsplash.com/photo-1505253716362-afb50c68a127",
                        "https://images.unsplash.com/photo-1588195538326-c5b1e9f80a1b", "https://images.unsplash.com/photo-1543339308-43e59d6b70a6", "https://images.unsplash.com/photo-1455619452474-d2be8b1e70cd", "https://images.unsplash.com/photo-1529990135899-764952093557",
                        "https://images.unsplash.com/photo-1484984532626-14342a34b4b2", "https://images.unsplash.com/photo-1564834744158-a0b7381275d7", "https://images.unsplash.com/photo-1506354666786-959d6d497f1a", "https://images.unsplash.com/photo-1470337458703-46ad1756a187"
                    ],
                    lifestyle: [
                        "https://images.unsplash.com/photo-1541533267759-d8f48866174c", "https://images.unsplash.com/photo-1441986300917-64674bd600d8", "https://images.unsplash.com/photo-1555212697-194d092e3b8f", "https://images.unsplash.com/photo-1524758631624-e2822e304c36",
                        "https://images.unsplash.com/photo-1493663284031-b7e3aefcae8e", "https://images.unsplash.com/photo-1502672260266-1c1ef2d93688", "https://images.unsplash.com/photo-1505691938895-1758d7feb511", "https://images.unsplash.com/photo-1512212675885-3996924b22c3",
                        "https://images.unsplash.com/photo-1522771739844-6a9f6d5f14af", "https://images.unsplash.com/photo-1501876725168-00c445821c9e", "https://images.unsplash.com/photo-1484154218962-a197022b5858", "https://images.unsplash.com/photo-1505693416388-ac5ce0687954",
                        "https://images.unsplash.com/photo-1460518451285-97b6aa326961", "https://images.unsplash.com/photo-1516131206008-dd041a97645a", "https://images.unsplash.com/photo-1530018607932-a2538b2dfa43", "https://images.unsplash.com/photo-1519710164239-da123dc03ef4",
                        "https://images.unsplash.com/photo-1523475256011-38ae2b5a4bf4", "https://images.unsplash.com/photo-1503174971373-b1f69850bded", "https://images.unsplash.com/photo-1512918728675-ed5a71a580bd", "https://images.unsplash.com/photo-1497366811353-6870744d04b2",
                        "https://images.unsplash.com/photo-1497032628192-86f99d791b7e", "https://images.unsplash.com/photo-1521783964894-38c64a382170", "https://images.unsplash.com/photo-1504275107627-0c2ba7a43dba", "https://images.unsplash.com/photo-1511974278737-68b868945836"
                    ]
                };

                const renderGalleryGrid = (images) => {
                    return `
                        <div class="columns-2 md:columns-3 lg:columns-4 gap-4 space-y-4">
                           ${images.map(src => `
                                <a href="${src}?q=80&w=2070&auto=format&fit=crop" download class="relative group block rounded-lg overflow-hidden break-inside-avoid">
                                    <img class="h-auto w-full" src="${src}?q=80&w=800&auto=format&fit=crop" alt="Gallery image">
                                    <div class="absolute inset-0 bg-black/20 opacity-0 group-hover:opacity-100 flex items-center justify-center transition-opacity">
                                        <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path></svg>
                                    </div>
                                </a>
                           `).join('')}
                        </div>
                    `;
                };

                return `
                <section class="relative h-[70vh] md:h-[90vh] text-white overflow-hidden" x-data="{ activeSlide: 0 }" x-init="setInterval(() => { activeSlide = (activeSlide + 1) % ${heroSlides.length} }, 5000)">
                    ${heroSlides.map((slide, index) => `
                        <div class="hero-slide" :class="{ 'active': activeSlide === ${index} }">
                            ${slide.type === 'video' ? 
                                `<video autoplay loop muted playsinline class="hero-media"><source src="${slide.src}" type="video/mp4"></video>` : 
                                `<img src="${slide.src}" class="hero-media">`
                            }
                            <div class="absolute inset-0 bg-black/50 z-10"></div>
                            <div class="relative z-20 h-full flex items-center justify-center text-center">
                                <div class="hero-content p-6">
                                    <h1 class="text-4xl md:text-6xl font-serif leading-tight">${slide.title}</h1>
                                    <p class="text-lg md:text-2xl mt-4 font-light">${slide.subtitle}</p>
                                    <a href="#" data-target="explore-stories-page" class="page-link mt-8 inline-block bg-white text-brand-base py-3 px-10 text-sm font-semibold cta-button uppercase tracking-wider">Explore Stories</a>
                                </div>
                            </div>
                        </div>
                    `).join('')}
                </section>

                <section class="bg-brand-bg py-8 animate-on-scroll">
                    <div class="container mx-auto px-6">
                        <div class="flex justify-center md:justify-around items-center gap-x-8 md:gap-x-12 gap-y-6 flex-wrap">
                            <span class="w-full text-center font-serif text-brand-gray text-sm md:w-auto mb-2 md:mb-0">As Seen In</span>
                            <img src="https://logotyp.us/files/vogue.svg" alt="Vogue logo" class="h-6 md:h-7 filter grayscale opacity-60 hover:opacity-100 transition-opacity" title="Vogue">
                            <img src="https://logotyp.us/files/elle.svg" alt="Elle logo" class="h-5 md:h-6 filter grayscale opacity-60 hover:opacity-100 transition-opacity" title="Elle">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Harper%27s_Bazaar_logo.svg/1200px-Harper%27s_Bazaar_logo.svg.png" alt="Harper's Bazaar logo" class="h-5 md:h-6 filter grayscale opacity-60 hover:opacity-100 transition-opacity" title="Harper's Bazaar">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1e/GQ_logo.svg/1280px-GQ_logo.svg.png" alt="GQ logo" class="h-6 md:h-7 filter grayscale opacity-60 hover:opacity-100 transition-opacity" title="GQ">
                            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Tatler_logo.svg/1280px-Tatler_logo.svg.png" alt="Tatler logo" class="h-6 md:h-7 filter grayscale opacity-60 hover:opacity-100 transition-opacity" title="Tatler">
                        </div>
                    </div>
                </section>
                
                <section id="pillars" class="pt-20 pb-10 bg-brand-bg px-6 animate-on-scroll">
                    <div class="text-center mb-12">
                        <h2 class="text-3xl font-serif text-brand-base">Browse by Pillar</h2>
                        <p class="text-brand-gray mt-2">Explore content designed for every facet of your life.</p>
                    </div>
                    <div class="grid grid-cols-2 md:grid-cols-3 gap-4 md:gap-8 max-w-6xl mx-auto">
                        ${pillars.map(pillar => `
                            <a href="#" class="page-link group relative overflow-hidden rounded-lg block" data-target="${pillar.target}">
                                <img src="${pillar.image}" class="w-full h-48 md:h-80 object-cover group-hover:scale-105 transition-transform duration-300">
                                <div class="absolute inset-0 bg-black/40"></div>
                                <div class="absolute inset-0 flex items-center justify-center">
                                    <h3 class="text-white text-xl font-serif text-center">${pillar.name}</h3>
                                </div>
                            </a>`
                        ).join('')}
                    </div>
                </section>
                
                 <section class="relative bg-brand-base text-white py-20 px-6 animate-on-scroll">
                     <div class="absolute inset-0 opacity-10">
                        <img src="https://images.unsplash.com/photo-1505691938895-1758d7feb511?q=80&w=2070&auto=format&fit=crop" class="w-full h-full object-cover">
                     </div>
                    <div class="relative container mx-auto text-center max-w-2xl">
                        <h2 class="text-3xl font-serif">Our Philosophy</h2>
                        <p class="mt-4 text-gray-300">At Memuci, we believe in the power of intention. We are dedicated to curating content and products that inspire a slower, more beautiful, and more conscious way of life. Our pillars are built on authenticity, quality, and a deep appreciation for the everyday moments that make life truly rich.</p>
                        <a href="#" data-target="about-page" class="page-link mt-8 inline-block bg-white text-brand-base py-3 px-10 text-sm font-semibold cta-button uppercase tracking-wider">Learn More About Us</a>
                    </div>
                </section>

                <section class="py-20 bg-white animate-on-scroll">
                    <div class="container mx-auto px-6 text-center" x-data="{ activeSlide: 0 }" x-init="setInterval(() => { activeSlide = (activeSlide + 1) % ${trendingArticles.length} }, 5000)">
                        <h2 class="text-2xl font-serif tracking-widest uppercase text-gray-500"><a href="#" data-target="explore-stories-page" class="page-link hover:text-brand-base transition-colors">Trending Now</a></h2>
                        <div class="mt-12 relative h-[500px] overflow-hidden rounded-lg">
                             ${trendingArticles.map((article, index) => `
                                <div class="trending-slide absolute inset-0 w-full h-full" :class="{'opacity-100': activeSlide === ${index}, 'opacity-0': activeSlide !== ${index}}">
                                    <img src="${article.image}" alt="${article.title}" class="w-full h-full object-cover">
                                    <div class="absolute inset-0 bg-black/40"></div>
                                    <div class="absolute bottom-0 left-0 p-8 text-white text-left">
                                        <p class="text-sm font-semibold uppercase tracking-widest">${article.category}</p>
                                        <h3 class="text-3xl font-serif mt-2">${article.title.split('–')[0]}</h3>
                                        <a href="#" class="page-link mt-4 inline-block font-semibold border-b-2 border-white pb-1" data-target="explore-stories-page">Read More</a>
                                    </div>
                                </div>
                            `).join('')}
                            <button @click="activeSlide = (activeSlide - 1 + ${trendingArticles.length}) % ${trendingArticles.length}" class="absolute left-4 top-1/2 -translate-y-1/2 bg-white/50 hover:bg-white text-brand-base rounded-full p-2 transition-colors focus:outline-none">
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path></svg>
                            </button>
                             <button @click="activeSlide = (activeSlide + 1) % ${trendingArticles.length}" class="absolute right-4 top-1/2 -translate-y-1/2 bg-white/50 hover:bg-white text-brand-base rounded-full p-2 transition-colors focus:outline-none">
                                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path></svg>
                            </button>
                        </div>
                        <div id="slider-dots" class="flex justify-center gap-2 mt-4">
                            ${trendingArticles.map((_, index) => `
                                <button class="slider-dot w-2.5 h-2.5 rounded-full bg-gray-300" :class="{ 'active': activeSlide === ${index} }" @click="activeSlide = ${index}"></button>
                            `).join('')}
                        </div>
                         <div class="mt-8">
                             <a href="#" data-target="explore-stories-page" class="page-link inline-block font-semibold text-brand-base border-b-2 border-brand-base pb-1">View All Stories</a>
                        </div>
                    </div>
                </section>
                
                ${renderArticleScrollerSection('The Latest in Style', 
                    Object.entries(content.articles).filter(([_,a]) => a.category === 'Style & Beauty').slice(0,6).map(([title, article]) => ({ ...article, title })), 'style-beauty-page')}

                ${renderGridSection('Love & Relationships', relationshipArticles, 'relationships-page')}
                
                <section class="py-20 bg-brand-bg px-6 animate-on-scroll">
                    <div class="container mx-auto">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-8 md:gap-12 items-center">
                            <div class="md:order-2">
                                 <a href="#" class="page-link group block" data-target="article-page" data-title="${fitnessArticles[0].title}">
                                    <div class="overflow-hidden rounded-lg">
                                        <img src="${fitnessArticles[0].image}" alt="${fitnessArticles[0].title}" class="w-full h-96 object-cover group-hover:scale-105 transition-transform duration-300">
                                    </div>
                                 </a>
                            </div>
                            <div class="text-center md:text-left md:order-1">
                                <h2 class="text-3xl lg:text-4xl font-serif text-brand-base">Health & Fitness</h2>
                                <p class="mt-4 text-brand-gray max-w-md mx-auto md:mx-0">Nourish your body, strengthen your mind. Explore workouts, wellness tips, and health advice for a balanced life.</p>
                                <a href="#" data-target="fitness-page" class="page-link mt-8 inline-block bg-brand-base text-white py-3 px-10 text-sm font-semibold cta-button uppercase tracking-wider">View All</a>
                            </div>
                        </div>
                    </div>
                </section>

                <section class="py-12 md:py-20 relative animate-on-scroll">
                    <div class="text-center mb-12 px-6">
                        <h2 class="text-brand-gray uppercase tracking-widest text-sm">Kenyan Corner</h2>
                        <h3 class="text-3xl font-serif text-brand-base mt-2">A Taste of Home</h3>
                    </div>
                    <div class="max-w-6xl mx-auto px-6">
                        <div id="recipe-scroller-content" class="hide-scrollbar flex overflow-x-auto snap-x snap-mandatory scroll-smooth gap-8">
                            ${Object.entries(content.recipes).map(([title, recipe]) => `
                                <a href="#" class="page-link group flex-shrink-0 w-80 snap-center" data-target="recipe-page" data-title="${title}">
                                    <div class="overflow-hidden rounded-md"><img src="${recipe.image}" class="w-full h-80 object-cover group-hover:opacity-80 transition-opacity duration-300"></div>
                                    <div class="pt-4 text-center">
                                        <p class="text-xs uppercase tracking-widest text-brand-gray">Recipes</p>
                                        <h3 class="text-base font-sans font-medium uppercase tracking-wider text-brand-base mt-2 group-hover:text-brand-accent">${title}</h3>
                                    </div>
                                </a>
                            `).join('')}
                        </div>
                    </div>
                </section>
                
                <section id="mega-sale-banner" class="bg-[#d9e5dc] animate-on-scroll">
                    <div class="container mx-auto grid grid-cols-1 md:grid-cols-2 items-center">
                        <div class="text-center md:text-left p-8 lg:p-16">
                            <h2 class="text-5xl md:text-7xl font-serif font-light text-brand-base leading-none">50% OFF!</h2>
                            <p class="text-xl uppercase tracking-wider text-brand-base mt-2">Leather Bags Mega Sale</p>
                            <a href="#" data-target="shop-page" class="page-link mt-8 inline-flex items-center gap-2 bg-white text-brand-base py-3 px-6 text-sm font-semibold cta-button rounded-md border border-gray-300 hover:bg-brand-base hover:text-white hover:border-brand-base transition-colors">
                                <span>Shop Now</span>
                                <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3" /></svg>
                            </a>
                        </div>
                        <div class="h-80 md:h-[28rem]">
                            <img src="https://images.unsplash.com/photo-1584917865442-de89df76afd3?q=80&w=1887&auto=format&fit=crop" class="w-full h-full object-cover">
                        </div>
                    </div>
                </section>

                <section class="py-20 bg-brand-bg px-6 animate-on-scroll">
                    <div class="container mx-auto max-w-3xl text-center">
                        <h2 class="text-3xl font-serif text-brand-base">From Our Community</h2>
                        <div x-data="{ activeTestimonial: 0 }" x-init="setInterval(() => { activeTestimonial = (activeTestimonial + 1) % 3 }, 6000)" class="relative mt-8 h-48">
                            <div x-show="activeTestimonial === 0" x-transition:enter="transition ease-out duration-1000" x-transition:enter-start="opacity-0" x-transition:enter-end="opacity-100" x-transition:leave="transition ease-in duration-1000" x-transition:leave-start="opacity-100" x-transition:leave-end="opacity-0" class="absolute inset-0">
                                <p class="text-xl font-serif text-brand-gray">"Memuci has completely changed how I approach my daily routines. The content is so inspiring and the products are simply beautiful. It's more than a brand, it's a feeling."</p>
                                <p class="mt-4 font-semibold text-brand-base uppercase tracking-wider text-sm">- Jessica W.</p>
                            </div>
                            <div x-show="activeTestimonial === 1" x-cloak x-transition:enter="transition ease-out duration-1000" x-transition:enter-start="opacity-0" x-transition:enter-end="opacity-100" x-transition:leave="transition ease-in duration-1000" x-transition:leave-start="opacity-100" x-transition:leave-end="opacity-0" class="absolute inset-0">
                                <p class="text-xl font-serif text-brand-gray">"I look forward to the articles every week. They're a calming presence in my busy life. The focus on intentional living has genuinely made a positive impact."</p>
                                <p class="mt-4 font-semibold text-brand-base uppercase tracking-wider text-sm">- Aisha K.</p>
                            </div>
                            <div x-show="activeTestimonial === 2" x-cloak x-transition:enter="transition ease-out duration-1000" x-transition:enter-start="opacity-0" x-transition:enter-end="opacity-100" x-transition:leave="transition ease-in duration-1000" x-transition:leave-start="opacity-100" x-transition:leave-end="opacity-0" class="absolute inset-0">
                                <p class="text-xl font-serif text-brand-gray">"The skincare products are divine. My skin has never felt better, and I love knowing they are curated with such care and intention. Highly recommend the Vitamin C Serum!"</p>
                                <p class="mt-4 font-semibold text-brand-base uppercase tracking-wider text-sm">- Maria O.</p>
                            </div>
                        </div>
                    </div>
                </section>
                 
                <section class="relative bg-brand-base text-white py-20 px-6 animate-on-scroll">
                     <div class="absolute inset-0 opacity-10">
                        <img src="https://images.unsplash.com/photo-1556761175-b413da4baf72?q=80&w=1974&auto=format&fit=crop" class="w-full h-full object-cover">
                     </div>
                    <div class="relative container mx-auto text-center max-w-2xl">
                        <h2 class="text-3xl font-serif">Want More Help to Grow Your Business?</h2>
                        <p class="mt-4 text-gray-300">Id torquent dignissim parturient sagittis nisl venenatis nascetur eu dolor imperdiet. Sit nam accumsan interdum habitasse dui lacinia. Torquent curabitur laoreet duis himenaeos id nostra sollicitudin vehicula est pellentesque.</p>
                        <a href="#" data-target="contact-page" class="page-link mt-8 inline-block bg-white text-brand-base py-3 px-10 text-sm font-semibold cta-button uppercase tracking-wider">Contact Us</a>
                    </div>
                </section>

                <section class="py-20 bg-white px-6 animate-on-scroll">
                    <div class="container mx-auto" x-data="{ activeTab: 'travels' }">
                        <div class="text-center mb-12">
                            <h2 class="text-3xl font-serif text-brand-base">Gallery</h2>
                            <p class="text-brand-gray mt-2">A glimpse into the Memuci lifestyle.</p>
                            <div class="mt-6 flex justify-center border border-brand-border rounded-full p-1 max-w-lg mx-auto">
                                <button @click="activeTab = 'travels'" :class="{'active': activeTab === 'travels'}" class="gallery-tab w-1/5 py-2 px-4 rounded-full text-sm font-semibold transition-colors">Travels</button>
                                <button @click="activeTab = 'tours'" :class="{'active': activeTab === 'tours'}" class="gallery-tab w-1/5 py-2 px-4 rounded-full text-sm font-semibold transition-colors">Tours</button>
                                <button @click="activeTab = 'mom-diaries'" :class="{'active': activeTab === 'mom-diaries'}" class="gallery-tab w-1/5 py-2 px-4 rounded-full text-sm font-semibold transition-colors">Mom Diaries</button>
                                <button @click="activeTab = 'food'" :class="{'active': activeTab === 'food'}" class="gallery-tab w-1/5 py-2 px-4 rounded-full text-sm font-semibold transition-colors">Food</button>
                                <button @click="activeTab = 'lifestyle'" :class="{'active': activeTab === 'lifestyle'}" class="gallery-tab w-1/5 py-2 px-4 rounded-full text-sm font-semibold transition-colors">Lifestyle</button>
                            </div>
                        </div>
                        
                        <div x-show="activeTab === 'travels'" x-transition>
                           ${renderGalleryGrid(galleryImages.travels)}
                        </div>
                        <div x-show="activeTab === 'tours'" x-cloak x-transition>
                           ${renderGalleryGrid(galleryImages.tours)}
                        </div>
                         <div x-show="activeTab === 'mom-diaries'" x-cloak x-transition>
                           ${renderGalleryGrid(galleryImages['mom-diaries'])}
                        </div>
                        <div x-show="activeTab === 'food'" x-cloak x-transition>
                            ${renderGalleryGrid(galleryImages.food)}
                        </div>
                        <div x-show="activeTab === 'lifestyle'" x-cloak x-transition>
                            ${renderGalleryGrid(galleryImages.lifestyle)}
                        </div>
                    </div>
                </section>

                 <section class="relative bg-brand-base text-white py-20 px-6 animate-on-scroll">
                     <div class="absolute inset-0 opacity-10">
                        <img src="https://images.unsplash.com/photo-1516414447565-b14be0adf13e?q=80&w=1887&auto=format&fit=crop" class="w-full h-full object-cover">
                     </div>
                    <div class="relative container mx-auto text-center max-w-2xl">
                        <h2 class="text-3xl font-serif">Join The Club</h2>
                        <p class="mt-4 text-gray-300">Subscribe to our newsletter for exclusive content, early access to new collections, and a 10% discount on your first order. Become part of a community that values intentional living.</p>
                        <form class="mt-8 flex flex-col sm:flex-row gap-2 max-w-md mx-auto">
                            <input type="email" placeholder="Enter your email address" class="flex-grow p-3 bg-white/10 border border-white/20 rounded-md text-white placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-brand-accent">
                            <button type="submit" class="bg-white text-brand-base py-3 px-6 text-sm font-semibold rounded-md hover:bg-gray-200 transition-colors">Subscribe</button>
                        </form>
                    </div>
                </section>
                `;
            };

            const renderArticleScrollerSection = (sectionTitle, articles, pillarPageTarget) => {
                const sectionId = sectionTitle.toLowerCase().replace(/\s+/g, '-');
                return `
                    <section class="py-20 bg-brand-secondary-bg animate-on-scroll">
                        <div class="container mx-auto px-6">
                            <div class="flex justify-between items-center mb-12">
                                <div>
                                    <p class="text-sm text-brand-gray">Discover</p>
                                    <h2 class="text-3xl font-serif text-brand-base">${sectionTitle}</h2>
                                </div>
                                <a href="#" data-target="${pillarPageTarget}" class="page-link text-sm font-semibold text-brand-base border-b-2 border-brand-base pb-1">View All</a>
                            </div>
                            <div class="relative">
                                <div id="${sectionId}-scroller" class="hide-scrollbar grid grid-flow-col auto-cols-[80%] sm:auto-cols-[40%] md:auto-cols-[30%] lg:auto-cols-[22%] gap-6 overflow-x-auto snap-x snap-mandatory scroll-smooth">
                                    ${articles.map(article => `
                                        <a href="#" class="page-link group relative flex-shrink-0 rounded-lg overflow-hidden snap-start" data-target="article-page" data-title="${article.title}">
                                            <img src="${article.image}" class="w-full h-80 object-cover group-hover:scale-105 transition-transform duration-300">
                                            <div class="absolute inset-0 bg-gradient-to-t from-black/70 to-transparent"></div>
                                            <div class="absolute bottom-0 left-0 p-4 text-white">
                                                <p class="text-xs uppercase tracking-widest">${article.category}</p>
                                                <h3 class="text-base font-serif mt-1">${article.title.split('–')[0]}</h3>
                                            </div>
                                        </a>
                                    `).join('')}
                                </div>
                            </div>
                        </div>
                    </section>
                `;
            };

            const renderGenericPage = (title, articles) => {
                return `
                <div class="py-12 px-6">
                    <div class="text-center mb-12">
                        <h2 class="text-lg font-sans font-medium tracking-[0.2em] uppercase text-brand-base">${title}</h2>
                    </div>
                    <div class="max-w-7xl mx-auto grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-x-6 gap-y-12">
                        ${articles.map(article => `
                             <a href="#" class="page-link group" data-target="article-page" data-title="${article.title}">
                                <div class="overflow-hidden rounded-md"><img src="${article.image}" class="w-full h-80 object-cover group-hover:opacity-80 transition-opacity duration-300"></div>
                                <div class="pt-4 text-center">
                                    <p class="text-xs uppercase tracking-widest text-brand-gray">${article.category}</p>
                                    <h3 class="text-lg font-serif text-brand-base mt-2 group-hover:text-brand-accent">${article.title.split('–')[0]}</h3>
                                </div>
                            </a>
                        `).join('')}
                    </div>
                </div>`;
            };

            const renderExploreStoriesPage = () => {
                 const allArticles = Object.entries(content.articles).map(([title, article]) => ({ ...article, title }));
                 return renderGenericPage('All Stories', allArticles);
            };

            const renderArticlePage = (data) => {
                const article = content.articles[data.title];
                if(!article) return `<div class="p-12 text-center"><h1 class="text-4xl font-serif">Article Not Found</h1></div>`;

                const relatedProductsHtml = article.relatedProducts && article.relatedProducts.length > 0 ? `
                    <div class="mt-16 pt-12 border-t border-brand-border">
                        <h2 class="text-2xl font-serif text-center mb-8">Shop The Story</h2>
                        <div class="grid grid-cols-2 md:grid-cols-3 gap-6">
                            ${article.relatedProducts.map(title => {
                                const product = content.products[title];
                                return `
                                <a href="#" class="page-link group" data-target="product-page" data-title="${title}">
                                    <div class="overflow-hidden rounded-lg bg-brand-secondary-bg"><img src="${product.image}" class="w-full h-48 md:h-64 object-cover group-hover:opacity-80 transition-opacity"></div>
                                    <div class="pt-3 text-center">
                                        <h3 class="text-sm font-semibold text-brand-base mt-1 group-hover:text-brand-accent">${title}</h3>
                                        <p class="text-xs text-brand-gray">Ksh ${product.price.toLocaleString()}</p>
                                    </div>
                                </a>`
                            }).join('')}
                        </div>
                    </div>` : '';

                const relatedArticles = Object.entries(content.articles)
                    .filter(([title, a]) => a.category === article.category && title !== data.title)
                    .slice(0, 2);
                
                const relatedArticlesHtml = relatedArticles.length > 0 ? `
                    <div class="mt-16 pt-12 border-t border-brand-border">
                        <h2 class="text-2xl font-serif text-center mb-8">You Might Also Like</h2>
                        <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
                            ${relatedArticles.map(([title, a]) => `
                                <a href="#" class="page-link group" data-target="article-page" data-title="${title}">
                                    <div class="overflow-hidden rounded-lg"><img src="${a.image}" class="w-full h-64 object-cover group-hover:scale-105 transition-transform duration-300"></div>
                                    <div class="pt-4">
                                        <p class="text-xs uppercase tracking-widest text-brand-gray">${a.category}</p>
                                        <h3 class="text-lg font-serif text-brand-base mt-1 group-hover:text-brand-accent">${title.split('–')[0]}</h3>
                                    </div>
                                </a>
                            `).join('')}
                        </div>
                    </div>
                ` : '';
                
                return `
                <div class="py-16">
                    <div class="container mx-auto px-6 max-w-3xl">
                        <a href="#" onclick="history.back()" class="text-sm uppercase tracking-widest text-brand-gray mb-8 inline-block">&larr; Back</a>
                        <p class="text-xs uppercase tracking-widest text-brand-gray">${article.category}</p>
                        <h1 class="text-4xl md:text-5xl font-serif text-brand-base mt-2">${data.title}</h1>
                        <p class="text-sm text-brand-gray mt-4">By ${article.author}</p>
                        <img src="${article.image}" class="w-full rounded-lg mt-8 mb-12">
                        <div class="prose text-brand-base">${article.body}</div>
                        ${relatedProductsHtml}
                        ${relatedArticlesHtml}
                    </div>
                </div>`;
            };

            const renderRecipePage = (data) => {
                const recipe = content.recipes[data.title];
                if(!recipe) return `<div class="p-12 text-center"><h1 class="text-4xl font-serif">Recipe Not Found</h1></div>`;
                const recipeText = createRecipeTextForDownload(data.title);

                return `
                <div class="py-16">
                    <div class="container mx-auto px-6 max-w-3xl">
                         <div class="flex justify-between items-center mb-8">
                            <a href="#" onclick="history.back()" class="text-sm uppercase tracking-widest text-brand-gray inline-block">&larr; Back</a>
                            <a href="data:text/plain;charset=utf-8,${recipeText}" download="${data.title}.txt" class="inline-block bg-brand-base text-white py-2 px-4 text-xs font-semibold cta-button rounded-md">Download Recipe</a>
                         </div>
                        <h1 class="text-4xl md:text-5xl font-serif text-brand-base mt-2">${data.title}</h1>
                        <div class="flex flex-wrap gap-x-6 gap-y-2 text-sm text-brand-gray my-6">
                            <span><strong>Prep Time:</strong> ${recipe.prepTime}</span>
                            <span><strong>Cook Time:</strong> ${recipe.cookTime}</span>
                            <span><strong>Servings:</strong> ${recipe.servings}</span>
                        </div>
                        <img src="${recipe.image}" class="w-full rounded-lg mt-8 mb-12">
                        <div class="prose text-brand-base">
                            <p>${recipe.description}</p>
                            <h3>Ingredients</h3>
                            <ul>${recipe.ingredients.map(i => `<li>${i}</li>`).join('')}</ul>
                            <h3>Instructions</h3>
                            <ol>${recipe.instructions.map(i => `<li>${i}</li>`).join('')}</ol>
                        </div>
                    </div>
                </div>`;
            };
            
            const renderRecipesCollectionPage = () => {
                const allRecipes = Object.entries(content.recipes).map(([title, recipe]) => ({...recipe, title}));
                
                const renderTag = (tag) => {
                    let color = 'bg-gray-200 text-gray-700';
                    if(tag.toLowerCase().includes('protein')) color = 'bg-blue-100 text-blue-700';
                    if(!tag) return '';
                    return `<span class="text-[10px] font-semibold px-2 py-1 rounded-full ${color}">${tag}</span>`;
                }

                return `
                <div class="bg-brand-secondary-bg py-16 px-6">
                    <div class="container mx-auto">
                        <div class="text-center max-w-2xl mx-auto">
                            <h1 class="text-4xl font-serif text-brand-base">Our Curated Recipes</h1>
                            <p class="text-lg text-brand-gray mt-2">Delicious and intentional recipes for every occasion.</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8 mt-12">
                            ${allRecipes.map(recipe => `
                                <a href="#" class="page-link group bg-white rounded-lg overflow-hidden shadow-sm hover:shadow-lg transition-shadow" data-target="recipe-page" data-title="${recipe.title}">
                                    <div class="relative">
                                        <img src="${recipe.image}" alt="${recipe.title}" class="w-full h-56 object-cover">
                                        <div class="absolute top-3 left-3 flex flex-wrap gap-2">
                                            ${recipe.tags.map(tag => renderTag(tag)).join('')}
                                        </div>
                                    </div>
                                    <div class="p-5">
                                        <h3 class="font-serif text-lg text-brand-base group-hover:text-brand-accent transition-colors">${recipe.title}</h3>
                                        <p class="text-sm text-brand-gray mt-2">${recipe.cookTime} · ${recipe.calories} kcal</p>
                                    </div>
                                </a>
                            `).join('')}
                        </div>
                    </div>
                </div>
                `;
            };

            const renderProductPage = (data) => {
                const product = content.products[data.title];
                if (!product) return `<div class="p-12 text-center"><h1 class="text-4xl font-serif">Product Not Found</h1></div>`;
                return `
                 <div class="py-12 bg-white">
                    <div class="container mx-auto px-6 grid grid-cols-1 lg:grid-cols-2 gap-12 items-start">
                        <div class="sticky top-28 bg-brand-bg rounded-lg p-2">
                            <img src="${product.image}" id="main-product-image" class="w-full h-full object-cover rounded-md">
                        </div>
                        <div class="pt-4">
                            <a href="#" data-target="shop-page" class="page-link text-xs uppercase tracking-widest text-brand-gray mb-4 inline-block">&larr; Back to shop</a>
                            <h1 class="text-3xl md:text-4xl font-serif">${data.title}</h1>
                            <p class="text-2xl text-brand-base font-medium mt-3">Ksh ${product.price.toLocaleString()}</p>
                            <div class="mt-6 text-sm text-green-600 flex items-center gap-2">
                                <svg class="w-4 h-4" fill="currentColor" viewBox="0 0 20 20"><path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-9.293a1 1 0 00-1.414-1.414L9 10.586 7.707 9.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4z" clip-rule="evenodd"></path></svg>
                                <span>In stock, ready to ship</span>
                            </div>
                            <div class="mt-8 flex flex-col gap-3">
                                 <button id="buy-now-btn" class="w-full bg-brand-base text-white py-4 text-sm font-semibold cta-button uppercase tracking-wider rounded-md">Buy Now</button>
                                 <button id="add-to-cart-btn" class="w-full border border-brand-base text-brand-base py-4 text-sm font-semibold uppercase tracking-wider rounded-md hover:bg-brand-base hover:text-white transition-colors">Add to Cart</button>
                            </div>
                            <div class="mt-8 border-t border-brand-border">
                                <div class="py-4 border-b border-brand-border" x-data="{ open: true }">
                                    <h3 class="font-semibold cursor-pointer flex justify-between items-center" @click="open = !open">
                                        Description
                                        <svg class="w-4 h-4 transition-transform" :class="{ 'rotate-180': open }" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path></svg>
                                    </h3>
                                    <div class="prose text-sm mt-2" x-show="open" style="display: none;" x-transition>${product.description}</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>`;
            };
            
            const renderCartPage = () => {
                const total = cart.reduce((acc, item) => acc + (item.price || 0) * item.quantity, 0);
                return `
                <div class="py-16 px-6">
                    <div class="max-w-2xl mx-auto">
                        <h1 class="text-4xl font-serif text-center mb-2">Shopping Cart</h1>
                        <p class="text-center text-brand-gray mb-10">You have ${cart.length} item(s) in your cart.</p>
                        ${cart.length === 0 ? '<p class="text-center text-brand-gray py-12">Your cart is currently empty.</p>' : `
                        <div class="space-y-6">
                            ${cart.map((item, index) => `
                                <div class="flex items-start gap-6 border-b border-brand-border pb-6" data-index="${index}">
                                    <div class="w-24 h-24 bg-brand-secondary-bg rounded-lg overflow-hidden flex-shrink-0">
                                        <img src="${item.image}" alt="${item.title}" class="w-full h-full object-cover">
                                    </div>
                                    <div class="flex-grow">
                                        <h3 class="font-serif text-lg">${item.title}</h3>
                                        <div class="flex items-center mt-2">
                                            <label for="quantity-${index}" class="text-sm mr-2">Quantity:</label>
                                            <input type="number" id="quantity-${index}" value="${item.quantity}" min="1" class="w-16 text-center border border-brand-border rounded-md py-1 quantity-input">
                                        </div>
                                    </div>
                                    <div class="text-right">
                                        <p class="font-semibold">Ksh ${(item.price * item.quantity).toLocaleString()}</p>
                                        <button class="text-xs text-brand-gray hover:text-red-500 underline mt-2 remove-item-btn">Remove</button>
                                    </div>
                                </div>
                            `).join('')}
                        </div>
                        <div class="mt-10 bg-brand-secondary-bg rounded-lg p-6">
                            <div class="flex justify-between items-center">
                                <span class="text-lg font-serif">Subtotal</span>
                                <span class="text-xl font-semibold">Ksh ${total.toLocaleString()}</span>
                            </div>
                            <p class="text-xs text-brand-gray mt-2">Shipping & taxes calculated at checkout.</p>
                            <button id="checkout-btn" class="mt-6 w-full bg-brand-base text-white py-4 text-sm font-semibold cta-button uppercase tracking-wider">Buy Now on WhatsApp</button>
                        </div>`}
                    </div>
                </div>`;
            };

            const renderShopPage = () => {
                return `
                <section class="relative h-[50vh] bg-cover bg-center text-white flex items-center" style="background-image: url('https://images.unsplash.com/photo-1590854199460-a7d084c7e2a9?q=80&w=1932&auto=format&fit=crop');">
                    <div class="absolute inset-0 bg-black/40"></div>
                    <div class="relative z-10 container mx-auto px-6">
                        <h1 class="text-4xl md:text-5xl font-serif leading-tight max-w-lg">The Memuci Collection</h1>
                        <p class="text-lg mt-4 max-w-lg">Curated essentials for a beautiful, intentional life.</p>
                    </div>
                </section>
                <div id="product-grid" class="py-20 px-6">
                    <div class="max-w-6xl mx-auto grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-8">
                        ${Object.entries(content.products).map(([title, product]) => `
                             <div class="group relative">
                                <a href="#" class="page-link block" data-target="product-page" data-title="${title}">
                                    <div class="overflow-hidden rounded-lg bg-brand-secondary-bg"><img src="${product.image}" class="w-full h-96 object-cover group-hover:opacity-80 transition-opacity"></div>
                                    <div class="pt-4 text-center">
                                        <h3 class="text-base font-semibold text-brand-base mt-1 group-hover:text-brand-accent">${title}</h3>
                                        <p class="text-sm text-brand-gray">Ksh ${product.price.toLocaleString()}</p>
                                    </div>
                                </a>
                                <button class="add-to-cart-quick-btn absolute top-4 right-4 bg-white/80 rounded-full p-2 opacity-0 group-hover:opacity-100 transition-opacity" data-title="${title}">
                                    <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-brand-base" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" stroke-linejoin="round" d="M16 11V7a4 4 0 00-8 0v4M5 9h14l1 12H4L5 9z" /></svg>
                                </button>
                             </div>
                        `).join('')}
                    </div>
                </div>`;
            };

            const renderAboutPage = () => {
                const editorPicks = [
                    content.articles["Business Playbook – Strategies, Entrepreneurial Tips, Money Talk"],
                    content.articles["The Wardrobe – Fashion Inspiration, Capsule Wardrobes, Trends"],
                    content.articles["Travel Diaries – Weekend Getaways, Kenyan Gems, Destination Guides"]
                ];
                 const editorPickTitles = ["Business Playbook – Strategies, Entrepreneurial Tips, Money Talk", "The Wardrobe – Fashion Inspiration, Capsule Wardrobes, Trends", "Travel Diaries – Weekend Getaways, Kenyan Gems, Destination Guides"];

                return `
                <div class="bg-white">
                    <!-- Founder Section -->
                    <section class="py-20 px-6">
                        <div class="container mx-auto grid grid-cols-1 md:grid-cols-2 items-center gap-12">
                             <div class="md:order-1">
                                <img src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?q=80&w=1887&auto=format&fit=crop" class="w-full max-w-sm mx-auto object-cover rounded-lg shadow-lg">
                            </div>
                            <div class="md:order-2 text-center md:text-left">
                                <h2 class="text-4xl md:text-5xl font-serif text-brand-base leading-tight">A Word From Our Founder</h2>
                                <p class="text-brand-gray mt-6 max-w-md mx-auto md:mx-0">"Memuci began with a simple idea: that living intentionally can transform the ordinary into the extraordinary. We wanted to create a space that feels like a deep, calming breath—a source of inspiration and support for a more mindful life. Thank you for being a part of this journey. We're so glad you're here."</p>
                                <p class="font-serif text-xl mt-6">Carolyne</p>
                                <p class="text-sm text-brand-gray">Founder & CEO, Memuci Lifestyle</p>
                            </div>
                        </div>
                    </section>

                    <!-- Our Profile -->
                    <section class="py-20 px-6 bg-brand-bg">
                        <div class="prose text-center">
                            <h2 class="text-4xl">Our Profile</h2>
                            <p class="text-lg">Memuci is a lifestyle brand dedicated to the art of intentional living. We believe in quality over quantity, purpose over pressure, and finding beauty in the everyday. Our mission is to provide a curated space for content and products that inspire a more thoughtful and beautiful life, rooted in our Kenyan heritage and designed for the modern world. We are more than just a brand; we are a community built on the shared values of authenticity, curiosity, and conscious living.</p>
                        </div>
                    </section>
                    
                    <!-- Editor's Picks -->
                    <section class="py-20 px-6">
                        <div class="text-center mb-12">
                            <h2 class="text-3xl font-serif text-brand-base">Editor's Picks</h2>
                            <p class="text-brand-gray mt-2">A few of our favorite reads right now.</p>
                        </div>
                        <div class="max-w-5xl mx-auto grid grid-cols-1 sm:grid-cols-3 gap-8">
                            ${editorPicks.map((article, index) => `
                                <a href="#" class="page-link group" data-target="article-page" data-title="${editorPickTitles[index]}">
                                    <div class="overflow-hidden rounded-lg"><img src="${article.image}" class="w-full h-64 object-cover group-hover:scale-105 transition-transform duration-300"></div>
                                    <div class="pt-4">
                                        <p class="text-xs uppercase tracking-widest text-brand-gray">${article.category}</p>
                                        <h3 class="text-lg font-serif text-brand-base mt-1 group-hover:text-brand-accent">${editorPickTitles[index].split('–')[0]}</h3>
                                    </div>
                                </a>
                            `).join('')}
                        </div>
                    </section>

                    <!-- Our Team -->
                    <section class="py-20 bg-brand-bg px-6">
                        <h2 class="text-3xl font-serif text-center mb-12">Meet the Team</h2>
                        <div class="max-w-4xl mx-auto grid grid-cols-1 md:grid-cols-3 gap-8 text-center">
                            ${content.teamMembers.map(member => `
                                <div>
                                    <img src="${member.image}" class="w-40 h-40 rounded-full object-cover mx-auto mb-4 shadow-md">
                                    <h3 class="font-serif text-xl">${member.name}</h3>
                                    <p class="text-brand-gray">${member.title}</p>
                                </div>
                            `).join('')}
                        </div>
                    </section>
                </div>
            `;
            };
            const renderContactPage = () => `
                <div class="py-20 px-6 bg-white">
                    <div class="container mx-auto">
                        <div class="text-center mb-16">
                            <h1 class="text-4xl md:text-5xl font-serif text-brand-base">Get In Touch</h1>
                            <p class="text-brand-gray mt-4 max-w-2xl mx-auto">We'd love to hear from you. Whether you have a question about our products, a partnership proposal, or just want to say hello, our team is ready to answer all your questions.</p>
                        </div>
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-12 max-w-5xl mx-auto">
                            <div class="bg-brand-bg p-8 rounded-lg">
                                <h3 class="font-serif text-2xl mb-6">Contact Information</h3>
                                <div class="space-y-4 text-brand-gray">
                                    <div class="flex items-start gap-4">
                                        <svg class="w-5 h-5 text-brand-accent mt-1 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 002-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"></path></svg>
                                        <div>
                                            <p class="font-semibold text-brand-base">Email</p>
                                            <a href="mailto:hello@memuci.com" class="hover:text-brand-accent">hello@memuci.com</a>
                                        </div>
                                    </div>
                                    <div class="flex items-start gap-4">
                                        <svg class="w-5 h-5 text-brand-accent mt-1 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path></svg>
                                        <div>
                                            <p class="font-semibold text-brand-base">Phone</p>
                                            <p>+254 700 123 456</p>
                                        </div>
                                    </div>
                                    <div class="flex items-start gap-4">
                                         <svg class="w-5 h-5 text-brand-accent mt-1 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z"></path><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z"></path></svg>
                                        <div>
                                            <p class="font-semibold text-brand-base">Office</p>
                                            <p>123 Riverside Drive, Nairobi, Kenya</p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="bg-brand-bg p-8 rounded-lg">
                                <h3 class="font-serif text-2xl mb-6">Send Us a Message</h3>
                                <form action="#" method="POST" class="space-y-4">
                                    <div>
                                        <label for="name" class="text-sm font-medium text-brand-gray">Full Name</label>
                                        <input type="text" name="name" id="name" class="mt-1 block w-full border border-brand-border rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-brand-accent focus:border-brand-accent">
                                    </div>
                                    <div>
                                        <label for="email" class="text-sm font-medium text-brand-gray">Email Address</label>
                                        <input type="email" name="email" id="email" class="mt-1 block w-full border border-brand-border rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-brand-accent focus:border-brand-accent">
                                    </div>
                                     <div>
                                        <label for="message" class="text-sm font-medium text-brand-gray">Message</label>
                                        <textarea id="message" name="message" rows="4" class="mt-1 block w-full border border-brand-border rounded-md shadow-sm py-2 px-3 focus:outline-none focus:ring-brand-accent focus:border-brand-accent"></textarea>
                                    </div>
                                    <div>
                                        <button type="submit" class="w-full bg-brand-base text-white py-3 px-6 text-sm font-semibold cta-button rounded-md">Send Message</button>
                                    </div>
                                </form>
                            </div>
                        </div>
                    </div>
                </div>
            `;
            const renderFaqPage = () => `<div class="py-16 px-6 prose"><h1 class="text-center">FAQ</h1><h2>Shipping</h2><p>We currently ship within Kenya. Standard shipping is free on all orders over Ksh 5,000.</p><h2>Returns</h2><p>We accept returns on unworn, unused items within 14 days of purchase. Please contact us to initiate a return.</p></div>`;
            const renderTermsPage = () => `<div class="py-16 px-6 prose"><h1 class="text-center">Terms of Service</h1><p>Welcome to Memuci. By accessing our website, you agree to comply with and be bound by the following terms and conditions of use. All content provided on this site is for informational purposes only. We make no representations as to the accuracy or completeness of any information on this site or found by following any link on this site.</p></div>`;

            // --- ROUTER & PAGE DISPLAY LOGIC ---
            const showPage = (pageId, data = {}, pushState = true) => {
                document.querySelectorAll('.page').forEach(p => { p.innerHTML = ''; p.classList.add('hidden'); });
                const targetPage = document.getElementById(pageId);
                
                if (targetPage) {
                    if (pushState) history.pushState({ pageId, data }, '', `#${pageId}`);
                    let contentToRender = '';
                    switch(pageId) {
                        case 'home-page': contentToRender = renderHomePage(); break;
                        case 'epicure-page': contentToRender = renderGenericPage('Epicure & Entertaining', Object.entries(content.articles).filter(([_,a]) => a.category === 'Epicure & Entertaining').map(([title, article])=>({title, ...article}))); break;
                        case 'motherhood-page': contentToRender = renderGenericPage('Modern Motherhood', Object.entries(content.articles).filter(([_,a]) => a.category === 'Modern Motherhood').map(([title, article])=>({title, ...article}))); break;
                        case 'style-beauty-page': contentToRender = renderGenericPage('Style & Beauty', Object.entries(content.articles).filter(([_,a]) => a.category === 'Style & Beauty').map(([title, article])=>({title, ...article}))); break;
                        case 'culture-escapes-page': contentToRender = renderGenericPage('Culture & Escapes', Object.entries(content.articles).filter(([_,a]) => a.category === 'Culture & Escapes').map(([title, article])=>({title, ...article}))); break;
                        case 'power-purpose-page': contentToRender = renderGenericPage('Power & Purpose', Object.entries(content.articles).filter(([_,a]) => a.category === 'Power & Purpose').map(([title, article])=>({title, ...article}))); break;
                        case 'health-page': contentToRender = renderGenericPage('Health', Object.entries(content.articles).filter(([_,a]) => a.category === 'Health').map(([title, article])=>({title, ...article}))); break;
                        case 'fitness-page': contentToRender = renderGenericPage('Fitness', Object.entries(content.articles).filter(([_,a]) => a.category === 'Fitness').map(([title, article])=>({title, ...article}))); break;
                        case 'relationships-page': contentToRender = renderGenericPage('Relationships', Object.entries(content.articles).filter(([_,a]) => a.category === 'Relationships').map(([title, article])=>({title, ...article}))); break;
                        case 'shop-page': contentToRender = renderShopPage(); break;
                        case 'explore-stories-page': contentToRender = renderExploreStoriesPage(); break;
                        case 'article-page': contentToRender = renderArticlePage(data); break;
                        case 'recipe-page': contentToRender = renderRecipePage(data); break;
                        case 'recipes-collection-page': contentToRender = renderRecipesCollectionPage(); break;
                        case 'product-page': contentToRender = renderProductPage(data); break;
                        case 'cart-page': contentToRender = renderCartPage(); break;
                        case 'about-page': contentToRender = renderAboutPage(); break;
                        case 'contact-page': contentToRender = renderContactPage(); break;
                        case 'faq-page': contentToRender = renderFaqPage(); break;
                        case 'terms-page': contentToRender = renderTermsPage(); break;
                        default: contentToRender = `<div class="p-12 text-center"><h1 class="text-4xl font-serif">Page Not Found</h1></div>`;
                    }
                    targetPage.innerHTML = contentToRender;
                    targetPage.classList.remove('hidden');
                    if (pushState) window.scrollTo(0, 0);

                    // --- ATTACH DYNAMIC EVENT LISTENERS ---
                    if (pageId === 'product-page') {
                        document.getElementById('add-to-cart-btn').addEventListener('click', () => {
                            const productData = { title: data.title, ...content.products[data.title] };
                            addToCart(productData);
                        });
                        document.getElementById('buy-now-btn').addEventListener('click', () => {
                            const message = `Hello! I'd like to purchase the following item: ${data.title}`;
                            window.open(`https://wa.me/?text=${encodeURIComponent(message)}`, '_blank');
                        });
                    } else if (pageId === 'cart-page') {
                         document.getElementById('checkout-btn')?.addEventListener('click', () => {
                            const total = cart.reduce((acc, item) => acc + (item.price || 0) * item.quantity, 0);
                            let message = "Hello! I'd like to place an order for the following items:\n";
                            cart.forEach(item => {
                                message += `- ${item.quantity} x ${item.title}\n`;
                            });
                            message += `\nTotal: Ksh ${total.toLocaleString()}`;
                            window.open(`https://wa.me/?text=${encodeURIComponent(message)}`, '_blank');
                        });
                        document.querySelectorAll('.remove-item-btn').forEach(btn => {
                            btn.addEventListener('click', e => {
                                const index = e.target.closest('[data-index]').dataset.index;
                                cart.splice(index, 1);
                                updateCartCount();
                                showPage('cart-page', {}, false);
                            });
                        });
                        document.querySelectorAll('.quantity-input').forEach(input => {
                            input.addEventListener('change', e => {
                                const index = e.target.closest('[data-index]').dataset.index;
                                const newQuantity = parseInt(e.target.value);
                                if (newQuantity > 0) cart[index].quantity = newQuantity;
                                else cart.splice(index, 1);
                                updateCartCount();
                                showPage('cart-page', {}, false);
                            });
                        });
                    }
                }
            };
            
            // --- MEGA MENU & SEARCH ---
            const populateMegaMenu = () => {
                const menuContainer = document.getElementById('pillars-mega-menu');
                const pillars = [
                    { name: 'Epicure & Entertaining', target: 'epicure-page' },
                    { name: 'Modern Motherhood', target: 'motherhood-page' },
                    { name: 'Style & Beauty', target: 'style-beauty-page' },
                    { name: 'Culture & Escapes', target: 'culture-escapes-page' },
                    { name: 'Power & Purpose', target: 'power-purpose-page' },
                ];
                
                let menuHtml = `
                    <div class="grid grid-cols-3 gap-x-8">
                        <div class="col-span-2">
                            <h3 class="text-sm font-semibold uppercase tracking-wider text-brand-gray mb-4">Explore by Pillar</h3>
                            <div class="grid grid-cols-2 gap-x-6 gap-y-3">
                                ${pillars.map(pillar => `
                                    <a href="#" @click="open = false" class="page-link text-brand-base hover:text-brand-accent py-1" data-target="${pillar.target}">${pillar.name}</a>
                                `).join('')}
                                <a href="#" @click="open = false" class="page-link text-brand-base hover:text-brand-accent py-1" data-target="recipes-collection-page">Recipes</a>
                            </div>
                        </div>
                        <div>
                             <a href="#" @click="open = false" class="page-link group block" data-target="shop-page">
                                <div class="overflow-hidden rounded-md">
                                    <img src="https://images.unsplash.com/photo-1523275335684-37898b6baf30?q=80&w=1999&auto=format&fit=crop" class="w-full h-40 object-cover group-hover:scale-105 transition-transform duration-300">
                                </div>
                                <h4 class="font-serif text-brand-base mt-3 group-hover:text-brand-accent">Shop The Collection</h4>
                                <p class="text-sm text-brand-gray">Curated essentials for your lifestyle.</p>
                             </a>
                        </div>
                    </div>
                `;
                menuContainer.innerHTML = menuHtml;
            };

            const handleSearch = (query) => {
                if (query.length < 2) { searchResultsContainer.innerHTML = ''; return; }
                const lowerQuery = query.toLowerCase();
                const articles = Object.entries(content.articles).filter(([title, article]) => title.toLowerCase().includes(lowerQuery) || article.body.toLowerCase().includes(lowerQuery));
                const products = Object.entries(content.products).filter(([title]) => title.toLowerCase().includes(lowerQuery));
                let resultsHtml = '';
                if (articles.length === 0 && products.length === 0) {
                    resultsHtml = '<p class="text-brand-gray text-center">No results found.</p>';
                } else {
                    if (articles.length > 0) {
                        resultsHtml += `<h3 class="font-serif text-lg mb-2">Articles</h3>`;
                        articles.forEach(([title, article]) => { resultsHtml += `<a href="#" data-target="article-page" data-title="${title}" class="page-link search-result-item block p-3 hover:bg-brand-bg rounded-md">${title}</a>`; });
                    }
                    if (products.length > 0) {
                        resultsHtml += `<h3 class="font-serif text-lg mt-4 mb-2">Products</h3>`;
                        products.forEach(([title, product]) => { resultsHtml += `<a href="#" data-target="product-page" data-title="${title}" class="page-link search-result-item block p-3 hover:bg-brand-bg rounded-md">${title}</a>`; });
                    }
                }
                searchResultsContainer.innerHTML = resultsHtml;
            };

            // --- GLOBAL EVENT LISTENERS ---
            document.getElementById('mobile-menu-button').addEventListener('click', () => mobileMenu.classList.toggle('hidden'));
            document.getElementById('search-button').addEventListener('click', () => searchOverlay.classList.remove('hidden'));
            document.getElementById('close-search-button').addEventListener('click', () => searchOverlay.classList.add('hidden'));
            searchInput.addEventListener('input', (e) => handleSearch(e.target.value));
            
            // Sale pop-up logic
            closeSalePopupBtn.addEventListener('click', () => salePopupOverlay.classList.add('hidden'));
            document.querySelector('.sale-popup-shop-now').addEventListener('click', () => salePopupOverlay.classList.add('hidden'));


            document.body.addEventListener('click', (e) => {
                if (e.target.closest('.page-link')) {
                    e.preventDefault();
                    const target = e.target.closest('.page-link');
                    const pageId = target.dataset.target;
                    const data = { title: target.dataset.title };
                    showPage(pageId, data);
                    if (e.target.closest('.search-result-item')) searchOverlay.classList.add('hidden');
                    if (mobileMenu.offsetParent !== null) mobileMenu.classList.add('hidden');
                }
                if (e.target.closest('.add-to-cart-quick-btn')) {
                    const title = e.target.closest('.add-to-cart-quick-btn').dataset.title;
                    const productData = { title, ...content.products[title] };
                    addToCart(productData);
                }
            });
            
            window.addEventListener('popstate', (event) => {
                if (event.state) showPage(event.state.pageId, event.state.data, false);
                else showPage('home-page', {}, false);
            });

            // --- INITIALIZATION ---
            populateMegaMenu();
            const initialHash = window.location.hash.substring(1);
            const initialPage = initialHash || 'home-page';
            showPage(initialPage, {}, true);

            // Show sale pop-up on scroll
            const saleBanner = document.getElementById('mega-sale-banner');
            const handleScroll = () => {
                if(saleBanner && !sessionStorage.getItem('salePopupShown')) {
                    const bannerPosition = saleBanner.getBoundingClientRect();
                    if(bannerPosition.top < window.innerHeight && bannerPosition.bottom >= 0) {
                       setTimeout(() => {
                            salePopupOverlay.classList.remove('hidden');
                            sessionStorage.setItem('salePopupShown', 'true');
                            window.removeEventListener('scroll', handleScroll);
                       }, 1000);
                    }
                }
            };
            window.addEventListener('scroll', handleScroll);

            // Animate sections on scroll
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                    if (entry.isIntersecting) {
                        entry.target.classList.add('is-visible');
                    }
                });
            }, { threshold: 0.1 });

            document.querySelectorAll('.animate-on-scroll').forEach(section => {
                observer.observe(section);
            });

        });
    </script>
</body>
</html>

