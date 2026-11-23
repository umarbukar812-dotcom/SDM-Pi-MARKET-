<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SDM Pi MARKET</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;background:#f5f5f5;margin:0;padding:10px}
.header{background:#6a1b9a;color:#fff;padding:20px 10px;text-align:center;border-radius:12px}
.hexagon{width:90px;height:90px;background:#ff9800;color:#fff;font-size:28px;font-weight:bold;display:flex;align-items:center;justify-content:center;margin:0 auto 10px;clip-path:polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);border:3px solid #fff}
.header h1{margin:5px 0}
.header p{margin:5px 0}
#user{text-align:center;font-weight:bold;color:green;background:#fff;padding:10px;border-radius:8px;margin:10px 0}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.card{background:#fff;padding:10px;border-radius:12px;text-align:center;box-shadow:0 2px 8px rgba(0,0,0,0.1)}
.card img{width:100%;height:130px;object-fit:cover;border-radius:10px}
.card h3{margin:8px 0 2px;font-size:15px}
.card p{margin:2px 0;color:#666;font-size:13px}
.price{color:#6a1b9a;font-weight:bold;font-size:16px !important}
button{width:100%;padding:10px;background:#6a1b9a;color:#fff;border:none;border-radius:8px;font-size:14px;margin-top:6px}
button.pay{background:#ff9800;font-size:16px;padding:13px}
input{width:95%;padding:11px;margin:6px 0;border:1px solid #ddd;border-radius:8px}
.checkout{background:#fff;padding:15px;border-radius:12px;margin-top:15px}
.footer{text-align:center;color:#888;font-size:12px;margin:20px 0}
.location{background:#fff;padding:10px;text-align:center;border-radius:8px;margin:10px 0;font-weight:bold;color:#333}
</style>
</head>
<body>

<div class="header">
<div class="hexagon">SDM</div>
<h1>🛒 SDM Pi MARKET</h1>
<p>Buy With Pi - Rice, Sugar, Salt, Oil & Maggi</p>
<p>📍 Maiduguri, Borno State, Nigeria</p>
</div>

<div class="location">📍 Location: Maiduguri, Borno State<br>🚚 Fast Delivery in Maiduguri</div>

<p id="user">Not Logged In</p>
<button onclick="loginWithPi()">🔐 Login with Pi</button>

<div class="grid">
<div class="card">
<img src="https://images.unsplash.com/photo-1586201375761-83865001e31c?w=400">
<h3>SDM Rice 5kg</h3>
<p>Premium Local Rice</p>
<p class="price">1 Pi</p>
<button onclick="selectProduct('SDM Rice 5kg', 1)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1581441363689-1f3c3c414635?w=400">
<h3>SDM Sugar 2kg</h3>
<p>Sweet White Sugar</p>
<p class="price">0.5 Pi</p>
<button onclick="selectProduct('SDM Sugar 2kg', 0.5)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1518110925495-5fe2fda0442c?w=400">
<h3>SDM Salt 1kg</h3>
<p>Fine Iodized Salt</p>
<p class="price">0.2 Pi</p>
<button onclick="selectProduct('SDM Salt 1kg', 0.2)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1474979266404-7eaacbcd87c5?w=400">
<h3>SDM Palm Oil 3L</h3>
<p>Original Red Palm Oil</p>
<p class="price">0.6 Pi</p>
<button onclick="selectProduct('SDM Palm Oil 3L', 0.6)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1620706857370-e1b9770e8bb1?w=400">
<h3>SDM Groundnut Oil 3L</h3>
<p>Clean Groundnut Oil</p>
<p class="price">0.7 Pi</p>
<button onclick="selectProduct('SDM Groundnut Oil 3L', 0.7)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1585032226651-759b368d7246?w=400">
<h3>SDM Maggi 1 Pack</h3>
<p>Maggi Seasoning Cubes</p>
<p class="price">0.3 Pi</p>
<button onclick="selectProduct('SDM Maggi 1 Pack', 0.3)">Buy Now</button>
</div>
</div>

<div class="checkout" id="checkout" style="display:none">
<h2>📦 Buyer Details</h2>
<p id="selected">No product selected</p>
<input id="buyerName" placeholder="Your Full Name">
<input id="buyerPhone" placeholder="Phone Number - e.g 0803...">
<input id="buyerAddress" placeholder="Delivery Address - e.g Maiduguri, Borno">
<button class="pay" onclick="payWithPi()">Pay with Pi 💜</button>
<p id="status"></p>
</div>

<p class="footer">SDM Pi MARKET - Powered by Pi Network<br>📍 Maiduguri, Borno State, Nigeria<br>🚚 Delivery Available in Maiduguri</p>

<script>
Pi.init({ version: "2.0", sandbox: true });
let currentProduct=""; let currentPrice=0; let currentUser=null;
function onIncompletePaymentFound(p){console.log(p)}
async function loginWithPi(){
 try{const auth=await Pi.authenticate(['username','payments'], onIncompletePaymentFound); currentUser=auth.user; document.getElementById('user').innerText="Welcome @"+auth.user.username+" ✅ Logged In!"; alert("Welcome "+auth.user.username+"!")}catch(e){alert("Login Failed: "+e)}
}
function selectProduct(name,price){currentProduct=name;currentPrice=price;document.getElementById('checkout').style.display="block";document.getElementById('selected').innerText="Selected: "+name+" - "+price+" Pi";window.scrollTo(0,document.body.scrollHeight);alert("You selected "+name+"! Fill details below!")}
async function payWithPi(){
 if(!currentUser){alert("Tap Login with Pi first!");return}
 let name=document.getElementById('buyerName').value; let phone=document.getElementById('buyerPhone').value; let address=document.getElementById('buyerAddress').value;
 if(!name||!phone||!address){alert("Fill ALL details! Name, Phone, Address");return}
 try{document.getElementById('status').innerText="Creating Payment... Approve in Pi Wallet";
 Pi.createPayment({amount:currentPrice,memo:"SDM - "+currentProduct+" for "+name,metadata:{product:currentProduct,buyer:name,phone:phone,address:address}},{
  onReadyForServerApproval:function(id){document.getElementById('status').innerText="Payment Approved! Waiting..."},
  onReadyForServerCompletion:function(id,txid){document.getElementById('status').innerText="Success! Tx: "+txid;alert("Payment Successful! Thank you "+name+"!")},
  onCancel:function(id){alert("Payment Cancelled")},
  onError:function(e){alert("Payment Error: "+e)}
 })}catch(e){alert("Pay Error: "+e)}
}
</script>
</body>
</html>
