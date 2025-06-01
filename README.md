# Billing-app
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
<title>Pharmacy Stock & Billing App</title>
<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&display=swap");
  body {
    margin: 0;
    font-family: "Montserrat", sans-serif;
    background: #f5f7fa;
    color: #333;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  header {
    background: #3f51b5;
    color: white;
    padding: 1rem;
    text-align: center;
    font-size: 1.6rem;
    font-weight: 600;
    letter-spacing: 1px;
    user-select: none;
  }
  #shop-info-section {
    max-width: 600px;
    margin: 1rem auto 1rem auto;
    padding: 1rem 1rem;
    background: white;
    border-radius: 10px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
  }
  #shop-info-section h3 {
    margin-top: 0;
    color: #3f51b5;
    font-weight: 700;
    margin-bottom: 1rem;
    border-bottom: 2px solid #3f51b5;
    padding-bottom: 0.4rem;
  }
  #shop-info-section .info-line {
    margin: 0.3rem 0;
    font-size: 1rem;
  }
  main {
    max-width: 600px;
    margin: 0 auto 2rem auto;
    padding: 0 1rem 1rem 1rem;
  }
  section {
    background: white;
    border-radius: 10px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
    padding: 1rem 1rem 1rem 1rem;
    margin-bottom: 1.5rem;
  }
  h2 {
    margin-top: 0;
    color: #3f51b5;
    font-weight: 700;
    margin-bottom: 1rem;
    border-bottom: 2px solid #3f51b5;
    padding-bottom: 0.4rem;
    font-size: 1.25rem;
  }
  label {
    display: block;
    margin: 0.35rem 0 0.15rem 0;
    font-weight: 600;
    font-size: 1rem;
  }
  input,
  select,
  textarea,
  button {
    width: 100%;
    padding: 0.45rem 0.6rem;
    margin-bottom: 0.8rem;
    font-size: 1rem;
    border-radius: 8px;
    border: 1.5px solid #ccc;
    font-family: "Montserrat", sans-serif;
    box-sizing: border-box;
  }
  textarea {
    resize: vertical;
  }
  input:focus,
  select:focus,
  textarea:focus {
    outline: none;
    border-color: #3f51b5;
  }
  button {
    background: #3f51b5;
    color: white;
    border: none;
    font-weight: 700;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  button:hover {
    background: #303f9f;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.9rem;
  }
  th,
  td {
    text-align: left;
    padding: 0.5rem 0.4rem;
    border-bottom: 1px solid #ddd;
  }
  th {
    background: #e8eaf6;
    font-weight: 700;
  }
  .danger-btn {
    background: #e53935;
    color: white;
    border-radius: 6px;
    padding: 0.3rem 0.6rem;
    font-size: 0.9rem;
    cursor: pointer;
    border: none;
  }
  .danger-btn:hover {
    background: #b71c1c;
  }
  .bill-summary {
    background: #f1f8e9;
    padding: 1rem;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1.1rem;
    margin-top: 0.5rem;
  }
  .no-stock,
  .no-bill-items {
    text-align: center;
    color: #999;
    font-style: italic;
    margin-top: 0.5rem;
  }
  #finalize-bill-btn,
  #print-bill-btn,
  #clear-bill-btn {
    margin-top: 0.5rem;
  }
  #print-bill-btn {
    background-color: #4caf50;
  }
  @media (min-width: 480px) {
    input,
    select,
    textarea,
    button {
      font-size: 1.1rem;
    }
  }
</style>
</head>
<body>
<header>Pharmacy Stock & Billing App</header>

<section id="shop-info-section" aria-label="Shop information">
  <h3>Shop Information</h3>
  <div class="info-line"><strong>Shop Name:</strong> Singh Medical Store</div>
  <div class="info-line"><strong>Address:</strong> Sahson bypass prayagraj</div>
  <div class="info-line"><strong>Contact:</strong> 9198320548</div>
</section>

