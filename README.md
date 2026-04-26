[Faisal Enterprise ERP.html](https://github.com/user-attachments/files/27098070/Faisal.Enterprise.ERP.html)
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Faisal Enterprise - Full ERP</title>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-database.js"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        :root { --primary: #4338ca; --dark: #0f172a; --bg: #f8fafc; }
        body { font-family: 'Segoe UI', sans-serif; margin: 0; background: var(--bg); padding-bottom: 70px; }
        
        /* Navbar */
        .navbar { background: var(--dark); padding: 10px 0; display: flex; justify-content: space-around; position: fixed; bottom: 0; width: 100%; z-index: 1000; box-shadow: 0 -2px 10px rgba(0,0,0,0.1); }
        .nav-link { color: #94a3b8; text-decoration: none; font-size: 11px; display: flex; flex-direction: column; align-items: center; gap: 4px; flex: 1; border: none; background: none; cursor: pointer; }
        .nav-link.active { color: white; }
        .nav-link i { font-size: 18px; }

        .container { padding: 15px; max-width: 800px; margin: auto; }
        .page { display: none; }
        .page.active { display: block; animation: fadeIn 0.3s; }
        @keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }

        .card { background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1); margin-bottom: 15px; border: 1px solid #e2e8f0; }
        h3 { margin: 0 0 15px 0; font-size: 17px; color: var(--primary); border-bottom: 2px solid #f1f5f9; padding-bottom: 8px; }
        
        label { display: block; margin-bottom: 5px; font-weight: 600; font-size: 13px; color: #475569; }
        input, select { width: 100%; padding: 10px; border-radius: 8px; border: 1px solid #cbd5e1; margin-bottom: 12px; box-sizing: border-box; font-size: 14px; }
        .btn { padding: 12px; border-radius: 8px; border: none; cursor: pointer; font-weight: bold; width: 100%; transition: 0.2s; }
        .btn-primary { background: var(--primary); color: white; }
        .btn-dark { background: var(--dark); color: white; }
        .btn-danger { background: #ef4444; color: white; width: auto; padding: 5px 10px; font-size: 11px; }

        table { width: 100%; border-collapse: collapse; font-size: 13px; }
        th { background: #f1f5f9; padding: 10px; text-align: left; }
        td { padding: 10px; border-bottom: 1px solid #f1f5f9; }

        #loginOverlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: var(--dark); display: flex; align-items: center; justify-content: center; z-index: 2000; }
        @media print { .no-print { display: none !important; } #printArea { display: block !important; } .memo { border: 2px solid #000; padding: 25px; margin-bottom: 30px; page-break-after: always; color: black; background: white; } }
    </style>
</head>
<body>

<div id="loginOverlay" style="display: none;">
    <div style="background:white; padding:30px; border-radius:15px; text-align:center; width:80%; max-width:300px;">
        <h3>Admin Access</h3>
        <input type="password" id="passInput" placeholder="Password">
        <button class="btn btn-primary" onclick="handleLogin()">Login</button>
    </div>
</div>

<div class="container no-print">
    <div id="sales" class="page active">
        <div class="card">
            <h3><i class="fas fa-file-invoice"></i> Create Invoice</h3>
            <div style="display:flex; gap:10px;">
                <div style="flex:1;"><label>Inv No</label><input type="text" id="invNo" readonly style="background:#f1f5f9"></div>
                <div style="flex:1;"><label>Date</label><input type="date" id="orderDate"></div>
            </div>
            <label>Shop & Customer</label>
            <input type="text" id="custShop" placeholder="Shop Name">
            <input type="text" id="custName" placeholder="Customer Name">
            <hr>
            <label>Select Product</label>
            <select id="pSelect"><option value="">-- Loading Products... --</option></select>
            <label>Quantity</label>
            <input type="number" id="pQty" value="1" min="1">
            <button class="btn btn-primary" onclick="addToCart()"><i class="fas fa-plus"></i> Add to Cart</button>
        </div>

        <div class="card">
            <h3>Cart List</h3>
            <table>
                <thead><tr><th>Item</th><th>Qty</th><th>Subtotal</th><th>X</th></tr></thead>
                <tbody id="cartBody"></tbody>
            </table>
            <h2 style="text-align:right; margin-top:15px; color:var(--primary);">Total: <span id="grandTotal">0</span> TK</h2>
            <button class="btn btn-dark" onclick="finalizeOrder()"><i class="fas fa-save"></i> Save & Print</button>
        </div>
    </div>

    <div id="inventory" class="page">
        <div class="card">
            <h3><i class="fas fa-plus-circle"></i> Add New Product</h3>
            <label>Product Name</label>
            <input type="text" id="newPName" placeholder="Ex: Sample Box">
            <label>Price</label>
            <input type="number" id="newPPrice" placeholder="Ex: 500">
            <button class="btn btn-primary" onclick="saveProduct()">Save Product to Cloud</button>
        </div>
        <div class="card">
            <h3>Cloud Inventory</h3>
            <table>
                <thead><tr><th>Product Name</th><th>Rate</th><th>Action</th></tr></thead>
                <tbody id="productTable"></tbody>
            </table>
        </div>
    </div>

    <div id="reports" class="page">
        <div class="card">
            <h3>Monthly Report</h3>
            <input type="month" id="reportMonth">
            <button class="btn btn-primary" onclick="generateReport('month')">Show Monthly Report</button>
        </div>
        <div class="card">
            <h3>Yearly Report</h3>
            <select id="reportYear">
                <option value="2026">2026</option>
                <option value="2027">2027</option>
            </select>
            <button class="btn btn-dark" onclick="generateReport('year')">Show Yearly Report</button>
        </div>
        <div class="card">
            <h3>Reprint Invoice</h3>
            <input type="text" id="searchID" placeholder="FE000XX">
            <button class="btn btn-dark" onclick="reprint()">Search & Print</button>
        </div>
    </div>
</div>

<nav class="navbar no-print">
    <button class="nav-link active" onclick="showPage('sales', this)"><i class="fas fa-shopping-cart"></i>Sales</button>
    <button class="nav-link" onclick="showPage('inventory', this)"><i class="fas fa-boxes"></i>Items</button>
    <button class="nav-link" onclick="showPage('reports', this)"><i class="fas fa-chart-line"></i>Reports</button>
</nav>

<div id="printArea" style="display:none;"><div id="printContent"></div></div>

<script>
    // Firebase Setup
    const firebaseConfig = { databaseURL: "https://faisal-enterprise-erp-default-rtdb.firebaseio.com/" };
    firebase.initializeApp(firebaseConfig);
    const db = firebase.database();

    let cart = [], allOrders = [], allProducts = [];

    // Auth Logic (No logout on refresh)
    if (localStorage.getItem("faisal_auth") !== "true") {
        document.getElementById('loginOverlay').style.display = 'flex';
    }
    function handleLogin() {
        if(document.getElementById('passInput').value === "admin123") {
            localStorage.setItem("faisal_auth", "true");
            document.getElementById('loginOverlay').style.display = 'none';
        }
    }

    function showPage(id, btn) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
        document.getElementById(id).classList.add('active');
        btn.classList.add('active');
    }

    // --- REALTIME SYNC ---
    db.ref('products').on('value', (snapshot) => {
        const data = snapshot.val();
        const table = document.getElementById('productTable');
        const select = document.getElementById('pSelect');
        table.innerHTML = "";
        select.innerHTML = '<option value="">-- Select Product --</option>';
        allProducts = [];
        if(data) {
            Object.entries(data).forEach(([id, p]) => {
                allProducts.push({id, ...p});
                table.innerHTML += `<tr><td>${p.name}</td><td>${p.price}</td><td><button class="btn-danger" onclick="deleteP('${id}')">X</button></td></tr>`;
                select.innerHTML += `<option value="${p.name}" data-price="${p.price}">${p.name} (${p.price} TK)</option>`;
            });
        }
    });

    db.ref('orders').on('value', (s) => {
        const data = s.val();
        allOrders = data ? Object.values(data) : [];
        document.getElementById('invNo').value = "FE" + (allOrders.length + 1010).toString();
    });

    // --- LOGIC FUNCTIONS ---
    function saveProduct() {
        const name = document.getElementById('newPName').value;
        const price = document.getElementById('newPPrice').value;
        if(name && price) {
            db.ref('products').push({ name, price: parseFloat(price) });
            document.getElementById('newPName').value = ""; document.getElementById('newPPrice').value = "";
            alert("Product Added!");
        }
    }

    function deleteP(id) { if(confirm("Delete?")) db.ref('products/' + id).remove(); }

    document.getElementById('orderDate').value = new Date().toISOString().split('T')[0];

    function addToCart() {
        const s = document.getElementById('pSelect');
        const opt = s.options[s.selectedIndex];
        if(!s.value) return;
        cart.push({ name: s.value, price: parseFloat(opt.getAttribute('data-price')), qty: parseInt(document.getElementById('pQty').value), subtotal: parseFloat(opt.getAttribute('data-price')) * parseInt(document.getElementById('pQty').value) });
        renderCart();
    }

    function renderCart() {
        const b = document.getElementById('cartBody');
        b.innerHTML = ""; let t = 0;
        cart.forEach((i, idx) => { t += i.subtotal; b.innerHTML += `<tr><td>${i.name}</td><td>${i.qty}</td><td>${i.subtotal}</td><td onclick="cart.splice(${idx},1);renderCart()">❌</td></tr>`; });
        document.getElementById('grandTotal').innerText = t;
    }

    function finalizeOrder() {
        if(cart.length === 0) return alert("Cart empty");
        const order = { 
            invID: document.getElementById('invNo').value, 
            date: document.getElementById('orderDate').value, 
            shop: document.getElementById('custShop').value || "N/A", 
            customer: document.getElementById('custName').value || "N/A", 
            items: [...cart], 
            total: document.getElementById('grandTotal').innerText 
        };
        db.ref('orders/' + order.invID).set(order).then(() => { printInvoice(order); });
    }

    function printInvoice(o) {
        let rows = o.items.map(i => `<tr><td>${i.name}</td><td>${i.price}</td><td>${i.qty}</td><td>${i.subtotal}</td></tr>`).join('');
        let html = ["CUSTOMER COPY", "OFFICE COPY"].map(tag => `
            <div class="memo">
                <center><h2>FAISAL ENTERPRISE</h2><p>${tag}</p></center>
                <hr>
                <p><b>Inv:</b> ${o.invID} | <b>Date:</b> ${o.date}</p>
                <p><b>Shop:</b> ${o.shop} | <b>Name:</b> ${o.customer}</p>
                <table border="1" style="width:100%; border-collapse:collapse;">
                    <thead><tr><th>Product</th><th>Rate</th><th>Qty</th><th>Total</th></tr></thead>
                    <tbody>${rows}</tbody>
                </table>
                <h3 style="text-align:right">Total: ${o.total} TK</h3>
            </div>
        `).join('');
        document.getElementById('printContent').innerHTML = html;
        window.print();
        location.reload();
    }

    function generateReport(type) {
        let filter = type === 'month' ? document.getElementById('reportMonth').value : document.getElementById('reportYear').value;
        if(!filter) return alert("Select Date/Year");
        const filtered = allOrders.filter(o => o.date.startsWith(filter));
        let total = 0;
        let rows = filtered.map(o => { total += parseFloat(o.total); return `<tr><td>${o.date}</td><td>${o.invID}</td><td>${o.shop}</td><td>${o.total}</td></tr>`; }).join('');
        document.getElementById('printContent').innerHTML = `<div class="memo"><h2>Report: ${filter}</h2><table border="1" style="width:100%">${rows}</table><h3>Total Sales: ${total} TK</h3></div>`;
        window.print();
    }

    function reprint() {
        const id = document.getElementById('searchID').value;
        const o = allOrders.find(x => x.invID === id);
        if(o) printInvoice(o); else alert("Not Found");
    }
</script>
</body>
</html>
