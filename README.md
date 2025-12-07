# BoiKini.com
<html lang="bn">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>boikini.com </title>
  <style>
    /* ====== Reset & base ====== */
    *{box-sizing:border-box;margin:0;padding:0}
    html,body{height:100%;font-family:Inter, system-ui, -apple-system, 'Noto Sans Bengali', Arial, sans-serif;background:#a507d1;color:#111}
    a{color:inherit;text-decoration:none}
    img{max-width:100%;display:block}

    /* ====== Layout ====== */
    header{background:linear-gradient(90deg,#cbd40f,#8ce81c);color:#fff;padding:18px}
    .container{max-width:1100px;margin:18px auto;padding:0 16px}
    .brand{display:flex;align-items:center;gap:12px}
    .brand h1{font-size:20px}
    nav{margin-left:auto;display:flex;gap:8px;align-items:center}
    .btn{background:#fff;color:#036; padding:8px 14px;border-radius:10px;font-weight:600;cursor:pointer}
    .btn.outline{background:transparent;border:1px solid rgba(255,255,255,.3);color:#fff}

    /* ====== Hero ====== */
    .hero{display:grid;grid-template-columns:1fr 360px;gap:18px;align-items:center;margin-top:18px}
    .hero-card{background:#fff;border-radius:14px;padding:18px;box-shadow:0 6px 18px rgba(12,15,30,.06)}
    .hero h2{font-size:26px;margin-bottom:10px}
    .search{display:flex;gap:8px;margin-top:10px}
    input.search-input{flex:1;padding:10px 12px;border-radius:10px;border:1px solid #e6eef5}

    /* ====== Product grid ====== */
    .grid{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;margin:18px 0}
    .card{background:#fff;border-radius:12px;padding:12px;box-shadow:0 6px 16px rgba(12,15,30,.04);display:flex;flex-direction:column}
    .card .meta{display:flex;gap:10px;align-items:center}
    .card h3{font-size:16px;margin:8px 0}
    .price{font-weight:700;color:#0b7285}
    .actions{margin-top:auto;display:flex;gap:8px}

    /* ====== Sidebar cart ====== */
    .sidebar{background:#fff;padding:12px;border-radius:12px;box-shadow:0 6px 18px rgba(12,15,30,.06)}
    .cart-list{max-height:320px;overflow:auto;margin:8px 0}
    .cart-item{display:flex;gap:10px;align-items:center;justify-content:space-between;padding:8px 0;border-bottom:1px dashed #eee}

    /* ====== Admin panel ====== */
    .admin-panel{display:none;background:#fff;padding:12px;border-radius:12px;margin-top:12px}
    .form-row{display:flex;gap:10px}
    .form-row input, textarea{flex:1;padding:8px;border-radius:8px;border:1px solid #e4eef6}

    /* ====== Footer ====== */
    footer{margin-top:30px;padding:18px;text-align:center;color:#1bd312}

    /* ====== Modals ====== */
    .modal-backdrop{position:fixed;inset:0;background:rgba(2,6,23,.5);display:none;align-items:center;justify-content:center;padding:18px}
    .modal{width:100%;max-width:520px;background:#fff;padding:16px;border-radius:12px}

    /* ====== Responsive ====== */
    @media (max-width:980px){
      .hero{grid-template-columns:1fr}
      .grid{grid-template-columns:repeat(2,1fr)}
    }
    @media (max-width:640px){
      nav{display:none}
      .grid{grid-template-columns:1fr}
      .brand h1{font-size:18px}
      .hero{gap:10px}
    }

    /* small helpers */
    .muted{color:#64748b;font-size:13px}
    .badge{background:#eef2ff;color:#3730a3;padding:6px 8px;border-radius:999px;font-size:12px}
    .input,textarea{padding:8px;border:1px solid #e5eef8;border-radius:8px}
  </style>
</head>
<body>
  <header>
    <div class="container" style="display:flex;align-items:center">
      <div class="brand">
        <svg width="40" height="40" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="24" height="24" rx="6" fill="#fff"/><path d="M6 7h12v2H6zM6 11h12v2H6zM6 15h8v2H6z" fill="#06b6d4"/></svg>
        <div>
          <h1>boikini.com</h1>
          <div class="muted">বাংলার সবচেয়ে সহজ অনলাইন বুকশপ</div>
        </div>
      </div>

      <nav>
        <button class="btn" id="openSignup">সাইন আপ</button>
        <button class="btn outline" id="openLogin">লগ ইন</button>
        <button class="btn" id="openAdminLogin">অ্যাডমিন</button>
        <button class="btn" id="toggleCart">কার্ট (<span id="cartCount">0</span>)</button>
      </nav>
    </div>
  </header>

  <main class="container">
    <section class="hero">
      <div class="hero-card">
        <h2>Welcome - boikini.com</h2>
        <p class="muted">বুক দিতেই চান? বই সারান, কার্টে যোগ করুন, অর্ডার করুন — সব এক পেজেই।</p>

        <div class="search">
          <input class="search-input" id="searchInput" placeholder="বই খুঁজুন — শিরোনাম, লেখক...">
          <button class="btn" id="searchBtn">খুঁজুন</button>
        </div>

        <div style="margin-top:12px;display:flex;gap:8px;flex-wrap:wrap">
          <span class="badge" id="userBadge">অতিথি</span>
          <button class="btn outline" id="showAll">সব বই</button>
          <button class="btn" id="exportCSV">CSV ডাউনলোড</button>
        </div>

        <div id="productSection" style="margin-top:14px"></div>
      </div>

      <aside class="sidebar">
        <h3>আপনার কার্ট</h3>
        <div class="cart-list" id="cartList"></div>
        <div style="display:flex;justify-content:space-between;align-items:center;margin-top:10px">
          <strong>মোট: ৳<span id="cartTotal">0</span></strong>
          <button class="btn" id="checkoutBtn">চেকআউট</button>
        </div>

        <div class="admin-panel" id="adminPanel">
          <h4>অ্যাডমিন প্যানেল</h4>
          <div style="margin-top:8px">
            <div class="form-row" style="margin-bottom:8px">
              <input id="newTitle" placeholder="বইয়ের শিরোনাম">
              <input id="newAuthor" placeholder="লেখক">
            </div>
            <div class="form-row" style="margin-bottom:8px">
              <input id="newPrice" placeholder="মূল্য (৳)">
              <input id="newImage" placeholder="ছবির URL (ঐচ্ছিক)">
            </div>
            <textarea id="newDesc" placeholder="বর্ণনা" rows="3" style="width:100%"></textarea>
            <div style="display:flex;gap:8px;margin-top:8px">
              <button class="btn" id="addProductBtn">বই যোগ করুন</button>
              <button class="btn outline" id="clearProducts">সব মুছুন</button>
            </div>
          </div>
        </div>
      </aside>
    </section>

    <section>
      <h3 style="margin-top:18px">Bestseller</h3>
      <div class="grid" id="productGrid"></div>
    </section>

    <footer>
      © boikini.com — 2025. Developed By SHAREA SOBUJ SHISHIR
    </footer>
  </main>

  <!-- ====== Modals ====== -->
  <div class="modal-backdrop" id="modalBackdrop">
    <div class="modal" id="modalContent"></div>
  </div>

  <script>
    /***** Simple one-page dynamic bookstore *****/

    // --- initial sample products ---
    const SAMPLE_PRODUCTS = [
      {id:genId(),title:'শিয়াল দৌড়',author:'হুমায়ূন আহমেদ',price:220,desc:'কিছু টিডি লেখা বিবরণ',img:''},
      {id:genId(),title:'কাঁচা বাদাম',author:'রবীন্দ্রনাথ',price:150,desc:'প্রিয় কাব্য',img:''},
      {id:genId(),title:'জানু কাঁদে',author:'সুনীল গঙ্গোপাধ্যায়',price:300,desc:'উপন্যাস',img:''},
    ];

    // --- admin credential (demo) ---
    const ADMIN_CREDENTIAL = {email:'admin@boikini.com', password:'admin123'};

    // --- DOM refs ---
    const productGrid = document.getElementById('productGrid');
    const cartList = document.getElementById('cartList');
    const cartCount = document.getElementById('cartCount');
    const cartTotal = document.getElementById('cartTotal');
    const userBadge = document.getElementById('userBadge');
    const adminPanel = document.getElementById('adminPanel');
    const productSection = document.getElementById('productSection');

    // --- local storage keys ---
    const KEY_PRODUCTS = 'boikini_products_v1';
    const KEY_CART = 'boikini_cart_v1';
    const KEY_USER = 'boikini_user_v1';

    // --- initial boot ---
    function boot(){
      if(!localStorage.getItem(KEY_PRODUCTS)){
        localStorage.setItem(KEY_PRODUCTS, JSON.stringify(SAMPLE_PRODUCTS));
      }
      renderProducts();
      renderCart();
      renderUserBadge();
    }

    // --- util ---
    function genId(){return 'p_'+Math.random().toString(36).slice(2,9)}

    function getProducts(){return JSON.parse(localStorage.getItem(KEY_PRODUCTS) || '[]')}
    function setProducts(arr){localStorage.setItem(KEY_PRODUCTS, JSON.stringify(arr))}

    function getCart(){return JSON.parse(localStorage.getItem(KEY_CART) || '[]')}
    function setCart(arr){localStorage.setItem(KEY_CART, JSON.stringify(arr))}

    function getUser(){return JSON.parse(localStorage.getItem(KEY_USER) || 'null')}
    function setUser(u){localStorage.setItem(KEY_USER, JSON.stringify(u))}

    // --- render products list (grid + section) ---
    function renderProducts(filter=''){
      const products = getProducts().filter(p => (p.title+ ' '+ p.author + ' '+ (p.desc||'')).toLowerCase().includes(filter.toLowerCase()));
      productGrid.innerHTML = '';
      productSection.innerHTML = '';
      products.forEach(p => {
        const card = document.createElement('div');
        card.className='card';
        card.innerHTML = `
          <div style="height:160px;background:#f8fafc;border-radius:8px;display:flex;align-items:center;justify-content:center;overflow:hidden">
            ${p.img? `<img src="${escapeHtml(p.img)}" alt="${escapeHtml(p.title)}">` : `<div style=\"font-size:40px;color:#94a3b8\">📚</div>`}
          </div>
          <h3>${escapeHtml(p.title)}</h3>
          <div class="muted">${escapeHtml(p.author)}</div>
          <div style="display:flex;justify-content:space-between;align-items:center;margin-top:8px">
            <div class="price">৳${Number(p.price).toFixed(0)}</div>
            <div class="actions">
              <button class="btn" onclick="viewProduct('${p.id}')">বিস্তারিত</button>
              <button class="btn outline" onclick="addToCart('${p.id}')">কার্টে যোগ</button>
            </div>
          </div>
        `;
        productGrid.appendChild(card);

        // also render a compact item in productSection
        const short = document.createElement('div');
        short.style.marginTop='8px';
        short.innerHTML = `<strong>${escapeHtml(p.title)}</strong> — <span class="muted">${escapeHtml(p.author)}</span> <div class=\"muted\">৳${Number(p.price)}</div>`;
        productSection.appendChild(short);
      });
    }

    // --- view product modal ---
    function viewProduct(id){
      const p = getProducts().find(x=>x.id===id);
      if(!p) return alert('পণ্য পাওয়া যায়নি');
      showModal(`
        <h3>${escapeHtml(p.title)}</h3>
        <div class="muted">${escapeHtml(p.author)}</div>
        <div style="margin:12px 0">${p.img? `<img src="${escapeHtml(p.img)}" alt="${escapeHtml(p.title)}">` : ''}</div>
        <p>${escapeHtml(p.desc||'বর্ণনা নেই')}</p>
        <div style="display:flex;gap:8px;justify-content:flex-end;margin-top:12px">
          <button class="btn outline" onclick="closeModal()">বন্ধ</button>
          <button class="btn" onclick="addToCart('${p.id}'); closeModal();">কার্টে যোগ</button>
        </div>
      `);
    }

    // --- cart functions ---
    function addToCart(id){
      const cart = getCart();
      const prod = getProducts().find(p=>p.id===id);
      if(!prod) return alert('পণ্য পাওয়া যায়নি');
      const found = cart.find(c=>c.id===id);
      if(found) found.qty += 1; else cart.push({id:id, qty:1, title:prod.title, price:prod.price});
      setCart(cart); renderCart();
    }

    function renderCart(){
      const cart = getCart();
      cartList.innerHTML='';
      let total=0; let count=0;
      cart.forEach(item=>{
        total += item.qty * Number(item.price);
        count += item.qty;
        const div = document.createElement('div');
        div.className='cart-item';
        div.innerHTML = `
          <div style="flex:1">
            <div><strong>${escapeHtml(item.title)}</strong></div>
            <div class="muted">৳${Number(item.price)} × ${item.qty}</div>
          </div>
          <div style="display:flex;gap:6px;align-items:center">
            <button class="btn outline" onclick="changeQty('${item.id}', -1)">−</button>
            <button class="btn" onclick="changeQty('${item.id}', 1)">+</button>
            <button class="btn outline" onclick="removeFromCart('${item.id}')">এখাল</button>
          </div>
        `;
        cartList.appendChild(div);
      });
      cartTotal.textContent = total.toFixed(0);
      cartCount.textContent = count;
    }

    function changeQty(id,delta){
      const cart = getCart();
      const item = cart.find(c=>c.id===id);
      if(!item) return;
      item.qty += delta;
      if(item.qty<=0) {
        const idx = cart.findIndex(c=>c.id===id); cart.splice(idx,1);
      }
      setCart(cart); renderCart();
    }
    function removeFromCart(id){
      const cart = getCart();
      const idx = cart.findIndex(c=>c.id===id); if(idx>-1) cart.splice(idx,1); setCart(cart); renderCart();
    }

    // --- simple checkout (demo) ---
    document.getElementById('checkoutBtn').addEventListener('click', ()=>{
      const user = getUser();
      if(!user) return showLoginModal('আপনি অর্ডার করতে লগ ইন করুন');
      const cart = getCart();
      if(cart.length===0) return alert('আপনার কার্ট খালি');
      // For demo we just clear cart and show success
      setCart([]); renderCart(); alert('অর্ডার প্লেইস হয়েছে — (ডেমো)। ধন্যবাদ, '+user.name);
    });

    // --- auth (signup/login) ---
    document.getElementById('openSignup').addEventListener('click', ()=>{
      showModal(`
        <h3>সাইন আপ</h3>
        <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
          <input id=\"su_name\" placeholder=\"নাম\"> 
          <input id=\"su_email\" placeholder=\"ইমেইল\"> 
          <input id=\"su_password\" placeholder=\"পাসওয়ার্ড\" type=\"password\"> 
          <div style=\"display:flex;gap:8px;justify-content:flex-end\">
            <button class=\"btn outline\" onclick=\"closeModal()\">বন্ধ</button>
            <button class=\"btn\" onclick=\"doSignup()\">রেজিস্টার</button>
          </div>
        </div>
      `);
    });

    function doSignup(){
      const name = document.getElementById('su_name').value.trim();
      const email = document.getElementById('su_email').value.trim();
      const password = document.getElementById('su_password').value;
      if(!name||!email||!password) return alert('সব ফিল্ড পূরণ করুন');
      setUser({name,email});
      closeModal(); renderUserBadge(); alert('রেজিস্ট্রেশন সম্পন্ন — আপনি এখন লগ ইন।');
    }

    document.getElementById('openLogin').addEventListener('click', ()=> showLoginModal());

    function showLoginModal(msg='লগ ইন করুন'){
      showModal(`
        <h3>${msg}</h3>
        <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
          <input id=\"li_email\" placeholder=\"ইমেইল\"> 
          <input id=\"li_password\" placeholder=\"পাসওয়ার্ড\" type=\"password\"> 
          <div style=\"display:flex;gap:8px;justify-content:flex-end\">
            <button class=\"btn outline\" onclick=\"closeModal()\">বন্ধ</button>
            <button class=\"btn\" onclick=\"doLogin()\">লগ ইন</button>
          </div>
        </div>
      `);
    }

    function doLogin(){
      const email = document.getElementById('li_email').value.trim();
      const password = document.getElementById('li_password').value;
      if(!email||!password) return alert('প্রয়োজনীয় তথ্য দিন');
      // For demo: any sign-up saved user or admin
      if(email === ADMIN_CREDENTIAL.email && password === ADMIN_CREDENTIAL.password){
        setUser({name:'Admin',email, isAdmin:true}); closeModal(); renderUserBadge(); alert('অ্যাডমিন হিসেবে লগ ইন সফল'); adminPanel.style.display='block';
        return;
      }
      const user = getUser();
      if(user && user.email === email){ setUser({...user}); closeModal(); renderUserBadge(); alert('লগ ইন সফল — '+user.name); return; }
      // else minimal login: accept and save
      setUser({name:email.split('@')[0], email}); closeModal(); renderUserBadge(); alert('লগ ইন সফল — '+email);
    }

    function renderUserBadge(){
      const u = getUser();
      if(u){ userBadge.textContent = u.name + (u.isAdmin? ' (অ্যাডমিন)':''); if(u.isAdmin) adminPanel.style.display='block'; }
      else{ userBadge.textContent='অতিথি'; adminPanel.style.display='none'; }
    }

    // --- admin login ---
    document.getElementById('openAdminLogin').addEventListener('click', ()=>{
      showModal(`
        <h3>অ্যাডমিন লগ ইন</h3>
        <div style="display:flex;flex-direction:column;gap:8px;margin-top:8px">
          <input id=\"ad_email\" placeholder=\"ইমেইল\" value=\"${ADMIN_CREDENTIAL.email}\"> 
          <input id=\"ad_password\" placeholder=\"পাসওয়ার্ড\" type=\"password\" value=\"${ADMIN_CREDENTIAL.password}\"> 
          <div style=\"display:flex;gap:8px;justify-content:flex-end\">
            <button class=\"btn outline\" onclick=\"closeModal()\">বন্ধ</button>
            <button class=\"btn\" onclick=\"doAdminLogin()\">লগ ইন</button>
          </div>
        </div>
      `);
    });

    function doAdminLogin(){
      const e = document.getElementById('ad_email').value.trim();
      const p = document.getElementById('ad_password').value;
      if(e===ADMIN_CREDENTIAL.email && p===ADMIN_CREDENTIAL.password){
        setUser({name:'Admin',email:e,isAdmin:true}); closeModal(); renderUserBadge(); adminPanel.style.display='block'; alert('অ্যাডমিন একসেস পাওয়া গেছে');
      } else alert('ভুল ক্রিডেনশিয়াল');
    }

    // --- add product (admin) ---
    document.getElementById('addProductBtn').addEventListener('click', ()=>{
      const user = getUser(); if(!user || !user.isAdmin) return alert('অ্যাডমিন হিসেবে লগ ইন করুন');
      const title = document.getElementById('newTitle').value.trim();
      const author = document.getElementById('newAuthor').value.trim();
      const price = document.getElementById('newPrice').value.trim();
      const img = document.getElementById('newImage').value.trim();
      const desc = document.getElementById('newDesc').value.trim();
      if(!title||!author||!price) return alert('শিরোনাম, লেখক এবং মূল্য দিন');
      const p = {id:genId(), title, author, price: Number(price), img, desc};
      const products = getProducts(); products.unshift(p); setProducts(products); renderProducts();
      document.getElementById('newTitle').value=''; document.getElementById('newAuthor').value=''; document.getElementById('newPrice').value=''; document.getElementById('newImage').value=''; document.getElementById('newDesc').value='';
      alert('নতুন বই যোগ করা হয়েছে');
    });

    document.getElementById('clearProducts').addEventListener('click', ()=>{
      if(!confirm('সব বই লোকাল থেকে মুছে ফেলবেন?')) return; setProducts([]); renderProducts();
    });

    // --- search & events ---
    document.getElementById('searchBtn').addEventListener('click', ()=>{
      const q = document.getElementById('searchInput').value.trim(); renderProducts(q);
    });
    document.getElementById('showAll').addEventListener('click', ()=>{ document.getElementById('searchInput').value=''; renderProducts(); });

    // --- export CSV ---
    document.getElementById('exportCSV').addEventListener('click', ()=>{
      const rows = getProducts().map(p=> [p.title, p.author, p.price, p.desc||''].map(v=> '"'+String(v).replace(/"/g,'""')+'"').join(','));
      const csv = 'Title,Author,Price,Desc\n' + rows.join('\n');
      const blob = new Blob([csv],{type:'text/csv'}); const url = URL.createObjectURL(blob);
      const a = document.createElement('a'); a.href=url; a.download='boikini_products.csv'; a.click(); URL.revokeObjectURL(url);
    });

    // --- modal helpers ---
    const backdrop = document.getElementById('modalBackdrop');
    const modalContent = document.getElementById('modalContent');
    function showModal(html){ modalContent.innerHTML = html; backdrop.style.display='flex'; }
    function closeModal(){ backdrop.style.display='none'; modalContent.innerHTML=''; }
    backdrop.addEventListener('click', (e)=>{ if(e.target===backdrop) closeModal(); });

    // --- small helpers ---
    function escapeHtml(s){ if(!s) return ''; return String(s).replace(/[&<>\"]/g, c=>({ '&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;' })[c]); }

    // --- utility UI actions accessible from HTML strings ---
    window.viewProduct = viewProduct; window.addToCart = addToCart; window.changeQty = changeQty; window.removeFromCart = removeFromCart; window.closeModal = closeModal; window.showLoginModal = showLoginModal;

    // --- toggle cart visible (simple) ---
    document.getElementById('toggleCart').addEventListener('click', ()=>{
      const aside = document.querySelector('aside'); aside.style.display = aside.style.display === 'none' ? 'block' : 'block'; window.scrollTo({top:0,behavior:'smooth'});
    });

    // --- quick product view on load ---
    function seedIfEmpty(){ if(getProducts().length===0){ setProducts(SAMPLE_PRODUCTS); } }

    // --- export / import backup (hidden) ---

    // init
    seedIfEmpty(); boot();

    // --- small accessibility: expose admin credential in console for demo ---
    console.log('Admin demo credential — email:', ADMIN_CREDENTIAL.email, 'password:', ADMIN_CREDENTIAL.password);

  </script>

