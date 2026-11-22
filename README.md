<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SDM Pi MARKET</title>
<script src="https://sdk.minepi.com/pi-sdk.js"></script>
<style>
body{font-family:Arial;background:#f5f5f5;margin:0;padding:15px}
h1{text-align:center;color:#6a1b9a}
.card{background:#fff;padding:15px;border-radius:12px;margin:10px 0;box-shadow:0 2px 8px rgba(0,0,0,0.1)}
button{width:100%;padding:12px;background:#6a1b9a;color:#fff;border:none;border-radius:8px;font-size:16px;margin-top:8px}
button.pay{background:#ff9800}
input{width:95%;padding:10px;margin:5px 0;border:1px solid #ddd;border-radius:8px}
#user{text-align:center;font-weight:bold;color:green}
</style>
</head>
<body>

<h1>🛒 SDM Pi MARKET</h1>
<p id="user">Not Logged In</p>
<button onclick="loginWithPi()">Login with Pi</button>

<div class="card">
<h2>Product 1 - SDM Rice 5kg</h2>
<p>Price: 1 Pi</p>
<p>Fresh Rice - Delivery in Lagos</p>
<button onclick="selectProduct('SDM Rice 5kg', 1)">Buy This Product</button>
</div>

<div class="card">
<h2>Product 2 - SDM Oil 3L</h2>
<p>Price: 0.5 Pi</p>
<p>Quality Palm Oil</p>
<button onclick="selectProduct('SDM Oil 3L', 0.5)">Buy This Product</button>
</div>

<div class="card" id="checkout" style="display:none">
<h2>Buyer Details</h2>
<p id="selected">No product selected</p>
<input id="buyerName" placeholder="Buyer Name - Your Full Name">
<input id="buyerPhone" placeholder="Phone Number - e.g 0803...">
<input id="buyerAddress" placeholder="Delivery Address - e.g Lagos, Nigeria">
<button class="pay" onclick="payWithPi()">Pay with Pi</button>
<p id="status"></p>
</div>

<script>
Pi.init({ version: "2.0", sandbox: true });
let currentProduct = "";
let currentPrice = 0;
let currentUser = null;

function onIncompletePaymentFound(payment) {
  console.log("Incomplete payment", payment);
}

async function loginWithPi() {
  try {
    const auth = await Pi.authenticate(['username', 'payments'], onIncompletePaymentFound);
    currentUser = auth.user;
    document.getElementById('user').innerText = "Welcome @" + auth.user.username + " ✅ Logged In!";
    alert("Welcome " + auth.user.username + "! Login Success!");
  } catch (err) {
    alert("Login Failed: " + err);
  }
}

function selectProduct(name, price) {
  currentProduct = name;
  currentPrice = price;
  document.getElementById('checkout').style.display = "block";
  document.getElementById('selected').innerText = "Selected: " + name + " - " + price + " Pi";
  window.scrollTo(0, document.body.scrollHeight);
  alert("You selected " + name + ". Now fill buyer details below!");
}

async function payWithPi() {
  if (!currentUser) {
    alert("Please tap Login with Pi first!");
    return;
  }
  let name = document.getElementById('buyerName').value;
  let phone = document.getElementById('buyerPhone').value;
  let address = document.getElementById('buyerAddress').value;
  if (!name || !phone || !address) {
    alert("Please fill ALL buyer details first! Name, Phone, Address");
    return;
  }
  if (!currentProduct) {
    alert("Please select a product first!");
    return;
  }
  try {
    document.getElementById('status').innerText = "Creating Payment... Please Approve in Pi Wallet";
    Pi.createPayment({
      amount: currentPrice,
      memo: "SDM Pi MARKET - " + currentProduct + " for " + name,
      metadata: { product: currentProduct, buyer: name, phone: phone, address: address }
    }, {
      onReadyForServerApproval: function(paymentId) {
        document.getElementById('status').innerText = "Payment Approved by Pi! Waiting...";
      },
      onReadyForServerCompletion: function(paymentId, txid) {
        document.getElementById('status').innerText = "Payment Successful! Tx: " + txid;
        alert("Payment Successful! Thank you " + name + "!");
      },
      onCancel: function(paymentId) {
        alert("Payment Cancelled");
        document.getElementById('status').innerText = "Payment Cancelled";
      },
      onError: function(error, payment) {
        alert("Payment Error: " + error);
        document.getElementById('status').innerText = "Payment Error: " + error;
      }
    });
  } catch (err) {
    alert("Pay Error: " + err);
  }
}
</script>
</body>
</html>
