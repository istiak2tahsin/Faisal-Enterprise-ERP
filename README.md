
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes" />
<title>Faisal Enterprise | Neomorphic ERP</title>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #e0e5ec;
  font-family: 'Inter', system-ui, 'Segoe UI', -apple-system, sans-serif;
  padding-bottom: 90px;
  min-height: 100vh;
}

/* neomorphic core */
.neu-card {
  background: #e0e5ec;
  border-radius: 32px;
  box-shadow: 9px 9px 16px #a3b1c6, -9px -9px 16px #ffffff;
  padding: 1.6rem;
  margin-bottom: 1.5rem;
  transition: all 0.2s ease;
}

.neu-btn {
  background: #e0e5ec;
  border: none;
  border-radius: 48px;
  padding: 12px 20px;
  font-weight: 600;
  font-size: 0.9rem;
  cursor: pointer;
  box-shadow: 6px 6px 12px #a3b1c6, -4px -4px 10px #ffffff;
  transition: all 0.12s linear;
  color: #2c3e66;
}

.neu-btn:active {
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -3px -3px 8px #ffffff;
  transform: scale(0.98);
}

.neu-btn-primary {
  background: #2c3e66;
  color: white;
  box-shadow: 6px 6px 12px #a3b1c6, -4px -4px 10px #ffffff;
}

.neu-btn-primary:active {
  background: #1f2c4b;
}

.neu-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

.neu-input, .neu-select {
  background: #e0e5ec;
  border: none;
  border-radius: 48px;
  padding: 12px 18px;
  font-size: 0.9rem;
  box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff;
  width: 100%;
  outline: none;
  transition: all 0.2s ease;
  color: #1e2a3a;
  font-weight: 500;
}

.neu-input:focus, .neu-select:focus {
  box-shadow: inset 4px 4px 10px #a3b1c6, inset -3px -3px 8px #ffffff;
}

