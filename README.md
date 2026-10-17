
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TradeFlow | Realistic Trading UI</title>
  <!-- Font Awesome for icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    /* GLOBAL RESET & TYPOGRAPHY */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    }

    body {
      background: #0b0e14;
      display: flex;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      padding: 16px;
    }

    /* MAIN DASHBOARD CONTAINER – GLASSMORPHIC / DARK THEME */
    .dashboard {
      max-width: 1440px;
      width: 100%;
      background: #13161f;
      border-radius: 32px;
      box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), inset 0 1px 1px rgba(255, 255, 255, 0.05);
      padding: 24px;
      display: flex;
      flex-direction: column;
      gap: 24px;
      border: 1px solid #2a2f3a;
      transition: all 0.2s ease;
    }

    /* HEADER / TOP BAR */
    .top-bar {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      justify-content: space-between;
      gap: 16px;
    }

    .logo-area {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .logo-icon {
      width: 36px;
      height: 36px;
      background: linear-gradient(135deg, #3b82f6, #8b5cf6);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 20px;
      color: white;
      box-shadow: 0 6px 14px rgba(59, 130, 246, 0.3);
    }

    .logo-text {
      font-size: 22px;
      font-weight: 700;
      color: #ffffff;
      letter-spacing: -0.5px;
    }

    .logo-text span {
      color: #3b82f6;
    }

    .search-bar {
      display: flex;
      align-items: center;
      background: #1e222d;
      border-radius: 40px;
      padding: 8px 18px;
      gap: 10px;
      border: 1px solid #2f3542;
      flex: 1;
      max-width: 400px;
      transition: all 0.2s;
    }

    .search-bar i {
      color: #7a8499;
      font-size: 16px;
    }

    .search-bar input {
      background: transparent;
      border: none;
      outline: none;
      color: #eef2ff;
      font-size: 14px;
      width: 100%;
      font-weight: 400;
    }

    .search-bar input::placeholder {
      color: #6b7280;
    }

    .user-actions {
      display: flex;
      align-items: center;
      gap: 22px;
    }

    .icon-btn {
      background: #1e222d;
      border: 1px solid #2a2f3a;
      color: #b0b8c8;
      width: 42px;
      height: 42px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 18px;
      cursor: pointer;
      transition: all 0.15s;
      position: relative;
    }

    .icon-btn:hover {
      background: #2a2f3a;
      color: white;
      border-color: #3b82f6;
    }

    .badge {
      position: absolute;
      top: -2px;
      right: -2px;
      background: #ef4444;
      color: white;
      font-size: 10px;
      font-weight: 700;
      width: 18px;
      height: 18px;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 2px solid #13161f;
    }

    .user-profile {
      display: flex;
      align-items: center;
      gap: 12px;
      background: #1e222d;
      padding: 6px 12px 6px 6px;
      border-radius: 40px;
      border: 1px solid #2a2f3a;
      cursor: pointer;
      transition: all 0.15s;
    }

    .user-profile:hover {
      border-color: #3b82f6;
    }

    .avatar {
      width: 36px;
      height: 36px;
      background: linear-gradient(145deg, #2d3748, #1a202c);
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 600;
      color: #cbd5e1;
      border: 2px solid #3b82f6;
      font-size: 15px;
    }

    .user-info h4 {
      font-size: 14px;
      font-weight: 600;
      color: #f1f5f9;
    }

    .user-info p {
      font-size: 11px;
      color: #7e8a9a;
    }

    /* MAIN GRID LAYOUT */
    .main-grid {
      display: grid;
      grid-template-columns: 2.2fr 1fr;
      gap: 24px;
    }

    /* LEFT PANEL (CHART + ORDERS) */
    .left-panel {
      display: flex;
      flex-direction: column;
      gap: 24px;
    }

    /* CARD STYLING */
    .card {
      background: #1a1e28;
      border-radius: 24px;
      padding: 20px;
      border: 1px solid #2a2f3a;
      box-shadow: 0 8px 20px -8px rgba(0, 0, 0, 0.5);
      transition: all 0.2s;
    }

    .card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 16px;
    }

    .card-header h3 {
      font-size: 16px;
      font-weight: 600;
      color: #e2e8f0;
      letter-spacing: -0.2px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .card-header h3 i {
      color: #3b82f6;
      font-size: 14px;
    }

    .time-filter {
      display: flex;
      gap: 6px;
      background: #12161f;
      padding: 4px;
      border-radius: 12px;
    }

    .time-filter button {
      background: transparent;
      border: none;
      color: #8b95a9;
      font-size: 12px;
      font-weight: 600;
      padding: 6px 12px;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.15s;
    }

    .time-filter button.active {
      background: #2a2f3a;
      color: #ffffff;
    }

    .time-filter button:hover:not(.active) {
      color: #cbd5e1;
    }

    /* CHART CONTAINER */
    .chart-container {
      width: 100%;
      height: 200px;
      position: relative;
      margin-bottom: 8px;
    }

    canvas {
      display: block;
      width: 100% !important;
      height: 200px !important;
      border-radius: 12px;
    }

    /* BALANCE & PNL ROW */
    .balance-row {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 12px;
      padding-top: 12px;
      border-top: 1px solid #2a2f3a;
    }

    .balance h2 {
      font-size: 26px;
      font-weight: 700;
      color: white;
      letter-spacing: -1px;
    }

    .balance p {
      font-size: 13px;
      color: #8b95a9;
      margin-top: 2px;
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .balance p i {
      color: #22c55e;
      font-size: 12px;
    }

    .pnl {
      text-align: right;
    }

    .pnl .value {
      font-size: 22px;
      font-weight: 700;
      color: #22c55e;
    }

    .pnl .label {
      font-size: 12px;
      color: #8b95a9;
      margin-top: 4px;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 4px;
    }

    /* ORDERS TABLE SECTION */
    .orders-section .card-header {
      margin-bottom: 12px;
    }

    .orders-tabs {
      display: flex;
      gap: 16px;
    }

    .orders-tabs span {
      font-size: 13px;
      font-weight: 500;
      color: #7e8a9a;
      cursor: pointer;
      padding-bottom: 4px;
      border-bottom: 2px solid transparent;
      transition: all 0.15s;
    }

    .orders-tabs span.active {
      color: #ffffff;
      border-bottom-color: #3b82f6;
    }

    .orders-tabs span:hover:not(.active) {
      color: #b0c0d0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 13px;
    }

    th {
      text-align: left;
      padding: 10px 0 6px 0;
      color: #6f7a8c;
      font-weight: 500;
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    td {
      padding: 10px 0;
      border-bottom: 1px solid #242a36;
      color: #d1d9e6;
      font-weight: 500;
    }

    tr:last-child td {
      border-bottom: none;
    }

    .pair {
      font-weight: 600;
      color: #ffffff;
    }

    .buy {
      color: #22c55e;
      font-weight: 600;
    }

    .sell {
      color: #ef4444;
      font-weight: 600;
    }

    .status {
      font-size: 11px;
      background: #1e3a2e;
      color: #22c55e;
      padding: 4px 10px;
      border-radius: 20px;
      font-weight: 600;
      display: inline-block;
    }

    .status.pending {
      background: #3a2e1e;
      color: #f59e0b;
    }

    /* RIGHT PANEL (ORDER FORM + WATCHLIST) */
    .right-panel {
      display: flex;
      flex-direction: column;
      gap: 24px;
    }

    /* ORDER FORM CARD */
    .order-form .tabs {
      display: flex;
      background: #12161f;
      border-radius: 14px;
      padding: 5px;
      margin-bottom: 20px;
    }

    .order-form .tabs button {
      flex: 1;
      background: transparent;
      border: none;
      color: #8b95a9;
      font-weight: 600;
      font-size: 14px;
      padding: 10px 0;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.2s;
    }

    .order-form .tabs button.active {
      background: #2a2f3a;
      color: #ffffff;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
    }

    .order-form .tabs button.buy-tab.active {
      background: #22c55e;
      color: #0b0e14;
    }

    .order-form .tabs button.sell-tab.active {
      background: #ef4444;
      color: white;
    }

    .input-group {
      margin-bottom: 18px;
    }

    .input-group label {
      display: block;
      font-size: 12px;
      font-weight: 500;
      color: #8b95a9;
      margin-bottom: 6px;
      letter-spacing: 0.3px;
    }

    .input-wrapper {
      display: flex;
      align-items: center;
      background: #12161f;
      border-radius: 14px;
      padding: 4px 16px;
      border: 1px solid #2a2f3a;
      transition: all 0.2s;
    }

    .input-wrapper:focus-within {
      border-color: #3b82f6;
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2);
    }

    .input-wrapper i {
      color: #6b7280;
      font-size: 14px;
    }

    .input-wrapper input {
      background: transparent;
      border: none;
      outline: none;
      padding: 14px 10px;
      color: #ffffff;
      font-size: 15px;
      font-weight: 500;
      width: 100%;
    }

    .input-wrapper input::placeholder {
      color: #4b5563;
      font-weight: 400;
    }

    .input-wrapper .currency {
      color: #8b95a9;
      font-weight: 600;
      font-size: 13px;
    }

    .percentage-buttons {
      display: flex;
      gap: 8px;
      margin-top: 8px;
    }

    .percentage-buttons button {
      flex: 1;
      background: #12161f;
      border: 1px solid #2a2f3a;
      color: #b0b8c8;
      font-size: 12px;
      font-weight: 500;
      padding: 8px 0;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.15s;
    }

    .percentage-buttons button:hover {
      background: #2a2f3a;
      color: white;
      border-color: #3b82f6;
    }

    .action-btn {
      width: 100%;
      background: linear-gradient(135deg, #3b82f6, #2563eb);
      border: none;
      border-radius: 14px;
      padding: 16px;
      color: white;
      font-weight: 700;
      font-size: 16px;
      letter-spacing: 0.3px;
      cursor: pointer;
      transition: all 0.2s;
      margin-top: 8px;
      box-shadow: 0 8px 18px -6px rgba(59, 130, 246, 0.4);
    }

    .action-btn:hover {
      background: linear-gradient(135deg, #2563eb, #1d4ed8);
      transform: translateY(-1px);
      box-shadow: 0 12px 22px -8px rgba(59, 130, 246, 0.5);
    }

    .action-btn.sell-btn {
      background: linear-gradient(135deg, #ef4444, #dc2626);
      box-shadow: 0 8px 18px -6px rgba(239, 68, 68, 0.4);
    }

    .action-btn.sell-btn:hover {
      background: linear-gradient(135deg, #dc2626, #b91c1c);
      box-shadow: 0 12px 22px -8px rgba(239, 68, 68, 0.5);
    }

    /* WATCHLIST CARD */
    .watchlist-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px 0;
      border-bottom: 1px solid #242a36;
    }

    .watchlist-item:last-child {
      border-bottom: none;
    }

    .watchlist-left {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .coin-icon {
      width: 34px;
      height: 34px;
      background: #12161f;
      border-radius: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-size: 14px;
      color: #f0b90b;
    }

    .coin-icon.eth {
      color: #627eea;
    }

    .coin-icon.sol {
      color: #14f195;
    }

    .coin-icon.xrp {
      color: #00a5e0;
    }

    .coin-info h4 {
      font-size: 14px;
      font-weight: 600;
      color: #ffffff;
    }

    .coin-info p {
      font-size: 11px;
      color: #7e8a9a;
      margin-top: 2px;
    }

    .coin-price {
      text-align: right;
    }

    .coin-price .price {
      font-size: 14px;
      font-weight: 600;
      color: #ffffff;
    }

    .coin-price .change {
      font-size: 12px;
      font-weight: 600;
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 3px;
      margin-top: 2px;
    }

    .change.up {
      color: #22c55e;
    }

    .change.down {
      color: #ef4444;
    }

    /* RESPONSIVENESS */
    @media (max-width: 1100px) {
      .main-grid {
        grid-template-columns: 1fr;
      }
      .right-panel {
        display: grid;
        grid-template-columns: 1fr 1fr;
      }
    }

    @media (max-width: 700px) {
      .right-panel {
        grid-template-columns: 1fr;
      }
      .dashboard {
        padding: 16px;
      }
      .top-bar {
        flex-direction: column;
        align-items: stretch;
      }
      .search-bar {
        max-width: none;
      }
      .user-actions {
        justify-content: space-between;
      }
      .balance-row {
        flex-direction: column;
        align-items: flex-start;
        gap: 12px;
      }
      .pnl {
        text-align: left;
      }
    }

    /* SCROLLBAR (optional) */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #1a1e28;
    }
    ::-webkit-scrollbar-thumb {
      background: #3b4252;
      border-radius: 10px;
    }
  </style>
</head>
<body>

<div class="dashboard">
  <!-- TOP BAR -->
  <header class="top-bar">
    <div class="logo-area">
      <div class="logo-icon"><i class="fas fa-chart-line"></i></div>
      <div class="logo-text">Trade<span>Flow</span></div>
    </div>

    <div class="search-bar">
      <i class="fas fa-search"></i>
      <input type="text" placeholder="Search markets, pairs, or assets..." id="searchInput">
    </div>

    <div class="user-actions">
      <button class="icon-btn" id="notificationBtn">
        <i class="fas fa-bell"></i>
        <span class="badge">3</span>
      </button>
      <div class="user-profile" id="userProfile">
        <div class="avatar">JD</div>
        <div class="user-info">
          <h4>John Doe</h4>
          <p>Pro Account</p>
        </div>
      </div>
    </div>
  </header>

  <!-- MAIN GRID -->
  <div class="main-grid">
    <!-- LEFT PANEL -->
    <div class="left-panel">
      <!-- BALANCE & CHART CARD -->
      <div class="card">
        <div class="card-header">
          <h3><i class="fas fa-wallet"></i> Portfolio Overview</h3>
          <div class="time-filter" id="timeFilter">
            <button class="active" data-time="1D">1D</button>
            <button data-time="1W">1W</button>
            <button data-time="1M">1M</button>
            <button data-time="1Y">1Y</button>
          </div>
        </div>

        <div class="balance-row">
          <div class="balance">
            <h2 id="balanceAmount">$48,620.50</h2>
            <p><i class="fas fa-arrow-up"></i> +$2,345.20 (5.1%) today</p>
          </div>
          <div class="pnl">
            <div class="value" id="pnlValue">+$1,283.40</div>
            <div class="label">Unrealized PnL <i class="fas fa-chevron-up" style="color:#22c55e;"></i></div>
          </div>
        </div>

        <div class="chart-container">
          <canvas id="tradingChart"></canvas>
        </div>
      </div>

      <!-- RECENT ORDERS CARD -->
      <div class="card orders-section">
        <div class="card-header">
          <h3><i class="fas fa-history"></i> Recent Orders</h3>
          <div class="orders-tabs" id="orderTabs">
            <span class="active" data-tab="open">Open</span>
            <span data-tab="filled">Filled</span>
            <span data-tab="all">All</span>
          </div>
        </div>

        <table>
          <thead>
            <tr>
              <th>Pair</th>
              <th>Type</th>
              <th>Price</th>
              <th>Amount</th>
              <th>Status</th>
            </tr>
          </thead>
          <tbody id="ordersBody">
            <tr>
              <td class="pair">BTC/USDT</td>
              <td class="buy">Buy</td>
              <td>$63,420.50</td>
              <td>0.25 BTC</td>
              <td><span class="status">Filled</span></td>
            </tr>
            <tr>
              <td class="pair">ETH/USDT</td>
              <td class="sell">Sell</td>
              <td>$3,125.20</td>
              <td>4.2 ETH</td>
              <td><span class="status pending">Pending</span></td>
            </tr>
            <tr>
              <td class="pair">SOL/USDT</td>
              <td class="buy">Buy</td>
              <td>$142.85</td>
              <td>18 SOL</td>
              <td><span class="status">Filled</span></td>
            </tr>
            <tr>
              <td class="pair">XRP/USDT</td>
              <td class="sell">Sell</td>
              <td>$0.6120</td>
              <td>1,500 XRP</td>
              <td><span class="status">Filled</span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>

    <!-- RIGHT PANEL -->
    <div class="right-panel">
      <!-- ORDER FORM CARD -->
      <div class="card order-form">
        <div class="card-header">
          <h3><i class="fas fa-exchange-alt"></i> Place Order</h3>
        </div>

        <div class="tabs" id="orderTypeTabs">
          <button class="buy-tab active" data-type="buy">Buy</button>
          <button class="sell-tab" data-type="sell">Sell</button>
        </div>

        <div class="input-group">
          <label>Price (USDT)</label>
          <div class="input-wrapper">
            <i class="fas fa-dollar-sign"></i>
            <input type="number" id="priceInput" value="63420.50" step="0.01">
            <span class="currency">USDT</span>
          </div>
        </div>

        <div class="input-group">
          <label>Amount (BTC)</label>
          <div class="input-wrapper">
            <i class="fab fa-bitcoin"></i>
            <input type="number" id="amountInput" value="0.25" step="0.001">
            <span class="currency">BTC</span>
          </div>
        </div>

        <div class="percentage-buttons" id="percentageButtons">
          <button data-percent="25">25%</button>
          <button data-percent="50">50%</button>
          <button data-percent="75">75%</button>
          <button data-percent="100">100%</button>
        </div>

        <button class="action-btn" id="actionButton">Buy BTC</button>
      </div>

      <!-- WATCHLIST CARD -->
      <div class="card">
        <div class="card-header">
          <h3><i class="fas fa-star"></i> Watchlist</h3>
          <i class="fas fa-ellipsis-h" style="color:#6f7a8c; cursor:pointer;"></i>
        </div>

        <div class="watchlist-item">
          <div class="watchlist-left">
            <div class="coin-icon">₿</div>
            <div class="coin-info">
              <h4>Bitcoin</h4>
              <p>BTC/USDT</p>
            </div>
          </div>
          <div class="coin-price">
            <div class="price">$63,420.50</div>
            <div class="change up"><i class="fas fa-arrow-up"></i> 2.34%</div>
          </div>
        </div>

        <div class="watc
