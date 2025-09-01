# well-is-age<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>E-SHOP — Marketplace</title>
  <style>
    :root{
      --brand:#2874f0; /* Flipkart-like blue */
      --muted:#6b7280;
      --card-bg: #fff;
      --page-bg: #f3f4f6;
      --accent:#ff9900;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family: Inter, system-ui, Arial, sans-serif;
      background:var(--page-bg);
      color:#111827;
      -webkit-font-smoothing:antialiased;
    }

    /* Header */
    .topbar{
      background:var(--brand);
      color:white;
      padding:10px 18px;
      display:flex;
      align-items:center;
      gap:20px;
      position:sticky;
      top:0;
      z-index:40;
      box-shadow:0 2px 6px rgba(0,0,0,0.08);
    }
    .logo{
      display:flex;
      align-items:center;
      gap:10px;
      font-weight:700;
      font-size:20px;
    }
    .logo .marker{
      width:36px;height:36px;border-radius:6px;background:linear-gradient(45deg,#fff 0 40%, rgba(255,255,255,0.2) 40%);display:inline-block;
    }
    /* Search */
    .search-wrap{flex:1;display:flex;align-items:center;gap:8px}
    .search{
      display:flex;align-items:center;
      width:100%;max-width:760px;background:white;border-radius:4px;padding:8px;
      box-shadow:0 1px 2px rgba(0,0,0,0.08);
    }
    .search input{flex:1;border:0;outline:none;padding:10px;font-size:15px}
    .search button{background:var(--accent);border:0;padding:9px 12px;border-radius:4px;font-weight:700;color:#111}

    .top-actions{display:flex;gap:12px;align-items:center}
    .top-actions a{color:white;text-decoration:none;font-weight:600}

    /* Categories bar */
    .cats{display:flex;gap:12px;padding:10px 18px;background:#fff;border-bottom:1px solid rgba(0,0,0,0.06)}
    .cat{background:transparent;padding:8px 12px;border-radius:4px;color:var(--muted);font-weight:600}

    /* Layout */
    .container{display:flex;gap:20px;padding:20px;max-width:1200px;margin:18px auto}

    /* Sidebar */
    .sidebar{width:250px;background:white;border-radius:8px;padding:14px;height:min-content;box-shadow:0 2px 8px rgba(0,0,0,0.06)}
    .filter h4{margin:0 0 8px 0;font-size:14px;color:var(--muted)}
    .filter label{display:block;margin:6px 0;color:#374151}

    /* Main content */
    .main{flex:1;display:flex;flex-direction:column;gap:18px}
    /* Hero carousel (basic) */
    .hero{position:relative;height:220px;border-radius:10px;overflow:hidden;background:linear-gradient(90deg,#e6f0ff,#fff)}
    .hero .slides{display:flex;height:100%;transition:transform .5s ease}
    .hero .slide{min-width:100%;display:flex;align-items:center;justify-content:space-between;padding:20px}
    .hero img{max-height:160px;border-radius:8px}
    .hero .info{max-width:60%}
    .hero h2{margin:0 0 10px 0;font-size:28px;color:var(--brand)}
    .hero p{margin:0;color:var(--muted)}

    .hero .nav{position:absolute;left:10px;right:10px;bottom:10px;display:flex;justify-content:center;gap:8px}
    .dot{width:10px;height:6px;border-radius:6px;background:rgba(0,0,0,0.2);cursor:pointer}
    .dot.active{background:var(--brand);height:8px}

    /* Product grid */
    .products-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));gap:16px}
    .card{
      background:var(--card-bg);padding:12px;border-radius:10px;box-shadow:0 2px 8px rgba(0,0,0,0.06);
      display:flex;flex-direction:column;align-items:center;text-align:center;gap:8px;
    }
    .card img{width:100%;height:140px;object-fit:cover;border-radius:8px}
    .card h3{font-size:16px;margin:4px 0}
    .price{font-weight:800;color:var(--brand)}
    .rating{font-size:13px;color:#10b981}

    .card .btns{display:flex;gap:8px;margin-top:8px;width:100%}
    .btn{flex:1;padding:8px;border-radius:6px;border:0;cursor:pointer;font-weight:700}
    .btn.cart{background:var(--brand);color:white}
    .btn.order{background:#111;color:white}

    /* Cart drawer */
    .cart-drawer{position:fixed;right:18px;top:70px;width:360px;max-height:75vh;background:white;border-radius:10px;box-shadow:0 12px 30px rgba(0,0,0,0.12);overflow:auto;transform:translateX(120%);transition:transform .3s}
    .cart-drawer.open{transform:translateX(0)}
    .cart-drawer header{padding:12px;border-bottom:1px solid rgba(0,0,0,0.06);display:flex;justify-content:space-between;align-items:center;font-weight:700}
    .cart-item{display:flex;gap:10px;padding:10px;border-bottom:1px solid rgba(0,0,0,0.04);align-items:center}
    .cart-item img{width:60px;height:60px;object-fit:cover;border-radius:6px}
    .cart-actions{display:flex;justify-content:space-between;padding:12px}

    /* Login modal */
    .modal-backdrop{position:fixed;inset:0;background:rgba(0,0,0,0.5);display:none;align-items:center;justify-content:center;z-index:60}
    .modal{background:white;padding:20px;border-radius:10px;width:360px}
    .modal h3{margin-top:0}

    /* Footer */
    footer{padding:24px 18px;background:#111827;color:white;margin-top:30px;text-align:center}

    /* Responsive */
    @media (max-width:900px){
      .container{padding:12px}
      .sidebar{display:none}
      .hero{height:160px}
    }
  </style>
</head>
<body>

  <!-- Topbar -->
  <div class="topbar">
    <div class="logo">
      <span class="marker" aria-hidden></span>
      <span>E-SHOP</span>
    </div>

    <div class="search-wrap">
      <div class="search" role="search">
        <input id="globalSearch" placeholder="Search for products, brands and more" aria-label="Search">
        <button id="searchBtn">Search</button>
      </div>
    </div>

    <div class="top-actions">
      <a href="#" id="loginBtn">Login</a>
      <a href="#" id="ordersLink">Orders</a>
      <a href="#" id="cartToggle">Cart (<span id="cartCount">0</span>)</a>
    </div>
  </div>

  <!-- Categories -->
  <div class="cats">
    <div class="cat">Electronics</div>
    <div class="cat">Mobiles</div>
    <div class="cat">Fashion</div>
    <div class="cat">Home</div>
    <div class="cat">Appliances</div>
    <div class="cat">Beauty</div>
    <div class="cat">Grocery</div>
  </div>

  <!-- Main -->
  <div class="container">
    <!-- Sidebar -->
    <aside class="sidebar">
      <div class="filter">
        <h4>Filters</h4>
        <label><input type="checkbox" class="brand-filter" value="BrandA"> BrandA</label>
        <label><input type="checkbox" class="brand-filter" value="BrandB"> BrandB</label>
        <label><input type="checkbox" class="brand-filter" value="BrandC"> BrandC</label>
      </div>

      <div style="height:14px"></div>

      <div class="filter">
        <h4>Price</h4>
        <label><input type="radio" name="price" value="under1000"> Under ₹1,000</label>
        <label><input type="radio" name="price" value="1000-5000"> ₹1,000 - ₹5,000</label>
        <label><input type="radio" name="price" value="5000plus"> ₹5,000+</label>
      </div>
    </aside>

    <!-- Main content -->
    <main class="main">
      <!-- Hero / Carousel -->
      <div class="hero" id="hero">
        <div class="slides" id="slides">
          <div class="slide">
            <div class="info">
              <h2>Big Savings on Electronics</h2>
              <p>Latest smartphones, laptops and accessories — best deals of the season.</p>
            </div>
            <img src="https://via.placeholder.com/360x160?text=Electronics" alt="hero1">
          </div>
          <div class="slide">
            <div class="info">
              <h2>Fashion Sale: Up to 70% OFF</h2>
              <p>Refresh your wardrobe with trending looks and unbeatable prices.</p>
            </div>
            <img src="https://via.placeholder.com/360x160?text=Fashion" alt="hero2">
          </div>
          <div class="slide">
            <div class="info">
              <h2>Home & Kitchen Essentials</h2>
              <p>Everyday appliances and decor to beautify your home.</p>
            </div>
            <img src="https://via.placeholder.com/360x160?text=Home+%26+Kitchen" alt="hero3">
          </div>
        </div>

        <div class="nav" id="dots"></div>
      </div>

      <!-- Featured row -->
      <section>
        <h3 style="margin:8px 0 12px">Top Picks for You</h3>
        <div class="products-grid" id="productGrid">
          <!-- Product cards (generated by JS below) -->
        </div>
      </section>

      <!-- Large category banner row -->
      <section style="margin-top:18px">
        <div style="display:flex;gap:12px">
          <div style="flex:1;background:white;padding:14px;border-radius:10px;display:flex;align-items:center;gap:12px">
            <img src="https://via.placeholder.com/220x120?text=Big+Deals" style="border-radius:8px">
            <div>
              <h3 style="margin:0;color:var(--brand)">Super Value Offers</h3>
              <p style="margin:6px 0;color:var(--muted)">Daily discounts on essentials and trending products.</p>
            </div>
          </div>
          <div style="width:300px;background:white;padding:12px;border-radius:10px;display:flex;flex-direction:column;justify-content:center">
            <h4 style="margin:0 0 8px 0">Bank Offers</h4>
            <p style="margin:0;color:var(--muted)">Extra 10% off with selected cards. Free EMI available.</p>
          </div>
        </div>
      </section>

    </main>
  </div>

  <!-- Cart drawer -->
  <aside class="cart-drawer" id="cartDrawer" aria-hidden="true">
    <header>
      <span>Your Cart (<span id="drawerCount">0</span>)</span>
      <button onclick="toggleCart()">Close</button>
    </header>
    <div id="cartItems"></div>
    <div class="cart-actions">
      <div><strong>Total:</strong> ₹<span id="cartTotal">0</span></div>
      <button class="btn order" onclick="placeOrder()">Place Order</button>
    </div>
  </aside>

  <!-- Login modal -->
  <div class="modal-backdrop" id="modalBackdrop">
    <div class="modal" role="dialog" aria-modal="true">
      <h3>Sign in to E-SHOP</h3>
      <input id="loginEmail" placeholder="Email" style="width:100%;padding:10px;margin:8px 0;border:1px solid #e5e7eb;border-radius:6px">
      <input id="loginPass" placeholder="Password" type="password" style="width:100%;padding:10px;margin:8px 0;border:1px solid #e5e7eb;border-radius:6px">
      <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:8px">
        <button class="btn" onclick="closeModal()">Cancel</button>
        <button class="btn cart" onclick="fakeLogin()">Sign In</button>
      </div>
    </div>
  </div>

  <!-- Footer -->
  <footer>
    <div style="max-width:1200px;margin:0 auto;display:flex;justify-content:space-between;gap:20px;flex-wrap:wrap">
      <div>
        <strong>E-SHOP</strong>
        <p style="margin:6px 0;color:#9ca3af">Secure payments • Easy returns • 24/7 support</p>
      </div>
      <div>
        <strong>Company</strong>
        <p style="margin:6px 0;color:#9ca3af">About · Careers · Contact</p>
      </div>
      <div>
        <strong>Help</strong>
        <p style="margin:6px 0;color:#9ca3af">Shipping · Returns · FAQ</p>
      </div>
    </div>
    <div style="margin-top:14px;color:#9ca3af;font-size:14px">&copy; 2025 E-SHOP. All rights reserved.</div>
  </footer>

<script>
  /* ===== sample product data ===== */
  const sampleProducts = [
    {id:1,name:"Smartphone X200",brand:"BrandA",price:17999,rating:4.4,img:"https://via.placeholder.com/400x300?text=Phone+X200"},
    {id:2,name:"Wireless Headphones",brand:"BrandB",price:2499,rating:4.6,img:"https://via.placeholder.com/400x300?text=Headphones"},
    {id:3,name:"Smart LED TV 43\"",brand:"BrandA",price:25999,rating:4.3,img:"https://via.placeholder.com/400x300?text=Smart+TV"},
    {id:4,name:"Men's Sneakers",brand:"BrandC",price:1999,rating:4.1,img:"https://via.placeholder.com/400x300?text=Sneakers"},
    {id:5,name:"Blender Mixer",brand:"BrandB",price:3499,rating:4.0,img:"https://via.placeholder.com/400x300?text=Blender"},
    {id:6,name:"Women Handbag",brand:"BrandC",price:1299,rating:4.2,img:"https://via.placeholder.com/400x300?text=Handbag"},
    {id:7,name:"Laptop Pro 14\"",brand:"BrandA",price:74999,rating:4.7,img:"https://via.placeholder.com/400x300?text=Laptop+Pro"},
    {id:8,name:"Smart Watch",brand:"BrandB",price:3999,rating:4.0,img:"https://via.placeholder.com/400x300?text=Smart+Watch"},
  ];

  /* ===== render products ===== */
  const productGrid = document.getElementById('productGrid');
  const cartCountEl = document.getElementById('cartCount');
  const drawerCountEl = document.getElementById('drawerCount');
  const cartItemsEl = document.getElementById('cartItems');
  const cartTotalEl = document.getElementById('cartTotal');

  let cart = [];

  function renderProducts(list){
    productGrid.innerHTML = '';
    list.forEach(p=>{
      const card = document.createElement('div');
      card.className = 'card';
      card.innerHTML = `
        <img src="${p.img}" alt="${p.name}">
        <h3>${p.name}</h3>
        <div style="color:var(--muted);font-size:13px">${p.brand}</div>
        <div class="price">₹ ${p.price.toLocaleString()}</div>
        <div class="rating">★ ${p.rating}</div>
        <div class="btns">
          <button class="btn cart" onclick="addToCart(${p.id})">Add to Cart</button>
          <button class="btn order" onclick="orderNow(${p.id})">Order</button>
        </div>
      `;
      productGrid.appendChild(card);
    });
  }
  renderProducts(sampleProducts);

  /* ===== search/filter ===== */
  const searchInput = document.getElementById('globalSearch');
  searchInput.addEventListener('input', ()=>{
    const q = searchInput.value.trim().toLowerCase();
    const filtered = sampleProducts.filter(p=> p.name.toLowerCase().includes(q) || p.brand.toLowerCase().includes(q));
    renderProducts(filtered);
  });

  /* ===== cart functions ===== */
  function addToCart(id){
    const prod = sampleProducts.find(p=>p.id===id);
    const existing = cart.find(c=>c.id===id);
    if(existing){ existing.qty += 1; } else { cart.push({...prod, qty:1}); }
    updateCartUI();
    openCart();
  }

  function orderNow(id){
    const prod = sampleProducts.find(p=>p.id===id);
    alert('Order placed for: ' + prod.name + '\\n( Demo only — integrate backend to process real orders )');
  }

  function updateCartUI(){
    cartCountEl.textContent = cart.reduce((s,c)=>s+c.qty,0);
    drawerCountEl.textContent = cartCountEl.textContent;
    cartItemsEl.innerHTML = '';
    let total = 0;
    cart.forEach(i=>{
      total += i.price * i.qty;
      const item = document.createElement('div');
      item.className = 'cart-item';
      item.innerHTML = `
        <img src="${i.img}">
        <div style="flex:1">
          <div style="font-weight:700">${i.name}</div>
          <div style="color:var(--muted);font-size:13px">${i.brand} • ₹${i.price.toLocaleString()}</div>
          <div style="margin-top:8px;display:flex;gap:6px;align-items:center">
            <button onclick="changeQty(${i.id}, -1)">-</button>
            <div style="min-width:28px;text-align:center">${i.qty}</div>
            <button onclick="changeQty(${i.id}, 1)">+</button>
          </div>
        </div>
        <div>₹${(i.price*i.qty).toLocaleString()}</div>
      `;
      cartItemsEl.appendChild(item);
    });
    cartTotalEl.textContent = total.toLocaleString();
  }
  function changeQty(id, delta){
    const idx = cart.findIndex(c=>c.id===id);
    if(idx<0) return;
    cart[idx].qty += delta;
    if(cart[idx].qty<=0) cart.splice(idx,1);
    updateCartUI();
  }

  /* Cart drawer toggle */
  const cartDrawer = document.getElementById('cartDrawer');
  const cartToggle = document.getElementById('cartToggle');
  cartToggle.addEventListener('click', (e)=>{
    e.preventDefault();
    toggleCart();
  });
  function toggleCart(){
    cartDrawer.classList.toggle('open');
    cartDrawer.setAttribute('aria-hidden', !cartDrawer.classList.contains('open'));
  }
  function openCart(){ cartDrawer.classList.add('open'); cartDrawer.setAttribute('aria-hidden','false'); }

  /* Place order (demo) */
  function placeOrder(){
    if(cart.length===0){ alert('Your cart is empty'); return; }
    alert('Thanks! Your order has been placed (demo). Total: ₹' + cart.reduce((s,c)=>s+c.price*c.qty,0));
    cart = []; updateCartUI(); toggleCart();
  }

  /* ===== hero carousel ===== */
  let slideIndex = 0;
  const slidesEl = document.getElementById('slides');
  const dotsEl = document.getElementById('dots');
  const slidesCount = slidesEl.children.length;
  for(let i=0;i<slidesCount;i++){
    const d = document.createElement('div');
    d.className = 'dot' + (i===0?' active':'');
    d.dataset.i = i;
    d.addEventListener('click', ()=>{ gotoSlide(Number(d.dataset.i)); });
    dotsEl.appendChild(d);
  }
  function gotoSlide(i){
    slideIndex = i % slidesCount;
    slidesEl.style.transform = `translateX(-${slideIndex*100}%)`;
    Array.from(dotsEl.children).forEach((x,idx)=>x.classList.toggle('active', idx===slideIndex));
  }
  function nextSlide(){ gotoSlide((slideIndex+1)%slidesCount); }
  setInterval(nextSlide, 4000);

  /* ===== login modal ===== */
  const modal = document.getElementById('modalBackdrop');
  document.getElementById('loginBtn').addEventListener('click', (e)=>{
    e.preventDefault(); modal.style.display = 'flex';
  });
  function closeModal(){ modal.style.display = 'none'; }
  function fakeLogin(){
    const email = document.getElementById('loginEmail').value;
    if(!email){ alert('Enter email (demo)'); return; }
    alert('Signed in as ' + email + ' (demo only)');
    closeModal();
  }

  /* ===== small helpers ===== */
  document.getElementById('searchBtn').addEventListener('click', ()=>{
    const e = new Event('input'); searchInput.dispatchEvent(e);
  });

  // initial UI update
  updateCartUI();
</script>
</body>
</html>
