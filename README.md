<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Girls - المنتجات</title>
  <style>
    body { font-family: Arial; background-color: #ffe6f0; margin:0; padding:20px; }
    h1 { text-align:center; color:#e91e63; }
    .products-grid { display:grid; grid-template-columns:repeat(auto-fit,minmax(250px,1fr)); gap:20px; margin-top:30px; }
    .product-card { background:white; border:2px solid #e91e63; border-radius:12px; overflow:hidden; text-align:center; padding:10px; }
    .product-card img { width:100%; height:200px; object-fit:cover; }
    .product-info h2 { color:#e91e63; margin:10px 0; }
    .product-info p { color:#666; font-size:14px; }
    .product-info .price { font-weight:bold; color:#e91e63; margin-top:5px; }
    button { margin-top:10px; padding:5px 10px; background:#e91e63; color:white; border:none; border-radius:5px; cursor:pointer; }
  </style>
</head>
<body>

<h1>منتجات The Girls</h1>
<div class="products-grid" id="productsGrid"></div>

<button onclick="adminLogin()">إدارة المنتجات</button>

<script>
  const password = "1234"; // هنا تحطي الباسورد اللي تحبي
  let products = [
    {name:"منتج 1", desc:"وصف المنتج 1", price:200, img:"https://via.placeholder.com/250x200.png?text=منتج+1"},
    {name:"منتج 2", desc:"وصف المنتج 2", price:350, img:"https://via.placeholder.com/250x200.png?text=منتج+2"}
  ];

  function displayProducts() {
    const grid = document.getElementById("productsGrid");
    grid.innerHTML = "";
    products.forEach((p,i)=>{
      const card = document.createElement("div");
      card.className = "product-card";
      card.innerHTML = `
        <img src="${p.img}" alt="${p.name}">
        <div class="product-info">
          <h2>${p.name}</h2>
          <p>${p.desc}</p>
          <div class="price">${p.price} جنيه</div>
          <button onclick="editProduct(${i})">تعديل السعر</button>
        </div>`;
      grid.appendChild(card);
    });
  }

  function adminLogin() {
    const pass = prompt("ادخلي الباسورد للتحكم بالمنتجات:");
    if(pass === password) {
      const choice = prompt("اكتبي 1 لإضافة منتج جديد، 2 لتعديل السعر:");
      if(choice === "1") addProduct();
      else if(choice === "2") {
        const index = prompt("اكتبي رقم المنتج اللي تحبي تعدلي سعره (0 هو أول منتج):");
        editProduct(Number(index));
      }
    } else alert("الباسورد غلط!");
  }

  function addProduct() {
    const name = prompt("اسم المنتج:");
    const desc = prompt("وصف المنتج:");
    const price = prompt("سعر المنتج:");
    const img = prompt("رابط الصورة:");
    products.push({name, desc, price: Number(price), img});
    displayProducts();
  }

  function editProduct(i) {
    if(i>=0 && i<products.length) {
      const newPrice = prompt("ادخلي السعر الجديد:", products[i].price);
      products[i].price = Number(newPrice);
      displayProducts();
    }
  }

  displayProducts();
</script>
</body>
</html>
