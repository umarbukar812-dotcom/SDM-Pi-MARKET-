<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SDM Pi Market</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;margin:0;background:#f5f5f5;padding:10px}
header{background:#6a1b9a;color:white;padding:15px;text-align:center;border-radius:10px}
header h1{margin:0}
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
</style>
</head>
<body>

<header>
<h1>🛒 SDM Pi Market</h1>
<p>Buy With Pi - Fast Delivery in Maiduguri, Borno State</p>
</header>

<div class="basket-bar">
<span>🧺 Basket: <span id="basketCount">0</span></span>
<span>Total: <span id="totalPi">0</span> Pi</span>
</div>

<input id="search" onkeyup="searchProduct()" placeholder="🔍 Type product name... e.g Beans">

<div class="grid" id="productList">

<div class="card product">
<img src="https://images.unsplash.com/photo-1585996483592-8c0e0e6e2b3e?w=400" alt="Beans">
<h3>Beans</h3>
<p>1 Paint - Clean Beans</p>
<div class="price">10 Pi</div>
<button class="addBtn" onclick="addToCart('Beans',10)">➕ ADD TO BASKET</button>
</div>

<div class="card product">
<img src="https://images.unsplash.com/photo-1586201375761-83865001e31c?w=400" alt="Rice">
<h3>Rice</h3>
<p>1 Bag - Foreign Rice</p>
<div class="price">15 Pi</div>
<button class="addBtn" onclick="addToCart('Rice',15)">➕ ADD TO BASKET</button>
</div>

<div class="card product">
<img src="https://images.unsplash.com/photo-1474979266404-7eaacbcd87c5?w=400" alt="Oil">
<h3>Groundnut Oil</h3>
<p>1 Bottle - 5 Litres</p>
<div class="price">8 Pi</div>
<button class="addBtn" onclick="addToCart('Groundnut Oil',8)">➕ ADD TO BASKET</button>
</div>

<div class="card product">
<img src="https://sugar.dangote.com/wp-content/uploads/2021/06/products_list-non2.jpg" alt="Sugar">
<h3>Sugar</h3>
<p>1 Bag - Dangote Sugar</p>
<div class="price">5 Pi</div>
<button class="addBtn" onclick="addToCart('Sugar',5)">➕ ADD TO BASKET</button>
</div>

<div class="card product">
<img src="https://i.pinimg.com/736x/cd/c0/c3/cdc0c37c859a3f87210dc77406e7850f.jpg" alt="Garri">
<h3>Garri</h3>
<p>1 Paint - Ijebu Garri</p>
<div class="price">6 Pi</div>
<button class="addBtn" onclick="addToCart('Garri',6)">➕ ADD TO BASKET</button>
</div>

<div class="card product">
<img src="https://www.nigerianstore.com/cdn/shop/products/Maggi_Seasoning.jpg?v=1571718941&width=458" alt="Maggi">
<h3>Maggi Cubes</h3>
<p>1 Pack - Maggi Seasoning</p>
<div class="price">3 Pi</div>
<button class="addBtn" onclick="addToCart('Maggi Cubes',3)">➕ ADD TO BASKET</button>
</div>

</div>

<div class="cartBox">
<h3>🧺 Your Basket</h3>
<div id="cartList"><p style="color:#888">Basket is empty. Tap ADD TO BASKET!</p></div>

<div class="buyerTitle">✍️ BUYER - Fill Your Details Here</div>
<input id="custName" placeholder="BUYER Name - Type Your Name">
<input id="custPhone" placeholder="BUYER Phone Number">
<input id="custAddress" placeholder="BUYER Address in Maiduguri">

<button class="payBtn" onclick="payWithPi()">💜 CHECKOUT WITH PI</button>
<button class="waBtn" onclick="orderWhatsApp()">💬 SEND ORDER ON WHATSAPP</button>
<p id="status" style="text-align:center;color:#6a1b9a;font-weight:bold"></p>
<p style="text-align:center;color:#555">📍 Location: Maiduguri, Borno State<br>📞 Seller WhatsApp: 09047428383</p>
</div>

<script>
let cart = [];
function searchProduct(){
  let q = document.getElementById('search').value.toLowerCase();
  let items = document.getElementsByClassName('product');
  for(let i=0;i<items.length;i++){
    let name = items[i].getElementsByTagName('h3')[0].innerText.toLowerCase();
    if(name.includes(q)){ items[i].style.display='block'; } else { items[i].style.display='none'; }
  }
}
function addToCart(name, price){
  cart.push({name:name, price:price});
  updateBasket();
  alert(name + " added to Basket! 🧺");
}
function removeItem(index){ cart.splice(index,1); updateBasket(); }
function updateBasket(){
  document.getElementById('basketCount').innerText = cart.length;
  let total = 0; let html = "";
  if(cart.length==0){ html = "<p style='color:#888'>Basket is empty. Tap ADD TO BASKET!</p>"; }
  cart.forEach((item, i)=>{
    total += item.price;
    html += `<div class="cartItem"><span>${item.name} - ${item.price} Pi</span><button class="removeBtn" onclick="removeItem(${i})">X</button></div>`;
  });
  document.getElementById('cartList').innerHTML = html;
  document.getElementById('totalPi').innerText = total;
}
function getTotal(){ let t=0; cart.forEach(i=> t+=i.price); return t; }
function payWithPi(){
  if(cart.length==0){ alert("Basket is empty! Add product first!"); return; }
  let total = getTotal();
  let name = document.getElementById('custName').value;
  let phone = document.getElementById('custPhone').value;
  let addr = document.getElementById('custAddress').value;
  if(!name || !phone){ alert("BUYER: Please enter your Name and Phone first!"); return; }
  document.getElementById('status').innerText = "✅ Order Ready! Total: " + total + " Pi. Please send on WhatsApp below, then pay with Pi Wallet to SDM Market!";
  alert("Order Ready!\n\n" + cart.map(i=>i.name + " - " + i.price + " Pi").join("\n") + "\n\nTotal: " + total + " Pi\nBUYER Name: " + name + "\nBUYER Phone: " + phone + "\nBUYER Address: " + addr + "\n\nNow tap SEND ORDER ON WHATSAPP!");
}
function orderWhatsApp(){
  if(cart.length==0){ alert("Basket is empty!"); return; }
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
