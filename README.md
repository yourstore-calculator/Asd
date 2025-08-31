# Asd
<!DOCTYPE html>
<html lang="en" dir="ltr">
<head>
  <meta charset="UTF-8" />
  <title>Advanced Price Calculator</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

    :root {
        --bg-color: #1a1a1a;
        --surface-color: #252526;
        --primary-color: #007acc;
        --primary-hover: #005a9e;
        --secondary-color: #555;
        --secondary-hover: #777;
        --danger-color: #c0392b;
        --danger-hover: #a52f22;
        --accent-color: #00e676;
        --text-color: #f0f0f0;
        --border-color: #333;
    }

    body { 
        font-family: 'Poppins', 'Segoe UI', sans-serif; 
        background-color: var(--bg-color); 
        color: var(--text-color); 
        direction: ltr; 
        padding: 30px; 
        line-height: 1.6;
    }
    
    .container {
        max-width: 1200px;
        margin: auto;
    }

    h1, h2, h3, h4 {
        color: var(--accent-color);
        margin-top: 0;
    }

    h1 {
        text-align: center;
        margin-bottom: 40px;
        font-weight: 600;
        letter-spacing: 1px;
    }

    select, input, textarea { 
        padding: 12px; 
        margin-bottom: 10px; 
        width: 100%; 
        border: 1px solid var(--border-color); 
        border-radius: 6px; 
        box-sizing: border-box; 
        background-color: #3c3c3c; 
        color: var(--text-color);
        font-family: 'Poppins', sans-serif;
        transition: border-color 0.3s, box-shadow 0.3s;
    }
    
    select:focus, input:focus, textarea:focus {
        outline: none;
        border-color: var(--primary-color);
        box-shadow: 0 0 8px rgba(0, 122, 204, 0.5);
    }

    .section { 
        background-color: var(--surface-color); 
        padding: 25px; 
        border-radius: 12px; 
        margin-bottom: 25px; 
        border: 1px solid var(--border-color);
        box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
    
    .section-header {
        display: flex;
        align-items: center;
        gap: 10px;
        margin-bottom: 15px;
        border-bottom: 1px solid var(--border-color);
        padding-bottom: 10px;
    }
    .section-header i {
        color: var(--accent-color);
    }

    label { 
        font-weight: 400; 
        color: var(--accent-color); 
        display: block; 
        margin-bottom: 5px; 
        font-size: 0.9em;
    }
    
    button { 
        background-color: var(--primary-color); 
        color: white; 
        padding: 12px 25px; 
        border: none; 
        margin-top: 10px; 
        border-radius: 6px; 
        cursor: pointer; 
        font-size: 16px; 
        font-weight: 600;
        transition: background-color 0.3s, transform 0.2s; 
    }
    button:hover { 
        background-color: var(--primary-hover); 
        transform: translateY(-2px);
    }
    
    .btn-secondary { background-color: var(--secondary-color); }
    .btn-secondary:hover { background-color: var(--secondary-hover); }
    .btn-danger { background-color: var(--danger-color); }
    .btn-danger:hover { background-color: var(--danger-hover); }

    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        gap: 20px;
    }

    .results { background: none; border: none; padding: 0; box-shadow: none; }
    .result-item { 
        background-color: var(--surface-color); 
        border: 1px solid var(--border-color); 
        border-radius: 12px; 
        padding: 20px; 
        margin-bottom: 20px;
        box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }
    .summary { 
        font-weight: 600; 
        color: var(--accent-color); 
        padding: 25px; 
        border: 1px solid var(--accent-color);
        border-radius: 12px;
        margin-top: 25px; 
        background: linear-gradient(145deg, #2a2a2a, #212121);
    }
    .summary-row {
        display: flex;
        justify-content: space-between;
        padding: 8px 0;
        font-size: 1.1em;
    }
    .grand-total {
        background-color: var(--accent-color);
        color: var(--bg-color);
        padding: 20px;
        border-radius: 8px;
        text-align: center;
        margin-top: 15px;
    }
    .grand-total .label {
        font-size: 1.2em;
        font-weight: 600;
    }
    .grand-total .value {
        font-size: 2.2em;
        font-weight: 600;
        letter-spacing: 1px;
    }
    
    .item-header { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--border-color); padding-bottom: 10px; margin-bottom: 15px; }
    .item-header h4 { margin: 0; font-size: 1.3em; }
    
    #addonsHost div { margin-bottom: 10px; }
  </style>