<main>
  <section id="stock-section">
    <h2>Stock Management</h2>
    <form id="stock-form" autocomplete="off">
      <label for="medicine-name">Medicine Name</label>
      <input type="text" id="medicine-name" placeholder="Eg. Paracetamol" required autocomplete="off" />

      <label for="medicine-quantity">Quantity</label>
      <input type="number" id="medicine-quantity" min="1" step="1" required />

      <label for="medicine-price">Price per unit (₹)</label>
      <input type="number" id="medicine-price" min="0.01" step="0.01" required />

      <label for="medicine-expiry">Expiry Date</label>
      <input type="date" id="medicine-expiry" required />

      <button type="submit" id="add-stock-btn">Add / Update Stock</button>
    </form>
    <div id="stock-list">
      <h3>Current Stock</h3>
      <table id="stock-table" aria-label="Stock table">
        <thead>
          <tr>
            <th>Medicine</th>
            <th>Qty</th>
            <th>Price (₹)</th>
            <th>Expiry</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <!-- Stock rows go here -->
        </tbody>
      </table>
      <p class="no-stock">No stock available.</p>
    </div>
  </section>
  <section id="billing-section">
    <h2>Billing</h2>
    <form id="billing-form" autocomplete="off">
      <label for="customer-mobile">Customer Mobile Number</label>
      <input type="text" id="customer-mobile" placeholder="Enter Customer Mobile Number"
        pattern="^[+0-9\s-]{7,15}$" title="Enter valid mobile number" autocomplete="off" />

      <label for="bill-medicine-select">Select Medicine</label>
      <select id="bill-medicine-select" required>
        <option value="" disabled selected>Choose medicine</option>
      </select>

      <label for="bill-quantity">Quantity</label>
      <input type="number" id="bill-quantity" min="1" step="1" required />

      <button type="button" id="add-to-bill-btn">Add to Bill</button>
    </form>
    <div id="bill-order-list">
      <h3>Bill Items</h3>
      <table id="bill-table" aria-label="Bill items table">
        <thead>
          <tr>
            <th>Medicine</th>
            <th>Qty</th>
            <th>Unit Price (₹)</th>
            <th>Total (₹)</th>
            <th>Remove</th>
          </tr>
        </thead>
        <tbody>
          <!-- Bill items go here -->
        </tbody>
      </table>
      <p class="no-bill-items">No items added to bill.</p>
      <div class="bill-summary" id="bill-total-container" style="display:none;">
        Total Amount: ₹<span id="bill-total">0.00</span>
      </div>
      <button type="button" id="finalize-bill-btn" style="margin-top:1rem;" disabled>Finalize Bill</button>
      <button type="button" id="print-bill-btn" style="margin-left:10px; margin-top:1rem; background:#4caf50;">Print Bill</button>
      <button type="button" id="clear-bill-btn" style="margin-top:0.5rem; background:#f57f17;">Clear Bill</button>
    </div>
    <div id="bill-receipt" style="margin-top:1rem; display:none;">
      <h3>Bill Receipt</h3>
      <pre id="bill-receipt-content"
        style="background:#e0e0e0; padding:1rem; border-radius:8px; white-space: pre-wrap;"></pre>
      <button type="button" id="close-receipt-btn" style="margin-top:0.5rem; background:#757575;">Close Receipt</button>
    </div>
  </section>
</main>

