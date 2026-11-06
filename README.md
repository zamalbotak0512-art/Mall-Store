<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MALL STORE - Game Store</title>
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:Arial,sans-serif;background:#090b14;color:white}
header{height:75px;background:#101321;display:flex;align-items:center;justify-content:space-between;padding:0 7%;border-bottom:1px solid #292d40;position:sticky;top:0;z-index:10}
.logo{font-size:24px;font-weight:900;color:#a78bfa}
.logo span{color:#fff}
nav{display:flex;gap:25px}
nav a{color:#c6c8d5;text-decoration:none;font-size:14px}
nav a:hover{color:#a78bfa}
.btn{background:#7957f5;color:white;border:0;padding:12px 20px;border-radius:9px;cursor:pointer;font-weight:bold}
.container{max-width:1150px;margin:auto;padding:35px 20px}
.hero{padding:55px 40px;border-radius:20px;background:linear-gradient(120deg,#25165d,#171e48,#101321);border:1px solid #38305f}
.hero h1{font-size:42px;margin-bottom:15px}
.hero h1 span{color:#a78bfa}
.hero p{color:#c1bfd6;line-height:1.7;max-width:550px}
.hero .btn{margin-top:25px}
.section-title{font-size:23px;margin:35px 0 20px}
.search{width:100%;padding:15px;background:#151827;border:1px solid #30354c;border-radius:10px;color:white;margin-bottom:20px;outline:none}
.games{display:grid;grid-template-columns:repeat(4,1fr);gap:18px}
.game{background:#151827;border:1px solid #292e43;border-radius:14px;overflow:hidden;cursor:pointer;transition:.2s}
.game:hover{transform:translateY(-5px);border-color:#987bff}
.game img{width:100%;height:140px;object-fit:cover}
.game-info{padding:15px}
.game-info h3{font-size:15px;margin-bottom:6px}
.game-info p{font-size:12px;color:#969bad}
.tag{color:#b8a4ff;font-size:11px;margin-top:10px;display:block}
.panel{display:none;background:#151827;border:1px solid #30354c;padding:25px;border-radius:15px;margin-top:30px}
.panel h2{margin-bottom:20px}
label{display:block;color:#c5c7d4;font-size:13px;margin:15px 0 8px}
input,select{width:100%;padding:13px;background:#0d1020;border:1px solid #343951;border-radius:8px;color:white;outline:none}
.products{display:grid;grid-template-columns:repeat(3,1fr);gap:12px}
.product{padding:16px 10px;border:1px solid #363b52;border-radius:10px;background:#101321;color:white;cursor:pointer;text-align:center}
.product small{display:block;color:#a3a6b7;margin-top:8px}
.product.active{border:2px solid #987bff;background:#29204d}
.payment{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.payment button{padding:15px;border-radius:9px;border:1px solid #343951;background:#101321;color:white;cursor:pointer}
.payment button.active{border:2px solid #987bff;background:#29204d}
.summary{background:#0d1020;padding:18px;border-radius:10px;margin:20px 0;line-height:2;color:#c7c9d5}
.summary strong{color:white}
footer{text-align:center;padding:35px;color:#85899b;border-top:1px solid #292d40;margin-top:60px;font-size:13px}
.notice{color:#a9a2c9;font-size:12px;line-height:1.7;margin-top:15px}
@media(max-width:750px){
header{padding:0 4%}nav{gap:10px}nav a{font-size:11px}
.games{grid-template-columns:repeat(2,1fr)}
.hero h1{font-size:30px}.hero{padding:35px 23px}
.products{grid-template-columns:repeat(2,1fr)}
.payment{grid-template-columns:repeat(2,1fr)}
}
</style>
</head>
<body>

<header>
 <div class="logo">NEXORA<span> TOPUP</span></div>
 <nav>
  <a href="#">Beranda</a>
  <a href="#games">Daftar Game</a>
  <a href="#transaksi">Top Up</a>
 </nav>
 <button class="btn" onclick="document.getElementById('games').scrollIntoView()">Top Up</button>
</header>

<main class="container">
 <section class="hero">
  <h1>TOP UP GAME <span>MUDAH & CEPAT!</span></h1>
  <p>Tempat top up game favorit kamu dengan proses praktis, pilihan nominal lengkap, dan pengalaman belanja yang nyaman.</p>
  <button class="btn" onclick="document.getElementById('games').scrollIntoView()">Mulai Top Up →</button>
 </section>

 <section id="games">
  <h2 class="section-title">🔥 Game Populer</h2>
  <input class="search" id="search" placeholder="Cari game favorit kamu..." oninput="searchGame()">
  <div class="games" id="gameList"></div>
 </section>

 <section class="panel" id="transaksi">
  <h2 id="selectedGame">Top Up Game</h2>
  <p style="color:#999;font-size:13px">Lengkapi informasi akun dan pilih nominal yang ingin dibeli.</p>

  <label>User ID</label>
  <input id="userId" placeholder="Masukkan User ID">

  <label>Zone ID / Server (jika diperlukan)</label>
  <input id="zoneId" placeholder="Masukkan Zone ID (opsional)">

  <h3 style="margin:25px 0 15px">Pilih Nominal</h3>
  <div class="products" id="productList"></div>

  <h3 style="margin:25px 0 15px">Metode Pembayaran</h3>
  <div class="payment" id="paymentList">
   <button onclick="choosePayment(this,'QRIS')">QRIS</button>
   <button onclick="choosePayment(this,'DANA')">DANA</button>
   <button onclick="choosePayment(this,'GoPay')">GoPay</button>
   <button onclick="choosePayment(this,'OVO')">OVO</button>
   <button onclick="choosePayment(this,'Transfer Bank')">Transfer Bank</button>
   <button onclick="choosePayment(this,'ShopeePay')">ShopeePay</button>
  </div>

  <div class="summary">
   <div>Game: <strong id="sumGame">-</strong></div>
   <div>Produk: <strong id="sumProduct">-</strong></div>
   <div>Harga: <strong id="sumPrice">Rp0</strong></div>
   <div>Pembayaran: <strong id="sumPayment">-</strong></div>
   <hr style="border-color:#343951;margin:10px 0">
   <div>Total: <strong id="sumTotal" style="color:#b69aff">Rp0</strong></div>
  </div>
  <button class="btn" style="width:100%" onclick="checkout()">Buat Pesanan Sekarang</button>
  <p class="notice">Demo frontend: pembayaran belum terhubung dengan payment gateway. Jangan mengirimkan pembayaran sungguhan melalui halaman demo ini.</p>
 </section>

 <section class="panel" id="result">
  <h2>Pesanan Berhasil Dibuat!</h2>
  <div class="summary" id="orderDetail"></div>
  <button class="btn" onclick="document.getElementById('games').scrollIntoView()">Kembali ke Beranda</button>
 </section>
</main>

<footer>
 <h3 style="color:#a78bfa;margin-bottom:10px">NEXORA TOPUP</h3>
 <p>Platform Top Up Game | Cepat, Aman, dan Praktis</p>
 <p style="margin-top:12px">© 2026 NEXORA TOPUP. All Rights Reserved.</p>
</footer>

<script>
const games=[
 {name:"Mobile Legends",category:"MOBA",emoji:"⚔️",color:"linear-gradient(135deg,#172c59,#4789cc)",items:[["86 Diamonds",20000],["172 Diamonds",39000],["257 Diamonds",58000],["344 Diamonds",77000],["514 Diamonds",115000],["706 Diamonds",155000]]},
 {name:"Free Fire",category:"Battle Royale",emoji:"🔥",color:"linear-gradient(135deg,#63220e,#e77c24)",items:[["70 Diamonds",10000],["140 Diamonds",20000],["355 Diamonds",49000],["720 Diamonds",95000],["1450 Diamonds",190000],["2180 Diamonds",280000]]},
 {name:"PUBG Mobile",category:"Battle Royale",emoji:"🎯",color:"linear-gradient(135deg,#4c3713,#c29a45)",items:[["60 UC",16000],["325 UC",79000],["660 UC",159000],["1800 UC",399000],["3850 UC",799000],["8100 UC",1599000]]},
 {name:"Genshin Impact",category:"RPG",emoji:"✨",color:"linear-gradient(135deg,#293f61,#8c9fd4)",items:[["60 Genesis Crystals",16000],["300 + 30 Crystals",79000],["980 + 110 Crystals",249000],["1980 + 260 Crystals",479000]]},
 {name:"Honor of Kings",category:"MOBA",emoji:"👑",color:"linear-gradient(135deg,#402b17,#d9a34c)",items:[["80 Tokens",15000],["240 Tokens",45000],["400 Tokens",75000],["800 Tokens",149000]]},
 {name:"Valorant",category:"FPS",emoji:"🔫",color:"linear-gradient(135deg,#4a171e,#e44b60)",items:[["125 VP",15000],["420 VP",50000],["700 VP",80000],["1375 VP",150000]]},
 {name:"Roblox",category:"Sandbox",emoji:"🧱",color:"linear-gradient(135deg,#252525,#777777)",items:[["80 Robux",16000],["400 Robux",79000],["800 Robux",149000],["1700 Robux",299000]]},
 {name:"Call of Duty Mobile",category:"FPS",emoji:"💥",color:"linear-gradient(135deg,#263322,#79985c)",items:[["63 CP",15000],["320 CP",65000],["645 CP",125000],["1300 CP",249000]]}
];
let currentGame=null,selected=null,payment=null;

function renderGames(list=games){
 document.getElementById("gameList").innerHTML=list.map((g)=>`
 <div class="game" onclick="openGame('${g.name}')">
 <div style="height:140px;background:${g.color};display:flex;align-items:center;justify-content:center;font-size:55px">${g.emoji}</div>
 <div class="game-info"><h3>${g.name}</h3><p>${g.category}</p><span class="tag">TOP UP SEKARANG →</span></div>
 </div>`).join("");
}
function searchGame(){
 const q=document.getElementById("search").value.toLowerCase();
 renderGames(games.filter(g=>g.name.toLowerCase().includes(q)));
}
function openGame(name){
 currentGame=games.find(g=>g.name===name);
 selected=null;payment=null;
 document.getElementById("selectedGame").innerText="Top Up "+name;
 document.getElementById("sumGame").innerText=name;
 document.getElementById("sumProduct").innerText="-";
 document.getElementById("sumPrice").innerText="Rp0";
 document.getElementById("sumTotal").innerText="Rp0";
 document.getElementById("sumPayment").innerText="-";
 document.getElementById("productList").innerHTML=currentGame.items.map((p,i)=>`
 <button class="product" onclick="chooseProduct(${i},this)">
 ${p[0]}<small>${rupiah(p[1])}</small>
 </button>`).join("");
 document.querySelectorAll("#paymentList button").forEach(b=>b.classList.remove("active"));
 document.getElementById("result").style.display="none";
 document.getElementById("transaksi").style.display="block";
 document.getElementById("transaksi").scrollIntoView({behavior:"smooth"});
}
function rupiah(n){return "Rp"+n.toLocaleString("id-ID")}
function chooseProduct(i,el){
 selected=currentGame.items[i];
 document.querySelectorAll(".product").forEach(b=>b.classList.remove("active"));
 el.classList.add("active");
 document.getElementById("sumProduct").innerText=selected[0];
 document.getElementById("sumPrice").innerText=rupiah(selected[1]);
 document.getElementById("sumTotal").innerText=rupiah(selected[1]);
}
function choosePayment(el,name){
 payment=name;
 document.querySelectorAll("#paymentList button").forEach(b=>b.classList.remove("active"));
 el.classList.add("active");
 document.getElementById("sumPayment").innerText=name;
}
function checkout(){
 const id=document.getElementById("userId").value.trim();
 if(!id||!selected||!payment){
 alert("Mohon isi User ID, pilih nominal, dan metode pembayaran!");
 return;
 }
 const order="NX"+Date.now().toString().slice(-9);
 document.getElementById("orderDetail").innerHTML=`
 <div>Nomor Pesanan: <strong>${order}</strong></div>
 <div>Game: <strong>${currentGame.name}</strong></div>
 <div>User ID: <strong>${id}</strong></div>
 <div>Zone ID: <strong>${document.getElementById("zoneId").value||"-"}</strong></div>
 <div>Produk: <strong>${selected[0]}</strong></div>
 <div>Metode: <strong>${payment}</strong></div>
 <div>Total: <strong>${rupiah(selected[1])}</strong></div>
 <p style="color:#f5c56b;margin-top:15px">Status: Menunggu integrasi pembayaran</p>`;
 document.getElementById("result").style.display="block";
 document.getElementById("result").scrollIntoView({behavior:"smooth"});
}
renderGames();
</script>
</body>
</html>
