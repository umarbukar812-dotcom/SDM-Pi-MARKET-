<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SDM Pi MARKET</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;background:#f5f5f5;margin:0;padding:10px}
.header{background:#6a1b9a;color:#fff;padding:20px;text-align:center;border-radius:12px}
.header h1{margin:0}
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
</style>
</head>
<body>

<div class="header">
<h1>🛒 SDM Pi MARKET</h1>
<p>Buy With Pi - Fast Delivery in Jos & Lagos</p>
</div>

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
<img src="https://images.unsplash.com/photo-1474979266404-7eaacbcd87c5?w=400">
<h3>SDM Oil 3L</h3>
<p>Quality Palm Oil</p>
<p class="price">0.5 Pi</p>
<button onclick="selectProduct('SDM Oil 3L', 0.5)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1567620905732-2d1ec7ab7445?w=400">
<h3>SDM Garri 2kg</h3>
<p>Clean White Garri</p>
<p class="price">0.3 Pi</p>
<button onclick="selectProduct('SDM Garri 2kg', 0.3)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1553530666-ba11a7da3888?w=400">
<h3>SDM Beans 2kg</h3>
<p>Fresh Brown Beans</p>
<p class="price">0.4 Pi</p>
<button onclick="selectProduct('SDM Beans 2kg', 0.4)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1587049352846-4a222e784d38?w=400">
<h3>SDM Honey 500ml</h3>
<p>Original Natural Honey</p>
<p class="price">0.8 Pi</p>
<button onclick="selectProduct('SDM Honey 500ml', 0.8)">Buy Now</button>
</div>

<div class="card">
<img src="https://images.unsplash.com/photo-1588964895597-cfccd6e2dbf9?w=400">
<h3>SDM Yam 5 Tubers</h3>
<p>Fresh Farm Yam</p>
<p class="price">1.2 Pi</p>
<button onclick="selectProduct('SDM Yam 5 Tubers', 1.2)">Buy Now</button>
</div>
</div>

<div class="checkout" id="checkout" style="display:none">
<h2>📦 Buyer Details</h2>
<p id="selected">No product selected</p>
<input id="buyerName" placeholder="Your Full Name">
<input id="buyerPhone" placeholder="Phone Number - e.g 0803...">
<input id="buyerAddress" placeholder="Delivery Address - e.g Jos, Plateau">
<button class="pay" onclick="payWithPi()">Pay with Pi 💜</button>
<p id="status"></p>
</div>

<p class="footer">SDM Pi MARKET - Powered by Pi Network<br>WhatsApp: 0803-XXX-XXXX</p>

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
