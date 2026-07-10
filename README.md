Final code of that we need

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ledger — Personal Finance Tracker</title>
<style>
:root {
  --ink: #22262B;
  --paper: #EDF0EA;
  --surface: #FFFFFF;
  --rule: #D9DED4;
  --brass: #A9793E;
  --brass-dark: #8C5F2E;
  --forest: #2F5D4E;
  --forest-bg: #E1EBE6;
  --brick: #A83E32;
  --brick-bg: #F3E2DF;
  --flag: #B8863B;
  --flag-bg: #F1E6D3;
  --radius: 10px;
  --radius-sm: 7px;
  --shadow: 0 1px 2px rgba(34,38,43,0.06), 0 2px 6px rgba(34,38,43,0.06);
  --serif: Georgia, 'Iowan Old Style', 'Palatino Linotype', 'Book Antiqua', serif;
  --sans: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
}
* { box-sizing: border-box; }
html, body { margin:0; padding:0; }
body {
  font-family: var(--sans);
  background:
    repeating-linear-gradient(to bottom, transparent, transparent 35px, rgba(34,38,43,0.035) 35px, rgba(34,38,43,0.035) 36px),
    var(--paper);
  color: var(--ink);
  line-height: 1.5;
  -webkit-font-smoothing: antialiased;
  min-height: 100vh;
}
h1, h2, h3 { font-family: var(--serif); font-weight: 700; }
.num, .card-value, .ratio-value, .loan-stats strong, .total-pill span, .data-table td.amt {
  font-variant-numeric: tabular-nums;
}

.storage-banner {
  background: var(--flag-bg);
  color: #6b4a1a;
  font-size: 0.82rem;
  padding: 10px 16px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  border-bottom: 1px solid var(--flag);
}
.storage-banner button {
  background: none;
  border: none;
  font-size: 1.1rem;
  cursor: pointer;
  color: #6b4a1a;
  line-height: 1;
  padding: 0 4px;
}

