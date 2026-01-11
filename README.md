<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ESHART | Ironclad V35</title>
    
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://unpkg.com/@solana/web3.js@1.95.8/lib/index.iife.min.js"></script>
    
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@900&family=Inter:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root { --accent: #14F195; --bg: #010204; }
        body { background-color: var(--bg); color: white; font-family: 'Inter', sans-serif; }
        .font-heading { font-family: 'Orbitron', sans-serif; }
        .shart-gradient { background: linear-gradient(90deg, #9945FF, #14F195); -webkit-background-clip: text; -webkit-text-fill-color: transparent; }
        .glass { background: rgba(255,255,255,0.03); border: 1px solid rgba(255, 255, 255, 0.08); backdrop-filter: blur(12px); }
    </style>
</head>
<body>

    <nav class="fixed top-0 w-full z-[100] glass border-b border-white/5 px-6 py-4 flex justify-between items-center">
        <div class="flex items-center gap-3">
            <img src="https://i.ibb.co/0jdXM3fZ/1767978719058-2.jpg" class="h-10 w-10 rounded-lg">
            <span class="text-xl font-black font-heading shart-gradient uppercase italic">ESHART</span>
        </div>
        <button id="syncBtn" onclick="handleConnect()" class="bg-[#14F195] text-black px-6 py-2 rounded-xl font-black text-[10px] uppercase shadow-lg shadow-green-500/10">Sync Dashboard</button>
    </nav>

    <main class="pt-48 px-6 max-w-7xl mx-auto text-center">
        <h1 class="text-7xl lg:text-9xl font-black font-heading uppercase italic mb-10">ELON <span class="shart-gradient">SHART.</span></h1>
        
        <div class="max-w-md mx-auto glass p-10 rounded-[3rem] border-white/10">
            <p class="text-gray-500 text-[10px] uppercase font-bold mb-4 tracking-widest">Live Portfolio</p>
            <h2 id="tokenBalance" class="text-7xl font-black shart-gradient mb-6 tracking-tighter">0</h2>
            <button onclick="handleConnect()" class="w-full py-5 bg-[#14F195] text-black font-black rounded-2xl uppercase text-xs tracking-widest hover:scale-105 transition">Connect Wallet</button>
            <p id="statusMsg" class="mt-4 text-[8px] text-gray-600 font-mono uppercase">Status: System Standby</p>
        </div>
    </main>

    <script>
        const CA = "t9uEjUYugPdhLv9NHMR3CB6s3HZRM1xbaT2wDKvpump";
        const RPC = "https://mainnet.helius-rpc.com/?api-key=b4f863b0-2443-499c-bc1c-c612f8d7c249";
        
        // --- 1. THE DEEP LINK FIX ---
        function getProvider() {
            if ("phantom" in window) {
                const provider = window.phantom?.solana;
                if (provider?.isPhantom) return provider;
            }
            if ("solana" in window) return window.solana;
            return null;
        }

        async function handleConnect() {
            const status = document.getElementById('statusMsg');
            const provider = getProvider();

            // Check if mobile user is NOT in Phantom browser
            const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
            
            if (!provider && isMobile) {
                status.innerText = "REDIRECTING TO PHANTOM APP...";
                const url = window.location.href.replace(/^https?:\/\//, "");
                window.location.href = `https://phantom.app/ul/browse/https://${url}`;
                return;
            }

            if (!provider) {
                alert("Please install Phantom Wallet extension!");
                window.open("https://phantom.app/", "_blank");
                return;
            }

            try {
                status.innerText = "AUTHENTICATING...";
                const resp = await provider.connect();
                const wallet = resp.publicKey.toString();
                status.innerText = "CONNECTED: " + wallet.slice(0,8) + "...";

                const connection = new solanaWeb3.Connection(RPC, "confirmed");
                const accounts = await connection.getParsedTokenAccountsByOwner(
                    new solanaWeb3.PublicKey(wallet), 
                    { mint: new solanaWeb3.PublicKey(CA) }
                );
                
                if (accounts.value.length > 0) {
                    const amount = accounts.value[0].account.data.parsed.info.tokenAmount.uiAmount;
                    document.getElementById('tokenBalance').innerText = Math.floor(amount).toLocaleString();
                }
                document.getElementById('syncBtn').innerText = "DASHBOARD SYNCED";
            } catch (err) {
                status.innerText = "CONNECTION REFUSED";
                console.error(err);
            }
        }
    </script>
</body>
</html>
