<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ESHART | Official Portal</title>
    
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
        #jupiter-terminal { width: 100%; max-width: 440px; height: 520px; border-radius: 24px; border: 1px solid rgba(255,255,255,0.1); margin: 0 auto; }
    </style>
</head>
<body>

    <nav class="fixed top-0 w-full z-[100] glass border-b border-white/5 px-6 py-4">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <div class="flex items-center gap-3">
                <img src="https://i.ibb.co/0jdXM3fZ/1767978719058-2.jpg" class="h-10 w-10 rounded-lg">
                <span class="text-xl font-black font-heading shart-gradient italic uppercase">ESHART</span>
            </div>
            <button onclick="handleConnect()" class="bg-[#14F195] text-black px-6 py-2 rounded-xl font-black text-[10px] uppercase shadow-lg shadow-green-500/10 hover:scale-105 transition">Sync Dashboard</button>
        </div>
    </nav>

    <section class="pt-48 pb-20 px-6 max-w-7xl mx-auto grid lg:grid-cols-2 gap-20 items-center">
        <div class="space-y-8">
            <h1 class="text-7xl lg:text-9xl font-black font-heading leading-none uppercase italic">ELON <br><span class="shart-gradient">SHART.</span></h1>
            <p class="text-gray-400 text-lg leading-relaxed max-w-lg">Aggressive deflationary meme-ecosystem. 0% Tax. 100% Scarcity.</p>
        </div>

        <div class="glass p-10 rounded-[3rem] border-white/10 text-center relative">
            <p class="text-gray-500 text-[10px] uppercase font-bold mb-4 tracking-widest">Investor Holdings</p>
            <h2 id="tokenBalance" class="text-7xl font-black shart-gradient mb-2">0</h2>
            <div class="p-4 bg-black/40 rounded-2xl border border-white/5 mb-8">
                <p id="walletAddr" class="text-[9px] font-mono text-gray-600 truncate uppercase italic tracking-widest">Wallet Not Linked</p>
            </div>
            <button onclick="handleConnect()" class="w-full py-5 bg-[#14F195] text-black font-black rounded-2xl transition uppercase text-xs tracking-widest">Connect Blockchain</button>
        </div>
    </section>

    <div class="py-20 max-w-7xl mx-auto px-6" id="swap">
        <div id="jupiter-terminal"></div>
    </div>

    <script>
        const CA = "t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump";
        const HELIUS_URL = "https://mainnet.helius-rpc.com/?api-key=b4f863b0-2443-499c-bc1c-c612f8d7c249";

        // 2. DETECT PROVIDER (PHANTOM/SOLFLARE/IN-APP)
        const getProvider = () => {
            if ('phantom' in window) {
                const provider = window.phantom?.solana;
                if (provider?.isPhantom) return provider;
            }
            if ('solana' in window) return window.solana;
            return null;
        };

        // Initialize Jupiter with fallback
        try {
            window.Jupiter.init({
                displayMode: "integrated",
                integratedTargetId: "jupiter-terminal",
                endpoint: HELIUS_URL,
                strictTokenList: false,
                formProps: { initialOutputMint: CA, fixedOutputMint: true },
            });
        } catch (e) { console.error("Jupiter load failed", e); }

        async function handleConnect() {
            const provider = getProvider();
            
            if (!provider) {
                alert("Wallet not found! Please open this site inside the Phantom App browser.");
                window.open("https://phantom.app/", "_blank");
                return;
            }

            try {
                // Connect to Wallet
                const resp = await provider.connect();
                const walletAddress = resp.publicKey.toString();
                console.log("Connected to:", walletAddress);
                
                document.getElementById('walletAddr').innerText = walletAddress.slice(0,6) + "..." + walletAddress.slice(-4);
                
                // Fetch Balance
                const connection = new solanaWeb3.Connection(HELIUS_URL, "confirmed");
                const accounts = await connection.getParsedTokenAccountsByOwner(
                    new solanaWeb3.PublicKey(walletAddress), 
                    { mint: new solanaWeb3.PublicKey(CA) }
                );
                
                if (accounts.value.length > 0) {
                    const amount = accounts.value[0].account.data.parsed.info.tokenAmount.uiAmount;
                    document.getElementById('tokenBalance').innerText = Math.floor(amount).toLocaleString();
                } else {
                    document.getElementById('tokenBalance').innerText = "0";
                }
            } catch (err) {
                console.error("Connection Error:", err);
                if (err.code === 4001) alert("Connection rejected by user.");
            }
        }
    </script>
</body>
</html>
