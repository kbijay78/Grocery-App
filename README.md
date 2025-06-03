<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Simple Grocery App</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <h1>Grocery Store</h1>
  <div id="product-list"></div>
  <h2>Your Cart</h2>
  <ul id="cart-list"></ul>
  <button onclick="placeOrder()">Place Order</button>

  <script src="script.js"></script>
</body>
</html>

body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

#product-list {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
}

.product {
  border: 1px solid #ccc;
  padding: 10px;
  width: 150px;
}

button {
  margin-top: 10px;
}


const products = [
  { id: 1, name: "Apples", price: 1.5 },
  { id: 2, name: "Bananas", price: 1.0 },
  { id: 3, name: "Carrots", price: 0.75 },
];

let cart = [];

function renderProducts() {
  const list = document.getElementById("product-list");
  products.forEach(product => {
    const div = document.createElement("div");
    div.className = "product";
    div.innerHTML = `
      <h3>${product.name}</h3>
      <p>$${product.price.toFixed(2)}</p>
      <button onclick="addToCart(${product.id})">Add to Cart</button>
    `;
    list.appendChild(div);
  });
}

function addToCart(id) {
  const product = products.find(p => p.id === id);
  cart.push(product);
  renderCart();
}

function renderCart() {
  const list = document.getElementById("cart-list");
  list.innerHTML = "";
  cart.forEach(item => {
    const li = document.createElement("li");
    li.textContent = `${item.name} - $${item.price.toFixed(2)}`;
    list.appendChild(li);
  });
}

function placeOrder() {
  if (cart.length === 0) {
    alert("Your cart is empty!");
    return;
  }
  alert("Order placed! Thank you!");
  cart = [];
  renderCart();
}

renderProducts();
