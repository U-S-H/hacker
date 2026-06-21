<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Trading Platform</title>
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js";
        import { getFirestore, doc, getDoc, updateDoc, increment, addDoc, collection, serverTimestamp } from "https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore.js";

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

        // Global functions for buttons
        window.executeTrade = async (type) => {
            const amount = 100; // Default amount
            const uid = "test_user_id"; // Authentication ke baad dynamic hoga
            const userRef = doc(db, "users", uid);
            await updateDoc(userRef, { balance: increment(type === 'BUY' ? -amount : amount) });
            await addDoc(collection(db, "orders"), { uid, type, amount, timestamp: serverTimestamp() });
            alert(type + " Trade Successful!");
        };
    </script>
    <style>
        body { font-family: sans-serif; text-align: center; padding: 20px; }
        button { padding: 10px 20px; margin: 10px; cursor: pointer; }
        #adminPanel { display: none; margin-top: 20px; color: red; border: 1px solid red; padding: 10px; }
    </style>
</head>
<body>

    <h1 id="logo" onclick="handleTap()" style="cursor: pointer;">Trading Platform</h1>
    
    <div id="trading">
        <button onclick="executeTrade('BUY')">BUY</button>
        <button onclick="executeTrade('SELL')">SELL</button>
    </div>

    <div id="adminPanel">
        <h3>Admin Panel Active</h3>
        <p>Pending deposits will appear here.</p>
    </div>

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
