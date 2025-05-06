<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SIVA CHICKEN FARM</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f8f8f8;
    }
    header {
      background: #d62828;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .balance-summary {
      background: #fff3cd;
      padding: 10px;
      text-align: center;
      font-weight: bold;
      font-size: 18px;
    }
    .balance-summary input {
      padding: 5px;
      margin-left: 10px;
      font-size: 18px;
      width: 150px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    nav {
      background: #333;
      display: flex;
      justify-content: center;
      flex-wrap: wrap;
    }
    nav a {
      color: white;
      padding: 14px 20px;
      display: inline-block;
      text-decoration: none;
    }
    nav a:hover {
      background: #555;
    }
    .container {
      padding: 20px;
      display: none;
    }
    .container.active {
      display: block;
    }
    .price-list table, .admin-expense table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    .price-list th, .price-list td, .admin-expense th, .admin-expense td {
      padding: 10px;
      border: 1px solid #ccc;
      text-align: center;
    }
    form {
      background: #fff;
      padding: 20px;
      border-radius: 5px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
      max-width: 600px;
      margin: auto;
    }
    input, select, textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      background-color: #d62828;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    button:hover {
      background-color: #b91c1c;
    }
    footer {
      background: #d62828;
      color: white;
      text-align: center;
      padding: 10px;
      position: fixed;
      bottom: 0;
      width: 100%;
    }
    .export-button, .print-button {
      display: block;
      margin: 20px auto;
      padding: 10px 20px;
      background-color: #218380;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    .export-button:hover, .print-button:hover {
      background-color: #166a67;
    }
  </style>
