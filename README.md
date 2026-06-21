<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Prime Solutions Demo Trading</title>

<script src="https://unpkg.com/lightweight-charts/dist/lightweight-charts.standalone.production.js"></script>

<style>
*{
margin:0;
padding:0;
box-sizing:border-box;
font-family:Segoe UI,sans-serif;
}

:root{
--bg:#0b0e11;
--card:#1e2329;
--accent:#f0b90b;
--text:#eaecef;
--green:#0ecb81;
--red:#f6465d;
}

body{
background:var(--bg);
color:var(--text);
padding-bottom:80px;
}

.hidden{
display:none;
}

.navbar{
background:var(--card);
padding:15px;
display:flex;
justify-content:space-between;
align-items:center;
border-bottom:1px solid #333;
position:sticky;
top:0;
z-index:100;
}

.logo{
font-size:20px;
font-weight:bold;
color:var(--accent);
}

.balance-box{
font-weight:bold;
}

.screen{
padding:15px;
}

.card{
background:var(--card);
padding:15px;
border-radius:15px;
margin-bottom:15px;
}

input,select{
width:100%;
padding:12px;
margin-top:10px;
border:none;
border-radius:10px;
background:#2b3139;
color:white;
}

button{
border:none;
cursor:pointer;
}

.btn{
width:100%;
padding:12px;
margin-top:12px;
border-radius:10px;
font-weight:bold;
background:var(--accent);
color:black;
}

.btn-buy{
background:var(--green);
color:white;
}

.btn-sell{
background:var(--red);
color:white;
}

.stats{
display:grid;
grid-template-columns:1fr 1fr;
gap:10px;
}

.stat{
background:#2b3139;
padding:15px;
border-radius:10px;
text-align:center;
}

#chart{
width:100%;
height:300px;
margin-top:10px;
}

.coin-card{
background:var(--card);
padding:15px;
border-radius:12px;
margin-bottom:10px;
display:flex;
justify-content:space-between;
align-items:center;
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
border-top:1px solid #333;
}

.nav-btn{
cursor:pointer;
font-size:14px;
}

.history-item{
padding:10px;
background:#2b3139;
border-radius:10px;
margin-bottom:8px;
}

.login-box{
max-width:400px;
margin:auto;
padding-top:100px;
}

h2{
margin-bottom:10px;
}
</style>
</head>
<body>

<!-- LOGIN -->

<div id="loginScreen" class="screen">

<div class="login-box card">

<h2>Prime Solutions</h2>

<input type="text" id="username" placeholder="Username">

<input type="password" id="password" placeholder="Password">

<button class="btn" onclick="login()">Login / Register</button>

</div>

</div>

<!-- APP -->

<div id="app" class="hidden">

<div class="navbar">
<div class="logo">PRIME SOLUTIONS</div>
<div class="balance-box">
$<span id="balance">10000</span>
</div>
</div>

<div id="homePage" class="screen">

<div class="stats">

<div class="stat">
<h3>$<span id="portfolioValue">10000</span></h3>
<small>Portfolio</small>
</div>

<div class="stat">
<h3 id="profitLoss">$0</h3>
<small>P/L</small>
</div>

</div>

<div class="card">
<h3>Live Chart</h3>
<div id="chart"></div>
</div>

<div class="card">
<h3>Quick Trade</h3>

<select id="tradeCoin">
<option value="bitcoin">BTC</option>
<option value="ethereum">ETH</option>
<option value="solana">SOL</option>
<option value="binancecoin">BNB</option>
<option value="ripple">XRP</option>
</select>

<input type="number" id="tradeAmount" placeholder="Amount USD">

<button class="btn-buy btn" onclick="buyCoin()">BUY</button>

<button class="btn-sell btn" onclick="sellCoin()">SELL</button>

</div>

</div>

<div id="marketPage" class="screen hidden">

<h2>Markets</h2>

<div id="marketList"></div>

</div>

<div id="portfolioPage" class="screen hidden">

<h2>Portfolio</h2>

<div id="portfolioList"></div>

</div>

