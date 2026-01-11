
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ESHART | The Official Decentralized Portal</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/@solana/web3.js@1.95.8/lib/index.iife.min.js"></script>
    <script src="https://terminal.jup.ag/main-v3.js" defer></script>
    
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@900&family=Inter:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root { --accent: #14F195; --bg: #010204; --card: rgba(255,255,255,0.02); }
        body { background-color: var(--bg); color: white; font-family: 'Inter', sans-serif; overflow-x: hidden; scroll-behavior: smooth; }
        .font-heading { font-family: 'Orbitron', sans-serif; letter-spacing: -0.05em; }
        .shart-gradient { background: linear-gradient(90deg, #9945FF, #14F195); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .glass { background: var(--card); border: 1px solid rgba(255, 255, 255, 0.05); backdrop-filter: blur(12px); }
        .glow { box-shadow: 0 0 30px rgba(20, 241, 149, 0.1); }
        #jupiter-terminal { width: 100%; max-width: 440px; height: 520px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.1); margin: 0 auto; }
        .roadmap-item::before { content: ''; position: absolute; left: -1px; top: 0; bottom: 0; width: 2px; background: linear-gradient(to bottom, #14F195, transparent); }
    </style>
</head>
<body>

    <nav class="fixed top-0 w-full z-[100] glass border-b border-white/5 px-6 py-4">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <div class="flex items-center gap-3">
                <img src="https://i.ibb.co/0jdXM3fZ/1767978719058-2.jpg" class="h-10 w-10 rounded-lg">
                <span class="text-xl font-black font-heading shart-gradient italic uppercase">ESHART</span>
            </div>
            <div class="hidden md:flex gap-8 text-[10px] font-bold uppercase tracking-[0.2em] text-gray-500">
                <a href="#about" class="hover:text-green-400 transition">Mission</a>
                <a href="#tokenomics" class="hover:text-green-400 transition">Economics</a>
                <a href="#roadmap" class="hover:text-green-400 transition">Roadmap</a>
                <a href="#swap" class="hover:text-green-400 transition">Swap</a>
                <a href="#faq" class="hover:text-green-400 transition">FAQ</a>
            </div>
            <button onclick="handleConnect()" id="navSyncBtn" class="bg-[#14F195] text-black px-6 py-2 rounded-xl font-black text-[10px] uppercase shadow-lg shadow-green-500/10 hover:scale-105 transition">Sync Dashboard</button>
        </div>
    </nav>

    <section id="about" class="pt-48 pb-20 px-6 max-w-7xl mx-auto grid lg:grid-cols-2 gap-20 items-center">
        <div class="space-y-8">
            <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full glass border-green-500/20 text-green-400 text-[9px] font-bold uppercase tracking-widest">
                <span class="w-1.5 h-1.5 bg-green-400 rounded-full animate-pulse"></span> Helius Mainnet Tunnel Active
            </div>
            <h1 class="text-7xl lg:text-9xl font-black font-heading leading-none uppercase italic">ELON <br><span class="shart-gradient">SHART.</span></h1>
            <p class="text-gray-400 text-lg leading-relaxed max-w-lg">The world's most aggressive deflationary meme-ecosystem. We are building the future of decentralized pressure. 0% Tax. 100% Impact.</p>
            <div class="flex flex-wrap gap-4 pt-4">
                <a href="https://pump.fun/coin/t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump" target="_blank" class="bg-white text-black px-10 py-5 rounded-2xl font-black uppercase text-xs hover:bg-green-400 transition shadow-xl">Buy on Pump.fun</a>
                <a href="https://t.me/ElonSHARTS" target="_blank" class="glass px-10 py-5 rounded-2xl font-black border-white/10 text-sky-400 text-xs text-center flex items-center justify-center">Join the Shart Tank</a>
            </div>
        </div>

        <div class="glass p-10 rounded-[3rem] border-white/10 text-center relative glow">
            <p class="text-gray-500 text-[10px] uppercase font-bold mb-4 tracking-widest">Investor Holdings</p>
            <h2 id="tokenBalance" class="text-7xl font-black shart-gradient mb-2 tracking-tighter">0</h2>
            <div class="p-4 bg-black/40 rounded-2xl border border-white/5 mb-8">
                <p id="walletAddr" class="text-[9px] font-mono text-gray-600 truncate uppercase italic tracking-widest">Wallet Not Linked</p>
            </div>
            <div class="grid grid-cols-2 gap-4 mb-8">
                <div class="glass p-4 rounded-2xl"><p class="text-[8px] text-gray-500 uppercase mb-1">Tax</p><p class="font-bold text-green-400">0%</p></div>
                <div class="glass p-4 rounded-2xl"><p class="text-[8px] text-gray-500 uppercase mb-1">LP Status</p><p class="font-bold text-purple-400 uppercase italic">Burning</p></div>
            </div>
            <button onclick="handleConnect()" id="mainConnectBtn" class="w-full py-5 bg-[#14F195] text-black font-black rounded-2xl transition uppercase text-xs tracking-widest">Connect Blockchain</button>
        </div>
    </section>

    <section id="tokenomics" class="py-32 px-6 max-w-7xl mx-auto border-t border-white/5">
        <div class="text-center mb-20">
            <h3 class="text-4xl font-black font-heading mb-4 uppercase italic shart-gradient">Tokenomics Architecture</h3>
            <p class="text-gray-500 text-sm">Designed for maximum scarcity and long-term holding.</p>
        </div>
        <div class="grid md:grid-cols-4 gap-6">
            <div class="glass p-8 rounded-3xl border-white/5"><h5 class="text-green-400 font-bold uppercase text-[10px] mb-2 tracking-widest">Total Supply</h5><p class="text-2xl font-black">1 Billion</p></div>
            <div class="glass p-8 rounded-3xl border-white/5"><h5 class="text-purple-400 font-bold uppercase text-[10px] mb-2 tracking-widest">Buy/Sell Tax</h5><p class="text-2xl font-black">Zero</p></div>
            <div class="glass p-8 rounded-3xl border-white/5"><h5 class="text-sky-400 font-bold uppercase text-[10px] mb-2 tracking-widest">Security</h5><p class="text-2xl font-black italic">Renounced</p></div>
            <div class="glass p-8 rounded-3xl border-white/5"><h5 class="text-yellow-400 font-bold uppercase text-[10px] mb-2 tracking-widest">Liquidity</h5><p class="text-2xl font-black uppercase italic">Burnt</p></div>
        </div>
    </section>

    <section id="roadmap" class="py-32 bg-white/[0.01]">
        <div class="max-w-4xl mx-auto px-6">
            <h3 class="text-4xl font-black font-heading mb-20 uppercase italic text-center">Expansion Roadmap</h3>
            <div class="space-y-20">
                <div class="roadmap-item relative pl-12"><div class="absolute left-[-5px] top-1 w-3 h-3 bg-green-400 rounded-full glow"></div><h4 class="text-green-400 font-bold uppercase text-sm mb-4 tracking-widest">Phase 01: The Initial Leak</h4></div>
                <div class="roadmap-item relative pl-12 opacity-40"><div class="absolute left-[-5px] top-1 w-3 h-3 bg-gray-500 rounded-full"></div><h4 class="text-white font-bold uppercase text-sm mb-4 tracking-widest">Phase 02: Pressure Wave</h4></div>
            </div>
        </div>
    </section>

    <section id="swap" class="py-32 px-6 max-w-7xl mx-auto border-t border-white/5">
        <div class="grid lg:grid-cols-2 gap-20 items-center">
            <div class="space-y-6">
                <h2 class="text-5xl font-black font-heading uppercase italic shart-gradient">On-Site Terminal</h2>
                <div class="p-4 glass rounded-2xl border-white/10 font-mono text-[10px] text-green-400 truncate tracking-widest">MINT: t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump</div>
            </div>
            <div id="jupiter-terminal"></div>
        </div>
    </section>

    <script>
        const CA = "t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump";
        const RPC = "https://mainnet.helius-rpc.com/?api-key=b4f863b0-2443-499c-bc1c-c612f8d7c249";

        // --- 2. THE IRONCLAD PROVIDER DETECTOR ---
        function getProvider() {
            if ("phantom" in window) {
                const provider = window.phantom?.solana;
                if (provider?.isPhantom) return provider;
            }
            if ("solana" in window) return window.solana;
            return null;
        }

        // Initialize Jupiter
        window.onload = () => {
            setTimeout(() => {
                if (window.Jupiter) {
                    window.Jupiter.init({
                        displayMode: "integrated",
                        integratedTargetId: "jupiter-terminal",
                        endpoint: RPC,
                        strictTokenList: false,
                        formProps: { initialOutputMint: CA, fixedOutputMint: true },
                    });
                }
            }, 1000);
        };

        // --- 3. UNIFIED BUTTON LOGIC ---
        async function handleConnect() {
            const provider = getProvider();
            
            // Mobile Redirect Logic
            if (!provider && /iPhone|iPad|iPod|Android/i.test(navigator.userAgent)) {
                const url = window.location.href.replace(/^https?:\/\//, "");
                window.location.href = `https://phantom.app/ul/browse/https://${url}`;
                return;
            }

            if (!provider) {
                alert("Phantom Wallet not found! Install it or open this site in the Phantom App browser.");
                return;
            }

            try {
                const resp = await provider.connect();
                const wallet = resp.publicKey.toString();
                
                // Update UI
                document.getElementById('walletAddr').innerText = wallet.slice(0,8) + "..." + wallet.slice(-4);
                document.getElementById('navSyncBtn').innerText = "DASHBOARD ACTIVE";

                // Fetch Balance
                const connection = new solanaWeb3.Connection(RPC, "confirmed");
                const mintPubkey = new solanaWeb3.PublicKey(CA);
                const ownerPubkey = new solanaWeb3.PublicKey(wallet);

                const accounts = await connection.getParsedTokenAccountsByOwner(
                    ownerPubkey, 
                    { mint: mintPubkey }
                );
                
                if (accounts.value.length > 0) {
                    const amount = accounts.value[0].account.data.parsed.info.tokenAmount.uiAmount;
                    document.getElementById('tokenBalance').innerText = Math.floor(amount).toLocaleString();
                } else {
                    document.getElementById('tokenBalance').innerText = "0";
                }
            } catch (err) {
                console.error("Connection failed:", err);
            }
        }
    </script>
</body>
</html>
