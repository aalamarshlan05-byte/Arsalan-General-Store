<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Arslan General Store</title>

<style>
*{box-sizing:border-box}
body{margin:0;font-family:Arial,sans-serif;background:#f1f3f6;color:#172337}
button,input,textarea,select{font:inherit}
button{cursor:pointer;border:0}

header{
background:#2874f0;color:white;
position:sticky;top:0;z-index:100
}

.nav{
max-width:1250px;margin:auto;padding:10px 14px;
display:flex;align-items:center;gap:14px
}

.logo{font-size:21px;font-weight:900;white-space:nowrap}
.logo small{display:block;font-size:9px;color:#ffe500}

.search{
flex:1;background:white;border-radius:4px;
display:flex;overflow:hidden
}

.search input{
width:100%;padding:12px;border:0;outline:0
}

.search button{
background:white;color:#2874f0;padding:0 16px
}

.cartBtn{
background:none;color:white;font-weight:bold
}

.hero{
max-width:1250px;margin:12px auto;
padding:38px 25px;
background:linear-gradient(120deg,#101b2d,#2874f0);
border-radius:8px;color:white;
display:flex;justify-content:space-between;
align-items:center
}

.hero h1{font-size:40px;margin:0 0 10px}
.hero p{font-size:17px;line-height:1.5}
.hero button{
background:#ff9f00;padding:13px 24px;
border-radius:4px;font-weight:bold
}

.container{max-width:1250px;margin:auto;padding:0 10px}

.categories{
background:white;padding:13px;
display:flex;gap:8px;overflow:auto;
margin-bottom:12px
}

.category{
padding:10px 17px;
background:#f5f7fa;
border-radius:20px;
white-space:nowrap
}

.category.active{
background:#2874f0;color:white
}

.section{
background:white;margin-bottom:14px;
padding:18px
}

.section h2{margin:0 0 16px}

.grid{
display:grid;
grid-template-columns:repeat(4,1fr);
gap:14px
}

.product{
border:1px solid #e0e4e9;
padding:10px;
position:relative;
background:white
}

.product:hover{
box-shadow:0 5px 20px #0002
}

.productImg{
height:190px;
background:#f7f7f7;
display:flex;
align-items:center;
justify-content:center
}

.productImg img{
width:100%;height:100%;
object-fit:contain
}

.product h3{font-size:15px;margin:10px 0}
.price{font-size:20px;font-weight:bold}
.mrp{
text-decoration:line-through;
font-size:12px;color:#777;margin-left:5px
}

.discount{
color:#168b3b;font-size:12px;
font-weight:bold;margin-top:4px
}

.badge{
position:absolute;top:8px;left:8px;
background:#e53935;color:white;
padding:4px 7px;font-size:10px;
border-radius:3px
}

.actions{
display:flex;gap:7px;margin-top:10px
}

.actions button{
flex:1;padding:10px;
font-weight:bold;border-radius:4px
}

.add{background:#fb641b;color:white}
.buy{background:#ff9f00}

.muted{color:#667085;font-size:13px}

.modal{
display:none;
position:fixed;inset:0;
background:#0009;
z-index:500;
align-items:center;
justify-content:center;
padding:12px
}

.box{
background:white;
width:100%;max-width:680px;
max-height:94vh;
overflow:auto;
padding:20px;
border-radius:10px
}

.close{
float:right;
background:#eee;
padding:7px 11px;
border-radius:4px
}

.field{
width:100%;
padding:12px;
margin:6px 0;
border:1px solid #ccd4df;
border-radius:5px;
outline:none
}

.primary{
background:#2874f0;
color:white;
padding:12px 18px;
border-radius:5px;
font-weight:bold
}

.orange{
background:#ff9f00;
color:#111;
padding:12px 18px;
border-radius:5px;
font-weight:bold
}

.red{
background:#d93025;
color:white;
padding:8px;
border-radius:4px
}

.green{
color:#168b3b;
font-weight:bold
}

/* BILL */
.bill{
border:1px solid #ddd;
border-radius:6px;
padding:15px;
margin-top:15px
}

.billRow{
display:flex;
justify-content:space-between;
padding:7px 0
}

.billTotal{
border-top:1px solid #ddd;
margin-top:8px;
padding-top:12px;
font-size:20px;
font-weight:bold
}

/* CART */
.cartItem{
display:flex;
gap:12px;
padding:13px 0;
border-bottom:1px solid #ddd
}

.cartItem img{
width:75px;height:75px;
object-fit:contain
}

.qty button{
padding:4px 10px;
border:1px solid #ccc;
background:white
}

/* ORDER */
.order{
border:1px solid #ddd;
padding:14px;
margin:10px 0;
border-radius:6px
}

.status{
color:#2874f0;
font-weight:bold
}

.review{
padding:13px 0;
border-bottom:1px solid #ddd
}

.review img{
width:100px;height:80px;
object-fit:cover;
margin-top:7px;
border-radius:5px
}

footer{
background:#172337;
color:white;
text-align:center;
padding:30px;
margin-top:20px
}

@media(max-width:850px){
.grid{grid-template-columns:repeat(3,1fr)}
}

@media(max-width:600px){
.nav{flex-wrap:wrap}
.search{order:3;flex-basis:100%}
.grid{grid-template-columns:repeat(2,1fr)}
.productImg{height:150px}
.hero h1{font-size:28px}
.hero{margin:8px}
.hero>div:last-child{display:none}
}
</style>
</head>

<body>

<header>
<div class="nav">

<div class="logo">
ARSLAN<br>
<small>GENERAL STORE</small>
</div>

<div class="search">
<input id="search"
placeholder="Search products..."
oninput="renderProducts()">
<button>🔍</button>
</div>

<button class="cartBtn" onclick="openCart()">
🛒 Cart (<span id="cartCount">0</span>)
</button>

</div>
</header>


<div class="container">

<section class="hero">

<div>
<h1>Arslan General Store</h1>

<p>
Grocery • Snacks • Household • Daily Essentials
</p>

<button onclick="document.getElementById('products').scrollIntoView()">
SHOP NOW
</button>
</div>

<div style="font-size:70px">🛍️</div>

</section>


<div class="categories" id="categories"></div>


<section class="section">

<h2>🔥 Today's Offers</h2>

<div class="grid" id="offers"></div>

</section>


<section class="section" id="products">

<h2>🛒 All Products</h2>

<div class="grid" id="productGrid"></div>

</section>


<section class="section">

<h2>⭐ Customer Reviews</h2>

<div id="reviews"></div>

<button class="primary"
onclick="openModal('reviewModal')">
Write Review
</button>

</section>

</div>


<footer>

<h3>Arslan General Store</h3>

<p>💵 Cash on Delivery Available</p>

<p>Fast • Simple • Reliable</p>

<button class="primary"
onclick="openAdmin()">
🔐 Admin Panel
</button>

</footer>


<!-- CART -->

<div class="modal" id="cartModal">

<div class="box">

<button class="close"
onclick="closeModal('cartModal')">✕</button>

<h2>🛒 Your Cart</h2>

<div id="cartItems"></div>

<div class="bill">

<div class="billRow">
<span>Subtotal</span>
<b id="subtotal">₹0</b>
</div>

<div class="billRow">
<span>Delivery</span>
<b>FREE</b>
</div>

<div class="billTotal">
<span>Total</span>
<span id="cartTotal">₹0</span>
</div>

</div>

<br>

<button class="orange"
onclick="checkout()">
Continue to Checkout
</button>

</div>
</div>


<!-- CHECKOUT -->

<div class="modal" id="checkoutModal">

<div class="box">

<button class="close"
onclick="closeModal('checkoutModal')">✕</button>

<h2>📦 Checkout</h2>

<input class="field"
id="customerName"
placeholder="Full Name">

<input class="field"
id="customerPhone"
placeholder="Mobile Number">

<textarea class="field"
id="customerAddress"
placeholder="Complete Delivery Address">
</textarea>

<h3>💵 Payment Method</h3>

<div style="
padding:13px;
background:#f0fff4;
border:1px solid #b7e4c7;
border-radius:5px">

<b>✓ Cash on Delivery</b>

</div>

<div class="bill">

<div id="checkoutBill"></div>

</div>

<br>

<button class="primary"
onclick="placeOrder()">

PLACE COD ORDER

</button>

<p id="orderMessage"></p>

</div>
</div>


<!-- REVIEW -->

<div class="modal" id="reviewModal">

<div class="box">

<button class="close"
onclick="closeModal('reviewModal')">✕</button>

<h2>⭐ Customer Review</h2>

<input class="field"
id="reviewName"
placeholder="Your Name">

<select class="field"
id="reviewRating">

<option value="5">★★★★★ 5 Stars</option>
<option value="4">★★★★ 4 Stars</option>
<option value="3">★★★ 3 Stars</option>
<option value="2">★★ 2 Stars</option>
<option value="1">★ 1 Star</option>

</select>

<textarea class="field"
id="reviewText"
placeholder="Write your review">
</textarea>

<input class="field"
id="reviewPhoto"
type="file"
accept="image/*">

<button class="primary"
onclick="submitReview()">

Submit Review

</button>

</div>
</div>


<!-- ADMIN -->

<div class="modal" id="adminModal">

<div class="box">

<button class="close"
onclick="closeModal('adminModal')">✕</button>


<div id="adminLogin">

<h2>🔐 Admin Login</h2>

<input class="field"
id="adminUser"
placeholder="Username">

<input class="field"
id="adminPass"
type="password"
placeholder="Password">

<button class="primary"
onclick="loginAdmin()">

LOGIN

</button>

</div>


<div id="dashboard"
style="display:none">

<h2>⚙️ Admin Dashboard</h2>

<h3>📦 Customer Orders</h3>

<div id="orders"></div>


<hr>

<h3>➕ Add New Product</h3>

<input class="field"
id="productName"
placeholder="Product Name">

<input class="field"
id="productPrice"
type="number"
placeholder="Sale Price">

<input class="field"
id="productMRP"
type="number"
placeholder="MRP">

<input class="field"
id="productCategory"
placeholder="Category">

<textarea class="field"
id="productDescription"
placeholder="Product Description">
</textarea>

<input class="field"
id="productImage"
type="file"
accept="image/*">

<button class="primary"
onclick="addProduct()">

ADD PRODUCT

</button>


<h3>🛍️ Manage Products</h3>

<div id="adminProducts"></div>


<hr>

<h3>⭐ Reviews</h3>

<div id="adminReviews"></div>


<br>

<button class="red"
onclick="logout()">

LOGOUT

</button>

</div>

</div>
</div>


<script>

const PRODUCT_KEY="arslan_products";
const CART_KEY="arslan_cart";
const ORDER_KEY="arslan_orders";
const REVIEW_KEY="arslan_reviews";


let products=
JSON.parse(localStorage.getItem(PRODUCT_KEY)||"null")
||[

{
id:1,
name:"Daily Grocery Pack",
price:199,
mrp:249,
category:"Grocery",
description:"Daily-use grocery essentials.",
image:"https://images.unsplash.com/photo-1542838132-92c53300491e?auto=format&fit=crop&w=700&q=80"
},

{
id:2,
name:"Household Essentials",
price:299,
mrp:399,
category:"Household",
description:"Useful household products.",
image:"https://images.unsplash.com/photo-1583947215259-38e31be8751f?auto=format&fit=crop&w=700&q=80"
},

{
id:3,
name:"Snacks Combo",
price:149,
mrp:199,
category:"Snacks",
description:"Popular snacks combo.",
image:"https://images.unsplash.com/photo-1621939514649-280e2aa6e20f?auto=format&fit=crop&w=700&q=80"
},

{
id:4,
name:"Cleaning Essentials",
price:179,
mrp:229,
category:"Cleaning",
description:"Home cleaning essentials.",
image:"https://images.unsplash.com/photo-1585832770485-e68a5dbfad52?auto=format&fit=crop&w=700&q=80"
}

];


let cart=
JSON.parse(localStorage.getItem(CART_KEY)||"[]");

let orders=
JSON.parse(localStorage.getItem(ORDER_KEY)||"[]");

let reviews=
JSON.parse(localStorage.getItem(REVIEW_KEY)||"[]");

let currentCategory="All";


function save(){

localStorage.setItem(
PRODUCT_KEY,
JSON.stringify(products)
);

localStorage.setItem(
CART_KEY,
JSON.stringify(cart)
);

localStorage.setItem(
ORDER_KEY,
JSON.stringify(orders)
);

localStorage.setItem(
REVIEW_KEY,
JSON.stringify(reviews)
);

}


function safe(text){

return String(text||"")
.replace(/[&<>"']/g,function(x){

return {
"&":"&amp;",
"<":"&lt;",
">":"&gt;",
'"':"&quot;",
"'":"&#039;"
}[x];

});

}


function renderCategories(){

let categories=[
"All",
...new Set(products.map(p=>p.category))
];

document.getElementById("categories")
.innerHTML=categories.map(c=>`

<button class="category
${c===currentCategory?"active":""}"
onclick="setCategory('${safe(c)}')">

${safe(c)}

</button>

`).join("");

}


function setCategory(c){

currentCategory=c;
renderProducts();

}


function card(p){

let discount=p.mrp>p.price
?Math.round((1-p.price/p.mrp)*100)
:0;

return `

<article class="product">

${discount?
`<span class="badge">${discount}% OFF</span>`:""}

<div class="productImg">

<img src="${p.image}"
alt="${safe(p.name)}">

</div>

<h3>${safe(p.name)}</h3>

<div class="price">

₹${p.price}

<span class="mrp">
₹${p.mrp}
</span>

</div>

<div class="discount">
${discount}% OFF
</div>

<p class="muted">
${safe(p.description)}
</p>

<div class="actions">

<button class="add"
onclick="addCart(${p.id})">

ADD TO CART

</button>

<button class="buy"
onclick="buyNow(${p.id})">

BUY NOW

</button>

</div>

</article>

`;

}


function renderProducts(){

let search=
document.getElementById("search")
.value.toLowerCase();

let list=products.filter(p=>{

let categoryOK=
currentCategory==="All"||
p.category===currentCategory;

let searchOK=
(p.name+" "+p.category)
.toLowerCase()
.includes(search);

return categoryOK&&searchOK;

});

document.getElementById("productGrid")
.innerHTML=
list.map(card).join("")
||"<p>No products found.</p>";

document.getElementById("offers")
.innerHTML=
products
.filter(p=>p.mrp>p.price)
.slice(0,4)
.map(card)
.join("");

renderCategories();

updateCartCount();

}


function addCart(id){

let item=
cart.find(x=>x.id===id);

if(item)
item.quantity++;
else
cart.push({
id:id,
quantity:1
});

save();

renderProducts();

alert("Added to cart!");

}


function buyNow(id){

addCart(id);

checkout();

}


function updateCartCount(){

document.getElementById("cartCount")
.textContent=
cart.reduce(
(a,b)=>a+b.quantity,0
);

}


function cartTotal(){

return cart.reduce((total,item)=>{

let p=
products.find(x=>x.id===item.id);

return total+
(p?p.price*item.quantity:0);

},0);

}


function openCart(){

let html="";

cart.forEach(item=>{

let p=
products.find(x=>x.id===item.id);

if(!p)return;

html+=`

<div class="cartItem">

<img src="${p.image}">

<div style="flex:1">

<b>${safe(p.name)}</b>

<p>
₹${p.price} × ${item.quantity}
</p>

<div class="qty">

<button onclick="changeQty(${p.id},-1)">
−
</button>

${item.quantity}

<button onclick="changeQty(${p.id},1)">
+
</button>

</div>

</div>

</div>

`;

});

document.getElementById("cartItems")
.innerHTML=
html||"<p>Your cart is empty.</p>";

document.getElementById("subtotal")
.textContent="₹"+cartTotal();

document.getElementById("cartTotal")
.textContent="₹"+cartTotal();

openModal("cartModal");

}


function changeQty(id,n){

let item=
cart.find(x=>x.id===id);

if(item)
item.quantity+=n;

cart=
cart.filter(x=>x.quantity>0);

save();

openCart();

updateCartCount();

}


function checkout(){

if(!cart.length){

alert("Cart is empty!");

return;

}

closeModal("cartModal");

let bill="";

cart.forEach(item=>{

let p=
products.find(x=>x.id===item.id);

bill+=`

<div class="billRow">

<span>
${safe(p.name)} × ${item.quantity}
</span>

<b>
₹${p.price*item.quantity}
</b>

</div>

`;

});

bill+=`

<div class="billTotal">

<span>Total</span>

<span>₹${cartTotal()}</span>

</div>

`;

document.getElementById("checkoutBill")
.innerHTML=bill;

openModal("checkoutModal");

}


function placeOrder(){

let name=
document.getElementById("customerName")
.value.trim();

let phone=
document.getElementById("customerPhone")
.value.trim();

let address=
document.getElementById("customerAddress")
.value.trim();


if(!name||!phone||!address){

alert("Please fill Name, Mobile and Address.");

return;

}


let items=
cart.map(item=>{

let p=
products.find(x=>x.id===item.id);

return {

name:p.name,

price:p.price,

quantity:item.quantity

};

});


let total=
items.reduce(
(a,x)=>a+x.price*x.quantity,
0
);


let order={

id:"AGS-"+Date.now(),

customer:name,

phone:phone,

address:address,

items:items,

total:total,

payment:"Cash on Delivery",

status:"Pending",

date:new Date().toLocaleString()

};


orders.unshift(order);

cart=[];

save();

renderProducts();

document.getElementById("orderMessage")
.innerHTML=`

<p class="green">

✅ Order placed successfully!

<br>

Order ID: ${order.id}

<br>

Payment: Cash on Delivery

</p>

`;

}


function submitReview(){

let name=
document.getElementById("reviewName")
.value.trim();

let text=
document.getElementById("reviewText")
.value.trim();

let rating=
Number(
document.getElementById("reviewRating")
.value
);

let file=
document.getElementById("reviewPhoto")
.files[0];


if(!name||!text){

alert("Name and review required.");

return;

}


function finish(image=""){

reviews.unshift({

name:name,

text:text,

rating:rating,

image:image,

date:new Date().toLocaleDateString()

});

save();

renderReviews();

closeModal("reviewModal");

alert("Review submitted!");

}


if(file){

let reader=new FileReader();

reader.onload=()=>{
finish(reader.result);
};

reader.readAsDataURL(file);

}else{

finish();

}

}


function renderReviews(){

let html=
reviews.map(r=>`

<div class="review">

<b>${safe(r.name)}</b>

<span style="color:#f59e0b">
${"★".repeat(r.rating)}
</span>

<p>
${safe(r.text)}
</p>

${r.image?
`<img src="${r.image}">`
:""}

<br>

<small>${r.date}</small>

</div>

`).join("");

document.getElementById("reviews")
.innerHTML=
html||"<p class='muted'>No reviews yet.</p>";

}


function openAdmin(){

openModal("adminModal");

}


function loginAdmin(){

let u=
document.getElementById("adminUser").value;

let p=
document.getElementById("adminPass").value;


if(
u==="admin" &&
p==="MM@12345"
){

document.getElementById("adminLogin")
.style.display="none";

document.getElementById("dashboard")
.style.display="block";

renderAdmin();

}else{

alert("Wrong Username or Password");

}

}


function renderAdmin(){

renderOrders();

renderAdminProducts();

renderAdminReviews();

}


function renderOrders(){

let html="";

orders.forEach((o,i)=>{

html+=`

<div class="order">

<h3>${o.id}</h3>

<p>
👤 <b>${safe(o.customer)}</b>
<br>
📞 ${safe(o.phone)}
<br>
📍 ${safe(o.address)}
</p>

<p>

${o.items.map(x=>
safe(x.name)+
" × "+x.quantity+
" = ₹"+(x.price*x.quantity)
).join("<br>")}

</p>

<h3>Total: ₹${o.total}</h3>

<p>
💵 Cash on Delivery
</p>

<p>
Status:
<span class="status">
${o.status}
</span>
</p>

<select class="field"
onchange="changeStatus(${i},this.value)">

<option ${o.status==="Pending"?"selected":""}>
Pending
</option>

<option ${o.status==="Accepted"?"selected":""}>
Accepted
</option>

<option ${o.status==="Out for Delivery"?"selected":""}>
Out for Delivery
</option>

<option ${o.status==="Delivered"?"selected":""}>
Delivered
</option>

<option ${o.status==="Rejected"?"selected":""}>
Rejected
</option>

</select>

<button class="red"
onclick="deleteOrder(${i})">
Delete
</button>

</div>

`;

});

document.getElementById("orders")
.innerHTML=
html||"<p>No orders yet.</p>";

}


function changeStatus(i,status){

orders[i].status=status;

save();

renderOrders();

}


function deleteOrder(i){

if(confirm("Delete this order?")){

orders.splice(i,1);

save();

renderOrders();

}

}


function addProduct(){

let name=
document.getElementById("productName")
.value.trim();

let price=
Number(
document.getElementById("productPrice")
.value
);

let mrp=
Number(
document.getElementById("productMRP")
.value
);

let category=
document.getElementById("productCategory")
.value.trim();

let description=
document.getElementById("productDescription")
.value.trim();

let file=
document.getElementById("productImage")
.files[0];


if(
!name||
!price||
!mrp||
!category||
!description||
!file
){

alert("Please fill every field and select photo.");

return;

}


let reader=new FileReader();

reader.onload=function(){

products.push({

id:Date.now(),

name:name,

price:price,

mrp:mrp,

category:category,

description:description,

image:reader.result

});

save();

renderProducts();

renderAdminProducts();

alert("Product added!");

};

reader.readAsDataURL(file);

}


function renderAdminProducts(){

document.getElementById("adminProducts")
.innerHTML=
products.map((p,i)=>`

<div class="order">

<b>${safe(p.name)}</b>

— ₹${p.price}

<button
class="red"
style="float:right"
onclick="deleteProduct(${i})">

Delete

</button>

</div>

`).join("");

}


function deleteProduct(i){

if(confirm("Delete product?")){

products.splice(i,1);

save();

renderProducts();

renderAdminProducts();

}

}


function renderAdminReviews(){

document.getElementById("adminReviews")
.innerHTML=
reviews.map((r,i)=>`

<div class="order">

<b>${safe(r.name)}</b>

— ${r.rating}★

<p>${safe(r.text)}</p>

<button class="red"
onclick="deleteReview(${i})">

Delete Review

</button>

</div>

`).join("")
||"<p>No reviews.</p>";

}


function deleteReview(i){

reviews.splice(i,1);

save();

renderReviews();

renderAdminReviews();

}


function logout(){

document.getElementById("dashboard")
.style.display="none";

document.getElementById("adminLogin")
.style.display="block";

}


function openModal(id){

document.getElementById(id)
.style.display="flex";

}


function closeModal(id){

document.getElementById(id)
.style.display="none";

}


renderProducts();

renderReviews();

updateCartCount();

</script>

</body>
</html>
