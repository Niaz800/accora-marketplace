
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ACCORA Marketplace</title>

<style>
*{box-sizing:border-box}
body{
 margin:0;
 font-family:Arial,sans-serif;
 background:#0b1120;
 color:white;
}
header{
 background:#111b2e;
 padding:18px;
 display:flex;
 justify-content:space-between;
 align-items:center;
 flex-wrap:wrap;
 gap:12px;
 border-bottom:1px solid #27344b;
}
.logo{
 font-size:26px;
 font-weight:bold;
 color:#ff4747;
 letter-spacing:2px;
}
nav button{
 padding:10px 15px;
 margin:4px;
 border:0;
 border-radius:7px;
 cursor:pointer;
 font-weight:bold;
}
.buyer{background:#e63946;color:white}
.seller{background:#18a999;color:white}
.container{
 max-width:1100px;
 margin:auto;
 padding:20px;
}
.hero{
 background:linear-gradient(135deg,#17243b,#243957);
 padding:35px 20px;
 border-radius:16px;
 text-align:center;
 margin-bottom:25px;
}
.hero h1{font-size:34px;margin:0 0 12px}
.hero p{color:#cbd5e1}
.search{
 display:flex;
 gap:10px;
 flex-wrap:wrap;
 margin:20px 0;
}
.search input,.search select{
 flex:1;
 min-width:160px;
 padding:13px;
 border-radius:8px;
 border:1px solid #334155;
 background:#111b2e;
 color:white;
}
.products{
 display:grid;
 grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
 gap:18px;
}
.card{
 background:#152137;
 padding:18px;
 border-radius:12px;
 border:1px solid #263750;
}
.card h3{margin-top:0}
.price{
 color:#36d399;
 font-size:20px;
 font-weight:bold;
}
.tag{
 display:inline-block;
 background:#24344d;
 padding:5px 9px;
 border-radius:20px;
 color:#b9c9df;
 font-size:12px;
}
.card button{
 width:100%;
 padding:11px;
 background:#e63946;
 color:white;
 border:0;
 border-radius:7px;
 margin-top:12px;
 cursor:pointer;
}
footer{
 text-align:center;
 padding:30px;
 color:#8b9bb4;
}
.modal{
 display:none;
 position:fixed;
 inset:0;
 background:#000b;
 justify-content:center;
 align-items:center;
 padding:15px;
 z-index:10;
}
.modalbox{
 width:100%;
 max-width:420px;
 background:#142037;
 padding:22px;
 border-radius:14px;
 max-height:90vh;
 overflow:auto;
}
.modalbox input,.modalbox select{
 width:100%;
 padding:12px;
 margin:8px 0;
 border-radius:7px;
 background:#0b1120;
 color:white;
 border:1px solid #334155;
}
.modalbox button{
 padding:12px;
 width:100%;
 margin-top:10px;
 border:0;
 border-radius:7px;
 cursor:pointer;
 background:#18a999;
 color:white;
 font-weight:bold;
}
.close{
 background:#475569!important;
}
</style>
</head>

<body>

<header>
<div class="logo">ACCORA</div>
<nav>
<button class="buyer" onclick="openForm('Buyer')">Buyer Register</button>
<button class="seller" onclick="openForm('Seller')">Seller Register</button>
</nav>
</header>

<div class="container">

<div class="hero">
<h1>ACCORA Marketplace</h1>
<p>Discover Digital Products, Services & Opportunities</p>
<p>A global marketplace for buyers and sellers.</p>
</div>

<div class="search">
<input id="search" placeholder="Search products..." oninput="render()">
<select id="category" onchange="render()">
<option value="">All Categories</option>
<option>Websites</option>
<option>Domains</option>
<option>Gaming Assets</option>
<option>Digital Businesses</option>
<option>Verification Services</option>
</select>
</div>

<div id="products" class="products"></div>

</div>

<footer>
ACCORA Marketplace © 2026
</footer>

<div class="modal" id="modal">
<div class="modalbox">
<h2 id="formtitle">Registration</h2>

<form id="regform">
<input id="role" type="hidden">

<input id="fullname" placeholder="Full Name" required>
<input id="email" type="email" placeholder="Email Address" required>
<input id="country" placeholder="Country" required>
<input id="password" type="password" placeholder="Password" required>
<input id="confirm" type="password" placeholder="Confirm Password" required>

<button type="submit">Create Account</button>
<button type="button" class="close" onclick="closeForm()">Close</button>
</form>

<p style="font-size:12px;color:#94a3b8">
Demo registration only. Real accounts require secure authentication and a backend.
</p>
</div>
</div>

<script>
const products=[
{
name:"Premium Website",
category:"Websites",
price:"$250",
description:"Ready-made website project"
},
{
name:"Premium Domain",
category:"Domains",
price:"$120",
description:"Premium domain listing"
},
{
name:"Gaming Digital Asset",
category:"Gaming Assets",
price:"$50",
description:"Digital gaming asset listing"
},
{
name:"Online Business",
category:"Digital Businesses",
price:"$800",
description:"Digital business opportunity"
},
{
name:"Verification Support Service",
category:"Verification Services",
price:"Contact Seller",
description:"Business verification support service"
},
{
name:"E-commerce Store",
category:"Websites",
price:"$500",
description:"Online store website"
}
];

function render(){
 const q=document.getElementById("search").value.toLowerCase();
 const c=document.getElementById("category").value;
 const filtered=products.filter(p=>
  p.name.toLowerCase().includes(q) &&
  (!c||p.category===c)
 );
 document.getElementById("products").innerHTML=filtered.map(p=>`
  <div class="card">
   <span class="tag">${p.category}</span>
   <h3>${p.name}</h3>
   <p>${p.description}</p>
   <div class="price">${p.price}</div>
   <button onclick="contactSeller('${p.name}')">View Listing</button>
  </div>
 `).join("");
}

function contactSeller(name){
 alert("Listing: "+name+"\nContact and purchase features will be added later.");
}

function openForm(role){
 document.getElementById("modal").style.display="flex";
 document.getElementById("role").value=role;
 document.getElementById("formtitle").innerText=role+" Registration";
}

function closeForm(){
 document.getElementById("modal").style.display="none";
}

document.getElementById("regform").addEventListener("submit",function(e){
 e.preventDefault();
 const p=document.getElementById("password").value;
 const c=document.getElementById("confirm").value;

 if(p!==c){
  alert("Passwords do not match!");
  return;
 }

 alert("Registration demo completed!\nRole: "+document.getElementById("role").value+"\nEmail: "+document.getElementById("email").value+"\n\nReal account registration is not connected yet.");
 this.reset();
 closeForm();
});

render();
</script>

</body>
</html>