/* border animation for required fields */
@keyframes shakeBorder {
  0% { box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff; border: 2px solid transparent; }
  25% { box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff; border: 2px solid #c2410c; }
  50% { box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff; border: 2px solid #f97316; }
  75% { box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff; border: 2px solid #c2410c; }
  100% { box-shadow: inset 3px 3px 8px #a3b1c6, inset -2px -2px 6px #ffffff; border: 2px solid transparent; }
}

.required-shake {
  animation: shakeBorder 0.5s ease-in-out;
}

.container {
  max-width: 880px;
  margin: 0 auto;
  padding: 20px 16px;
}

h3 {
  font-size: 1.5rem;
  font-weight: 700;
  color: #1e2f4e;
  margin-bottom: 1.2rem;
  letter-spacing: -0.3px;
  border-left: 4px solid #2c3e66;
  padding-left: 14px;
}

.row {
  display: flex;
  gap: 14px;
}
.row > * {
  flex: 1;
}

hr {
  margin: 20px 0;
  border: 0;
  height: 2px;
  background: #cfd5e0;
  box-shadow: inset 0 1px 1px rgba(0,0,0,0.05);
}

.navbar {
  position: fixed;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
  width: 92%;
  max-width: 440px;
  background: #e0e5ec;
  border-radius: 60px;
  display: flex;
  justify-content: space-around;
  padding: 8px 12px;
  box-shadow: 8px 8px 16px #a3b1c6, -6px -6px 14px #ffffff;
  z-index: 1000;
}

.nav-link {
  background: transparent;
  border: none;
  color: #2c3e66;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3px;
  font-size: 12px;
  font-weight: 600;
  padding: 8px 14px;
  border-radius: 44px;
  cursor: pointer;
  transition: 0.1s;
}

.nav-link.active {
  background: #e0e5ec;
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -3px -3px 8px #ffffff;
  color: #1e3a8a;
}

.nav-icon {
  font-size: 24px;
}

.table-wrap {
  overflow-x: auto;
  border-radius: 28px;
  padding: 4px;
}

table {
  width: 100%;
  border-collapse: collapse;
  background: #e0e5ec;
  border-radius: 24px;
}

th {
  text-align: left;
  padding: 12px 8px;
  color: #1f3a64;
  font-weight: 700;
  font-size: 0.8rem;
}

td {
  padding: 10px 8px;
  border-bottom: 1px solid #c8d0dc;
  color: #1e2f3e;
}

.total {
  text-align: right;
  font-size: 1.9rem;
  font-weight: 800;
  margin-top: 20px;
  color: #1f3a64;
}

.toast {
  position: fixed;
  bottom: 100px;
  left: 50%;
  transform: translateX(-50%);
  background: #2c3e66;
  color: white;
  padding: 10px 22px;
  border-radius: 48px;
  font-weight: 500;
  font-size: 0.85rem;
  z-index: 2000;
  white-space: nowrap;
  box-shadow: 6px 6px 12px #a3b1c6;
  pointer-events: none;
}

.pill {
  display: inline-block;
  background: #e0e5ec;
  border-radius: 30px;
  padding: 4px 12px;
  font-size: 11px;
  font-weight: 700;
  color: #2c3e66;
  box-shadow: inset 1px 1px 2px #ffffff, inset -1px -1px 2px #a3b1c6;
}

.btn-danger {
  background: #c97e5a;
  color: white;
  border: none;
  border-radius: 32px;
  padding: 5px 12px;
  font-weight: 600;
  font-size: 0.7rem;
  box-shadow: 4px 4px 8px #a3b1c6, -2px -2px 6px #ffffff;
  cursor: pointer;
}
.btn-danger:active {
  box-shadow: inset 3px 3px 6px #7a5a44, inset -2px -2px 5px #f0e2d0;
}

.login-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #e0e5ec;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 9999;
}

.login-card {
  background: #e0e5ec;
  border-radius: 48px;
  padding: 2rem 1.8rem;
  width: 90%;
  max-width: 360px;
  box-shadow: 12px 12px 24px #a3b1c6, -10px -10px 20px #ffffff;
  text-align: center;
}

.login-card h2 {
  font-size: 1.9rem;
  color: #1f3a64;
  margin-bottom: 8px;
}

.login-card input {
  margin: 20px 0 10px;
}

.error-msg {
  color: #c2410c;
  font-size: 0.7rem;
  min-height: 26px;
  font-weight: 600;
}

.page {
  display: none;
}
.page.active {
  display: block;
  animation: fadeUp 0.2s ease;
}
@keyframes fadeUp {
  from { opacity: 0; transform: translateY(6px);}
  to { opacity: 1; transform: translateY(0);}
}

@media print {
  .no-print, .navbar, .toast, .login-overlay {
    display: none !important;
  }
  body { background: white; padding: 0; margin: 0; }
  .neu-card { box-shadow: none; background: white; padding: 0; }
  .container { padding: 0; }
  #printArea { display: block; }
  .memo { border: 1px solid #ccc; padding: 20px; margin-bottom: 30px; page-break-after: always; }
}
</style>
</head>
<body>

<div id="loginModal" class="login-overlay">
  <div class="login-card">
    <h2> Business Name Here </h2>
    <p style="font-size: 13px; color:#2c3e66;">secure access</p>
    <input type="password" id="loginPassword" class="neu-input" placeholder="password" autocomplete="off">
    <div id="loginError" class="error-msg"></div>
    <button class="neu-btn neu-btn-primary" id="submitLoginBtn" style="width:100%; margin-top:8px;">Unlock</button>
  </div>
</div>

<div class="container no-print" id="mainApp" style="display: none;">
  <div id="sales" class="page active">
    <div class="neu-card">
      <h3>Create Invoice</h3>
      <div class="row">
        <div><input id="invNo" class="neu-input" placeholder="Invoice No"></div>
        <div><input type="date" id="orderDate" class="neu-input"></div>
      </div>
      <input id="custShop" class="neu-input" placeholder="Shop Name *" style="margin-top:12px;">
      <input id="custName" class="neu-input" placeholder="Customer Name *" style="margin-top:12px;">
      <hr>
      <select id="pSelect" class="neu-select"><option value="">Select Product</option></select>
      <input type="number" id="pQty" class="neu-input" value="1" min="1" placeholder="Quantity" style="margin-top:12px;">
      <button class="neu-btn neu-btn-primary" id="addToCartBtn" onclick="attemptAddToCart()" style="margin-top:12px;">+ Add to Cart</button>
    </div>

    <div class="neu-card">
      <h3>Cart Summary</h3>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Item</th><th>Qty</th><th>Rate</th><th>Subtotal</th><th></th></tr></thead>
          <tbody id="cartBody"></tbody>
        </table>
      </div>
      <div class="total">Total: <span id="grandTotal">0</span> ৳</div>
      <button class="neu-btn" style="background:#2c3e66; color:white;" onclick="finalizeOrder(this)">Save & Print Invoice</button>
    </div>
  </div>

  <div id="inventory" class="page">
    <div class="neu-card">
      <h3>Add Product</h3>
      <span class="pill">offline storage</span>
      <input id="newPName" class="neu-input" placeholder="Product Name" style="margin-top:8px;">
      <input type="number" id="newPPrice" class="neu-input" placeholder="Price (TK)" style="margin-top:12px;">
      <button class="neu-btn neu-btn-primary" onclick="saveProduct(this)" style="margin-top:12px;">Save Product</button>
    </div>
    <div class="neu-card">
      <h3>Inventory</h3>
      <div class="table-wrap">
        <table>
          <thead><tr><th>Product</th><th>Price</th><th></th></tr></thead>
          <tbody id="productTable"></tbody>
        </table>
      </div>
    </div>
  </div>

  <div id="reports" class="page">
    <div class="neu-card"><h3>Monthly Report</h3><input type="month" id="reportMonth" class="neu-input"><button class="neu-btn" onclick="generateReport('month')" style="margin-top:12px;">View Monthly</button></div>
    <div class="neu-card"><h3>Yearly Report</h3><select id="reportYear" class="neu-select"></select><button class="neu-btn" onclick="generateReport('year')" style="margin-top:12px;">View Yearly</button></div>
    <div class="neu-card"><h3>Reprint Invoice</h3><input id="searchID" class="neu-input" placeholder="Invoice number"><button class="neu-btn" onclick="reprintInvoice()" style="margin-top:12px;">Search & Print</button></div>
  </div>
</div>

<nav class="navbar no-print" id="mainNav" style="display: none;">
  <button class="nav-link active" onclick="showPage('sales',this)"><span class="nav-icon">🧾</span><span>Sales</span></button>
  <button class="nav-link" onclick="showPage('inventory',this)"><span class="nav-icon">📦</span><span>Items</span></button>
  <button class="nav-link" onclick="showPage('reports',this)"><span class="nav-icon">📊</span><span>Reports</span></button>
</nav>

<div id="printArea"><div id="printContent"></div></div>

<script>
'use strict';

// ========== LOGIN SYSTEM ==========
const AUTH_KEY = 'neomorph_auth_session';
const MASTER_PASS = 'admin123';

function checkAuthAndShow() {
  const isLogged = sessionStorage.getItem(AUTH_KEY);
  if (isLogged === 'authenticated') {
    document.getElementById('loginModal').style.display = 'none';
    document.getElementById('mainApp').style.display = 'block';
    document.getElementById('mainNav').style.display = 'flex';
    if (typeof initERP === 'function') initERP();
  } else {
    document.getElementById('loginModal').style.display = 'flex';
    document.getElementById('mainApp').style.display = 'none';
    document.getElementById('mainNav').style.display = 'none';
  }
}

function performLogin() {
  const pwd = document.getElementById('loginPassword').value.trim();
  const errSpan = document.getElementById('loginError');
  if (pwd === MASTER_PASS) {
    sessionStorage.setItem(AUTH_KEY, 'authenticated');
    errSpan.innerText = '';
    document.getElementById('loginPassword').value = '';
    checkAuthAndShow();
  } else {
    errSpan.innerText = 'Incorrect password';
    document.getElementById('loginPassword').value = '';
  }
}

document.getElementById('submitLoginBtn')?.addEventListener('click', performLogin);
document.getElementById('loginPassword')?.addEventListener('keypress', (e) => { if(e.key === 'Enter') performLogin(); });

// ========== ERP CORE (Faisal Enterprise Full Functionality) ==========
const PROD_STORAGE = 'fe_products_v2';
const ORDER_STORAGE = 'fe_orders_v2';
let products = [];
let orders = [];
let cart = [];

function loadStorage() {
  try {
    products = JSON.parse(localStorage.getItem(PROD_STORAGE)) || [];
    orders = JSON.parse(localStorage.getItem(ORDER_STORAGE)) || [];
  } catch(e) { products = []; orders = []; }
}
function saveProducts() { localStorage.setItem(PROD_STORAGE, JSON.stringify(products)); }
function saveOrders() { localStorage.setItem(ORDER_STORAGE, JSON.stringify(orders)); }
function money(n) { return (Number(n) || 0).toFixed(0); }
function esc(s) { return String(s??'').replace(/[&<>]/g, (m) => ({'&':'&amp;','<':'&lt;','>':'&gt;'})[m]); }
function todayDate() { return new Date().toISOString().slice(0,10); }
function currentMonth() { return new Date().toISOString().slice(0,7); }
function genId(prefix) { return prefix + Date.now().toString(36) + Math.random().toString(36).slice(2,7); }
function showToast(msg) {
  const old = document.querySelector('.toast');
  if(old) old.remove();
  const t = document.createElement('div');
  t.className = 'toast';
  t.textContent = msg;
  document.body.appendChild(t);
  setTimeout(() => t.remove(), 2000);
}

function updateInvHint() {
  const invField = document.getElementById('invNo');
  if(invField && !invField.value.trim()) {
    invField.value = 'FE' + (1010 + orders.length);
  }
}

function fillYearOptions() {
  const yr = new Date().getFullYear();
  const sel = document.getElementById('reportYear');
  if(!sel) return;
  sel.innerHTML = '';
  for(let i=yr-2; i<=yr+3; i++) {
    sel.innerHTML += `<option value="${i}" ${i===yr ? 'selected' : ''}>${i}</option>`;
  }
}

function animateRequiredField(element) {
  if(!element) return;
  element.classList.remove('required-shake');
  void element.offsetWidth;
  element.classList.add('required-shake');
  setTimeout(() => {
    element.classList.remove('required-shake');
  }, 500);
}

function showPage(pageId, btnElem) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById(pageId).classList.add('active');
  document.querySelectorAll('.nav-link').forEach(b => b.classList.remove('active'));
  btnElem.classList.add('active');
  if(pageId === 'inventory') renderProductTable();
  if(pageId === 'sales') updateInvHint();
}

function renderProductTable() {
  const tbody = document.getElementById('productTable');
  const select = document.getElementById('pSelect');
  if(!tbody) return;
  tbody.innerHTML = '';
  select.innerHTML = '<option value="">Select Product</option>';
  if(products.length === 0) {
    tbody.innerHTML = '<tr><td colspan="3" style="text-align:center; padding:24px;">Add products first</td></tr>';
    select.innerHTML = '<option value="">— no items —</option>';
    return;
  }
  products.forEach(p => {
    tbody.innerHTML += `<tr><td>${esc(p.name)}</td><td>${money(p.price)} ৳</td><td><button class="btn-danger" onclick="deleteProduct('${p.id}')">remove</button></td></tr>`;
    const opt = document.createElement('option');
    opt.value = p.id;
    opt.textContent = `${p.name}  •  ${money(p.price)} ৳`;
    select.appendChild(opt);
  });
}

function saveProduct(btn) {
  const name = document.getElementById('newPName').value.trim();
  const price = Number(document.getElementById('newPPrice').value);
  if(!name) { 
    animateRequiredField(document.getElementById('newPName'));
    showToast('Enter product name');
    return; 
  }
  if(!price || price <= 0) { 
    animateRequiredField(document.getElementById('newPPrice'));
    showToast('Enter valid price');
    return; 
  }
  btn.disabled = true;
  const oldText = btn.textContent;
  btn.textContent = 'saving...';
  setTimeout(() => {
    products.push({ id: genId('p_'), name, price, createdAt: Date.now() });
    saveProducts();
    document.getElementById('newPName').value = '';
    document.getElementById('newPPrice').value = '';
    renderProductTable();
    btn.disabled = false;
    btn.textContent = oldText;
    showToast(`✓ ${name} added`);
  }, 150);
}

function deleteProduct(id) {
  if(!confirm('Delete product from inventory?')) return;
  products = products.filter(p => p.id !== id);
  saveProducts();
  renderProductTable();
  showToast('Product removed');
}

function attemptAddToCart() {
  const shopField = document.getElementById('custShop');
  const custField = document.getElementById('custName');
  let isValid = true;
  
  if(!shopField.value.trim()) {
    animateRequiredField(shopField);
    isValid = false;
  }
  if(!custField.value.trim()) {
    animateRequiredField(custField);
    isValid = false;
  }
  if(!isValid) return;
  
  const prodId = document.getElementById('pSelect').value;
  const qty = Number(document.getElementById('pQty').value);
  if(!prodId) { 
    animateRequiredField(document.getElementById('pSelect'));
    showToast('Please select a product');
    return; 
  }
  if(!qty || qty < 1) { 
    animateRequiredField(document.getElementById('pQty'));
    showToast('Enter valid quantity');
    return; 
  }
  const prod = products.find(p => p.id === prodId);
  if(!prod) { 
    showToast('Product not found'); 
    renderProductTable(); 
    return; 
  }
  cart.push({ id: prod.id, name: prod.name, price: prod.price, qty, subtotal: prod.price * qty });
  document.getElementById('pQty').value = 1;
  renderCart();
  showToast(`+ ${qty} × ${prod.name}`);
}

function renderCart() {
  const tbody = document.getElementById('cartBody');
  let total = 0;
  tbody.innerHTML = '';
  if(cart.length === 0) {
    tbody.innerHTML = '<tr><td colspan="5" style="text-align:center; padding:28px;">Cart is empty</td></tr>';
    document.getElementById('grandTotal').innerText = '0';
    return;
  }
  cart.forEach((item, idx) => {
    total += item.subtotal;
    tbody.innerHTML += `<tr><td>${esc(item.name)}</td><td>${item.qty}</td><td>${money(item.price)}</td><td>${money(item.subtotal)}</td><td><button class="btn-danger" onclick="removeCartItem(${idx})">✕</button></td></tr>`;
  });
  document.getElementById('grandTotal').innerText = money(total);
}

function removeCartItem(idx) {
  cart.splice(idx, 1);
  renderCart();
}

function clearPrintArea() {
  const printContainer = document.getElementById('printContent');
  if(printContainer) printContainer.innerHTML = '';
}

function finalizeOrder(btn) {
  const shopField = document.getElementById('custShop');
  const custField = document.getElementById('custName');
  let isValid = true;
  
  if(!shopField.value.trim()) {
    animateRequiredField(shopField);
    isValid = false;
  }
  if(!custField.value.trim()) {
    animateRequiredField(custField);
    isValid = false;
  }
  if(!isValid) return;
  
  if(cart.length === 0) { 
    showToast('Cart is empty'); 
    return; 
  }
  
  let invNo = document.getElementById('invNo').value.trim();
  if(!invNo) invNo = 'FE' + (1010 + orders.length);
  if(orders.some(o => String(o.invID).toLowerCase() === invNo.toLowerCase())) {
    animateRequiredField(document.getElementById('invNo'));
    showToast('Invoice number already exists');
    return;
  }
  
  btn.disabled = true;
  const originalBtnText = btn.textContent;
  btn.textContent = 'processing...';
  
  const orderDate = document.getElementById('orderDate').value || todayDate();
  const shopName = document.getElementById('custShop').value.trim();
  const customerName = document.getElementById('custName').value.trim();
  
  const newOrder = {
    invID: invNo,
    date: orderDate,
    shop: shopName || 'N/A',
    customer: customerName || 'N/A',
    items: cart.map(i => ({ ...i })),
    total: document.getElementById('grandTotal').innerText,
    timestamp: Date.now()
  };
  orders.push(newOrder);
  saveOrders();
  
  cart = [];
  renderCart();
  document.getElementById('custShop').value = '';
  document.getElementById('custName').value = '';
  document.getElementById('invNo').value = '';
  updateInvHint();
  
  btn.disabled = false;
  btn.textContent = originalBtnText;
  showToast(`✓ Invoice ${invNo} saved`);
  
  clearPrintArea();
  printInvoice(newOrder);
}

function printInvoice(order) {
  const rows = order.items.map(i => `<tr><td>${esc(i.name)}</td><td>${money(i.price)} ৳</td><td>${i.qty}</td><td class="right">${money(i.subtotal)} ৳</td></tr>`).join('');
  const block = (copyType) => `
    <div class="memo" style="background:white; border-radius:24px; padding:1.5rem; margin-bottom:2rem; border:1px solid #cbd5e1;">
      <h2 style="text-align:center;">FAISAL ENTERPRISE</h2>
      <p style="text-align:center; font-size:13px;">${copyType}</p>
      <hr>
      <p><strong>Invoice:</strong> ${esc(order.invID)} &nbsp;| <strong>Date:</strong> ${esc(order.date)}</p>
      <p><strong>Shop:</strong> ${esc(order.shop)} &nbsp;| <strong>Customer:</strong> ${esc(order.customer)}</p>
      <table style="width:100%; border-collapse:collapse; margin:14px 0;">
        <thead><tr style="background:#f1f5f9;"><th>Product</th><th>Rate</th><th>Qty</th><th>Amount</th></tr></thead>
        <tbody>${rows}</tbody>
      </table>
      <h3 style="text-align:right;">Total: ${money(order.total)} ৳</h3>
    </div>
  `;
  const printContainer = document.getElementById('printContent');
  printContainer.innerHTML = block('CUSTOMER COPY') + block('OFFICE COPY');
  
  setTimeout(() => {
    window.print();
    setTimeout(() => {
      clearPrintArea();
    }, 500);
  }, 100);
}

function generateReport(type) {
  const filterVal = type === 'month' ? document.getElementById('reportMonth').value : document.getElementById('reportYear').value;
  if(!filterVal) { 
    const field = type === 'month' ? document.getElementById('reportMonth') : document.getElementById('reportYear');
    animateRequiredField(field);
    showToast('Select date/year');
    return; 
  }
  const filtered = orders.filter(o => String(o.date).startsWith(filterVal));
  if(filtered.length === 0) { 
    alert('No sales found for ' + filterVal); 
    return; 
  }
  let totalSales = 0;
  const rows = filtered.map(o => { totalSales += Number(o.total)||0; return `<tr><td>${esc(o.date)}</td><td>${esc(o.invID)}</td><td>${esc(o.shop)}</td><td class="right">${money(o.total)} ৳</td></tr>`; }).join('');
  const reportHtml = `<div style="background:white; padding:20px; border-radius:24px;"><h2 style="text-align:center;">FAISAL ENTERPRISE</h2><h3>Report: ${esc(filterVal)}</h3><table style="width:100%; border-collapse:collapse;"><thead><tr style="background:#e2e8f0;"><th>Date</th><th>Invoice</th><th>Shop</th><th>Amount</th></tr></thead><tbody>${rows}</tbody></table><h3 style="text-align:right;">Total Sales: ${money(totalSales)} ৳</h3></div>`;
  document.getElementById('printContent').innerHTML = reportHtml;
  setTimeout(() => {
    window.print();
    setTimeout(() => clearPrintArea(), 500);
  }, 100);
}

function reprintInvoice() {
  const searchId = document.getElementById('searchID').value.trim();
  if(!searchId) { 
    animateRequiredField(document.getElementById('searchID'));
    showToast('Enter invoice number');
    return; 
  }
  const found = orders.find(o => o.invID.toLowerCase() === searchId.toLowerCase());
  if(!found) { 
    alert('Invoice not found'); 
    return; 
  }
  clearPrintArea();
  printInvoice(found);
}

function initERP() {
  loadStorage();
  const dateEl = document.getElementById('orderDate');
  if(dateEl) dateEl.value = todayDate();
  const monthReport = document.getElementById('reportMonth');
  if(monthReport) monthReport.value = currentMonth();
  fillYearOptions();
  updateInvHint();
  renderProductTable();
  renderCart();
  if(products.length === 0) {
    products.push({ id: genId('p_'), name: 'Premium Glass', price: 550, createdAt: Date.now() });
    products.push({ id: genId('p_'), name: 'Ceramic Mug', price: 290, createdAt: Date.now() });
    saveProducts();
    renderProductTable();
  }
}

window.attemptAddToCart = attemptAddToCart;
window.removeCartItem = removeCartItem;
window.saveProduct = saveProduct;
window.deleteProduct = deleteProduct;
window.finalizeOrder = finalizeOrder;
window.showPage = showPage;
window.generateReport = generateReport;
window.reprintInvoice = reprintInvoice;

window.addEventListener('DOMContentLoaded', () => {
  checkAuthAndShow();
  if(sessionStorage.getItem(AUTH_KEY) === 'authenticated') {
    initERP();
  }
});
</script>
</body>
</html>
```