<div id="historyPage" class="screen hidden">

<h2>Trade History</h2>

<div id="historyList"></div>

</div>

<div class="bottom-nav">

<div class="nav-btn" onclick="showPage('homePage')">
🏠 Home
</div>

<div class="nav-btn" onclick="showPage('marketPage')">
📈 Markets
</div>

<div class="nav-btn" onclick="showPage('portfolioPage')">
💼 Portfolio
</div>

<div class="nav-btn" onclick="showPage('historyPage')">
📜 History
</div>

</div>

</div>

<script>

let user =
JSON.parse(localStorage.getItem("demoUser"));

let balance = 10000;
let portfolio = {};
let history = [];

function login(){

const username =
document.getElementById("username").value;

if(!username){
alert("Enter username");
return;
}

if(!user){

user = {
username,
balance:10000,
portfolio:{},
history:[]
};

localStorage.setItem(
"demoUser",
JSON.stringify(user)
);

}

balance=user.balance;
portfolio=user.portfolio;
history=user.history;

document.getElementById("loginScreen")
.classList.add("hidden");

document.getElementById("app")
.classList.remove("hidden");

document.getElementById("balance")
.innerText=balance.toFixed(2);

loadHistory();
loadPortfolio();
createChart();
loadMarkets();

}

if(user){
login();
}
const coinMap = {
bitcoin:"BTC",
ethereum:"ETH",
solana:"SOL",
binancecoin:"BNB",
ripple:"XRP"
};

let marketData = {};

function saveUser(){

user.balance = balance;
user.portfolio = portfolio;
user.history = history;

localStorage.setItem(
"demoUser",
JSON.stringify(user)
);

}

function showPage(id){

document
.querySelectorAll(".screen")
.forEach(el=>{

if(
el.id!=="loginScreen"
){
el.classList.add("hidden");
}

});

document
.getElementById(id)
.classList.remove("hidden");

}

async function loadMarkets(){

try{

const res = await fetch(
"https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&ids=bitcoin,ethereum,solana,binancecoin,ripple"
);

const data = await res.json();

marketData = {};

data.forEach(c=>{
marketData[c.id]=c;
});

const marketList =
document.getElementById("marketList");

marketList.innerHTML="";

data.forEach(c=>{

marketList.innerHTML += `

<div class="coin-card">

<div>

<b>${c.symbol.toUpperCase()}</b>

<br>

<small>
$${c.current_price.toLocaleString()}
</small>

</div>

<div style="
color:${
c.price_change_percentage_24h>=0
?
'#0ecb81'
:
'#f6465d'
};
font-weight:bold;
">

${c.price_change_percentage_24h.toFixed(2)}%

</div>

</div>

`;

});

updatePortfolioValue();

}
catch(err){

console.log(err);

}

}

function buyCoin(){

const coin =
document.getElementById("tradeCoin").value;

const amount =
parseFloat(
document.getElementById("tradeAmount").value
);

if(
!amount ||
amount<=0
){
alert("Enter amount");
return;
}

if(
amount>balance
){
alert("Insufficient balance");
return;
}

const price =
marketData[coin]?.current_price;

if(!price){
alert("Market loading...");
return;
}

const qty =
amount/price;

if(!portfolio[coin]){

portfolio[coin]={
qty:0,
avg:price
};

}

portfolio[coin].qty += qty;

portfolio[coin].avg = price;

balance -= amount;

history.unshift({

type:"BUY",
coin,
amount,
qty,
price,
date:new Date()
.toLocaleString()

});

saveUser();

refreshUI();

alert(
`${coinMap[coin]} Purchased`
);

}

function sellCoin(){

const coin =
document.getElementById("tradeCoin").value;

const amount =
parseFloat(
document.getElementById("tradeAmount").value
);

if(
!portfolio[coin]
){
alert("No Holdings");
return;
}

const price =
marketData[coin]?.current_price;

const qty =
amount/price;

if(
qty >
portfolio[coin].qty
){
alert("Not enough coins");
return;
}

portfolio[coin].qty -= qty;

if(
portfolio[coin].qty<=0
){
delete portfolio[coin];
}

balance += amount;

history.unshift({

type:"SELL",
coin,
amount,
qty,
price,
date:new Date()
.toLocaleString()

});

saveUser();

refreshUI();

alert(
`${coinMap[coin]} Sold`
);

}