header.app-header {
  background: var(--surface);
  border-bottom: 1px solid var(--rule);
  padding: 18px 20px 16px;
  position: sticky;
  top: 0;
  z-index: 10;
}
header.app-header .header-inner {
  max-width: 980px;
  margin: 0 auto;
  display: flex;
  align-items: baseline;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 6px;
}
header.app-header h1 { margin: 0; font-size: 1.4rem; letter-spacing: 0.01em; }
header.app-header h1 span.mark { color: var(--brass); }
header.app-header p { margin: 2px 0 0; color: #5b6158; font-size: 0.82rem; font-family: var(--sans); }

nav.tabs {
  display: flex;
  overflow-x: auto;
  background: var(--surface);
  border-bottom: 1px solid var(--rule);
}
nav.tabs .tabs-inner { max-width: 980px; margin: 0 auto; display: flex; }
.tab-btn {
  background: none;
  border: none;
  padding: 11px 16px;
  font-family: var(--sans);
  font-size: 0.86rem;
  font-weight: 600;
  color: #6b7168;
  cursor: pointer;
  white-space: nowrap;
  border-bottom: 2px solid transparent;
  margin-bottom: -1px;
}
.tab-btn:hover { color: var(--ink); }
.tab-btn.active { color: var(--brass-dark); border-bottom-color: var(--brass); }

main { max-width: 980px; margin: 0 auto; padding: 22px 16px 60px; position: relative; }

.tab-section { display: none; }
.tab-section.active { display: block; animation: fade .25s ease; }
@keyframes fade { from { opacity: 0; transform: translateY(3px); } to { opacity: 1; transform: translateY(0); } }

.section-header { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 10px; margin-bottom: 14px; }
.section-header h2 { margin: 0; font-size: 1.2rem; }
h2 { font-size: 1.2rem; margin: 28px 0 4px; }
.tab-section > h2:first-of-type { margin-top: 0; }
.help-text { color: #6b7168; font-size: 0.83rem; margin: 0 0 14px; max-width: 60ch; }

.month-nav {
  display: flex; align-items: center; gap: 8px;
  background: var(--surface); border: 1px solid var(--rule); border-radius: 999px; padding: 4px 6px; width: fit-content;
}
.month-nav button {
  background: var(--paper); border: none; width: 26px; height: 26px; border-radius: 50%;
  cursor: pointer; font-size: 0.95rem; color: var(--ink); font-family: var(--sans);
}
.month-nav button:hover { background: var(--rule); }
.month-nav span { font-weight: 600; font-size: 0.88rem; min-width: 106px; text-align: center; font-family: var(--sans); }

.summary-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px,1fr)); gap: 12px; margin: 18px 0 14px; }
.card { background: var(--surface); border: 1px solid var(--rule); border-radius: var(--radius); padding: 14px 16px; box-shadow: var(--shadow); }
.card-label { font-size: 0.72rem; color: #6b7168; text-transform: uppercase; letter-spacing: .04em; font-weight: 600; }
.card-value { font-size: 1.5rem; margin-top: 6px; }
.card.highlight { border-color: var(--brass); background: linear-gradient(180deg, #fff, #fdfaf4); }
.card.highlight .card-value { border-bottom: 3px double var(--ink); padding-bottom: 7px; display: inline-block; }
.card-value.positive { color: var(--forest); }
.card-value.negative { color: var(--brick); }

.ratio-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px,1fr)); gap: 12px; margin-bottom: 18px; }
.ratio-card { background: var(--surface); border: 1px solid var(--rule); border-radius: var(--radius); padding: 13px 16px; display: flex; align-items: center; justify-content: space-between; }
.ratio-label { font-size: 0.78rem; color: #6b7168; font-weight: 600; }
.ratio-value { font-size: 1.25rem; margin-top: 2px; }
.badge { font-family: var(--sans); font-size: 0.68rem; font-weight: 700; padding: 4px 10px; border-radius: 999px; text-transform: uppercase; letter-spacing: .03em; white-space: nowrap; }
.badge.good { background: var(--forest-bg); color: var(--forest); }
.badge.warn { background: var(--flag-bg); color: var(--flag); }
.badge.bad { background: var(--brick-bg); color: var(--brick); }

.insights { display: flex; flex-direction: column; gap: 7px; margin-bottom: 22px; }
.insight { padding: 10px 14px; border-radius: var(--radius-sm); font-size: 0.84rem; border-left: 3px solid var(--rule); background: var(--surface); }
.insight.good { border-left-color: var(--forest); }
.insight.warn { border-left-color: var(--flag); }
.insight.bad { border-left-color: var(--brick); }
.insight.info { border-left-color: var(--brass); }

.charts-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
.chart-card { background: var(--surface); border: 1px solid var(--rule); border-radius: var(--radius); padding: 16px; }
.chart-card h3 { margin: 0 0 10px; font-size: 1rem; }
.chart-canvas-wrap { position: relative; height: 210px; }
.empty-note { color: #6b7168; font-size: 0.84rem; text-align: center; padding: 34px 10px; }

.inline-form { display: flex; flex-wrap: wrap; gap: 8px; background: var(--surface); border: 1px solid var(--rule); border-radius: var(--radius); padding: 14px; margin-bottom: 18px; align-items: flex-end; }
.inline-form input, .inline-form select { padding: 9px 10px; border: 1px solid var(--rule); border-radius: var(--radius-sm); font-size: 0.87rem; font-family: var(--sans); flex: 1 1 140px; min-width: 0; background: #fff; color: var(--ink); }
.inline-form input:focus, .inline-form select:focus { outline: 2px solid var(--brass); outline-offset: 1px; }
.inline-form label { display: flex; flex-direction: column; font-size: 0.7rem; color: #6b7168; gap: 3px; flex: 1 1 140px; font-weight: 600; }
.inline-form label input, .inline-form label select { width: 100%; }
.loan-form input, .loan-form select { flex: 1 1 170px; }

button { cursor: pointer; }
.inline-form button, .data-actions button { background: var(--brass); color: #fff; border: none; padding: 10px 18px; border-radius: var(--radius-sm); font-weight: 700; font-size: 0.85rem; font-family: var(--sans); }
.inline-form button:hover, .data-actions button:hover { background: var(--brass-dark); }
.inline-form button[type=button] { background: var(--paper); color: var(--ink); border: 1px solid var(--rule); }
.inline-form button[type=button]:hover { background: #e4e8de; }

.table-wrap { overflow-x: auto; border-radius: var(--radius); border: 1px solid var(--rule); }
.data-table { width: 100%; border-collapse: collapse; background: var(--surface); font-size: 0.85rem; min-width: 480px; }
.data-table th, .data-table td { text-align: left; padding: 10px 12px; border-bottom: 1px solid var(--rule); }
.data-table th { background: var(--paper); font-size: 0.72rem; text-transform: uppercase; color: #6b7168; font-weight: 700; letter-spacing: .03em; }
.data-table tr:last-child td { border-bottom: none; }
.data-table td.amt { text-align: right; font-weight: 600; }
.data-table .actions { white-space: nowrap; text-align: right; }
.data-table .actions button { background: none; border: 1px solid var(--rule); border-radius: 6px; padding: 4px 9px; font-size: 0.76rem; margin-left: 4px; font-family: var(--sans); color: var(--ink); }
.data-table .actions button.danger { color: var(--brick); border-color: var(--brick-bg); }
.cat-dot { display: inline-block; width: 8px; height: 8px; border-radius: 50%; margin-right: 6px; }

.unpaid-row td { color: #8e958a; background-color: #fafbf9; }
.status-toggle { cursor: pointer; accent-color: var(--brass); width: 14px !important; height: 14px !important; }
.status-cell { text-align: center; }

.total-pill { display: inline-block; margin-top: 12px; background: var(--surface); border: 1px solid var(--rule); border-radius: 999px; padding: 8px 18px; font-size: 0.85rem; font-weight: 600; }
.total-pill span.num { color: var(--brass-dark); font-weight: 700; }
.pending-text { color: #6b7168; font-size: 0.8rem; margin-left: 8px; font-weight: 400; }

.loan-cards { display: flex; flex-direction: column; gap: 12px; margin-top: 4px; }
.loan-card { background: var(--surface); border: 1px solid var(--rule); border-radius: var(--radius); padding: 14px 16px; }
.loan-card-header { display: flex; justify-content: space-between; align-items: baseline; flex-wrap: wrap; gap: 6px; }
.loan-card-header strong { font-family: var(--serif); font-size: 1.05rem; }
.loan-sub { color: #6b7168; font-size: 0.8rem; margin-top: 2px; }
.loan-actions button { background: none; border: 1px solid var(--rule); border-radius: 6px; padding: 4px 9px; font-size: 0.76rem; margin-left: 4px; font-family: var(--sans); color: var(--ink); }
.loan-actions button.danger { color: var(--brick); }
.loan-stats { display: grid; grid-template-columns: repeat(auto-fit,minmax(125px,1fr)); gap: 10px; margin-top: 12px; }
.loan-stats > div { font-size: 0.76rem; color: #6b7168; font-weight: 600; }
.loan-stats strong { display: block; font-size: 0.94rem; color: var(--ink); margin-top: 2px; font-weight: 700; }
.warn-text { color: var(--flag); }

.settings-row { display: flex; align-items: center; gap: 10px; margin-bottom: 18px; flex-wrap: wrap; }
.settings-row label { font-size: 0.85rem; font-weight: 600; }
.settings-row select { padding: 8px 10px; border-radius: var(--radius-sm); border: 1px solid var(--rule); font-family: var(--sans); }
.data-actions { display: flex; gap: 10px; flex-wrap: wrap; margin-bottom: 16px; }
.data-actions .danger { background: var(--brick); }
.data-actions .danger:hover { background: #8a3128; }
.file-btn { background: var(--paper); border: 1px solid var(--rule); padding: 10px 18px; border-radius: var(--radius-sm); font-weight: 700; font-size: 0.85rem; cursor: pointer; display: inline-block; font-family: var(--sans); }
.file-btn:hover { background: #e4e8de; }

@media (max-width: 720px) { .charts-grid { grid-template-columns: 1fr; } }
@media (max-width: 480px) {
  .inline-form input, .inline-form select, .inline-form label { flex: 1 1 100%; }
  header.app-header h1 { font-size: 1.2rem; }
  .card-value { font-size: 1.25rem; }
}

.checkbox-label {
  flex: 0 0 auto !important;
  flex-direction: row !important;
  align-items: center;
  gap: 6px;
  cursor: pointer;
  user-select: none;
}
.checkbox-label input {
  width: auto !important;
  margin: 0;
  cursor: pointer;
}
.recurring-icon {
  font-size: 0.8rem;
  margin-left: 4px;
  opacity: 0.6;
}
.next-month-badge {
  background: var(--flag-bg);
  color: var(--flag);
  font-size: 0.65rem;
  font-weight: 700;
  padding: 2px 6px;
  border-radius: 4px;
  margin-left: 6px;
  text-transform: uppercase;
  white-space: nowrap;
}
</style>
</head>
<body>

<header class="app-header">
  <div class="header-inner">
    <h1><span class="mark">Ledger</span> — Personal Finance Tracker</h1>
    <p>Everything below is stored only in this browser.</p>
  </div>
</header>

<nav class="tabs">
  <div class="tabs-inner">
    <button class="tab-btn active" data-tab="dashboard">Dashboard</button>
    <button class="tab-btn" data-tab="income">Income</button>
    <button class="tab-btn" data-tab="expenses">Expenses</button>
    <button class="tab-btn" data-tab="loans">Loans</button>
    <button class="tab-btn" data-tab="data">Data</button>
  </div>
</nav>

<main>

  <section id="tab-dashboard" class="tab-section active">
    <div class="section-header">
      <h2>Dashboard</h2>
      <div class="month-nav">
        <button id="dash-prev-month" aria-label="Previous month">‹</button>
        <span id="dash-month-label">—</span>
        <button id="dash-next-month" aria-label="Next month">›</button>
      </div>
    </div>

    <div class="summary-grid">
      <div class="card"><div class="card-label">Net Income</div><div class="card-value num" id="sum-income">₹0.00</div></div>
      <div class="card"><div class="card-label">Paid Expenses</div><div class="card-value num" id="sum-expenses">₹0.00</div></div>
      <div class="card"><div class="card-label">Pending Bills</div><div class="card-value num" id="sum-pending">₹0.00</div></div>
      <div class="card"><div class="card-label">Debt Payments</div><div class="card-value num" id="sum-debt">₹0.00</div></div>
      <div class="card highlight"><div class="card-label">Left to Spend</div><div class="card-value num" id="sum-left">₹0.00</div></div>
    </div>

    <div class="ratio-grid">
      <div class="ratio-card">
        <div><div class="ratio-label">Debt-to-Income</div><div class="ratio-value num" id="dti-value">0%</div></div>
        <div class="badge" id="dti-badge">—</div>
      </div>
      <div class="ratio-card">
        <div><div class="ratio-label">Savings Rate</div><div class="ratio-value num" id="savings-value">0%</div></div>
        <div class="badge" id="savings-badge">—</div>
      </div>
    </div>

    <div id="insights-list" class="insights"></div>

    <div class="charts-grid">
      <div class="chart-card">
        <h3>Spending by Category (Paid)</h3>
        <div class="chart-canvas-wrap"><canvas id="category-chart"></canvas></div>
        <p class="empty-note" id="category-chart-empty" style="display:none">No paid expenses logged for this month yet.</p>
      </div>
      <div class="chart-card">
        <h3>Expenses — Last 6 Months</h3>
        <div class="chart-canvas-wrap"><canvas id="trend-chart"></canvas></div>
        <p class="empty-note" id="trend-chart-empty" style="display:none">Charts need Chart.js to load from the CDN (requires internet).</p>
      </div>
    </div>
  </section>

  <section id="tab-income" class="tab-section">
    <div class="section-header">
      <h2>Income</h2>
      <div class="month-nav">
        <button id="inc-prev-month" aria-label="Previous month">‹</button>
        <span id="inc-month-label">—</span>
        <button id="inc-next-month" aria-label="Next month">›</button>
      </div>
    </div>
    <p class="help-text">Enter the net money you received. If you get paid at the end of the month, check "Use for next month's budget" so the money shows up in the correct month's dashboard.</p>
    
    <form id="income-form" class="inline-form">
      <input type="hidden" id="income-edit-id">
      <input type="date" id="income-date" required>
      <input type="text" id="income-name" placeholder="Source (e.g. Salary, Side Gig)" required>
      <input type="number" id="income-amount" placeholder="Amount" min="0" step="0.01" required>
      
      <label class="checkbox-label" title="App will automatically add this on the 1st of every month.">
        <input type="checkbox" id="income-recurring"> Repeat monthly
      </label>
      <label class="checkbox-label" title="Moves this money into next month's bucket.">
        <input type="checkbox" id="income-next-month"> Use for next month's budget
      </label>

      <button type="submit" id="income-submit-btn">Add income</button>
      <button type="button" id="income-cancel-btn" style="display:none">Cancel</button>
    </form>
    
    <div class="table-wrap">
      <table class="data-table">
        <thead><tr><th>Date</th><th>Source</th><th>Amount</th><th></th></tr></thead>
        <tbody id="income-table-body"></tbody>
      </table>
    </div>
    <p class="empty-note" id="income-empty">No income logged for this month yet.</p>
    <div class="total-pill">Month total: <span class="num" id="income-total">₹0.00</span></div>
  </section>

  <section id="tab-expenses" class="tab-section">
    <div class="section-header">
      <h2>Expenses</h2>
      <div class="month-nav">
        <button id="exp-prev-month" aria-label="Previous month">‹</button>
        <span id="exp-month-label">—</span>
        <button id="exp-next-month" aria-label="Next month">›</button>
      </div>
    </div>
    
    <form id="expense-form" class="inline-form">
      <input type="hidden" id="expense-edit-id">
      <input type="date" id="expense-date" required>
      <select id="expense-category"></select>
      <input type="text" id="expense-desc" placeholder="Description (optional)">
      <input type="number" id="expense-amount" placeholder="Amount" min="0" step="0.01" required>
      
      <label class="checkbox-label" title="App will automatically add this on the same day every month.">
        <input type="checkbox" id="expense-recurring"> Repeat monthly
      </label>
      <label class="checkbox-label" title="Unpaid bills will not deduct from your Left to Spend.">
        <input type="checkbox" id="expense-ispaid" checked> Mark as Paid
      </label>

      <button type="submit" id="expense-submit-btn">Add expense</button>
      <button type="button" id="expense-cancel-btn" style="display:none">Cancel</button>
    </form>

    <div class="table-wrap">
      <table class="data-table">
        <thead><tr><th>Date</th><th>Category</th><th>Description</th><th>Amount</th><th class="status-cell">Paid</th><th></th></tr></thead>
        <tbody id="expense-table-body"></tbody>
      </table>
    </div>
    <p class="empty-note" id="expense-empty">No expenses logged for this month yet.</p>
    
    <div class="total-pill">
      Total Paid: <span class="num" id="expense-total">₹0.00</span>
      <span class="pending-text">(Pending: <span class="num" id="expense-pending">₹0.00</span>)</span>
    </div>
  </section>

  <section id="tab-loans" class="tab-section">
    <h2>Short-Term Loans</h2>
    <p class="help-text">Personal loans, auto loans, credit installments — simplified to track by EMI payments.</p>
    
    <form id="stloan-form" class="inline-form loan-form">
      <input type="hidden" id="stloan-edit-id">
      <input type="text" id="stloan-name" placeholder="Loan name (e.g. Car Loan)" required>
      <input type="number" id="stloan-payment" placeholder="EMI Amount" min="0" step="0.01" required>
      <input type="number" id="stloan-term" placeholder="Total number of EMIs" min="1" step="1" required>
      <input type="number" id="stloan-paid" placeholder="EMIs already paid (default 0)" min="0" step="1">
      <label>Next due date<input type="date" id="stloan-due"></label>
      <button type="submit" id="stloan-submit-btn">Add loan</button>
      <button type="button" id="stloan-cancel-btn" style="display:none">Cancel</button>
    </form>
    
    <div class="loan-cards" id="stloan-list"></div>
    <p class="empty-note" id="stloan-empty">No short-term loans added.</p>
    <div class="total-pill">Total payments this month: <span class="num" id="stloan-total">₹0.00</span></div>

    <h2>Home Loan (Mortgage)</h2>
    <p class="help-text">Your recurring home loan. Taxes/insurance and property value are optional but improve the equity estimate.</p>
    <form id="hloan-form" class="inline-form loan-form">
      <input type="hidden" id="hloan-edit-id">
      <input type="text" id="hloan-name" placeholder="Loan name (e.g. Primary Residence)">
      <input type="text" id="hloan-lender" placeholder="Lender (optional)">
      <input type="number" id="hloan-principal" placeholder="Original loan amount" min="0" step="0.01">
      <input type="number" id="hloan-balance" placeholder="Outstanding balance" min="0" step="0.01">
      <input type="number" id="hloan-rate" placeholder="Interest rate % APR" min="0" step="0.01">
      <input type="number" id="hloan-payment" placeholder="Monthly payment (P&amp;I)" min="0" step="0.01">
      <input type="number" id="hloan-escrow" placeholder="Monthly taxes &amp; insurance (optional)" min="0" step="0.01">
      <label>Start date<input type="date" id="hloan-start"></label>
      <label>Term (years)<input type="number" id="hloan-term" min="1" step="1"></label>
      <label>Next due date<input type="date" id="hloan-due"></label>
      <input type="number" id="hloan-property-value" placeholder="Property value (optional)" min="0" step="0.01">
      <button type="submit" id="hloan-submit-btn">Add home loan</button>
      <button type="button" id="hloan-cancel-btn" style="display:none">Cancel</button>
    </form>
    <div class="loan-cards" id="hloan-list"></div>
    <p class="empty-note" id="hloan-empty">No home loan added.</p>
    <div class="total-pill">Total payment this month: <span class="num" id="hloan-total">₹0.00</span></div>
  </section>

  <section id="tab-data" class="tab-section">
    <h2>Data &amp; Settings</h2>
    <div class="settings-row">
      <label for="currency-select">Currency</label>
      <select id="currency-select">
        <option value="USD">USD ($)</option>
        <option value="EUR">EUR (€)</option>
        <option value="GBP">GBP (£)</option>
        <option value="INR">INR (₹)</option>
        <option value="JPY">JPY (¥)</option>
        <option value="AUD">AUD ($)</option>
        <option value="CAD">CAD ($)</option>
        <option value="SGD">SGD ($)</option>
        <option value="AED">AED</option>
        <option value="ZAR">ZAR (R)</option>
      </select>
    </div>
    
    <div class="data-actions">
      <button id="export-json-btn" type="button">⬇ Export backup (JSON)</button>
      <button id="copy-json-btn" type="button" style="background:#2F5D4E;">📋 Copy Data (JSON)</button>
      <label class="file-btn">⬆ Import backup<input type="file" id="import-input" accept="application/json" style="display:none"></label>
      <button id="export-excel-btn" type="button">⬇ Download Data (Excel)</button>
      <button id="reset-btn" type="button" class="danger">🗑 Reset all data</button>
    </div>
    <p class="help-text">Data lives only in this browser's local storage — it won't sync between devices or browsers. <strong>Note for iOS users:</strong> To use download buttons, open this file directly in Safari instead of a code editor app. Alternatively, use the "Copy Data" button above.</p>
  </section>

</main>

<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.5.0/chart.umd.min.js"></script>

<script>
(function () {
  'use strict';

  var STORAGE_KEY = 'ledgerFinanceTrackerData_v1';
  var CATEGORIES = ['Housing','Utilities','Groceries','Dining Out','Transportation','Healthcare','Insurance','Entertainment','Shopping','Personal Care','Education','Subscriptions','Savings/Investments','Other'];
  var CATEGORY_COLORS = {
    'Housing': '#8C5F2E', 'Utilities': '#5B8AA6', 'Groceries': '#2F5D4E', 'Dining Out': '#B8863B',
    'Transportation': '#5A6B8C', 'Healthcare': '#A83E32', 'Insurance': '#7A5C8C', 'Entertainment': '#B5568C',
    'Shopping': '#C2762E', 'Personal Care': '#3D8C82', 'Education': '#6B5CA5', 'Subscriptions': '#7D9A3A',
    'Savings/Investments': '#3E8F5E', 'Other': '#6b7168'
  };

  var state = null;
  var ui = { selectedMonth: currentMonthKey() };
  var categoryChartInstance = null;
  var trendChartInstance = null;
  var storageAvailable = false;
  var storageWarningShown = false;

  /* ---------- persistence ---------- */
  function testStorage() {
    try {
      var k = '__ledger_probe__';
      localStorage.setItem(k, '1');
      localStorage.removeItem(k);
      return true;
    } catch (e) { return false; }
  }
  function defaultState() {
    return { 
      settings: { currency: 'INR', lastOpenedMonth: currentMonthKey() }, 
      income: [], 
      expenses: [], 
      shortTermLoans: [], 
      homeLoans: [] 
    };
  }
  function loadState() {
    if (!storageAvailable) { state = defaultState(); return; }
    try {
      var raw = localStorage.getItem(STORAGE_KEY);
      if (raw) {
        var parsed = JSON.parse(raw);
        state = {
          settings: parsed.settings || { currency: 'INR', lastOpenedMonth: currentMonthKey() },
          income: Array.isArray(parsed.income) ? parsed.income : [],
          expenses: Array.isArray(parsed.expenses) ? parsed.expenses : [],
          shortTermLoans: Array.isArray(parsed.shortTermLoans) ? parsed.shortTermLoans : [],
          homeLoans: Array.isArray(parsed.homeLoans) ? parsed.homeLoans : []
        };
        
        if (!state.settings.lastOpenedMonth) state.settings.lastOpenedMonth = currentMonthKey();
        
        state.income.forEach(function(i) {
          if (!i.date) i.date = currentMonthKey() + '-01'; 
          if (i.isNextMonth === undefined) i.isNextMonth = false;
        });

      } else {
        state = defaultState();
      }
    } catch (e) {
      console.error('Could not read saved data, starting fresh.', e);
      state = defaultState();
    }
  }
  function saveState() {
    if (!storageAvailable) return;
    try {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    } catch (e) {
      storageAvailable = false;
      warnStorageUnavailable();
    }
  }
  function warnStorageUnavailable() {
    if (storageWarningShown) return;
    storageWarningShown = true;
    var banner = document.createElement('div');
    banner.className = 'storage-banner';
    var msg = document.createElement('span');
    msg.textContent = "This browser is blocking local storage, so nothing will be saved once you leave the page. Everything still works for now \u2014 try opening the saved HTML file directly in a browser, or hosting it on GitHub Pages.";
    var closeBtn = document.createElement('button');
    closeBtn.type = 'button';
    closeBtn.setAttribute('aria-label', 'Dismiss');
    closeBtn.textContent = '\u00D7';
    closeBtn.addEventListener('click', function () { banner.remove(); });
    banner.appendChild(msg);
    banner.appendChild(closeBtn);
    document.body.insertBefore(banner, document.body.firstChild);
  }

  /* ---------- AUTO-DEBIT LOGIC (Loans & Recurring Items) ---------- */
  function processAutoDebits() {
    if (!state) return;
    
    var today = new Date();
    today.setHours(0, 0, 0, 0);
    var updated = false;

    // 1. Process Short-Term Loans
    state.shortTermLoans.forEach(function(l) {
      if (!l.nextDueDate) return;
      var parts = l.nextDueDate.split('-');
      var due = new Date(parts[0], parts[1] - 1, parts[2]);
      
      while (due <= today && parseInt(l.emisPaid || 0) < parseInt(l.totalEmis || 0)) {
        l.emisPaid = (parseInt(l.emisPaid) || 0) + 1;
        due.setMonth(due.getMonth() + 1);
        l.nextDueDate = due.getFullYear() + '-' + String(due.getMonth() + 1).padStart(2, '0') + '-' + String(due.getDate()).padStart(2, '0');
        updated = true;
      }
    });

    // 2. Process Home Loans
    state.homeLoans.forEach(function(l) {
      if (!l.nextDueDate) return;
      var parts = l.nextDueDate.split('-');
      var due = new Date(parts[0], parts[1] - 1, parts[2]);

      while (due <= today && parseFloat(l.outstandingBalance || 0) > 0) {
        var bal = parseFloat(l.outstandingBalance) || 0;
        var pmt = parseFloat(l.monthlyPayment) || 0;
        var rateM = (parseFloat(l.interestRate) || 0) / 100 / 12;
        
        var interest = bal * rateM;
        var principal = pmt - interest;
        
        if (principal > 0) {
          l.outstandingBalance = Math.max(0, bal - principal);
        }
        
        due.setMonth(due.getMonth() + 1);
        l.nextDueDate = due.getFullYear() + '-' + String(due.getMonth() + 1).padStart(2, '0') + '-' + String(due.getDate()).padStart(2, '0');
        updated = true;
      }
    });

    // 3. Process Recurring Expenses & Income (Catch up missed months perfectly keeping exact day)
    var currentMKey = currentMonthKey();
    var lastMKey = state.settings.lastOpenedMonth || currentMKey;
    
    while (lastMKey < currentMKey) {
      var nextMonth = addMonthsToKey(lastMKey, 1);
      var nextParts = nextMonth.split('-');
      var daysInNextMonth = new Date(nextParts[0], nextParts[1], 0).getDate();
      
      // Expenses
      var recurringExpenses = state.expenses.filter(function(e) { 
        return monthKey(e.date) === lastMKey && e.isRecurring; 
      });
      recurringExpenses.forEach(function(r) {
        var newExp = Object.assign({}, r);
        var oldDay = parseInt(r.date.split('-')[2], 10);
        var safeDay = Math.min(oldDay, daysInNextMonth);
        
        newExp.id = generateId();
        newExp.date = nextMonth + '-' + String(safeDay).padStart(2, '0'); 
        newExp.isPaid = false; // Auto-generated bills are UNPAID by default
        state.expenses.push(newExp);
        updated = true;
      });

      // Income
      var recurringIncome = state.income.filter(function(i) { 
        return getEffectiveMonth(i) === lastMKey && i.isRecurring; 
      });
      recurringIncome.forEach(function(r) {
        var newInc = Object.assign({}, r);
        var oldDay = parseInt(r.date.split('-')[2], 10);
        var safeDay = Math.min(oldDay, daysInNextMonth);
        
        newInc.id = generateId();
        newInc.date = nextMonth + '-' + String(safeDay).padStart(2, '0'); 
        state.income.push(newInc);
        updated = true;
      });
      
      lastMKey = nextMonth;
    }
    
    state.settings.lastOpenedMonth = currentMKey;

    if (updated) {
      saveState();
    }
  }

  /* ---------- helpers ---------- */
  function generateId() {
    if (window.crypto && crypto.randomUUID) return crypto.randomUUID();
    return 'id-' + Date.now() + '-' + Math.random().toString(36).slice(2, 9);
  }
  function escapeHtml(str) {
    if (str === null || str === undefined) return '';
    return String(str).replace(/[&<>"']/g, function (c) {
      return { '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;' }[c];
    });
  }
  function formatCurrency(amount) {
    var code = (state.settings && state.settings.currency) || 'INR';
    var n = Number(amount) || 0;
    try {
      return new Intl.NumberFormat(undefined, { style: 'currency', currency: code, maximumFractionDigits: 2 }).format(n);
    } catch (e) {
      return n.toFixed(2) + ' ' + code;
    }
  }
  function todayIso() {
    var d = new Date();
    var local = new Date(d.getTime() - d.getTimezoneOffset() * 60000);
    return local.toISOString().slice(0, 10);
  }
  function monthKey(dateStr) { return (dateStr || '').slice(0, 7); }
  function currentMonthKey() { return todayIso().slice(0, 7); }
  function addMonthsToKey(key, delta) {
    var parts = key.split('-').map(Number);
    var y = parts[0], m = parts[1] + delta;
    while (m > 12) { m -= 12; y++; }
    while (m < 1) { m += 12; y--; }
    return y + '-' + String(m).padStart(2, '0');
  }
  function formatMonthLabel(key) {
    var parts = key.split('-').map(Number);
    var d = new Date(parts[0], parts[1] - 1, 1);
    return d.toLocaleString(undefined, { month: 'long', year: 'numeric' });
  }
  function formatMonthShort(key) {
    var parts = key.split('-').map(Number);
    var d = new Date(parts[0], parts[1] - 1, 1);
    return d.toLocaleString(undefined, { month: 'short', year: '2-digit' });
  }
  function addMonthsToDate(date, n) {
    var d = new Date(date);
    d.setMonth(d.getMonth() + n);
    return d;
  }
  
  function changeMonth(delta) {
    ui.selectedMonth = addMonthsToKey(ui.selectedMonth, delta);
    renderAll();
  }
  
  // Math helper for future/past loan calculations
  function monthDiff(k1, k2) {
    var p1 = k1.split('-').map(Number);
    var p2 = k2.split('-').map(Number);
    return (p2[0] - p1[0]) * 12 + (p2[1] - p1[1]);
  }

  /* ---------- amortization (Home Loans) ---------- */
  function computeRemaining(balance, ratePct, payment) {
    balance = Number(balance) || 0;
    payment = Number(payment) || 0;
    ratePct = Number(ratePct) || 0;
    if (balance <= 0) return { months: 0, payoffDate: null, warning: false };
    if (payment <= 0) return { months: null, payoffDate: null, warning: true };
    var r = ratePct / 100 / 12;
    var n;
    if (r === 0) {
      n = balance / payment;
    } else {
      var interestPortion = r * balance;
      if (payment <= interestPortion) return { months: null, payoffDate: null, warning: true };
      n = -Math.log(1 - (r * balance) / payment) / Math.log(1 + r);
    }
    n = Math.ceil(n);
    return { months: n, payoffDate: addMonthsToDate(new Date(), n), warning: false };
  }
  function remainingLabel(rem) {
    if (rem.warning) return '<span class="warn-text">\u26A0 payment may not cover interest</span>';
    if (rem.months === 0) return 'Paid off';
    var d = rem.payoffDate ? (' \u00B7 payoff ~' + rem.payoffDate.toLocaleDateString(undefined, { month: 'short', year: 'numeric' })) : '';
    return rem.months + ' mo. left' + d;
  }

  /* ---------- calculations ---------- */
  function getEffectiveMonth(incomeObj) {
    var baseMonth = monthKey(incomeObj.date);
    if (incomeObj.isNextMonth) {
      return addMonthsToKey(baseMonth, 1);
    }
    return baseMonth;
  }
  
  function totalMonthlyIncome(mKey) {
    return state.income.filter(function (i) { return getEffectiveMonth(i) === mKey; })
      .reduce(function (sum, i) { return sum + (Number(i.amount) || 0); }, 0);
  }
  
  function monthlyExpenseTotal(mKey, status) {
    return state.expenses.filter(function (e) { 
      var matchesMonth = monthKey(e.date) === mKey;
      var isPaid = e.isPaid !== false;
      return matchesMonth && (status === 'unpaid' ? !isPaid : isPaid);
    }).reduce(function (s, e) { return s + (Number(e.amount) || 0); }, 0);
  }
  
  function expensesByCategory(mKey) {
    var map = {};
    state.expenses.filter(function (e) { 
      return monthKey(e.date) === mKey && e.isPaid !== false; 
    }).forEach(function (e) {
      map[e.category] = (map[e.category] || 0) + (Number(e.amount) || 0);
    });
    return map;
  }
  
  // Time-Traveling Short Term Loan Calculator
  function totalShortTermPayments(mKey) {
    var curr = currentMonthKey();
    var diff = monthDiff(curr, mKey);
    return state.shortTermLoans.reduce(function (s, l) {
      var total = parseInt(l.totalEmis) || 0;
      var paid = parseInt(l.emisPaid) || 0;
      var amt = parseFloat(l.emiAmount) || 0;
      var rem = Math.max(0, total - paid);

      // If looking at a future month where it is paid off
      if (diff >= 0 && diff >= rem) return s;

      // If looking at a past month where it hadn't started yet
      if (diff < 0 && diff < -paid) return s;

      return s + amt;
    }, 0);
  }
  
  // Time-Traveling Home Loan Calculator
  function totalHomeLoanPayments(mKey) {
    var curr = currentMonthKey();
    var diff = monthDiff(curr, mKey);
    return state.homeLoans.reduce(function (s, l) {
      var pmt = (parseFloat(l.monthlyPayment) || 0) + (parseFloat(l.monthlyEscrow) || 0);
      if (pmt <= 0) return s;

      // Future Check
      var rem = computeRemaining(l.outstandingBalance, l.interestRate, l.monthlyPayment);
      if (diff >= 0 && rem.months !== null && diff >= rem.months) return s;

      // Past Check
      if (diff < 0 && l.startDate) {
         if (mKey < monthKey(l.startDate)) return s;
      }

      return s + pmt;
    }, 0);
  }

  /* ---------- dashboard ---------- */
  function renderDashboard() {
    document.getElementById('dash-month-label').textContent = formatMonthLabel(ui.selectedMonth);
    
    var income = totalMonthlyIncome(ui.selectedMonth);
    var expensesPaid = monthlyExpenseTotal(ui.selectedMonth, 'paid');
    var expensesPending = monthlyExpenseTotal(ui.selectedMonth, 'unpaid');
    var debt = totalShortTermPayments(ui.selectedMonth) + totalHomeLoanPayments(ui.selectedMonth);
    
    // The exact math we discussed
    var leftToSpend = income - expensesPaid - expensesPending - debt;

    document.getElementById('sum-income').textContent = formatCurrency(income);
    document.getElementById('sum-expenses').textContent = formatCurrency(expensesPaid);
    document.getElementById('sum-pending').textContent = formatCurrency(expensesPending);
    document.getElementById('sum-debt').textContent = formatCurrency(debt);
    
    var leftEl = document.getElementById('sum-left');
    leftEl.textContent = formatCurrency(leftToSpend);
    leftEl.classList.toggle('negative', leftToSpend < 0);
    leftEl.classList.toggle('positive', leftToSpend >= 0);

    // DTI and Savings uses true Left To Spend
    var dti = income > 0 ? (debt / income * 100) : 0;
    var savings = income > 0 ? (leftToSpend / income * 100) : 0;
    
    document.getElementById('dti-value').textContent = dti.toFixed(1) + '%';
    document.getElementById('savings-value').textContent = savings.toFixed(1) + '%';

    var dtiBadge = document.getElementById('dti-badge');
    if (income === 0) { dtiBadge.textContent = '\u2014'; dtiBadge.className = 'badge'; }
    else if (dti < 36) { dtiBadge.textContent = 'Healthy'; dtiBadge.className = 'badge good'; }
    else if (dti <= 43) { dtiBadge.textContent = 'Caution'; dtiBadge.className = 'badge warn'; }
    else { dtiBadge.textContent = 'High'; dtiBadge.className = 'badge bad'; }

    var savingsBadge = document.getElementById('savings-badge');
    if (income === 0) { savingsBadge.textContent = '\u2014'; savingsBadge.className = 'badge'; }
    else if (savings >= 20) { savingsBadge.textContent = 'Strong'; savingsBadge.className = 'badge good'; }
    else if (savings >= 0) { savingsBadge.textContent = 'Room to grow'; savingsBadge.className = 'badge warn'; }
    else { savingsBadge.textContent = 'Overspending'; savingsBadge.className = 'badge bad'; }

    renderInsights(income, debt, leftToSpend, dti, savings);
    renderCategoryChart(ui.selectedMonth);
    renderTrendChart();
  }

  function renderInsights(income, debt, leftToSpend, dti, savings) {
    var list = document.getElementById('insights-list');
    var items = [];
    if (income === 0) {
      items.push({ type: 'info', text: 'Add an income source to unlock debt-to-income and savings insights.' });
    } else {
      if (leftToSpend < 0) items.push({ type: 'bad', text: 'Warning: Expected bills and debt payments exceed your income this month.' });
      if (dti > 43) items.push({ type: 'bad', text: 'Debt payments are above 43% of income \u2014 a level many lenders treat as high risk.' });
      else if (dti > 36) items.push({ type: 'warn', text: 'Debt payments are above the commonly cited 36% comfort guideline.' });
      if (savings >= 20) items.push({ type: 'good', text: 'Savings rate is at or above the popular 20% guideline.' });
    }
    var catMap = expensesByCategory(ui.selectedMonth);
    var total = Object.keys(catMap).reduce(function (s, k) { return s + catMap[k]; }, 0);
    var topCat = null, topAmt = 0;
    Object.keys(catMap).forEach(function (c) { if (catMap[c] > topAmt) { topAmt = catMap[c]; topCat = c; } });
    if (topCat && total > 0 && topCat !== 'Housing' && (topAmt / total) > 0.3) {
      items.push({ type: 'warn', text: escapeHtml(topCat) + ' is over 30% of this month\'s spending (' + formatCurrency(topAmt) + ').' });
    }
    if (items.length === 0) items.push({ type: 'good', text: 'No red flags this month.' });
    list.innerHTML = items.map(function (i) { return '<div class="insight ' + i.type + '">' + i.text + '</div>'; }).join('');
  }

  function renderCategoryChart(mKey) {
    var canvas = document.getElementById('category-chart');
    var emptyNote = document.getElementById('category-chart-empty');
    if (typeof Chart === 'undefined') {
      canvas.style.display = 'none';
      emptyNote.style.display = 'block';
      emptyNote.textContent = 'Charts need Chart.js to load from the CDN (requires internet).';
      return;
    }
    var map = expensesByCategory(mKey);
    var labels = Object.keys(map);
    if (labels.length === 0) {
      canvas.style.display = 'none';
      emptyNote.style.display = 'block';
      emptyNote.textContent = 'No paid expenses logged for this month yet.';
      if (categoryChartInstance) { categoryChartInstance.destroy(); categoryChartInstance = null; }
      return;
    }
    canvas.style.display = 'block';
    emptyNote.style.display = 'none';
    var data = labels.map(function (l) { return map[l]; });
    var colors = labels.map(function (l) { return CATEGORY_COLORS[l] || '#6b7168'; });
    try {
      if (categoryChartInstance) categoryChartInstance.destroy();
      categoryChartInstance = new Chart(canvas.getContext('2d'), {
        type: 'doughnut',
        data: { labels: labels, datasets: [{ data: data, backgroundColor: colors, borderWidth: 0 }] },
        options: { responsive: true, maintainAspectRatio: false, cutout: '62%', plugins: { legend: { position: 'bottom', labels: { boxWidth: 10, font: { size: 10 } } } } }
      });
    } catch (e) { console.error('Chart render failed', e); }
  }

  function renderTrendChart() {
    var canvas = document.getElementById('trend-chart');
    var emptyNote = document.getElementById('trend-chart-empty');
    if (typeof Chart === 'undefined') {
      canvas.style.display = 'none';
      emptyNote.style.display = 'block';
      return;
    }
    canvas.style.display = 'block';
    emptyNote.style.display = 'none';
    var months = [];
    for (var i = 5; i >= 0; i--) months.push(addMonthsToKey(ui.selectedMonth, -i));
    var totals = months.map(function (m) { return monthlyExpenseTotal(m, 'paid'); });
    var labels = months.map(function (m) { return formatMonthShort(m); });
    try {
      if (trendChartInstance) trendChartInstance.destroy();
      trendChartInstance = new Chart(canvas.getContext('2d'), {
        type: 'bar',
        data: { labels: labels, datasets: [{ label: 'Expenses', data: totals, backgroundColor: '#A9793E', borderRadius: 4, maxBarThickness: 34 }] },
        options: { responsive: true, maintainAspectRatio: false, plugins: { legend: { display: false } }, scales: { y: { beginAtZero: true, ticks: { font: { size: 10 } } }, x: { ticks: { font: { size: 10 } } } } }
      });
    } catch (e) { console.error('Chart render failed', e); }
  }

  /* ---------- income ---------- */
  function renderIncome() {
    document.getElementById('inc-month-label').textContent = formatMonthLabel(ui.selectedMonth);
    var tbody = document.getElementById('income-table-body');
    var empty = document.getElementById('income-empty');
    
    var items = state.income.filter(function (i) { return getEffectiveMonth(i) === ui.selectedMonth; })
      .sort(function (a, b) { return b.date.localeCompare(a.date); });
      
    if (items.length === 0) {
      tbody.innerHTML = '';
      empty.style.display = 'block';
    } else {
      empty.style.display = 'none';
      tbody.innerHTML = items.map(function (i) {
        var recurringIcon = i.isRecurring ? '<span class="recurring-icon" title="Recurring income">🔁</span>' : '';
        var shiftedBadge = i.isNextMonth ? '<span class="next-month-badge">Rolled Over</span>' : '';
        
        return '<tr><td>' + escapeHtml(i.date) + '</td><td>' + escapeHtml(i.name) + shiftedBadge + recurringIcon + '</td><td class="amt">' + formatCurrency(i.amount) + '</td><td class="actions"><button data-action="edit-income" data-id="' + i.id + '">Edit</button><button data-action="delete-income" data-id="' + i.id + '" class="danger">Delete</button></td></tr>';
      }).join('');
    }
    document.getElementById('income-total').textContent = formatCurrency(totalMonthlyIncome(ui.selectedMonth));
  }
  document.getElementById('income-form').addEventListener('submit', function (e) {
    e.preventDefault();
    var id = document.getElementById('income-edit-id').value;
    var item = {
      id: id || generateId(),
      date: document.getElementById('income-date').value,
      name: document.getElementById('income-name').value.trim(),
      amount: parseFloat(document.getElementById('income-amount').value) || 0,
      isRecurring: document.getElementById('income-recurring').checked,
      isNextMonth: document.getElementById('income-next-month').checked
    };
    if (id) {
      var idx = state.income.findIndex(function (x) { return x.id === id; });
      if (idx > -1) state.income[idx] = item;
    } else { state.income.push(item); }
    saveState();
    
    ui.selectedMonth = getEffectiveMonth(item);
    
    resetIncomeForm();
    renderIncome();
    renderDashboard();
  });
  document.getElementById('income-cancel-btn').addEventListener('click', resetIncomeForm);
  function resetIncomeForm() {
    document.getElementById('income-form').reset();
    document.getElementById('income-edit-id').value = '';
    document.getElementById('income-date').value = todayIso();
    document.getElementById('income-recurring').checked = false;
    document.getElementById('income-next-month').checked = false;
    document.getElementById('income-submit-btn').textContent = 'Add income';
    document.getElementById('income-cancel-btn').style.display = 'none';
  }
  function editIncome(id) {
    var item = state.income.find(function (x) { return x.id === id; });
    if (!item) return;
    document.getElementById('income-edit-id').value = item.id;
    document.getElementById('income-date').value = item.date || todayIso();
    document.getElementById('income-name').value = item.name;
    document.getElementById('income-amount').value = item.amount;
    document.getElementById('income-recurring').checked = !!item.isRecurring;
    document.getElementById('income-next-month').checked = !!item.isNextMonth;
    document.getElementById('income-submit-btn').textContent = 'Update income';
    document.getElementById('income-cancel-btn').style.display = 'inline-block';
    document.getElementById('income-name').focus();
  }
  function deleteIncome(id) {
    if (!confirm('Delete this income source? (If it is repeating, deleting it this month will stop it from appearing in future months).')) return;
    state.income = state.income.filter(function (x) { return x.id !== id; });
    saveState();
    renderIncome();
    renderDashboard();
  }
  document.getElementById('income-table-body').addEventListener('click', function (e) {
    var btn = e.target.closest('button[data-action]');
    if (!btn) return;
    var id = btn.dataset.id;
    if (btn.dataset.action === 'edit-income') editIncome(id);
    if (btn.dataset.action === 'delete-income') deleteIncome(id);
  });

  document.getElementById('dash-prev-month').addEventListener('click', function () { changeMonth(-1); });
  document.getElementById('dash-next-month').addEventListener('click', function () { changeMonth(1); });
  document.getElementById('inc-prev-month').addEventListener('click', function () { changeMonth(-1); });
  document.getElementById('inc-next-month').addEventListener('click', function () { changeMonth(1); });
  document.getElementById('exp-prev-month').addEventListener('click', function () { changeMonth(-1); });
  document.getElementById('exp-next-month').addEventListener('click', function () { changeMonth(1); });

  /* ---------- expenses ---------- */
  function populateCategorySelect() {
    var sel = document.getElementById('expense-category');
    sel.innerHTML = CATEGORIES.map(function (c) { return '<option value="' + c + '">' + c + '</option>'; }).join('');
  }
  function renderExpenses() {
    document.getElementById('exp-month-label').textContent = formatMonthLabel(ui.selectedMonth);
    var tbody = document.getElementById('expense-table-body');
    var empty = document.getElementById('expense-empty');
    var items = state.expenses.filter(function (e) { return monthKey(e.date) === ui.selectedMonth; })
      .sort(function (a, b) { return b.date.localeCompare(a.date); });
    
    if (items.length === 0) {
      tbody.innerHTML = '';
      empty.style.display = 'block';
    } else {
      empty.style.display = 'none';
      tbody.innerHTML = items.map(function (e) {
        var color = CATEGORY_COLORS[e.category] || '#6b7168';
        var recurringIcon = e.isRecurring ? '<span class="recurring-icon" title="Recurring expense">🔁</span>' : '';
        var isPaid = e.isPaid !== false;
        var rowClass = isPaid ? '' : 'unpaid-row';
        var checkedAttr = isPaid ? 'checked' : '';
        
        return '<tr class="' + rowClass + '"><td>' + escapeHtml(e.date) + '</td><td><span class="cat-dot" style="background:' + color + '"></span>' + escapeHtml(e.category) + '</td><td>' + escapeHtml(e.description || '') + recurringIcon + '</td><td class="amt">' + formatCurrency(e.amount) + '</td><td class="status-cell"><input type="checkbox" class="status-toggle" data-action="toggle-paid" data-id="' + e.id + '" ' + checkedAttr + ' title="Mark as paid/unpaid"></td><td class="actions"><button data-action="edit-expense" data-id="' + e.id + '">Edit</button><button data-action="delete-expense" data-id="' + e.id + '" class="danger">Delete</button></td></tr>';
      }).join('');
    }
    
    document.getElementById('expense-total').textContent = formatCurrency(monthlyExpenseTotal(ui.selectedMonth, 'paid'));
    document.getElementById('expense-pending').textContent = formatCurrency(monthlyExpenseTotal(ui.selectedMonth, 'unpaid'));
  }
  document.getElementById('expense-form').addEventListener('submit', function (e) {
    e.preventDefault();
    var id = document.getElementById('expense-edit-id').value;
    var item = {
      id: id || generateId(),
      date: document.getElementById('expense-date').value,
      category: document.getElementById('expense-category').value,
      description: document.getElementById('expense-desc').value.trim(),
      amount: parseFloat(document.getElementById('expense-amount').value) || 0,
      isRecurring: document.getElementById('expense-recurring').checked,
      isPaid: document.getElementById('expense-ispaid').checked
    };
    if (id) {
      var idx = state.expenses.findIndex(function (x) { return x.id === id; });
      if (idx > -1) state.expenses[idx] = item;
    } else { state.expenses.push(item); }
    saveState();
    ui.selectedMonth = monthKey(item.date);
    resetExpenseForm();
    renderExpenses();
    renderDashboard();
  });
  document.getElementById('expense-cancel-btn').addEventListener('click', resetExpenseForm);
  function resetExpenseForm() {
    document.getElementById('expense-form').reset();
    document.getElementById('expense-edit-id').value = '';
    document.getElementById('expense-date').value = todayIso();
    document.getElementById('expense-recurring').checked = false;
    document.getElementById('expense-ispaid').checked = true;
    document.getElementById('expense-submit-btn').textContent = 'Add expense';
    document.getElementById('expense-cancel-btn').style.display = 'none';
  }
  function editExpense(id) {
    var item = state.expenses.find(function (x) { return x.id === id; });
    if (!item) return;
    document.getElementById('expense-edit-id').value = item.id;
    document.getElementById('expense-date').value = item.date;
    document.getElementById('expense-category').value = item.category;
    document.getElementById('expense-desc').value = item.description || '';
    document.getElementById('expense-amount').value = item.amount;
    document.getElementById('expense-recurring').checked = !!item.isRecurring;
    document.getElementById('expense-ispaid').checked = item.isPaid !== false;
    document.getElementById('expense-submit-btn').textContent = 'Update expense';
    document.getElementById('expense-cancel-btn').style.display = 'inline-block';
    document.getElementById('expense-amount').focus();
  }
  function deleteExpense(id) {
    if (!confirm('Delete this expense? (If it is repeating, deleting it this month will stop it from appearing in future months).')) return;
    state.expenses = state.expenses.filter(function (x) { return x.id !== id; });
    saveState();
    renderExpenses();
    renderDashboard();
  }
  
  document.getElementById('expense-table-body').addEventListener('click', function (e) {
    var target = e.target;
    if (target.dataset.action === 'toggle-paid') {
      var expId = target.dataset.id;
      var exp = state.expenses.find(function (x) { return x.id === expId; });
      if (exp) {
        exp.isPaid = target.checked;
        saveState();
        renderExpenses();
        renderDashboard();
      }
      return;
    }
    var btn = target.closest('button[data-action]');
    if (!btn) return;
    var id = btn.dataset.id;
    if (btn.dataset.action === 'edit-expense') editExpense(id);
    if (btn.dataset.action === 'delete-expense') deleteExpense(id);
  });

  /* ---------- short-term loans ---------- */
  function renderShortTermLoans() {
    var container = document.getElementById('stloan-list');
    var empty = document.getElementById('stloan-empty');
    if (state.shortTermLoans.length === 0) {
      container.innerHTML = '';
      empty.style.display = 'block';
    } else {
      empty.style.display = 'none';
      container.innerHTML = state.shortTermLoans.map(function (l) {
        
        let totalEmis = parseInt(l.totalEmis) || 0;
        let emisPaid = parseInt(l.emisPaid) || 0;
        let emiAmount = parseFloat(l.emiAmount) || 0;
        
        let remainingEmis = Math.max(0, totalEmis - emisPaid);
        let outstandingBalance = remainingEmis * emiAmount;

        let displayDate = l.nextDueDate ? escapeHtml(l.nextDueDate) : '—';
        let statusText = remainingEmis === 0 ? "Paid off" : remainingEmis + " EMIs left";

        return '<div class="loan-card"><div class="loan-card-header"><strong>' + escapeHtml(l.name) + '</strong><span class="loan-actions"><button data-action="edit-stloan" data-id="' + l.id + '">Edit</button><button data-action="delete-stloan" data-id="' + l.id + '" class="danger">Delete</button></span></div>' +
          '<div class="loan-stats">' + 
          '<div>Outstanding Balance<strong class="num">' + formatCurrency(outstandingBalance) + '</strong></div>' + 
          '<div>EMI Amount<strong class="num">' + formatCurrency(emiAmount) + '</strong></div>' + 
          '<div>EMIs Paid<strong class="num">' + emisPaid + ' / ' + totalEmis + '</strong></div>' + 
          '<div>Status<strong>' + statusText + '</strong></div>' + 
          '<div>Next due<strong>' + displayDate + '</strong></div>' + 
          '</div></div>';
      }).join('');
    }
    document.getElementById('stloan-total').textContent = formatCurrency(totalShortTermPayments(ui.selectedMonth));
  }

  document.getElementById('stloan-form').addEventListener('submit', function (e) {
    e.preventDefault();
    var id = document.getElementById('stloan-edit-id').value;
    
    var item = {
      id: id || generateId(),
      name: document.getElementById('stloan-name').value.trim(),
      emiAmount: parseFloat(document.getElementById('stloan-payment').value) || 0,
      totalEmis: parseInt(document.getElementById('stloan-term').value, 10) || 0,
      emisPaid: parseInt(document.getElementById('stloan-paid').value, 10) || 0,
      nextDueDate: document.getElementById('stloan-due').value
    };
    if (id) {
      var idx = state.shortTermLoans.findIndex(function (x) { return x.id === id; });
      if (idx > -1) state.shortTermLoans[idx] = item;
    } else { state.shortTermLoans.push(item); }
    saveState();
    resetStLoanForm();
    renderShortTermLoans();
    renderDashboard();
  });
  
  document.getElementById('stloan-cancel-btn').addEventListener('click', resetStLoanForm);
  function resetStLoanForm() {
    document.getElementById('stloan-form').reset();
    document.getElementById('stloan-edit-id').value = '';
    document.getElementById('stloan-submit-btn').textContent = 'Add loan';
    document.getElementById('stloan-cancel-btn').style.display = 'none';
  }
  
  function editStLoan(id) {
    var item = state.shortTermLoans.find(function (x) { return x.id === id; });
    if (!item) return;
    document.getElementById('stloan-edit-id').value = item.id;
    document.getElementById('stloan-name').value = item.name;
    document.getElementById('stloan-payment').value = item.emiAmount || '';
    document.getElementById('stloan-term').value = item.totalEmis || '';
    document.getElementById('stloan-paid').value = item.emisPaid || '0';
    document.getElementById('stloan-due').value = item.nextDueDate || '';
    document.getElementById('stloan-submit-btn').textContent = 'Update loan';
    document.getElementById('stloan-cancel-btn').style.display = 'inline-block';
    document.getElementById('stloan-name').focus();
  }
  
  function deleteStLoan(id) {
    if (!confirm('Delete this loan?')) return;
    state.shortTermLoans = state.shortTermLoans.filter(function (x) { return x.id !== id; });
    saveState();
    renderShortTermLoans();
    renderDashboard();
  }
  
  document.getElementById('stloan-list').addEventListener('click', function (e) {
    var btn = e.target.closest('button[data-action]');
    if (!btn) return;
    var id = btn.dataset.id;
    if (btn.dataset.action === 'edit-stloan') editStLoan(id);
    if (btn.dataset.action === 'delete-stloan') deleteStLoan(id);
  });

  /* ---------- home loans ---------- */
  function renderHomeLoans() {
    var container = document.getElementById('hloan-list');
    var empty = document.getElementById('hloan-empty');
    if (state.homeLoans.length === 0) {
      container.innerHTML = '';
      empty.style.display = 'block';
    } else {
      empty.style.display = 'none';
      container.innerHTML = state.homeLoans.map(function (l) {
        var rem = computeRemaining(l.outstandingBalance, l.interestRate, l.monthlyPayment);
        var totalMonthly = (Number(l.monthlyPayment) || 0) + (Number(l.monthlyEscrow) || 0);
        var equityLine = '';
        if (l.propertyValue) {
          var equity = Number(l.propertyValue) - Number(l.outstandingBalance || 0);
          var ltv = Number(l.outstandingBalance || 0) / Number(l.propertyValue) * 100;
          equityLine = '<div>Est. equity<strong class="num">' + formatCurrency(equity) + ' (LTV ' + ltv.toFixed(0) + '%)</strong></div>';
        }
        return '<div class="loan-card"><div class="loan-card-header"><strong>' + escapeHtml(l.name) + '</strong><span class="loan-actions"><button data-action="edit-hloan" data-id="' + l.id + '">Edit</button><button data-action="delete-hloan" data-id="' + l.id + '" class="danger">Delete</button></span></div>' +
          (l.lender ? '<div class="loan-sub">' + escapeHtml(l.lender) + '</div>' : '') +
          '<div class="loan-stats"><div>Balance<strong class="num">' + formatCurrency(l.outstandingBalance) + '</strong></div><div>Payment (P&amp;I)<strong class="num">' + formatCurrency(l.monthlyPayment) + '</strong></div>' +
          (l.monthlyEscrow ? '<div>Taxes &amp; insurance<strong class="num">' + formatCurrency(l.monthlyEscrow) + '</strong></div>' : '') +
          '<div>Total monthly<strong class="num">' + formatCurrency(totalMonthly) + '</strong></div><div>Rate<strong class="num">' + (Number(l.interestRate) || 0).toFixed(2) + '%</strong></div><div>Remaining<strong>' + remainingLabel(rem) + '</strong></div><div>Next due<strong>' + (l.nextDueDate ? escapeHtml(l.nextDueDate) : '\u2014') + '</strong></div>' + equityLine + '</div></div>';
      }).join('');
    }
    document.getElementById('hloan-total').textContent = formatCurrency(totalHomeLoanPayments(ui.selectedMonth));
  }
  document.getElementById('hloan-form').addEventListener('submit', function (e) {
    e.preventDefault();
    var id = document.getElementById('hloan-edit-id').value;
    var termYearsVal = parseFloat(document.getElementById('hloan-term').value);
    
    var loanName = document.getElementById('hloan-name').value.trim() || 'Unnamed Loan';

    var item = {
      id: id || generateId(),
      name: loanName,
      lender: document.getElementById('hloan-lender').value.trim(),
      principal: parseFloat(document.getElementById('hloan-principal').value) || 0,
      outstandingBalance: parseFloat(document.getElementById('hloan-balance').value) || 0,
      interestRate: parseFloat(document.getElementById('hloan-rate').value) || 0,
      monthlyPayment: parseFloat(document.getElementById('hloan-payment').value) || 0,
      monthlyEscrow: parseFloat(document.getElementById('hloan-escrow').value) || 0,
      startDate: document.getElementById('hloan-start').value,
      termMonths: termYearsVal ? Math.round(termYearsVal * 12) : null,
      nextDueDate: document.getElementById('hloan-due').value,
      propertyValue: parseFloat(document.getElementById('hloan-property-value').value) || 0
    };
    if (id) {
      var idx = state.homeLoans.findIndex(function (x) { return x.id === id; });
      if (idx > -1) state.homeLoans[idx] = item;
    } else { state.homeLoans.push(item); }
    saveState();
    resetHLoanForm();
    renderHomeLoans();
    renderDashboard();
  });
  document.getElementById('hloan-cancel-btn').addEventListener('click', resetHLoanForm);
  function resetHLoanForm() {
    document.getElementById('hloan-form').reset();
    document.getElementById('hloan-edit-id').value = '';
    document.getElementById('hloan-submit-btn').textContent = 'Add home loan';
    document.getElementById('hloan-cancel-btn').style.display = 'none';
  }
  function editHLoan(id) {
    var item = state.homeLoans.find(function (x) { return x.id === id; });
    if (!item) return;
    document.getElementById('hloan-edit-id').value = item.id;
    document.getElementById('hloan-name').value = item.name === 'Unnamed Loan' ? '' : item.name;
    document.getElementById('hloan-lender').value = item.lender || '';
    document.getElementById('hloan-principal').value = item.principal || '';
    document.getElementById('hloan-balance').value = item.outstandingBalance || '';
    document.getElementById('hloan-rate').value = item.interestRate || '';
    document.getElementById('hloan-payment').value = item.monthlyPayment || '';
    document.getElementById('hloan-escrow').value = item.monthlyEscrow || '';
    document.getElementById('hloan-start').value = item.startDate || '';
    document.getElementById('hloan-term').value = item.termMonths ? (item.termMonths / 12) : '';
    document.getElementById('hloan-due').value = item.nextDueDate || '';
    document.getElementById('hloan-property-value').value = item.propertyValue || '';
    document.getElementById('hloan-submit-btn').textContent = 'Update home loan';
    document.getElementById('hloan-cancel-btn').style.display = 'inline-block';
    document.getElementById('hloan-name').focus();
  }
  function deleteHLoan(id) {
    if (!confirm('Delete this home loan?')) return;
    state.homeLoans = state.homeLoans.filter(function (x) { return x.id !== id; });
    saveState();
    renderHomeLoans();
    renderDashboard();
  }
  document.getElementById('hloan-list').addEventListener('click', function (e) {
    var btn = e.target.closest('button[data-action]');
    if (!btn) return;
    var id = btn.dataset.id;
    if (btn.dataset.action === 'edit-hloan') editHLoan(id);
    if (btn.dataset.action === 'delete-hloan') deleteHLoan(id);
  });

  /* ---------- data tab ---------- */
  document.getElementById('currency-select').addEventListener('change', function () {
    state.settings.currency = this.value;
    saveState();
    renderAll();
  });
  
  document.getElementById('export-json-btn').addEventListener('click', function () {
    var blob = new Blob([JSON.stringify(state, null, 2)], { type: 'application/json' });
    var url = URL.createObjectURL(blob);
    var a = document.createElement('a');
    a.href = url;
    a.download = 'finance-tracker-backup-' + todayIso() + '.json';
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
  });
  
  document.getElementById('copy-json-btn').addEventListener('click', function () {
    var dataStr = JSON.stringify(state, null, 2);
    if (navigator.clipboard && window.isSecureContext) {
      navigator.clipboard.writeText(dataStr).then(function() {
        alert("Data safely copied to clipboard! You can paste it into a blank text file to save it.");
      }).catch(function(err) {
        alert("Failed to copy automatically. Please try again or open in Safari.");
      });
    } else {
      var textArea = document.createElement("textarea");
      textArea.value = dataStr;
      textArea.style.position = "fixed";
      document.body.appendChild(textArea);
      textArea.focus();
      textArea.select();
      try {
        document.execCommand('copy');
        alert("Data safely copied to clipboard! You can paste it into a blank text file to save it.");
      } catch (err) {
        alert("Copy failed.");
      }
      document.body.removeChild(textArea);
    }
  });
  
  document.getElementById('export-excel-btn').addEventListener('click', function () {
    if (typeof XLSX === 'undefined') {
      alert('Excel export requires an internet connection to load the necessary library.');
      return;
    }
    var wb = XLSX.utils.book_new();

    var incomeData = state.income.map(function(i) {
      return { Date: i.date, Source: i.name, Amount: i.amount, Recurring: !!i.isRecurring, RolledOverToNextMonth: !!i.isNextMonth };
    });
    var expensesData = state.expenses.map(function(e) {
      return { Date: e.date, Category: e.category, Description: e.description, Amount: e.amount, Paid: e.isPaid !== false };
    });
    var stLoansData = state.shortTermLoans.map(function(l) {
      return { Name: l.name, 'EMI Amount': l.emiAmount, 'Total EMIs': l.totalEmis, 'EMIs Paid': l.emisPaid, 'Next Due Date': l.nextDueDate };
    });
    var homeLoansData = state.homeLoans.map(function(l) {
      return { Name: l.name, Lender: l.lender, Principal: l.principal, Balance: l.outstandingBalance, 'Interest Rate (%)': l.interestRate, 'Monthly P&I': l.monthlyPayment, 'Monthly Escrow': l.monthlyEscrow, 'Property Value': l.propertyValue };
    });

    var wsIncome = XLSX.utils.json_to_sheet(incomeData.length ? incomeData : [{ Message: "No income recorded" }]);
    var wsExpenses = XLSX.utils.json_to_sheet(expensesData.length ? expensesData : [{ Message: "No expenses recorded" }]);
    var wsStLoans = XLSX.utils.json_to_sheet(stLoansData.length ? stLoansData : [{ Message: "No short term loans recorded" }]);
    var wsHomeLoans = XLSX.utils.json_to_sheet(homeLoansData.length ? homeLoansData : [{ Message: "No home loans recorded" }]);

    XLSX.utils.book_append_sheet(wb, wsIncome, "Income");
    XLSX.utils.book_append_sheet(wb, wsExpenses, "Expenses");
    XLSX.utils.book_append_sheet(wb, wsStLoans, "Short Term Loans");
    XLSX.utils.book_append_sheet(wb, wsHomeLoans, "Home Loans");

    var fileName = 'Ledger_Finance_Data_' + todayIso() + '.xlsx';
    XLSX.writeFile(wb, fileName);
  });

  document.getElementById('import-input').addEventListener('change', function (e) {
    var file = e.target.files[0];
    if (!file) return;
    var reader = new FileReader();
    reader.onload = function (evt) {
      try {
        var parsed = JSON.parse(evt.target.result);
        if (!parsed || typeof parsed !== 'object') throw new Error('Invalid file');
        if (!confirm('This will replace your current data with the imported backup. Continue?')) { e.target.value = ''; return; }
        state = {
          settings: parsed.settings || { currency: 'INR', lastOpenedMonth: currentMonthKey() },
          income: Array.isArray(parsed.income) ? parsed.income : [],
          expenses: Array.isArray(parsed.expenses) ? parsed.expenses : [],
          shortTermLoans: Array.isArray(parsed.shortTermLoans) ? parsed.shortTermLoans : [],
          homeLoans: Array.isArray(parsed.homeLoans) ? parsed.homeLoans : []
        };
        if (!state.settings.lastOpenedMonth) state.settings.lastOpenedMonth = currentMonthKey();
        
        state.income.forEach(function(i) {
          if (!i.date) i.date = currentMonthKey() + '-01'; 
        });

        saveState();
        document.getElementById('currency-select').value = state.settings.currency;
        renderAll();
        alert('Data imported successfully.');
      } catch (err) {
        alert('Could not import this file \u2014 make sure it is a valid backup JSON.');
      }
      e.target.value = '';
    };
    reader.readAsText(file);
  });

  document.getElementById('reset-btn').addEventListener('click', function () {
    if (!confirm('This will permanently delete all data in this browser. This cannot be undone. Continue?')) return;
    state = defaultState();
    saveState();
    document.getElementById('currency-select').value = state.settings.currency;
    renderAll();
  });

  /* ---------- tabs ---------- */
  var tabBtns = document.querySelectorAll('.tab-btn');
  tabBtns.forEach(function (btn) {
    btn.addEventListener('click', function () {
      tabBtns.forEach(function (b) { b.classList.remove('active'); });
      document.querySelectorAll('.tab-section').forEach(function (s) { s.classList.remove('active'); });
      btn.classList.add('active');
      document.getElementById('tab-' + btn.dataset.tab).classList.add('active');
      renderAll();
    });
  });

  /* ---------- init ---------- */
  function renderAll() {
    renderDashboard();
    renderIncome();
    renderExpenses();
    renderShortTermLoans();
    renderHomeLoans();
  }
  function init() {
    storageAvailable = testStorage();
    loadState();
    if (!storageAvailable) warnStorageUnavailable();
    
    // Process any overdue automated debits FIRST before rendering
    processAutoDebits();
    
    populateCategorySelect();
    document.getElementById('currency-select').value = state.settings.currency;
    document.getElementById('income-date').value = todayIso();
    document.getElementById('expense-date').value = todayIso();
    renderAll();
  }
  init();
})();
</script>
</body>
</html>