</head>
<body>
  <header>
    <h1>SIVA CHICKEN FARM</h1>
    <p>Fresh Chicken Daily | Broiler - Kalbird - Parents - Meat</p>
  </header>

  <div class="balance-summary">
    Balance: 
    <span id="balance-display">LKR 0.00</span>
    <button onclick="toggleBalanceEdit()">Edit</button>
    <div id="balance-edit" style="display: none;">
      <input type="number" id="balance-input" value="0" />
      <button onclick="saveBalance()">Save</button>
    </div>
    | Total Income: <span id="income">LKR 0.00</span> | Total Expenses: <span id="expenses">LKR 0.00</span>
  </div>

  <nav>
    <a href="#" onclick="showSection('home')">Home</a>
    <a href="#" onclick="showSection('prices')">Price List</a>
    <a href="#" onclick="showSection('order')">Order</a>
    <a href="#" onclick="showSection('admin')">Admin</a>
    <a href="#" onclick="showSection('contact')">Contact</a>
  </nav>

  <div class="container" id="home">
    <h2>Welcome to SIVA CHICKEN FARM</h2>
    <div class="balance-summary">
      <h3>Balance Information</h3>
      <p>Balance: <span id="balance">LKR 0.00</span></p>
      <p>Total Income: <span id="income">LKR 0.00</span></p>
      <p>Total Expenses: <span id="expenses">LKR 0.00</span></p>
    </div>

    <h3>Current Inventory & Stock</h3>
    <table>
      <thead>
        <tr>
          <th>Chicken Type</th>
          <th>Current Stock (KG/Pieces)</th>
        </tr>
      </thead>
      <tbody id="inventory-stock">
        <tr>
          <td>Broiler</td>
          <td id="broiler-stock">50</td>
        </tr>
        <tr>
          <td>Kalbird</td>
          <td id="kalbird-stock">40</td>
        </tr>
        <tr>
          <td>Parents</td>
          <td id="parents-stock">30</td>
        </tr>
        <tr>
          <td>Meat</td>
          <td id="meat-stock">60</td>
        </tr>
      </tbody>
    </table>
  </div>

  <div class="container price-list" id="prices">
    <h2>Daily Price List - <span id="date"></span></h2>
    <table>
      <tr>
        <th>Chicken Type</th>
        <th>Price (LKR)</th>
      </tr>
      <tr>
        <td>Broiler</td>
        <td>Rs. 750</td>
      </tr>
      <tr>
        <td>Kalbird</td>
        <td>Rs. 890</td>
      </tr>
      <tr>
        <td>Parents</td>
        <td>Rs. 950</td>
      </tr>
      <tr>
        <td>Meat</td>
        <td>Rs. 620</td>
      </tr>
    </table>
    <button class="print-button" onclick="printPriceList()">Print Price List</button>
  </div>

  <div class="container" id="order">
    <h2>Place Your Order</h2>
    <form>
      <label for="name">Customer Name</label>
      <input type="text" id="name" name="name" required />

      <label for="phone">Phone Number</label>
      <input type="tel" id="phone" name="phone" required />

      <label for="type">Chicken Type</label>
      <select id="type" name="type">
        <option value="Broiler">Broiler</option>
        <option value="Kalbird">Kalbird</option>
        <option value="Parents">Parents</option>
        <option value="Meat">Meat</option>
      </select>

      <label for="quantity">Quantity (in KG or pieces)</label>
      <input type="text" id="quantity" name="quantity" required />

      <label for="delivery">Delivery Option</label>
      <select id="delivery" name="delivery">
        <option value="Pickup">Pickup</option>
        <option value="Delivery">Delivery</option>
      </select>

      <button type="submit">Submit Order</button>
    </form>
  </div>

  <div class="container admin-expense" id="admin">
    <h2>Admin - Daily Expenses</h2>
    <form id="expense-form">
      <label for="expense-date">Date</label>
      <input type="date" id="expense-date" name="expense-date" required />

      <label for="category">Category</label>
      <select id="category" name="category">
        <option value="Feed">Feed</option>
        <option value="Chicks">Chicks</option>
        <option value="Salary">Salary</option>
        <option value="Transport">Transport</option>
        <option value="Other">Other</option>
        <option value="Income">Income</option>
      </select>

      <label for="amount">Amount (LKR)</label>
      <input type="number" id="amount" name="amount" required />

      <label for="notes">Notes</label>
      <textarea id="notes" name="notes" rows="3"></textarea>

      <button type="submit">Save Expense</button>
    </form>

    <button class="export-button" onclick="exportExpenseData()">Export to CSV</button>
  </div>

  <div class="container" id="contact">
    <h2>Contact Us</h2>
    <p>Call or WhatsApp: <strong>0756272065</strong></p>
  </div>

  <footer>
    &copy; 2025 SIVA CHICKEN FARM
  </footer>

  <script>
    const date = new Date();
    document.getElementById("date").innerText = date.toLocaleDateString();

    let totalIncome = 0;
    let totalExpenses = 0;

    // Inventory Stock Data (This could be updated dynamically if necessary)
    const inventory = {
      broiler: 50,
      kalbird: 40,
      parents: 30,
      meat: 60
    };

    // Update balance and stock data
    function updateBalance() {
      const balance = totalIncome - totalExpenses;
      document.getElementById("income").innerText = `LKR ${totalIncome.toFixed(2)}`;
      document.getElementById("expenses").innerText = `LKR ${totalExpenses.toFixed(2)}`;
      document.getElementById("balance-display").innerText = `LKR ${balance.toFixed(2)}`;
    }

    // Update inventory stock
    function updateInventory() {
      document.getElementById("broiler-stock").innerText = inventory.broiler;
      document.getElementById("kalbird-stock").innerText = inventory.kalbird;
      document.getElementById("parents-stock").innerText = inventory.parents;
      document.getElementById("meat-stock").innerText = inventory.meat;
    }

    document.getElementById("expense-form").addEventListener("submit", function(event) {
      event.preventDefault();
      const category = document.getElementById("category").value;
      const amount = parseFloat(document.getElementById("amount").value);
      if (category === "Income") {
        totalIncome += amount;
      } else {
        totalExpenses += amount;
      }
      updateBalance();
      alert("Entry saved and balance updated.");
    });

    function exportExpenseData() {
      const form = document.getElementById('expense-form');
      const date = form['expense-date'].value;
      const category = form['category'].value;
      const amount = form['amount'].value;
      const notes = form['notes'].value;

      const csvContent = `Date,Category,Amount,Notes\n"${date}","${category}","${amount}","${notes}"`;
      const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
      const url = URL.createObjectURL(blob);
      const link = document.createElement("a");
      link.setAttribute("href", url);
      link.setAttribute("download", `expense_${date}.csv`);
      link.style.display = "none";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }

    function printPriceList() {
      const priceSection = document.getElementById("prices").innerHTML;
      const originalBody = document.body.innerHTML;
      document.body.innerHTML = priceSection;
      window.print();
      document.body.innerHTML = originalBody;
    }

    function toggleBalanceEdit() {
      const balanceDisplay = document.getElementById("balance-display");
      const balanceEdit = document.getElementById("balance-edit");
      const balanceInput = document.getElementById("balance-input");

      if (balanceEdit.style.display === "none") {
        balanceEdit.style.display = "block";
        balanceDisplay.style.display = "none";
        balanceInput.value = parseFloat(balanceDisplay.innerText.replace('LKR', '').trim()).toFixed(2);
      } else {
        balanceEdit.style.display = "none";
        balanceDisplay.style.display = "inline";
      }
    }

    function saveBalance() {
      const balanceInput = document.getElementById("balance-input");
      totalIncome = parseFloat(balanceInput.value);
      totalExpenses = 0;
      updateBalance();
      toggleBalanceEdit();
    }

    function showSection(sectionId) {
      document.querySelectorAll(".container").forEach(container => {
        container.classList.remove("active");
      });
      document.getElementById(sectionId).classList.add("active");
    }

    updateBalance();
    updateInventory();
  </script>
</body>
</html>
