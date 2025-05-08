
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SIVA CHICKEN FARM - Management</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background: #fff8f0;
      margin: 0;
      padding: 20px;
    }
    h1 {
      color: #d35400;
      text-align: center;
    }
    nav {
      text-align: center;
      margin-bottom: 20px;
    }
    nav button {
      margin: 0 10px;
      padding: 10px 16px;
      background: #e67e22;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
    }
    .page {
      display: none;
      max-width: 800px;
      margin: auto;
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .active {
      display: block;
    }
    label {
      display: block;
      margin-top: 12px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 6px;
      border: 1px solid #ccc;
      border-radius: 6px;
    }
    .submit-btn {
      margin-top: 20px;
      padding: 12px;
      background: #e67e22;
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      font-size: 16px;
    }
    table {
      width: 100%;
      margin-top: 20px;
      border-collapse: collapse;
    }
    th, td {
      border: 1px solid #ccc;
      padding: 10px;
      text-align: center;
    }
    th {
      background: #f4a261;
      color: white;
    }
    .balance {
      text-align: center;
      font-size: 20px;
      margin-bottom: 10px;
      color: #2c3e50;
    }
  </style>
</head>
<body>

<h1>SIVA CHICKEN FARM</h1>

<div class="balance">Main Account Balance: LKR <span id="mainBalance">250000</span></div>

<nav>
  <button onclick="switchPage('purchasePage')">Hen Purchase</button>
  <button onclick="switchPage('sellingPage')">Selling</button>
</nav>

<!-- Hen Purchase Page -->
<div id="purchasePage" class="page active">
  <h2>Hen Purchase</h2>
  <form id="purchaseForm">
    <label>Hen Type:
      <select id="henType" required>
        <option value="Broiler">Broiler</option>
        <option value="Kalbird">Kalbird</option>
        <option value="Parents">Parents</option>
      </select>
    </label>
    <label>Hen Count:
      <input type="number" id="henCount" min="1" required>
    </label>
    <label>Purchase Price per Hen (LKR):
      <input type="number" id="purchasePrice" min="1" required>
    </label>
    <button type="submit" class="submit-btn">Add Purchase</button>
  </form>

  <table id="purchaseTable">
    <thead>
      <tr>
        <th>Hen Type</th>
        <th>Count</th>
        <th>Price/Unit</th>
        <th>Total Cost</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
</div>

<!-- Selling Page -->
<div id="sellingPage" class="page">
  <h2>Sell to Customer</h2>
  <form id="sellingForm">
    <label>Customer Contact:
      <input type="text" id="contactNumber" required>
    </label>
    <label>Hen Type:
      <select id="sellType" required>
        <option value="Broiler">Broiler</option>
        <option value="Kalbird">Kalbird</option>
        <option value="Parents">Parents</option>
      </select>
    </label>
    <label>Quantity (KG):
      <input type="number" id="sellQty" min="1" required>
    </label>
    <label>Price per KG (LKR):
      <input type="number" id="sellPrice" min="1" required>
    </label>
    <button type="submit" class="submit-btn">Add Sale</button>
  </form>

  <table id="sellingTable">
    <thead>
      <tr>
        <th>Contact</th>
        <th>Type</th>
        <th>Qty</th>
        <th>Price/Unit</th>
        <th>Total Sale</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody></tbody>
  </table>
</div>

<script>
  let mainBalance = JSON.parse(localStorage.getItem('mainBalance')) || 250000;
  document.getElementById("mainBalance").innerText = mainBalance.toFixed(2);

  function updateBalanceDisplay() {
    document.getElementById("mainBalance").innerText = mainBalance.toFixed(2);
    localStorage.setItem('mainBalance', JSON.stringify(mainBalance));
  }

  function switchPage(id) {
    document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }

  document.getElementById('purchaseForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const type = henType.value;
    const count = parseInt(henCount.value);
    const price = parseFloat(purchasePrice.value);
    const total = count * price;

    mainBalance -= total;
    updateBalanceDisplay();

    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${type}</td>
      <td>${count}</td>
      <td>${price}</td>
      <td>${total.toFixed(2)}</td>
      <td><button onclick="editRow(this, 'purchase')">Edit</button> <button onclick="deleteRow(this, 'purchase', ${total})">Delete</button></td>
    `;
    document.querySelector('#purchaseTable tbody').appendChild(row);
    this.reset();
  });

  document.getElementById('sellingForm').addEventListener('submit', function(e) {
    e.preventDefault();
    const contact = contactNumber.value;
    const type = sellType.value;
    const qty = parseFloat(sellQty.value);
    const price = parseFloat(sellPrice.value);
    const total = qty * price;

    mainBalance += total;
    updateBalanceDisplay();

    const row = document.createElement('tr');
    row.innerHTML = `
      <td>${contact}</td>
      <td>${type}</td>
      <td>${qty}</td>
      <td>${price}</td>
      <td>${total.toFixed(2)}</td>
      <td><button onclick="editRow(this, 'sell')">Edit</button> <button onclick="deleteRow(this, 'sell', ${total})">Delete</button></td>
    `;
    document.querySelector('#sellingTable tbody').appendChild(row);
    this.reset();
  });

  function editRow(btn, type) {
    const row = btn.parentElement.parentElement;
    const cells = row.querySelectorAll('td');
    if (type === 'purchase') {
      henType.value = cells[0].textContent;
      henCount.value = cells[1].textContent;
      purchasePrice.value = cells[2].textContent;
      mainBalance += parseFloat(cells[3].textContent);
    } else {
      contactNumber.value = cells[0].textContent;
      sellType.value = cells[1].textContent;
      sellQty.value = cells[2].textContent;
      sellPrice.value = cells[3].textContent;
      mainBalance -= parseFloat(cells[4].textContent);
    }
    row.remove();
    updateBalanceDisplay();
  }

  function deleteRow(btn, type, amount) {
    const row = btn.parentElement.parentElement;
    if (type === 'purchase') {
      mainBalance += amount;
    } else {
      mainBalance -= amount;
    }
    row.remove();
    updateBalanceDisplay();
  }
</script>

</body>
</html>
