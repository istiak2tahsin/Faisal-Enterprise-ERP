[Faisal Enterprise.html](https://github.com/user-attachments/files/27189962/Faisal.Enterprise.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes" />
<title>Faisal Enterprise | Pro Cloud ERP</title>
<style>
/* CSS Variables & Themes */
:root {
  --bg: #e0e5ec;
  --text: #2c3e66;
  --shadow-dark: #a3b1c6;
  --shadow-light: #ffffff;
  --accent: #1e3a8a;
  --danger: #c97e5a;
}
[data-theme="dark"] {
  --bg: #1a1d23;
  --text: #d1d5db;
  --shadow-dark: #0d0e12;
  --shadow-light: #262a34;
  --accent: #60a5fa;
  --danger: #f87171;
}

* { margin: 0; padding: 0; box-sizing: border-box; transition: background 0.3s, color 0.3s; }
body { background: var(--bg); font-family: 'Inter', system-ui, sans-serif; padding-bottom: 90px; min-height: 100vh; color: var(--text); }

/* Neomorphic Core */
.neu-card { background: var(--bg); border-radius: 28px; box-shadow: 9px 9px 16px var(--shadow-dark), -9px -9px 16px var(--shadow-light); padding: 1.5rem; margin-bottom: 1.5rem; }
.neu-btn { background: var(--bg); border: none; border-radius: 48px; padding: 12px 20px; font-weight: 600; cursor: pointer; box-shadow: 6px 6px 12px var(--shadow-dark), -4px -4px 10px var(--shadow-light); color: var(--text); }
.neu-btn:active { box-shadow: inset 4px 4px 8px var(--shadow-dark), inset -3px -3px 8px var(--shadow-light); transform: scale(0.97); }
.neu-btn-primary { background: var(--text); color: var(--bg); }
.neu-input, .neu-select { background: var(--bg); border: none; border-radius: 48px; padding: 12px 18px; box-shadow: inset 3px 3px 8px var(--shadow-dark), inset -2px -2px 6px var(--shadow-light); width: 100%; outline: none; margin-top: 10px; color: var(--text); }

/* Navigation */
.container { max-width: 880px; margin: 0 auto; padding: 20px 16px; }
.header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
.header-actions { display: flex; align-items: center; gap: 10px; }
.navbar { position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); width: 92%; max-width: 440px; background: var(--bg); border-radius: 60px; display: flex; justify-content: space-around; padding: 8px; box-shadow: 8px 8px 16px var(--shadow-dark); z-index: 1000; }
.nav-link { background: transparent; border: none; padding: 10px; border-radius: 40px; cursor: pointer; font-weight: 600; color: var(--text); font-size: 12px; }
.nav-link.active { box-shadow: inset 4px 4px 8px var(--shadow-dark), inset -3px -3px 8px var(--shadow-light); color: var(--accent); }

