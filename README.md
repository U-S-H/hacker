<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Trading Platform</title>
    <style>
        body { font-family: 'Segoe UI', sans-serif; background: #f4f4f9; text-align: center; padding: 20px; }
        .card { background: white; padding: 20px; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); max-width: 400px; margin: auto; }
        button { padding: 12px 20px; margin: 10px; border: none; border-radius: 5px; cursor: pointer; color: white; font-weight: bold; }
        .buy { background: #28a745; }
        .sell { background: #dc3545; }
        #adminPanel { display: none; margin-top: 20px; color: #d9534f; border: 2px dashed #d9534f; padding: 15px; }
    </style>
</head>
<body>

    <h1 id="logo" onclick="handleTap()" style="cursor: pointer;">Trading Platform</h1>
    
    <div class="card" id="trading">
        <h3>Balance: $<span id="balance">0</span></h3>
        <button class="buy" onclick="executeTrade('BUY')">BUY</button>
        <button class="sell" onclick="executeTrade('SELL')">SELL</button>
    </div>

    <div id="adminPanel" class="card">
        <h3>Admin Access Active</h3>
        <p>Pending Database Records Management.</p>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
        import { getFirestore, doc, getDoc, updateDoc, increment, addDoc, collection } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

        const firebaseConfig = {
            apiKey: "AIzaSyCsgXPW-h2NzAHMrDBIL_HjlU8wSpcgzvI",
            authDomain: "course-3cc77.firebaseapp.com",
            projectId: "course-3cc77",
            storageBucket: "course-3cc77.firebasestorage.app",
            messagingSenderId: "136140432667",
            appId: "1:136140432667:web:9f543dc3db8683944ddfbe"
        };

        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);

        // Trade Execution Function
        window.executeTrade = async (type) => {
            const uid = "test_user_id"; // Aap ise dynamic kar sakte hain
            const userRef = doc(db, "users", uid);
            const amount = 100;
            
            await updateDoc(userRef, { balance: increment(type === 'BUY' ? -amount : amount) });
            await addDoc(collection(db, "orders"), { uid, type, amount, status: 'SUCCESS' });
            alert(type + " order placed successfully!");
        };
    </script>

    <script>
        let tapCount = 0;
        function handleTap() {
            tapCount++;
            if (tapCount === 5) {
                let key = prompt("Enter Secret Key:");
                if (key === "5426224") {
                    document.getElementById('adminPanel').style.display = 'block';
                }
                tapCount = 0;
            }
        }
    </script>
</body>
</html>