</head>
<body>
<div class="container">

<h1><i class="fas fa-calculator"></i> Advanced Price Calculator</h1>

<div class="section">
    <div class="section-header">
        <i class="fas fa-user-circle"></i>
        <h2>Customer Information</h2>
    </div>
    <div class="grid-container">
        <div>
            <label for="customerName">Customer Name</label>
            <input type="text" id="customerName" placeholder="e.g., John Doe" />
        </div>
        <div>
            <label for="customerPhone">Customer Phone</label>
            <input type="text" id="customerPhone" placeholder="e.g., 99455082" />
        </div>
    </div>
</div>

<div class="section">
    <div class="section-header">
        <i class="fas fa-cogs"></i>
        <h2>Product Selection</h2>
    </div>
    <div class="grid-container">
        <div>
            <label for="mainCategory">Main Category</label>
            <select id="mainCategory" onchange="loadSubTypes()"></select>
        </div>
        <div>
            <label for="subType">Sub Type</label>
            <select id="subType" onchange="renderAddons()"></select>
        </div>
    </div>
</div>

<div class="section">
    <div class="section-header">
        <i class="fas fa-ruler-combined"></i>
        <h2>Dimensions & Quantity</h2>
    </div>
    <div class="grid-container">
        <div>
            <label for="height">Height (meter)</label>
            <input type="number" id="height" step="0.01" value="1" />
        </div>
        <div>
            <label for="width">Width (meter)</label>
            <input type="number" id="width" step="0.01" value="1" />
        </div>
        <div>
            <label for="quantity">Quantity</label>
            <input type="number" id="quantity" value="1" />
        </div>
    </div>
</div>

<div class="section" id="addonsHost"></div>

<div style="text-align: center; margin-bottom: 20px;">
    <button onclick="addItem()">➕ Add Item</button>
    <button onclick="clearAllResults()" class="btn-danger">🗑️ Clear All Results</button>
    <button onclick="saveAsWord()" class="btn-secondary">💾 Save as Word</button>
</div>

<div class="results" id="results"></div>
</div>

<script>
const SHIPPING_RATE = 48;
const addonPrices = { 
    curtain: 26, 
    net: { door: 39, folding: 18, sliding: 14 } 
};