.page { display: none; }
.page.active { display: block; animation: fadeInUp 0.3s ease; }
@keyframes fadeInUp { from { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }

table { width: 100%; border-collapse: collapse; margin-top: 10px; }
th, td { padding: 12px 8px; border-bottom: 1px solid var(--shadow-dark); text-align: left; font-size: 13px; }

@media print { .no-print { display: none !important; } #printArea { display: block; color: black; } .memo { border: 1px solid #000; padding: 20px; margin-bottom: 20px; page-break-after: always; } }
</style>
</head>
<body>

<div id="loginModal" style="position:fixed; top:0; left:0; width:100%; height:100%; background:var(--bg); display:flex; align-items:center; justify-content:center; z-index:9999;">
    <div class="neu-card" style="width:310px; text-align:center;">
        <h2 style="margin-bottom:15px;">Faisal ERP Login</h2>
        <input type="password" id="loginPass" class="neu-input" placeholder="Password">
        <button class="neu-btn neu-btn-primary" onclick="handleLogin()" style="width:100%; margin-top:20px;">Unlock</button>
    </div>
</div>

<div class="container no-print" id="mainApp" style="display:none;">
    <div class="header">
        <h3>Faisal Enterprise</h3>
        <div class="header-actions">
            <button class="neu-btn" id="themeBtn" onclick="toggleTheme()" style="padding:8px 12px;">🌙</button>
            <button class="neu-btn" onclick="showPasswordPrompt()" style="font-size:11px; padding:8px 12px;">🔑 Pass</button>
            <button class="neu-btn" onclick="handleLogout()" style="color:var(--danger); font-size:11px; padding:8px 12px;">Logout</button>
        </div>
    </div>

    <div id="sales" class="page active">
        <div class="neu-card">
            <h3>New Invoice</h3>
            <div style="display:flex; gap:10px;">
                <input id="invNo" class="neu-input" placeholder="Inv ID">
                <input type="date" id="orderDate" class="neu-input">
            </div>
            <input id="custShop" class="neu-input" placeholder="Buyer's Shop Name">
            <input id="custName" class="neu-input" placeholder="Buyer's Name">
            <hr style="margin:15px 0; border:0; border-top:1px solid var(--shadow-dark);">
            <select id="pSelect" class="neu-select"><option value="">Select Item</option></select>
            <input type="number" id="pQty" class="neu-input" value="1" min="1">
            <button class="neu-btn neu-btn-primary" onclick="addToCart()" style="width:100%; margin-top:10px;">+ Add to Cart</button>
        </div>
        <div class="neu-card">
            <h3>Cart</h3>
            <table id="cartTable"><thead><tr><th>Item</th><th>Qty</th><th>Subtotal</th><th></th></tr></thead><tbody id="cartBody"></tbody></table>
            <h2 style="text-align:right; margin-top:15px;">Total: <span id="grandTotal">0</span> ৳</h2>
            <button class="neu-btn neu-btn-primary" onclick="finalizeOrder()" style="width:100%; margin-top:10px;">Save & Print</button>
        </div>
    </div>

    <div id="inventory" class="page">
        <div class="neu-card">
            <h3>Add Item</h3>
            <input id="newPName" class="neu-input" placeholder="Product Name">
            <input type="number" id="newPPrice" class="neu-input" placeholder="Price (TK)">
            <button class="neu-btn neu-btn-primary" onclick="saveProduct()" style="width:100%; margin-top:10px;">Save Product</button>
        </div>
        <div class="neu-card">
            <h3>Item List</h3>
            <table>
                <thead><tr><th>Product</th><th>Price</th><th>Action</th></tr></thead>
                <tbody id="productTable"></tbody>
            </table>
        </div>
    </div>

    <div id="reports" class="page">
        <div class="neu-card">
            <h3>Daily Report</h3>
            <input type="date" id="dailyReportDate" class="neu-input">
            <button class="neu-btn neu-btn-primary" onclick="generateReport('daily')" style="margin-top:10px; width:100%;">View Daily Invoices</button>
        </div>
        <div class="neu-card">
            <h3>Monthly Report</h3>
            <input type="month" id="reportMonth" class="neu-input">
            <button class="neu-btn neu-btn-primary" onclick="generateReport('month')" style="margin-top:10px; width:100%;">View Monthly Invoices</button>
        </div>
        <div class="neu-card">
            <h3>Yearly Report</h3>
            <select id="reportYear" class="neu-select"></select>
            <button class="neu-btn neu-btn-primary" onclick="generateReport('year')" style="margin-top:10px; width:100%;">View Yearly Invoices</button>
        </div>
        <div class="neu-card">
            <h3>Reprint Invoice</h3>
            <input id="searchID" class="neu-input" placeholder="Invoice No">
            <button class="neu-btn" onclick="reprintInvoice()" style="width:100%; margin-top:10px;">Search & Print</button>
        </div>
    </div>
</div>

<nav class="navbar no-print" id="mainNav" style="display:none;">
    <button class="nav-link active" onclick="showPage('sales', this)">Sales</button>
    <button class="nav-link" onclick="showPage('inventory', this)">Items</button>
    <button class="nav-link" onclick="showPage('reports', this)">Reports</button>
</nav>

<div id="printArea"><div id="printContent"></div></div>

<script>
// Password set to 625125 as per user request
let products = JSON.parse(localStorage.getItem('fe_products')) || [];
let orders = JSON.parse(localStorage.getItem('fe_orders')) || [];
let currentPass = localStorage.getItem('fe_pass') || '625125';
let cart = [];

function toggleTheme() {
    const isDark = document.body.getAttribute('data-theme') === 'dark';
    document.body.setAttribute('data-theme', isDark ? 'light' : 'dark');
    document.getElementById('themeBtn').innerText = isDark ? '🌙' : '☀️';
    localStorage.setItem('fe_theme', isDark ? 'light' : 'dark');
}

function handleLogin() {
    if(document.getElementById('loginPass').value === currentPass) {
        sessionStorage.setItem('fe_auth', 'true');
        document.getElementById('loginModal').style.display = 'none';
        document.getElementById('mainApp').style.display = 'block';
        document.getElementById('mainNav').style.display = 'flex';
        initERP();
    } else alert('Wrong Password!');
}

function handleLogout() { sessionStorage.removeItem('fe_auth'); location.reload(); }

function showPasswordPrompt() {
    const newPass = prompt("Enter New Password:");
    if(newPass && newPass.length >= 4) {
        localStorage.setItem('fe_pass', newPass);
        currentPass = newPass;
        alert("Password Updated Successfully!");
    } else if(newPass) {
        alert("Password must be at least 4 characters.");
    }
}

function initERP() {
    if(localStorage.getItem('fe_theme') === 'dark') toggleTheme();
    document.getElementById('orderDate').value = new Date().toISOString().slice(0,10);
    document.getElementById('dailyReportDate').value = new Date().toISOString().slice(0,10);
    document.getElementById('reportMonth').value = new Date().toISOString().slice(0,7);
    const yrSel = document.getElementById('reportYear');
    const curYr = new Date().getFullYear();
    for(let i=curYr-2; i<=curYr+2; i++) yrSel.innerHTML += `<option value="${i}" ${i===curYr?'selected':''}>${i}</option>`;
    renderProductList();
    updateInvID();
}

function showPage(id, btn) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
    document.querySelectorAll('.nav-link').forEach(n => n.classList.remove('active'));
    btn.classList.add('active');
}

function updateInvID() { document.getElementById('invNo').value = 'FE-' + (1000 + orders.length + 1); }

function saveProduct() {
    const n = document.getElementById('newPName').value.trim();
    const p = document.getElementById('newPPrice').value;
    if(!n || !p) return alert("Please enter name and price.");
    products.push({ id: Date.now(), name: n, price: Number(p) });
    localStorage.setItem('fe_products', JSON.stringify(products));
    document.getElementById('newPName').value = '';
    document.getElementById('newPPrice').value = '';
    renderProductList();
}

function deleteProduct(id) {
    if(confirm("Are you sure you want to remove this product?")) {
        products = products.filter(p => p.id !== id);
        localStorage.setItem('fe_products', JSON.stringify(products));
        renderProductList();
    }
}

function renderProductList() {
    const s = document.getElementById('pSelect');
    const t = document.getElementById('productTable');
    s.innerHTML = '<option value="">Select Item</option>';
    t.innerHTML = '';
    products.forEach((p) => {
        s.innerHTML += `<option value="${p.id}">${p.name} (${p.price}৳)</option>`;
        t.innerHTML += `<tr><td>${p.name}</td><td>${p.price} ৳</td><td><button onclick="deleteProduct(${p.id})" style="color:var(--danger); border:none; background:none; cursor:pointer; font-weight:bold;">✕ Remove</button></td></tr>`;
    });
}

function addToCart() {
    const id = document.getElementById('pSelect').value;
    const q = Number(document.getElementById('pQty').value);
    if(!id) return;
    const p = products.find(x => x.id == id);
    cart.push({ name: p.name, price: p.price, qty: q, subtotal: p.price * q });
    renderCart();
}

function renderCart() {
    const b = document.getElementById('cartBody');
    let t = 0; b.innerHTML = '';
    cart.forEach((item, idx) => {
        t += item.subtotal;
        b.innerHTML += `<tr><td>${item.name}</td><td>${item.qty}</td><td>${item.subtotal}</td><td><button onclick="cart.splice(${idx},1);renderCart()" style="border:none; background:none; cursor:pointer;">✕</button></td></tr>`;
    });
    document.getElementById('grandTotal').innerText = t;
}

function finalizeOrder() {
    if(cart.length === 0) return alert("Cart is empty!");
    const order = {
        invID: document.getElementById('invNo').value,
        date: document.getElementById('orderDate').value,
        shop: document.getElementById('custShop').value || 'N/A',
        customer: document.getElementById('custName').value || 'N/A',
        items: [...cart],
        total: document.getElementById('grandTotal').innerText
    };
    orders.push(order);
    localStorage.setItem('fe_orders', JSON.stringify(orders));
    printInvoice(order);
    cart = []; renderCart(); updateInvID();
    document.getElementById('custShop').value = '';
    document.getElementById('custName').value = '';
}

function printInvoice(o) {
    const rows = o.items.map(i => `<tr><td>${i.name}</td><td>${i.price}</td><td>${i.qty}</td><td>${i.subtotal}</td></tr>`).join('');
    const html = `<div class="memo"><h2>FAISAL ENTERPRISE</h2><p>Inv: ${o.invID} | Date: ${o.date}</p><p>Buyer: ${o.shop} (${o.customer})</p><table border="1" style="width:100%; border-collapse:collapse; margin-top:10px;"><thead><tr><th>Item</th><th>Rate</th><th>Qty</th><th>Total</th></tr></thead><tbody>${rows}</tbody></table><h3 style="text-align:right;">Total: ${o.total} ৳</h3></div>`;
    document.getElementById('printContent').innerHTML = html + "<hr style='border:dashed; margin:30px 0;'>" + html;
    window.print();
}

function generateReport(type) {
    let filter = "";
    if(type === 'daily') filter = document.getElementById('dailyReportDate').value;
    else if(type === 'month') filter = document.getElementById('reportMonth').value;
    else filter = document.getElementById('reportYear').value;

    const filtered = orders.filter(o => o.date.startsWith(filter));
    if(filtered.length === 0) return alert('No Data found for this period!');

    let total = 0;
    const tableRows = filtered.map(o => {
        total += Number(o.total);
        return `<tr><td>${o.date}</td><td>${o.invID}</td><td>${o.shop}</td><td style="text-align:right;">${o.total} ৳</td></tr>`;
    }).join('');

    document.getElementById('printContent').innerHTML = `<div class="memo"><h2>FAISAL ENTERPRISE - REPORT</h2><h3>Range: ${filter}</h3><table border="1" style="width:100%; border-collapse:collapse; margin-top:15px;"><thead><tr style="background:#eee;"><th>Date</th><th>Invoice</th><th>Buyer Shop</th><th style="text-align:right;">Amount</th></tr></thead><tbody>${tableRows}</tbody></table><h2 style="text-align:right; margin-top:20px;">Grand Total: ${total} ৳</h2></div>`;
    window.print();
}

function reprintInvoice() {
    const sid = document.getElementById('searchID').value.trim();
    const f = orders.find(o => o.invID.toLowerCase() === sid.toLowerCase());
    if(f) printInvoice(f); else alert('Invoice Not Found!');
}

if(sessionStorage.getItem('fe_auth') === 'true') {
    document.getElementById('loginModal').style.display = 'none';
    document.getElementById('mainApp').style.display = 'block';
    document.getElementById('mainNav').style.display = 'flex';
    initERP();
}
</script>
</body>
</html>
