<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PrimeX Demo Trading</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">

<style>

*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:'Poppins',sans-serif;
}

:root{
--bg:#0b0f19;
--card:#141b2d;
--card2:#1b2338;
--accent:#f0b90b;
--green:#0ecb81;
--red:#f6465d;
--text:#ffffff;
--muted:#a9b1c7;
}

body{
background:var(--bg);
color:var(--text);
padding-bottom:80px;
}

.hidden{
display:none;
}

.login-screen{
min-height:100vh;
display:flex;
justify-content:center;
align-items:center;
padding:20px;
}

.login-card{
width:100%;
max-width:400px;
background:var(--card);
padding:25px;
border-radius:20px;
}

.logo{
font-size:32px;
font-weight:700;
color:var(--accent);
text-align:center;
margin-bottom:10px;
}

.subtitle{
text-align:center;
color:var(--muted);
margin-bottom:25px;
}

input{
width:100%;
padding:14px;
margin-bottom:12px;
background:var(--card2);
border:none;
border-radius:12px;
color:white;
}

.btn{
width:100%;
padding:14px;
border:none;
border-radius:12px;
background:var(--accent);
font-weight:700;
cursor:pointer;
}

.navbar{
padding:15px;
background:var(--card);
display:flex;
justify-content:space-between;
align-items:center;
position:sticky;
top:0;
z-index:100;
}

.balance{
font-weight:700;
font-size:18px;
}

.page{
padding:15px;
}