const productData = {
    "Windows": {
        "Window Double Glass Double Frame Fixed": { price: 34, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Double Frame 1-Way": { price: 34, fixed_component_cost: 39, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Double Frame 2-Way": { price: 34, fixed_component_cost: 58, cbm: 0.13, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame Fixed": { price: 26, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame 1-Way": { price: 26, fixed_component_cost: 20, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Double Glass Single Frame 2-Way": { price: 26, fixed_component_cost: 32, cbm: 0.07, method: 'per_meter', addons: 'curtain,net' },
        "Window Single Glass Single Frame Fixed": { price: 20, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Window Single Glass Single Frame 1-Way": { price: 20, fixed_component_cost: 13, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Window Single Glass Single Frame 2-Way": { price: 20, fixed_component_cost: 17, cbm: 0.07, method: 'per_meter', addons: 'net' },
        "Sliding Windows": { price: 41, fixed_component_cost: 10, cbm: 0.13, method: 'per_meter', addons: 'curtain' },
        "Electric Windows": { price: 102, cbm: 0.13, method: 'per_meter' },
        "Skylight without Motor": { price: 56, cbm: 0.13, method: 'per_meter' },
        "Skylight with Motor": { price: 145, cbm: 0.13, method: 'per_meter' },
        "Heavy Curtain Wall": { price: 56, cbm: 0.15, method: 'per_meter' },
        "Light Curtain Wall": { price: 45, cbm: 0.15, method: 'per_meter' },
    },
    "Doors": {
        "Entrance Door - Zinc": { price: 66, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "Entrance Door - Stainless Steel": { price: 120, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "Entrance Door - Cast Aluminum": { price: 168, cbm: 0.20, method: 'per_meter', special: 'add_10' },
        "WPC Door": { price: 45, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Wood": { price: 50, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Soundproof Filling": { price: 60, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "WPC Door - with Aluminum Frame": { price: 67, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door": { price: 65, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - with Wood": { price: 75, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Full": { price: 85, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Hidden": { price: 110, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Aluminum Door - Exterior": { price: 61, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 1.0 },
        "Bathroom Door - New Type": { price: 55, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
        "Bathroom Door - Old Type": { price: 45, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
        "Bathroom Door - Hidden Glass": { price: 65, cbm: 0.11, method: 'per_unit', std_h: 2.2, std_w: 0.8 },
    },
    "Sliding Doors": {
        "Interior Sliding Door - Glass": { price: 38, cbm: 0.15, method: 'per_meter', addons: 'curtain' },
        "Interior Sliding Door - Solid": { price: 41, cbm: 0.15, method: 'per_meter' },
        "Exterior Sliding Door - 1 Panel Open": { price: 55, cbm: 0.15, method: 'per_meter' },
        "Exterior Sliding Door - 2 Panels Open": { price: 58, cbm: 0.15, method: 'per_meter' },
        "WPC Sliding Door": { price: 61, cbm: 0.15, method: 'per_meter' },
    },
    "Folding Doors": {
        "Interior Folding Door": { price: 39, cbm: 0.15, method: 'per_meter' },
        "Exterior Folding Door": { price: 56, cbm: 0.15, method: 'per_meter' },
    },
    "Exterior Shutters": {
        "Rolling Shutter": { price: 28, cbm: 0.20, method: 'per_meter' },
    },
    "Garden Gates": {
        "Cast Aluminum Garden Gate": { price: 91, cbm: 0.20, method: 'per_meter' },
    },
    "Barriers": {
        "Stair Barrier": { price: 43, cbm: 0.05, method: 'per_meter' },
        "Bathroom Barrier": { price: 32, cbm: 0.05, method: 'per_meter' },
    }
};
let resultsList = [];

function initializeApp() {
    const mainCat = document.getElementById("mainCategory");
    mainCat.innerHTML = `<option value="">-- Select Category --</option>`;
    Object.keys(productData).forEach(cat => mainCat.innerHTML += `<option value="${cat}">${cat}</option>`);
    loadSubTypes();
}

function loadSubTypes() {
    const mainCatVal = document.getElementById("mainCategory").value;
    const subType = document.getElementById("subType");
    subType.innerHTML = "";
    if (mainCatVal && productData[mainCatVal]) {
        Object.keys(productData[mainCatVal]).forEach(sub => subType.innerHTML += `<option value="${sub}">${sub}</option>`);
    }
    renderAddons();
}

function renderAddons() {
    const subVal = document.getElementById("subType").value;
    const addonsHost = document.getElementById("addonsHost");
    addonsHost.innerHTML = "";
    const data = findProductData(subVal);
    if (data && data.addons) {
        const availableAddons = data.addons.split(',');
        let addonsHtml = `<div class="section-header"><i class="fas fa-puzzle-piece"></i><h3>Add-ons</h3></div>`;
        if (availableAddons.includes('curtain')) {
            addonsHtml += `<div><label><input type="checkbox" id="addon_curtain"> Add Curtain (+${addonPrices.curtain} OMR/m²)</label></div>`;
        }
        if (availableAddons.includes('net')) {
            addonsHtml += `<div><label for="addon_net_type">Add Net:</label><select id="addon_net_type"><option value="">-- None --</option><option value="door">Door (+${addonPrices.net.door} per 0.5m²)</option><option value="folding">Folding (+${addonPrices.net.folding} per 0.5m²)</option><option value="sliding">Sliding (+${addonPrices.net.sliding} per 0.5m²)</option></select></div>`;
        }
        addonsHost.innerHTML = addonsHtml;
    }
    setDefaultDimensions();
}

function setDefaultDimensions() {
    const subVal = document.getElementById("subType").value;
    const data = findProductData(subVal);
    if (data && data.method === 'per_unit') {
        document.getElementById("height").value = data.std_h || 2.2;
        document.getElementById("width").value = data.std_w || 1.0;
    } else {
        document.getElementById("height").value = 1;
        document.getElementById("width").value = 1;
    }
}

function findProductData(productName) {
    for (const category in productData) {
        if (productData[category][productName]) {
            return productData[category][productName];
        }
    }
    return null;
}

function calculateItemPrice(item) {
    const data = item.data;
    const area = item.h * item.w;
    let basePrice = 0, sizePenalty = 0, addonCost = 0;

    if (data.method === 'per_unit') {
        basePrice = data.price || 0;
        const stdArea = (data.std_h || 0) * (data.std_w || 0);
        if (stdArea > 0 && area > stdArea) {
            sizePenalty = Math.ceil((area - stdArea) / 0.1) * 2;
        }
    } else {
        basePrice = area * (data.price || 0);
    }
    
    if (item.selectedAddons.curtain) {
        addonCost += area * addonPrices.curtain;
    }
    if (item.selectedAddons.netType && addonPrices.net[item.selectedAddons.netType]) {
        addonCost += (area * 0.5) * addonPrices.net[item.selectedAddons.netType];
    }

    const fixedCost = data.fixed_component_cost || 0;
    const specialCost = data.special === 'add_10' ? 10 : 0;
    const shippingCost = area * (data.cbm || 0) * SHIPPING_RATE;
    const unitPrice = basePrice + sizePenalty + fixedCost + specialCost + shippingCost + addonCost;
    return { unitPrice, totalPrice: unitPrice * item.qty, shippingPerItem: shippingCost };
}

function addItem() {
    const subVal = document.getElementById("subType").value;
    if (!subVal) { alert("Please select a sub-type."); return; }
    
    const data = findProductData(subVal);
    const newItem = {
        id: Date.now(),
        name: subVal,
        qty: parseInt(document.getElementById("quantity").value) || 1,
        h: parseFloat(document.getElementById("height").value) || 1,
        w: parseFloat(document.getElementById("width").value) || 1,
        itemNotes: "",
        selectedAddons: {
            curtain: document.getElementById("addon_curtain")?.checked || false,
            netType: document.getElementById("addon_net_type")?.value || null
        },
        data: JSON.parse(JSON.stringify(data))
    };
    
    const prices = calculateItemPrice(newItem);
    newItem.unitPrice = prices.unitPrice;
    newItem.totalPrice = prices.totalPrice;
    resultsList.push(newItem);
    renderResults();
}

function deleteItem(id) {
    resultsList = resultsList.filter(item => item.id !== id);
    renderResults();
}

function clearAllResults() {
    resultsList = [];
    renderResults();
}

function renderResults() {
    const container = document.getElementById("results");
    container.innerHTML = "";
    let subtotal = 0;

    if (resultsList.length === 0) {
        container.innerHTML = `<p style="text-align:center; color: #ccc;">No items added yet.</p>`;
        return;
    }
    
    resultsList.forEach(item => {
        const prices = calculateItemPrice(item);
        subtotal += prices.totalPrice;
        
        let shippingInfo = '';
        if (item.qty > 1) {
            shippingInfo = `<p><strong>Shipping:</strong> ${prices.shippingPerItem.toFixed(2)} OMR (per item) | ${ (prices.shippingPerItem * item.qty).toFixed(2) } OMR (total)</p>`;
        } else {
            shippingInfo = `<p><strong>Shipping Cost:</strong> ${prices.shippingPerItem.toFixed(2)} OMR</p>`;
        }
        
        container.innerHTML += `
            <div class="result-item">
                <div class="item-header">
                    <h4>${item.name}</h4>
                    <button class="btn-danger" style="padding: 6px 12px; margin: 0;" onclick="deleteItem(${item.id})">Delete 🗑️</button>
                </div>
                <p><strong>Dimensions:</strong> ${item.h}m x ${item.w}m | <strong>Quantity:</strong> ${item.qty}</p>
                ${shippingInfo}
                <p style="font-weight: bold; font-size: 1.1em; color: var(--accent-color);">
                    Unit Price: ${prices.unitPrice.toFixed(2)} OMR | Total: ${prices.totalPrice.toFixed(2)} OMR
                </p>
            </div>`;
    });

    const commission = subtotal * 0.04;
    const total = subtotal + commission;
    container.innerHTML += `
        <div class="summary">
            <div class="summary-row"><span>Subtotal:</span><span>${subtotal.toFixed(2)} OMR</span></div>
            <div class="summary-row"><span>Office Commission (4%):</span><span>${commission.toFixed(2)} OMR</span></div>
            <div class="grand-total">
                <div class="label">💰 Grand Total</div>
                <div class="value">${total.toFixed(2)} OMR</div>
            </div>
        </div>`;
}

function formatNumber(num) {
    return Number(num.toFixed(3).replace(/\.?0+$/, ""));
}

function saveAsWord(){
    if (resultsList.length === 0) { alert("There are no results to save."); return; }
    const customerName = document.getElementById('customerName').value || 'Customer';
    const customerPhone = document.getElementById('customerPhone').value || 'N/A';
    const headerHtml = `<div style="width: 100%; font-family: Arial, sans-serif; text-align: center; margin-bottom: 30px; border-bottom: 2px solid #4472C4; padding-bottom: 20px;"><div style="font-size: 26px; font-weight: bold; color: #4472C4; margin-bottom: 15px;">BLUE WAVES SERVICES LLC</div><table width="100%" style="font-family: Arial, sans-serif; font-size: 15px; color: #4472C4; border-collapse: collapse;"><tr><td style="text-align: left; width: 33%;">OMAN – MUSCAT</td><td style="text-align: center; width: 34%;">SR. NO. : 1595256</td><td style="text-align: right; width: 33%;">TEL: 77 22 45 11 – 90 99 88 10</td></tr></table></div>`;
    const customerHtml = `<div style="background-color: #f2f2f2; border: 1px solid #ddd; color: #333; padding: 14px; font-family: Arial, sans-serif; font-size: 17px; margin-bottom: 25px; border-radius: 5px;"><b>Quotation for: </b> ${customerName} - ${customerPhone}</div>`;
    let tableHtml = `<table border="1" width="100%" style="border-collapse: collapse; font-family: Arial, sans-serif; text-align: center; font-size: 14px;">
                        <thead>
                            <tr style="background-color: #4472C4; color: white;">
                                <th style="padding: 10px;">NO</th>
                                <th style="padding: 10px;">H</th>
                                <th style="padding: 10px;">W</th>
                                <th style="padding: 10px;">m²</th>
                                <th style="padding: 10px;">Q</th>
                                <th style="padding: 10px;">RH/LH</th>
                                <th style="padding: 10px;">STYLE</th>
                                <th style="padding: 10px;">PRICE</th>
                                <th style="padding: 10px;">TOTAL</th>
                                <th style="padding: 10px;">DESCRIPTION</th>
                            </tr>
                        </thead>
                        <tbody>`;
    let subtotal = 0;
    let totalShippingCost = 0;
    resultsList.forEach((r, index) => {
        const prices = calculateItemPrice(r);
        subtotal += prices.totalPrice;
        totalShippingCost += prices.shippingPerItem * r.qty;
        let description = r.name;
        if (r.selectedAddons.curtain) description += ', with Curtain';
        if (r.selectedAddons.netType) description += `, with ${r.selectedAddons.netType} Net`;
        
        tableHtml += `<tr>
                        <td style="padding: 10px; font-weight: bold;">B${index + 1}</td>
                        <td style="padding: 10px;">${formatNumber(r.h)}</td>
                        <td style="padding: 10px;">${formatNumber(r.w)}</td>
                        <td style="padding: 10px;">${formatNumber(r.h * r.w)}</td>
                        <td style="padding: 10px;">${r.qty}</td>
                        <td style="padding: 10px;"></td>
                        <td style="padding: 10px;"></td>
                        <td style="padding: 10px; background-color: #f2f2f2;">${formatNumber(prices.unitPrice)}</td>
                        <td style="padding: 10px; background-color: #f2f2f2; font-weight: bold;">${formatNumber(prices.totalPrice)}</td>
                        <td style="padding: 10px; text-align: left; white-space: pre-wrap;">${description}</td>
                      </tr>`;
    });
    tableHtml += `</tbody></table>`;
    const commission = subtotal * 0.04;
    const grandTotal = subtotal + commission;
    const summaryTable = `<table width="45%" align="right" style="border-collapse: collapse; font-family: Arial, sans-serif; margin-top: 25px; font-size: 15px;"><tbody>
                <tr><td style="padding: 14px; font-weight: bold; border: 1px solid #ccc; font-size: 1.2em;">Subtotal</td><td style="padding: 14px; text-align: right; font-weight: bold; border: 1px solid #ccc; font-size: 1.2em;">${formatNumber(subtotal)} OMR</td></tr>
                <tr><td style="padding: 14px; font-weight: bold; border: 1px solid #ccc; font-size: 1.2em;">Total Shipping Cost</td><td style="padding: 14px; text-align: right; font-weight: bold; border: 1px solid #ccc; font-size: 1.2em;">${formatNumber(totalShippingCost)} OMR</td></tr>
                <tr><td style="padding: 14px; font-weight: bold; border: 1px solid #ccc; font-size: 1.2em;">Office Commission (4%)</td><td style="padding: 14px; text-align: right; font-weight: bold; background-color: #f2f2f2; border: 1px solid #ccc; font-size: 1.2em;">${formatNumber(commission)} OMR</td></tr>
                <tr style="background-color: #4472C4; color: white;"><td style="padding: 16px; font-weight: bold; border: 1px solid #4472C4; font-size: 1.5em;">Grand Total</td><td style="padding: 16px; text-align: right; font-weight: bold; border: 1px solid #4472C4; font-size: 1.9em; vertical-align: middle;">${formatNumber(grandTotal)} OMR</td></tr>
                </tbody></table>`;
    const footerNotesHtml = `<div style="clear: both; font-family: Arial, sans-serif; margin-top: 50px; text-align: center; border-top: 2px solid #4472C4; padding-top: 15px; font-size: 16px; color: #333;"><p style="margin: 5px 0;"><b>*Price includes delivery*</b></p><p style="margin: 5px 0;"><b>*Price does not include installation*</b></p></div>`;
    const finalHtml = `<html xmlns:o='urn:schemas-microsoft-com:office:office' xmlns:w='urn:schemas-microsoft-com:office:word' xmlns='http://www.w3.org/TR/REC-html40'><head><meta charset='utf-8'><title>Quotation for - ${customerName}</title></head><body dir="ltr" style="padding: 20px;">`+ headerHtml + customerHtml + tableHtml + summaryTable + footerNotesHtml +`</body></html>`;
    const source = 'data:application/vnd.ms-word;charset=utf-8,' + encodeURIComponent(finalHtml);
    const fileDownload = document.createElement("a");
    document.body.appendChild(fileDownload);
    fileDownload.href = source;
    fileDownload.download = `Quotation for - ${customerName}.doc`;
    fileDownload.click();
    document.body.removeChild(fileDownload);
}

initializeApp();
</script>

</body>
</html>