<script>
  (() => {
    const STOCK_KEY = 'pharmacy_stock';

    const SHOP_NAME = "Singh Medical Store";
    const SHOP_ADDRESS = "Sahson bypass prayagraj";
    const SHOP_CONTACT = "9198320548";

    const stockForm = document.getElementById('stock-form');
    const medNameInput = document.getElementById('medicine-name');
    const medQtyInput = document.getElementById('medicine-quantity');
    const medPriceInput = document.getElementById('medicine-price');
    const medExpiryInput = document.getElementById('medicine-expiry');
    const stockTableBody = document.querySelector('#stock-table tbody');
    const noStockMsg = document.querySelector('.no-stock');

    const billMedicineSelect = document.getElementById('bill-medicine-select');
    const billQtyInput = document.getElementById('bill-quantity');
    const addToBillBtn = document.getElementById('add-to-bill-btn');
    const billTableBody = document.querySelector('#bill-table tbody');
    const noBillItemsMsg = document.querySelector('.no-bill-items');
    const billTotalContainer = document.getElementById('bill-total-container');
    const billTotalSpan = document.getElementById('bill-total');
    const finalizeBillBtn = document.getElementById('finalize-bill-btn');
    const printBillBtn = document.getElementById('print-bill-btn');
    const clearBillBtn = document.getElementById('clear-bill-btn');
    const billReceipt = document.getElementById('bill-receipt');
    const billReceiptContent = document.getElementById('bill-receipt-content');
    const closeReceiptBtn = document.getElementById('close-receipt-btn');
    const customerMobileInput = document.getElementById('customer-mobile');

    let stock = [];
    let billItems = [];

    function loadStock() {
      const stored = localStorage.getItem(STOCK_KEY);
      if (stored) {
        try {
          const parsed = JSON.parse(stored);
          if (Array.isArray(parsed)) {
            stock = parsed;
          }
        } catch { }
      }
    }

    function saveStock() {
      localStorage.setItem(STOCK_KEY, JSON.stringify(stock));
    }

    function renderStock() {
      stockTableBody.innerHTML = '';
      if (stock.length === 0) {
        noStockMsg.style.display = 'block';
        populateMedicineSelect();
        return;
      } else {
        noStockMsg.style.display = 'none';
      }
      stock.forEach((med, idx) => {
        const tr = document.createElement('tr');
        const expiryDate = new Date(med.expiry);
        const expiryStr = expiryDate.toLocaleDateString();

        tr.innerHTML = `
        <td>${med.name}</td>
        <td>${med.quantity}</td>
        <td>₹${med.price.toFixed(2)}</td>
        <td>${expiryStr}</td>
        <td><button class="danger-btn" data-index="${idx}" aria-label="Remove ${med.name}">Remove</button></td>
      `;
        stockTableBody.appendChild(tr);
      });
      populateMedicineSelect();
    }

    function populateMedicineSelect() {
      billMedicineSelect.innerHTML = '<option value="" disabled selected>Choose medicine</option>';
      const today = new Date();
      today.setHours(0, 0, 0, 0);

      stock.forEach(med => {
        const expiryDate = new Date(med.expiry);
        if (med.quantity > 0 && expiryDate >= today) {
          const option = document.createElement('option');
          option.value = med.name;
          option.textContent = `${med.name} (₹${med.price.toFixed(2)}, ${med.quantity} pcs)`;
          billMedicineSelect.appendChild(option);
        }
      });
    }

    function renderBill() {
      billTableBody.innerHTML = '';
      if (billItems.length === 0) {
        noBillItemsMsg.style.display = 'block';
        billTotalContainer.style.display = 'none';
        finalizeBillBtn.disabled = true;
        return;
      }
      noBillItemsMsg.style.display = 'none';
      billTotalContainer.style.display = 'block';
      finalizeBillBtn.disabled = false;

      let totalAmount = 0;
      billItems.forEach((item, idx) => {
        const itemTotal = item.quantity * item.price;
        totalAmount += itemTotal;

        const tr = document.createElement('tr');
        tr.innerHTML = `
        <td>${item.name}</td>
        <td>${item.quantity}</td>
        <td>₹${item.price.toFixed(2)}</td>
        <td>₹${itemTotal.toFixed(2)}</td>
        <td><button class="danger-btn" data-index="${idx}" aria-label="Remove ${item.name} from bill">X</button></td>
      `;
        billTableBody.appendChild(tr);
      });
      billTotalSpan.textContent = totalAmount.toFixed(2);
    }

    stockForm.addEventListener('submit', e => {
      e.preventDefault();
      const name = medNameInput.value.trim();
      const quantity = Number(medQtyInput.value);
      const price = Number(medPriceInput.value);
      const expiry = medExpiryInput.value;

      if (!name || quantity < 1 || price <= 0 || !expiry) {
        alert('Please fill all fields correctly.');
        return;
      }

      const expiryDate = new Date(expiry);
      if (isNaN(expiryDate.getTime())) {
        alert('Please enter a valid expiry date.');
        return;
      }

      const today = new Date();
      today.setHours(0, 0, 0, 0);
      if (expiryDate < today) {
        alert('Medicine expiry date cannot be in the past.');
        return;
      }

      const idx = stock.findIndex(m => m.name.toLowerCase() === name.toLowerCase());

      if (idx >= 0) {
        stock[idx].quantity += quantity;
        stock[idx].price = price;
        stock[idx].expiry = expiry;
        alert(`Updated stock for "${stock[idx].name}".`);
      } else {
        stock.push({ name, quantity, price, expiry });
        alert(`Added new medicine "${name}" to stock.`);
      }
      saveStock();
      renderStock();
      stockForm.reset();
    });

    stockTableBody.addEventListener('click', e => {
      if (e.target.tagName === 'BUTTON') {
        const idx = Number(e.target.getAttribute('data-index'));
        if (idx >= 0 && idx < stock.length) {
          if (confirm(`Remove "${stock[idx].name}" from stock?`)) {
            stock.splice(idx, 1);
            saveStock();
            renderStock();
          }
        }
      }
    });

    addToBillBtn.addEventListener('click', () => {
      const medName = billMedicineSelect.value;
      const quantity = Number(billQtyInput.value);

      if (!medName) {
        alert('Please select a medicine.');
        return;
      }
      if (!quantity || quantity < 1) {
        alert('Please enter a valid quantity.');
        return;
      }
      const med = stock.find(m => m.name === medName);
      if (!med) {
        alert('Selected medicine not found in stock.');
        populateMedicineSelect();
        return;
      }
      if (quantity > med.quantity) {
        alert(`Only ${med.quantity} pieces of "${med.name}" are available in stock.`);
        return;
      }
      const billIdx = billItems.findIndex(item => item.name === medName);
      if (billIdx >= 0) {
        if ((billItems[billIdx].quantity + quantity) > med.quantity) {
          alert(`Total quantity exceeds stock available (${med.quantity}) for "${med.name}".`);
          return;
        }
        billItems[billIdx].quantity += quantity;
      } else {
        billItems.push({ name: medName, quantity, price: med.price });
      }
      renderBill();
      billQtyInput.value = '';
      billMedicineSelect.value = '';
    });

    billTableBody.addEventListener('click', e => {
      if (e.target.tagName === 'BUTTON') {
        const idx = Number(e.target.getAttribute('data-index'));
        if (idx >= 0 && idx < billItems.length) {
          billItems.splice(idx, 1);
          renderBill();
        }
      }
    });

    finalizeBillBtn.addEventListener('click', () => {
      const custMobile = customerMobileInput.value.trim();
      if (!custMobile || !customerMobileInput.checkValidity()) {
        alert('Please enter a valid Customer Mobile Number.');
        customerMobileInput.focus();
        return;
      }

      if (billItems.length === 0) {
        alert('Add items to bill before finalizing.');
        return;
      }

      billItems.forEach(billItem => {
        const stockMed = stock.find(m => m.name === billItem.name);
        if (stockMed) {
          stockMed.quantity -= billItem.quantity;
          if (stockMed.quantity < 0) stockMed.quantity = 0;
        }
      });

      saveStock();
      renderStock();

      const now = new Date();
      let receiptText = 'PHARMACY BILL RECEIPT\n';
      receiptText += '------------------------\n';
      receiptText += `Date: ${now.toLocaleString()}\n\n`;

      receiptText += `Shop Name: ${SHOP_NAME}\n`;
      receiptText += `Address:\n${SHOP_ADDRESS}\n`;
      receiptText += `Contact: ${SHOP_CONTACT}\n`;
      receiptText += '------------------------\n\n';

      receiptText += `Customer Mobile: ${custMobile}\n\n`;

      let totalAmount = 0;
      billItems.forEach(item => {
        const itemTotal = item.quantity * item.price;
        receiptText += `${item.name} x ${item.quantity} @ ₹${item.price.toFixed(2)} = ₹${itemTotal.toFixed(2)}\n`;
        totalAmount += itemTotal;
      });

      receiptText += '\n------------------------\n';
      receiptText += `TOTAL: ₹${totalAmount.toFixed(2)}\n\n`;
      receiptText += 'Thank you for your purchase!\n';

      billReceiptContent.textContent = receiptText;
      billReceipt.style.display = 'block';

      sendSms(custMobile, receiptText);

      billItems = [];
      renderBill();
    });

    function sendSms(number, message) {
      const encodedMsg = encodeURIComponent(message);
      const smsUrl = `sms:${number}?body=${encodedMsg}`;
      window.open(smsUrl);
    }

    printBillBtn.addEventListener('click', () => {
      if (!billReceipt.style.display || billReceipt.style.display === 'none') {
        alert('Please finalize the bill first to print the receipt.');
        return;
      }
      const printContents = billReceiptContent.innerText;
      const printWindow = window.open('', '', 'height=600,width=800');
      printWindow.document.write('<html><head><title>Print Bill Receipt</title>');
      printWindow.document.write('<style>body { font-family: Montserrat, sans-serif; white-space: pre-wrap; padding: 1rem; }</style>');
      printWindow.document.write('</head><body >');
      printWindow.document.write('<pre>' + printContents + '</pre>');
      printWindow.document.write('</body></html>');
      printWindow.document.close();
      printWindow.focus();
      printWindow.onload = () => {
        printWindow.print();
        printWindow.close();
      };
    });

    clearBillBtn.addEventListener('click', () => {
      if (confirm('Clear all items from the current bill?')) {
        billItems = [];
        renderBill();
      }
    });

    closeReceiptBtn.addEventListener('click', () => {
      billReceipt.style.display = 'none';
    });

    loadStock();
    renderStock();
    renderBill();
  })();
</script>
</body>
</html>