.hero{
background:linear-gradient(135deg,#f0b90b,#ffda63);
color:black;
padding:20px;
border-radius:20px;
margin-bottom:15px;
}

.hero h2{
font-size:28px;
}

.stats{
display:grid;
grid-template-columns:1fr 1fr;
gap:12px;
margin-bottom:15px;
}

.stat{
background:var(--card);
padding:20px;
border-radius:18px;
text-align:center;
}

.stat h2{
margin-bottom:8px;
}

.card{
background:var(--card);
padding:15px;
border-radius:18px;
margin-bottom:15px;
}

.card-title{
margin-bottom:12px;
font-size:18px;
font-weight:600;
}

.search{
margin-bottom:15px;
}

.search input{
margin:0;
}

.coin{
display:flex;
justify-content:space-between;
align-items:center;
padding:14px;
background:var(--card2);
border-radius:14px;
margin-bottom:10px;
}

.coin-left{
display:flex;
align-items:center;
gap:10px;
}

.coin-icon{
width:42px;
height:42px;
border-radius:50%;
background:#2a3553;
display:flex;
align-items:center;
justify-content:center;
font-size:20px;
}

.green{
color:var(--green);
}

.red{
color:var(--red);
}

.bottom-nav{
position:fixed;
bottom:0;
left:0;
width:100%;
height:65px;
background:var(--card);
display:flex;
justify-content:space-around;
align-items:center;
}

.nav-item{
cursor:pointer;
font-size:14px;
}

</style>
</head>
<body>

<div id="loginScreen" class="login-screen">

<div class="login-card">

<div class="logo">PrimeX</div>

<div class="subtitle">
Demo Crypto Trading Platform
</div>

<input type="text" id="username" placeholder="Username">

<input type="password" id="password" placeholder="Password">

<button class="btn" onclick="loginUser()">
ENTER PLATFORM
</button>

</div>

</div>

<div id="app" class="hidden">

<div class="navbar">

<h2>PrimeX</h2>

<div class="balance">
$<span id="balance">10000</span>
</div>

</div>

<div id="homePage" class="page">

<div class="hero">

<h2>Demo Account</h2>

<p>
Trade crypto with virtual funds.
</p>

</div>

<div class="stats">

<div class="stat">
<h2 id="portfolioValue">$10000</h2>
<p>Portfolio</p>
</div>

<div class="stat">
<h2 id="profitLoss" class="green">
+$0
</h2>
<p>P/L</p>
</div>

</div>

<div class="card">

<div class="card-title">
🔥 Top Gainers
</div>

<div id="topGainers">
Loading...
</div>

</div>

<div class="card">

<div class="card-title">
📊 Market Overview
</div>

<div id="marketPreview">
Loading...
</div>

</div>

</div>

<div id="marketsPage" class="page hidden">

<div class="search">
<input type="text" placeholder="Search Coin">
</div>

<div id="marketList"></div>

</div>

<div id="portfolioPage" class="page hidden">

<div class="card-title">
💼 Portfolio
</div>

<div id="portfolioList"></div>

</div>

<div id="historyPage" class="page hidden">

<div class="card-title">
📜 Trade History
</div>

<div id="historyList"></div>

</div>

<div class="bottom-nav">

<div class="nav-item" onclick="showPage('homePage')">
🏠 Home
</div>

<div class="nav-item" onclick="showPage('marketsPage')">
📈 Markets
</div>

<div class="nav-item" onclick="showPage('portfolioPage')">
💼 Portfolio
</div>

<div class="nav-item" onclick="showPage('historyPage')">
📜 History
</div>

</div>

</div>

<script>

let balance = 10000;
let portfolio = {};
let history = [];

function loginUser(){

const user =
document.getElementById("username").value;

if(!user){
alert("Enter Username");
return;
}

document.getElementById("loginScreen")
.classList.add("hidden");

document.getElementById("app")
.classList.remove("hidden");

}

function showPage(id){

[
"homePage",
"marketsPage",
"portfolioPage",
"historyPage"
].forEach(page=>{

document
.getElementById(page)
.classList.add("hidden");

});

document
.getElementById(id)
.classList.remove("hidden");

}

</script>const API =
"https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=bitcoin,ethereum,binancecoin,solana,ripple&order=market_cap_desc";

let marketData = [];

async function loadMarkets(){

try{

const res = await fetch(API);
const data = await res.json();

marketData = data;

renderMarkets();
renderTopGainers();

}catch(err){

console.log(err);

}

}

function renderTopGainers(){

const box =
document.getElementById(
"topGainers"
);

const sorted =
[...marketData]
.sort(
(a,b)=>
b.price_change_percentage_24h -
a.price_change_percentage_24h
);

box.innerHTML="";

sorted.slice(0,3)
.forEach(c=>{

box.innerHTML += `

<div class="coin">

<div class="coin-left">

<div class="coin-icon">
🚀
</div>

<div>

<b>
${c.symbol.toUpperCase()}
</b>

<br>

<small>
$${c.current_price}
</small>

</div>

</div>

<div class="green">

+${c.price_change_percentage_24h
.toFixed(2)}%

</div>

</div>

`;

});

}

function renderMarkets(){

const list =
document.getElementById(
"marketList"
);

const preview =
document.getElementById(
"marketPreview"
);

list.innerHTML="";
preview.innerHTML="";

marketData.forEach(c=>{

const card = `

<div class="coin">

<div class="coin-left">

<div class="coin-icon">
💰
</div>

<div>

<b>
${c.name}
</b>

<br>

<small>
${c.symbol.toUpperCase()}
</small>

</div>

</div>

<div>

<div>
$${c.current_price}
</div>

<div class="${
c.price_change_percentage_24h >=0
?
'green'
:
'red'
}">
${c.price_change_percentage_24h
.toFixed(2)}%
</div>

</div>

</div>

`;

list.innerHTML += card;

});

marketData
.slice(0,3)
.forEach(c=>{

preview.innerHTML += `

<div class="coin">

<div>
${c.symbol.toUpperCase()}
</div>

<div>
$${c.current_price}
</div>

</div>

`;

});

}

function updateBalance(){

document
.getElementById("balance")
.innerText =
balance.toFixed(2);

}

function updatePortfolio(){

const box =
document.getElementById(
"portfolioList"
);

box.innerHTML="";

let totalValue = balance;

for(const coin in portfolio){

const market =
marketData.find(
c=>c.id===coin
);

if(!market) continue;

const value =
portfolio[coin].qty *
market.current_price;

totalValue += value;

box.innerHTML += `

<div class="card">

<h3>
${market.symbol.toUpperCase()}
</h3>

<p>
Qty:
${portfolio[coin].qty
.toFixed(5)}
</p>

<p>
Value:
$${value.toFixed(2)}
</p>

</div>

`;

}

document
.getElementById(
"portfolioValue"
)
.innerText =
"$" +
totalValue.toFixed(2);

const pnl =
totalValue - 10000;

const pnlBox =
document.getElementById(
"profitLoss"
);

pnlBox.innerText =
(pnl>=0?"+":"")
+
"$"
+
pnl.toFixed(2);

pnlBox.className =
pnl>=0
?
"green"
:
"red";

}

function saveTrade(
type,
coin,
amount
){

history.unshift({

type,
coin,
amount,
date:new Date()
.toLocaleString()

});

renderHistory();

}

function renderHistory(){

const box =
document.getElementById(
"historyList"
);

box.innerHTML="";

if(history.length===0){

box.innerHTML=
"<div class='card'>No Trades Yet</div>";

return;

}

history.forEach(h=>{

box.innerHTML += `

<div class="card">

<b>
${h.type}
</b>

<br>

${h.coin}

<br>

$${h.amount}

<br>

<small>
${h.date}
</small>

</div>

`;

});

}

loadMarkets();

setInterval(
loadMarkets,
15000
);function buyCoin(coinId){

const amount =
parseFloat(
prompt("Enter USD Amount")
);

if(
!amount ||
amount<=0
){
return;
}

if(
amount > balance
){
alert("Insufficient Balance");
return;
}

const coin =
marketData.find(
c=>c.id===coinId
);

if(!coin){
return;
}

const qty =
amount /
coin.current_price;

if(!portfolio[coinId]){

portfolio[coinId]={
qty:0
};

}

portfolio[coinId].qty += qty;

balance -= amount;

saveTrade(
"BUY",
coin.symbol.toUpperCase(),
amount
);

updateBalance();
updatePortfolio();
saveData();

alert(
"Trade Executed Successfully"
);

}

function sellCoin(coinId){

if(
!portfolio[coinId]
){
alert("No Holdings");
return;
}

const amount =
parseFloat(
prompt("Enter USD Amount")
);

if(
!amount ||
amount<=0
){
return;
}

const coin =
marketData.find(
c=>c.id===coinId
);

if(!coin){
return;
}

const qty =
amount /
coin.current_price;

if(
qty >
portfolio[coinId].qty
){
alert("Not Enough Holdings");
return;
}

portfolio[coinId].qty -= qty;

if(
portfolio[coinId].qty <= 0
){
delete portfolio[coinId];
}

balance += amount;

saveTrade(
"SELL",
coin.symbol.toUpperCase(),
amount
);

updateBalance();
updatePortfolio();
saveData();

alert(
"Sell Order Completed"
);

}

function renderMarkets(){

const list =
document.getElementById(
"marketList"
);

const preview =
document.getElementById(
"marketPreview"
);

list.innerHTML="";
preview.innerHTML="";

marketData.forEach(c=>{

list.innerHTML += `

<div class="coin">

<div class="coin-left">

<div class="coin-icon">
💰
</div>

<div>

<b>
${c.name}
</b>

<br>

<small>
${c.symbol.toUpperCase()}
</small>

</div>

</div>

<div>

<div>
$${c.current_price}
</div>

<div class="${
c.price_change_percentage_24h>=0
?
'green'
:
'red'
}">
${c.price_change_percentage_24h.toFixed(2)}%
</div>

<button
onclick="buyCoin('${c.id}')"
style="
margin-top:6px;
padding:6px 10px;
border:none;
border-radius:8px;
background:#0ecb81;
color:white;
cursor:pointer;
">
Buy
</button>

<button
onclick="sellCoin('${c.id}')"
style="
margin-top:6px;
padding:6px 10px;
border:none;
border-radius:8px;
background:#f6465d;
color:white;
cursor:pointer;
">
Sell
</button>

</div>

</div>

`;

});

marketData
.slice(0,3)
.forEach(c=>{

preview.innerHTML += `

<div class="coin">

<div>
${c.symbol.toUpperCase()}
</div>

<div>
$${c.current_price}
</div>

</div>

`;

});

}

function demoDeposit(){

balance += 1000;

saveTrade(
"DEPOSIT",
"USD",
1000
);

updateBalance();
updatePortfolio();
saveData();

alert(
"$1000 Added"
);

}

function saveData(){

localStorage.setItem(
"primex_balance",
balance
);

localStorage.setItem(
"primex_portfolio",
JSON.stringify(
portfolio
)
);

localStorage.setItem(
"primex_history",
JSON.stringify(
history
)
);

}

function loadData(){

balance =
parseFloat(
localStorage.getItem(
"primex_balance"
)
) || 10000;

portfolio =
JSON.parse(
localStorage.getItem(
"primex_portfolio"
)
) || {};

history =
JSON.parse(
localStorage.getItem(
"primex_history"
)
) || [];

updateBalance();
renderHistory();

}

function resetAccount(){

if(
confirm(
"Reset Account?"
)
){

localStorage.clear();

location.reload();

}

}

window.onload=()=>{

loadData();

setTimeout(()=>{

const home =
document.getElementById(
"homePage"
);

home.innerHTML += `

<div class="card">

<div class="card-title">
⚙ Demo Controls
</div>

<button
class="btn"
onclick="demoDeposit()">
Add $1000
</button>

<br><br>

<button
class="btn"
style="
background:#f6465d;
color:white;
"
onclick="resetAccount()">
Reset Account
</button>

</div>

`;

},500);

};const searchInput =
document.querySelector(
'.search input'
);

if(searchInput){

searchInput.addEventListener(
'input',
function(){

const value =
this.value
.toLowerCase();

const coins =
document.querySelectorAll(
'#marketList .coin'
);

coins.forEach(card=>{

const text =
card.innerText
.toLowerCase();

card.style.display =
text.includes(value)
?
'flex'
:
'none';

});

}
);

}

function renderTradingStats(){

const home =
document.getElementById(
'homePage'
);

const buys =
history.filter(
x=>x.type==="BUY"
).length;

const sells =
history.filter(
x=>x.type==="SELL"
).length;

const deposits =
history.filter(
x=>x.type==="DEPOSIT"
).length;

home.innerHTML += `

<div class="stats">

<div class="stat">
<h2>${buys}</h2>
<p>Buy Orders</p>
</div>

<div class="stat">
<h2>${sells}</h2>
<p>Sell Orders</p>
</div>

<div class="stat">
<h2>${deposits}</h2>
<p>Deposits</p>
</div>

<div class="stat">
<h2>${history.length}</h2>
<p>Total Activity</p>
</div>

</div>

`;

}

setTimeout(()=>{

renderTradingStats();

},1000);

updateBalance();
updatePortfolio();
renderHistory();

</script>

</body>
</html>
