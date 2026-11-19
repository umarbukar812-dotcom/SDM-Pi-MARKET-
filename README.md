<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>SDM Pi Market - Buy Food With Pi in Maiduguri</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;margin:0;background:#fff8e1;text-align:center}
.header{background:#6a1b9a;color:white;padding:25px}
.header h1{margin:0;font-size:30px}
.grid{display:flex;flex-wrap:wrap;justify-content:center;padding:10px}
.card{background:white;width:160px;margin:8px;border-radius:12px;box-shadow:0 2px 8px #ccc;padding:10px}
.card img{width:100%;height:110px;object-fit:cover;border-radius:10px}
.card h3{margin:8px 0 3px;font-size:16px}
.price{color:#6a1b9a;font-weight:bold}
button{background:#6a1b9a;color:white;border:none;padding:10px;width:100%;border-radius:8px;font-size:15px;margin-top:5px}
.wa{background:#25D366}
#status{background:yellow;padding:10px;font-weight:bold}
</style>
</head>
<body>
<div class="header">
<h1>🛒 SDM Pi Market</h1>
<p>Buy Food With Pi in Maiduguri</p>
<p>By Umar Bukar Saduma</p>
<p>📍 Maiduguri, Borno State</p>
<p>📱 WhatsApp: 0903 309 8693</p>
</div>
<div id="status">TEST MODE - Using Test-Pi Only</div>

<div class="grid">
<div class="card">
<img src="https://images.unsplash.com/photo-1585996483592-8a5d7f1b1e3a?w=400">
<h3>Beans 5kg</h3>
<p class="price">0.8 Pi</p>
<button onclick="payPi(0.8,'Beans 5kg')">Pay With Pi 🟣 TEST</button>
<a href="https://wa.me/2349033098693?text=Hello%20SDM%20I%20want%20to%20buy%20Beans%20with%20Pi"><button class="wa">Order on WhatsApp</button></a>
</div>

<div class="card">
<img src="https://gonavest.com/assets/rice-K2X2vmP5.png">
<h3>Rice 5kg</h3>
<p class="price">1 Pi</p>
<button onclick="payPi(1,'Rice 5kg')">Pay With Pi 🟣 TEST</button>
<a href="https://wa.me/2349033098693?text=Hello%20SDM%20I%20want%20to%20buy%20Rice%20with%20Pi"><button class="wa">Order on WhatsApp</button></a>
</div>

<div class="card">
<img src="http://www.osiafrik.com/cdn/shop/products/image_64d5a541-551d-4e8a-95d5-a35d8c2df3e2_1024x1024.jpg?v=1630667997">
<h3>Palm Oil 1 Litre</h3>
<p class="price">0.5 Pi</p>
<button onclick="payPi(0.5,'Palm Oil 1 Litre')">Pay With Pi 🟣 TEST</button>
<a href="https://wa.me/2349033098693?text=Hello%20SDM%20I%20want%20to%20buy%20Palm%20Oil%20with%20Pi"><button class="wa">Order on WhatsApp</button></a>
</div>

<div class="card">
<img src="https://africangoodsmarket.shop/cdn/shop/files/MaggiStarSeasoning2.jpg?v=1713884220&width=713">
<h3>Maggi Cubes</h3>
<p class="price">0.1 Pi</p>
<button onclick="payPi(0.1,'Maggi Cubes')">Pay With Pi 🟣 TEST</button>
<a href="https://wa.me/2349033098693?text=Hello%20SDM%20I%20want%20to%20buy%20Maggi%20with%20Pi"><button class="wa">Order on WhatsApp</button></a>
</div>
</div>

<div style="padding:15px;background:#333;color:white">
<p>💬 Order on WhatsApp - Pay With Pi</p>
<p>Delivery Available in Maiduguri</p>
<p>© 2026 SDM Pi Market</p>
</div>

<script>
Pi.init({version:"2.0", sandbox:true});
async function payPi(amount, itemName){
  document.getElementById('status').innerText = "Connecting to Pi...";
  try{
    const auth = await Pi.authenticate(['username','payments'], onIncompletePaymentFound);
    document.getElementById('status').innerText = "Hello " + auth.user.username + " - Paying " + amount + " Test-Pi for " + itemName;
    const payment = await Pi.createPayment({
      amount: amount,
      memo: "SDM Pi Market - " + itemName,
      metadata: {item: itemName}
    }, {
      onReadyForServerApproval: function(paymentId){ console.log(paymentId); },
      onReadyForServerCompletion: function(paymentId, txid){ document.getElementById('status').innerText = "✅ TEST PAYMENT SUCCESS! Tx: " + txid; },
      onCancel: function(paymentId){ document.getElementById('status').innerText = "Payment Cancelled"; },
      onError: function(error){ document.getElementById('status').innerText = "Error: " + error; }
    });
  }catch(e){
    document.getElementById('status').innerText = "Please open this shop INSIDE Pi Browser to test payment. Error: " + e;
    alert("Open this shop inside Pi Browser, not Chrome!");
  }
}
function onIncompletePaymentFound(payment){ console.log(payment); }
</script>
</body>
</html>

