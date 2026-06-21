import React, { useState, useEffect } from 'react';
import { initializeApp } from "firebase/app";
import { getFirestore, doc, updateDoc, getDoc, addDoc, collection, serverTimestamp, increment } from "firebase/firestore";
import { getAuth, createUserWithEmailAndPassword, signInWithEmailAndPassword, signInWithPopup, GoogleAuthProvider, onAuthStateChanged } from "firebase/auth";

// 1. Firebase Config
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
const auth = getAuth(app);
const provider = new GoogleAuthProvider();

function App() {
  const [user, setUser] = useState(null);
  const [isAdmin, setIsAdmin] = useState(false);
  const [tapCount, setTapCount] = useState(0);

  useEffect(() => {
    onAuthStateChanged(auth, (currentUser) => setUser(currentUser));
  }, []);

  // Admin Tap Logic
  const handleLogoTap = () => {
    const count = tapCount + 1;
    setTapCount(count);
    if (count === 5) {
      const key = prompt("Enter Secret Key:");
      if (key === "5426224") setIsAdmin(true);
      setTapCount(0);
    }
  };

  // Trading Function
  const executeTrade = async (type, amount) => {
    const userRef = doc(db, "users", user.uid);
    const userSnap = await getDoc(userRef);
    if (userSnap.exists()) {
      await updateDoc(userRef, { balance: increment(type === 'BUY' ? -amount : amount) });
      await addDoc(collection(db, "orders"), { uid: user.uid, type, amount, timestamp: serverTimestamp() });
      alert("Trade Successful!");
    }
  };

  return (
    <div style={{ padding: '20px' }}>
      <h1 onClick={handleLogoTap} style={{ cursor: 'pointer' }}>Trading Platform</h1>
      
      {!user ? (
        <div>
          <button onClick={() => signInWithPopup(auth, provider)}>Login with Google</button>
        </div>
      ) : (
        <div>
          <h2>Welcome, {user.email}</h2>
          <button onClick={() => executeTrade('BUY', 100)}>BUY 100</button>
          <button onClick={() => executeTrade('SELL', 100)}>SELL 100</button>
        </div>
      )}

      {isAdmin && <div style={{marginTop: '20px', color: 'red'}}><h3>Admin Panel Active</h3></div>}
    </div>
  );
}

export default App;
