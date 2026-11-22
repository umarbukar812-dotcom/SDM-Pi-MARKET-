<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SDM Pi Market - Pi Next Hackathon</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;margin:0;background:#f5f5f5;padding:10px}
header{background:#6a1b9a;color:white;padding:15px;text-align:center;border-radius:10px}
header h1{margin:0}
.topbar{background:white;padding:10px;margin:10px 0;border-radius:10px;display:flex;justify-content:space-between;align-items:center}
.loginBtn{background:#6a1b9a;color:white;border:none;padding:10px 15px;border-radius:10px;font-weight:bold;cursor:pointer}
.basket-bar{background:white;padding:12px;margin:10px 0;border-radius:10px;display:flex;justify-content:space-between;align-items:center;font-weight:bold;position:sticky;top:0}
#search{width:100%;padding:12px;border-radius:10px;border:1px solid #ccc;font-size:16px;margin:10px 0;box-sizing:border-box}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.card{background:white;padding:12px;border-radius:12px;text-align:center;box-shadow:0 2px 5px rgba(0,0,0,0.1)}
.card img{width:100%;height:110px;object-fit:cover;border-radius:10px;background:#eee}
.card h3{margin:8px 0 2px;font-size:16px}
.price{color:#6a1b9a;font-weight:bold;margin:5px 0}
.addBtn{background:#FFD700;border:none;padding:10px;width:100%;border-radius:10px;font-weight:bold;font-size:15px;cursor:pointer}
.payBtn{background:#6a1b9a;color:white;border:none;padding:15px;width:100%;border-radius:12px;font-weight:bold;font-size:17px;margin-top:10px}
.waBtn{background:#25D366;color:white;border:none;padding:15px;width:100%;border-radius:12px;font-weight:bold;font-size:17px;margin-top:10px}
.cartBox{background:white;padding:12px;border-radius:12px;margin-top:12px}
.cartItem{display:flex;justify-content:space-between;padding:8px 0;border-bottom:1px solid #eee}
.removeBtn{background:red;color:white;border:none;padding:5px 10px;border-radius:5px}
input{width:100%;padding:12px;margin:5px 0;border-radius:10px;border:1px solid #ccc;box-sizing:border-box}
.buyerTitle{background:#FFF9C4;padding:10px;border-radius:10px;text-align:center;font-weight:bold;margin-bottom:5px}
.badge{background:#FFD700;color:black;padding:3px 8px;border-radius:20px;font-size:12px;font-weight:bold}
</style>
</head>
<body>

<header>
<h1>🛒 SDM Pi Market</h1>
<p>Buy With Pi - Fast Delivery in Maiduguri, Borno State</p>
<span class="badge">🏆 Pi Next Hackathon 2026</span>
</header>

<div class="topbar">
<span id="userInfo">👤 Not Logged In</span>
<button class="loginBtn" id="loginBtn" onclick="loginWithPi()">💜 Login with Pi</button>
</div>

<div class="basket-bar">
<span>🧺 Basket: <span id="basketCount">0</span></span>
<span>Total: <span id="totalPi">0</span> Pi</span>
</div>

<input id="search" onkeyup="searchProduct()" placeholder="🔍 Type product name... e.g Beans">

<div class="grid" id="productList">
<div class="card product">
<img src="https://images.unsplash.com/photo-1585996483592-8c0e0e6e2b3e?w=400" alt="Beans">
<h3>Beans</h3><p>1 Paint - Clean Beans</p><div class="price">0.5 Pi</div>
<button class="addBtn" onclick="addToCart('Beans',0.5)">➕ ADD TO BASKET</button>
</div>
<div class="card product">
<img src="https://images.unsplash.com/photo-1586201375761-83865001e31c?w=400" alt="Rice">
<h3>Rice</h3><p>1 Bag - Foreign Rice</p><div class="price">1.2 Pi</div>
<button class="addBtn" onclick="addToCart('Rice',1.2)">➕ ADD TO BASKET</button>
</div>
<div class="card product">
<img src="https://images.unsplash.com/photo-1474979266404-7eaacbcd87c5?w=400" alt="Oil">
<h3>Groundnut Oil</h3><p>1 Bottle - 5 Litres</p><div class="price">0.8 Pi</div>
<button class="addBtn" onclick="addToCart('Groundnut Oil',0.8)">➕ ADD TO BASKET</button>
</div>
<div class="card product">
<img src="https://sugar.dangote.com/wp-content/uploads/2021/06/products_list-non2.jpg" alt="Sugar">
<h3>Sugar</h3><p>1 Bag - Dangote Sugar</p><div class="price">0.4 Pi</div>
<button class="addBtn" onclick="addToCart('Sugar',0.4)">➕ ADD TO BASKET</button>
</div>
<div class="card product">
<img src="https://i.pinimg.com/736x/cd/c0/c3/cdc0c37c859a3f87210dc77406e7850f.jpg" alt="Garri">
<h3>Garri</h3><p>1 Paint - Ijebu Garri</p><div class="price">0.6 Pi</div>
<button class="addBtn" onclick="addToCart('Garri',0.6)">➕ ADD TO BASKET</button>
</div>
<div class="card product">
<img src="https://www.nigerianstore.com/cdn/shop/products/Maggi_Seasoning.jpg?v=1571718941&width=458" alt="Maggi">
<h3>Maggi Cubes</h3><p>1 Pack - Maggi Seasoning</p><div class="price">0.2 Pi</div>
<button class="addBtn" onclick="addToCart('Maggi Cubes',0.2)">➕ ADD TO BASKET</button>
</div>
</div>

<div class="cartBox">
<h3>🧺 Your Basket</h3>
<div id="cartList"><p style="color:#888">Basket is empty. Tap ADD TO BASKET!</p></div>
<div class="buyerTitle">✍️ BUYER - Fill Your Details Here</div>
<input id="custName" placeholder="BUYER Name - Type Your Name">
<input id="custPhone" placeholder="BUYER Phone Number">
<input id="custAddress" placeholder="BUYER Address in Maiduguri">
<button class="payBtn" onclick="payWithPi()">💜 PAY WITH PI - REAL PI PAYMENT</button>
<button class="waBtn" onclick="orderWhatsApp()">💬 SEND ORDER ON WHATSAPP</button>
<p id="status" style="text-align:center;color:#6a1b9a;font-weight:bold"></p>
<h4>📜 My Orders</h4>
<div id="orderHistory"><p style="color:#888">No orders yet</p></div>
<p style="text-align:center;color:#555">📍 Maiduguri, Borno State<br>📞 Seller WhatsApp: 09047428383<br>🏆 Built for Pi Next Hackathon</p>
</div>

<script>
// ===== HACKATHON CONFIG - REPLACE THESE 2 LINES! =====
const PI_APP_ID = "YOUR_APP_ID";
const PI_API_KEY = "YOUR_API_KEY";
// Get these from developers.minepi.com > SDM Pi Market

let cart = [];
let piUser = null;
let piAccessToken = null;

window.onload = function(){
  try{
    Pi.init({version:"2.0", sandbox:false});
    document.getElementById('status').innerText = "Pi SDK Ready - Please Login with Pi";
  }catch(e){ document.getElementById('status').innerText = "Open in Pi Browser to use Pi Payment"; }
};

function loginWithPi(){
  try{
    Pi.authenticate(['username','payments','wallet_address'], function(auth){
      piUser = auth.user;
      piAccessToken = auth.accessToken;
      document.getElementById('userInfo').innerText = "👤 Hello, @" + piUser.username;
      document.getElementById('loginBtn').innerText = "✅ Logged In";
      document.getElementById('custName').value = piUser.username;
      document.getElementById('status').innerText = "✅ Welcome @" + piUser.username + "! You can now pay with Pi!";
      alert("Welcome @" + piUser.username + "! Login Success!");
    }, function(err){ alert("Login failed. Open in Pi Browser! " + err); });
  }catch(e){ alert("Please open this shop inside Pi Browser!"); }
}

function searchProduct(){
  let q = document.getElementById('search').value.toLowerCase();
  let items = document.getElementsByClassName('product');
  for(let i=0;i<items.length;i++){
    let name = items[i].getElementsByTagName('h3')[0].innerText.toLowerCase();
    items[i].style.display = name.includes(q) ? 'block' : 'none';
  }
}
function addToCart(name, price){
  cart.push({name:name, price:price});
  updateBasket();
  alert(name + " added! 🧺");
}
function removeItem(i){ cart.splice(i,1); updateBasket(); }
function updateBasket(){
  document.getElementById('basketCount').innerText = cart.length;
  let total = 0; let html = "";
  if(cart.length==0){ html = "<p style='color:#888'>Basket is empty.</p>"; }
  cart.forEach((item,i)=>{
    total += item.price;
    html += `<div class="cartItem"><span>${item.name} - ${item.price} Pi</span><button class="removeBtn" onclick="removeItem(${i})">X</button></div>`;
  });
  document.getElementById('cartList').innerHTML = html;
  document.getElementById('totalPi').innerText = total.toFixed(2);
}
function getTotal(){ let t=0; cart.forEach(i=> t+=i.price); return t; }

function payWithPi(){
  if(cart.length==0){ alert("Basket is empty!"); return; }
  if(!piUser){ alert("Please tap LOGIN WITH PI first!"); loginWithPi(); return; }
  let total = getTotal();
  let name = document.getElementById('custName').value;
  let phone = document.getElementById('custPhone').value;
  let addr = document.getElementById('custAddress').value;
  if(!name || !phone || !addr){ alert("BUYER: Fill Name, Phone, Address first!"); return; }
  document.getElementById('status').innerText = "💜 Opening Pi Wallet... Please approve payment of " + total + " Pi";

  Pi.createPayment({
    amount: total,
    memo: "SDM Pi Market Order - " + cart.map(i=>i.name).join(", "),
    metadata: { buyerName:name, buyerPhone:phone, buyerAddress:addr, items: cart, username: piUser.username }
  }, {
    onReadyForServerApproval: function(paymentId){
      document.getElementById('status').innerText = "Approving payment...";
      // APPROVE via Pi Platform API - Needs your API KEY
      fetch("https://api.minepi.com/v2/payments/" + paymentId + "/approve", {
        method:"POST",
        headers:{ "Authorization":"Key " + PI_API_KEY, "Content-Type":"application/json" }
      }).then(r=>r.json()).then(d=>{ console.log("Approved", d); }).catch(e=>{ console.log(e); });
    },
    onReadyForServerCompletion: function(paymentId, txid){
      document.getElementById('status').innerText = "Completing payment... TX: " + txid;
      fetch("https://api.minepi.com/v2/payments/" + paymentId + "/complete", {
        method:"POST",
        headers:{ "Authorization":"Key " + PI_API_KEY, "Content-Type":"application/json" },
        body: JSON.stringify({txid: txid})
      }).then(()=>{
        document.getElementById('status').innerText = "✅ Payment Success! Thank you @" + piUser.username;
        alert("✅ Payment Success! " + total + " Pi Paid! Your order is coming to " + addr);
        saveOrder(total, txid);
        cart = []; updateBasket();
        orderWhatsApp();
      });
    },
    onCancel: function(){ document.getElementById('status').innerText = "Payment Cancelled by user"; },
    onError: function(e){ document.getElementById('status').innerText = "Payment Error: " + e; alert("Payment Error: " + e + ". Try WhatsApp order."); }
  });
}

function saveOrder(total, txid){
  let orders = JSON.parse(localStorage.getItem("sdm_orders") || "[]");
  orders.push({total: total, txid: txid, date: new Date().toLocaleString(), items: cart});
  localStorage.setItem("sdm_orders", JSON.stringify(orders));
  showOrders();
}
function showOrders(){
  let orders = JSON.parse(localStorage.getItem("sdm_orders") || "[]");
  if(orders.length==0) return;
  let html = "";
  orders.forEach(o=>{ html += `<p>✅ ${o.date} - ${o.total} Pi - TX: ${o.txid.substring(0,10)}...</p>`; });
  document.getElementById('orderHistory').innerHTML = html;
}
showOrders();

function orderWhatsApp(){
  if(cart.length==0 && !piUser){ return; }
  let total = getTotal();
  let name = document.getElementById('custName').value || "Customer";
  let phone = document.getElementById('custPhone').value || "";
  let addr = document.getElementById('custAddress').value || "";
  let msg = "Hello SDM Pi Market! I am a BUYER, I want to order:%0A%0A" + cart.map(i=> "- " + i.name + " - " + i.price + " Pi").join("%0A") + "%0A%0ATotal: " + total + " Pi%0ABUYER Name: " + name + "%0ABUYER Phone: " + phone + "%0ABUYER Address: " + addr + "%0A%0A I will pay with Pi!";
  window.open("https://wa.me/2349047428383?text=" + msg, "_blank");
}
</script>
</body>
</html>
