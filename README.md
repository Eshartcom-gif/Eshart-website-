<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ESHART | Official Ecosystem</title>
    
    <script src="https://bundle.run/buffer@6.0.3"></script>
    <script src="https://unpkg.com/@solana/web3.js@1.95.8/lib/index.iife.min.js"></script>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@900&family=Inter:wght@400;700&display=swap" rel="stylesheet">
    
    <style>
        :root { --accent: #14F195; --bg: #010204; }
        body { 
            background-color: var(--bg); color: white; font-family: 'Inter', sans-serif; scroll-behavior: smooth;
            background-image: linear-gradient(rgba(1, 2, 4, 0.94), rgba(1, 2, 4, 0.94)), url('https://images.unsplash.com/photo-1639322537228-f710d846310a?q=80&w=2000&auto=format&fit=crop');
            background-size: cover; background-position: center; background-attachment: fixed;
        }
        .font-heading { font-family: 'Orbitron', sans-serif; }
        .shart-gradient { background: linear-gradient(90deg, #9945FF, #14F195); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .glass { background: rgba(255,255,255,0.02); border: 1px solid rgba(255, 255, 255, 0.05); backdrop-filter: blur(20px); }
        
        /* TELEGRAM PULSE PIN */
        .tg-pin {
            position: fixed; bottom: 30px; right: 30px; z-index: 1000;
            background: #0088cc; width: 60px; height: 60px; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            box-shadow: 0 0 20px rgba(0, 136, 204, 0.6); animation: pulse 2s infinite;
        }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(0, 136, 204, 0.7); } 70% { box-shadow: 0 0 0 15px rgba(0, 136, 204, 0); } 100% { box-shadow: 0 0 0 0 rgba(0, 136, 204, 0); } }

        .roadmap-line { position: absolute; left: 20px; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, #14F195, transparent); }
    </style>
</head>
<body class="pb-24">

    <a href="https://t.me/ElonSHARTS" target="_blank" class="tg-pin">
        <svg width="30" height="30" viewBox="0 0 24 24" fill="white"><path d="M12 0c-6.627 0-12 5.373-12 12s5.373 12 12 12 12-5.373 12-12-5.373-12-12-12zm4.462 15.998l-.017.012-3.469 1.912c-.272.149-.599.045-.747-.227l-1.012-1.874-1.712.851-.001.001-.001.001c-.662.333-1.42-.147-1.42-.888v-4.52l-2.062-1.031c-.272-.137-.382-.464-.245-.736s.464-.382.736-.245l11.161 5.58c.272.137.382.464.245.736s-.463.382-.736.241z"/></svg>
    </a>

    <nav class="fixed top-0 w-full z-[100] glass border-b border-white/5 px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="https://i.ibb.co/0jdXM3fZ/1767978719058-2.jpg" class="h-10 w-10 rounded-lg">
            <span class="text-xl font-black font-heading shart-gradient uppercase italic">ESHART</span>
        </div>
        <div class="hidden md:flex gap-6 text-[9px] font-bold uppercase tracking-widest text-gray-500">
            <a href="#about" class="hover:text-green-400">Mission</a>
            <a href="#manifesto" class="hover:text-green-400">Whitepaper</a>
            <a href="#roadmap" class="hover:text-green-400">Roadmap</a>
        </div>
        <button onclick="handleConnect()" class="bg-[#14F195] text-black px-6 py-2 rounded-xl font-black text-[9px] uppercase shadow-lg shadow-green-500/10">Sync Dashboard</button>
    </nav>

    <main id="about" class="pt-48 px-6 max-w-7xl mx-auto grid lg:grid-cols-2 gap-20 items-center">
        <div class="space-y-8 text-center lg:text-left">
            <h1 class="text-7xl lg:text-9xl font-black font-heading leading-none uppercase italic">ELON <br><span class="shart-gradient">SHART.</span></h1>
            <p class="text-gray-400 text-lg leading-relaxed max-w-lg italic">The definitive deflationary ecosystem on Solana. Built for pressure, sustained by the community. 0% Tax.</p>
            <div class="flex flex-wrap gap-4 pt-4 justify-center lg:justify-start">
                <a href="https://pump.fun/coin/t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump" target="_blank" class="bg-white text-black px-12 py-5 rounded-2xl font-black uppercase text-xs hover:bg-[#14F195] transition shadow-2xl">Buy on Pump.fun</a>
            </div>
        </div>

        <div class="glass p-10 rounded-[3.5rem] border-white/10 text-center relative overflow-hidden">
            <div class="absolute top-0 left-0 w-full h-1 bg-gradient-to-r from-transparent via-[#14F195] to-transparent opacity-20"></div>
            <p class="text-gray-500 text-[10px] uppercase font-bold mb-4 tracking-widest italic">Live Holdings</p>
            <h2 id="tokenBalance" class="text-7xl font-black shart-gradient mb-4 tracking-tighter">0</h2>
            <p id="walletAddr" class="text-[8px] font-mono text-gray-600 truncate uppercase mb-10">Wallet Not Linked</p>
            <button onclick="handleConnect()" class="w-full py-5 bg-[#14F195] text-black font-black rounded-2xl transition uppercase text-xs tracking-widest hover:scale-[1.02]">Connect Blockchain</button>
        </div>
    </main>

    <section id="manifesto" class="py-32 px-6 max-w-4xl mx-auto border-t border-white/5 mt-32">
        <h3 class="text-4xl font-black font-heading mb-12 uppercase italic text-center shart-gradient">The Manifesto</h3>
        <div class="glass p-10 rounded-[2.5rem] border-white/5 space-y-10 leading-relaxed text-gray-400 text-sm">
            <div>
                <h4 class="text-white font-bold uppercase tracking-widest text-xs mb-4">01. High-Frequency Deflation</h4>
                <p>Unlike standard meme projects, $ESHART utilizes a burn-heavy ecosystem where scarcity is not a promise, but a protocol requirement. Our ZOO assets are pegged to current supply metrics.</p>
            </div>
            <div>
                <h4 class="text-white font-bold uppercase tracking-widest text-xs mb-4">02. Ownership Architecture</h4>
                <p>The contract is renounced. Liquidity is burnt upon successful bonding. There are no developer allocations or team taxes. The "Elite 300" own the future of the zoo.</p>
            </div>
        </div>
    </section>

    <section id="roadmap" class="py-32 px-6 max-w-4xl mx-auto border-t border-white/5">
        <h3 class="text-4xl font-black font-heading mb-20 uppercase italic text-center">Protocol Roadmap</h3>
        <div class="relative space-y-20 pl-12">
            <div class="roadmap-line"></div>
            