function refreshUI(){

document
.getElementById("balance")
.innerText =
balance.toFixed(2);

loadPortfolio();

loadHistory();

updatePortfolioValue();

saveUser();

}

function loadPortfolio(){

const box =
document.getElementById(
"portfolioList"
);

box.innerHTML="";

if(
Object.keys(portfolio)
.length===0
){

box.innerHTML=
"<div class='card'>No Holdings</div>";

return;

}

for(
const coin in portfolio
){

const p =
portfolio[coin];

const current =
marketData[coin]
?
marketData[coin].current_price
:
0;

const value =
p.qty*current;

box.innerHTML += `

<div class="card">

<h3>
${coinMap[coin]}
</h3>

<p>
Quantity:
${p.qty.toFixed(6)}
</p>

<p>
Value:
$${value.toFixed(2)}
</p>

</div>

`;

}

}

function loadHistory(){

const box =
document.getElementById(
"historyList"
);

box.innerHTML="";

if(
history.length===0
){

box.innerHTML=
"<div class='card'>No History</div>";

return;

}

history.forEach(h=>{

box.innerHTML += `

<div class="history-item">

<b>
${h.type}
</b>

-
${coinMap[h.coin]}

<br>

$${h.amount.toFixed(2)}

<br>

<small>
${h.date}
</small>

</div>

`;

});

    }function updatePortfolioValue(){

let total = balance;

for(const coin in portfolio){

if(!marketData[coin]) continue;

total +=
portfolio[coin].qty *
marketData[coin].current_price;

}

document
.getElementById("portfolioValue")
.innerText =
total.toFixed(2);

const pnl =
total - 10000;

const pnlBox =
document.getElementById("profitLoss");

pnlBox.innerText =
(pnl >= 0 ? "+" : "") +
"$" +
pnl.toFixed(2);

pnlBox.style.color =
pnl >= 0
?
"#0ecb81"
:
"#f6465d";

}

function createChart(){

const chart =
LightweightCharts
.createChart(
document.getElementById("chart"),
{
width:window.innerWidth-30,
height:300,
layout:{
background:{
color:"#0b0e11"
},
textColor:"#eaecef"
},
grid:{
vertLines:{
color:"#1e2329"
},
horzLines:{
color:"#1e2329"
}
}
}
);

const series =
chart.addAreaSeries({
lineColor:"#f0b90b",
topColor:"rgba(240,185,11,0.4)",
bottomColor:"rgba(240,185,11,0.05)"
});

const data = [];

let value = 50000;

for(let i=1;i<=100;i++){

value +=
(Math.random()-0.5)
*1500;

data.push({

time:i,
value:value

});

}

series.setData(data);

window.addEventListener(
"resize",
()=>{

chart.applyOptions({

width:
window.innerWidth-30

});

}
);

}

function demoDeposit(){

balance += 1000;

history.unshift({

type:"DEPOSIT",
coin:"bitcoin",
amount:1000,
qty:0,
price:0,
date:new Date()
.toLocaleString()

});

refreshUI();

alert(
"$1000 Demo Added"
);

}

function resetAccount(){

if(
confirm(
"Reset Demo Account?"
)
){

localStorage.removeItem(
"demoUser"
);

location.reload();

}

}

setInterval(()=>{

loadMarkets();

},15000);

setTimeout(()=>{

const home =
document.getElementById(
"homePage"
);

if(home){

home.innerHTML += `

<div class="card">

<h3>
Demo Controls
</h3>

<button
class="btn"
onclick="demoDeposit()">

Add Demo $1000

</button>

<button
class="btn-sell btn"
onclick="resetAccount()">

Reset Account

</button>

</div>

`;

}

},1000);

</script>

</body>
</html>
