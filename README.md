# Gamedukc
Quay vong quay
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Vòng Đu Quay Hoàng Gia 🎡</title>
  <style>
    :root {
      --bg-dark: #0f172a;
      --bg-card: #1e293b;
      --gold: #f59e0b;
      --gold-light: #fde047;
      --text-main: #f8fafc;
      --text-muted: #94a3b8;
      --danger: #ef4444;
      --success: #10b981;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
    }

    body {
      background: radial-gradient(circle at top, #1e1b4b, var(--bg-dark));
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    /* Màn hình đăng nhập */
    #auth-screen {
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      width: 100%;
      padding: 16px;
    }

    .auth-box {
      background: var(--bg-card);
      border: 1px solid rgba(245, 158, 11, 0.4);
      border-radius: 16px;
      padding: 32px;
      width: 100%;
      max-width: 400px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
      text-align: center;
    }

    .auth-box h1 {
      font-size: 26px;
      color: var(--gold-light);
      margin-bottom: 8px;
    }

    .auth-box p {
      color: var(--text-muted);
      font-size: 14px;
      margin-bottom: 24px;
    }

    .input-group {
      text-align: left;
      margin-bottom: 16px;
    }

    .input-group label {
      display: block;
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .input-group input {
      width: 100%;
      padding: 12px 14px;
      border-radius: 10px;
      border: 1px solid #475569;
      background: #0f172a;
      color: #fff;
      font-size: 15px;
      outline: none;
    }

    .input-group input:focus {
      border-color: var(--gold);
    }

    .btn-primary {
      width: 100%;
      padding: 13px;
      border: none;
      border-radius: 10px;
      background: linear-gradient(135deg, #f59e0b, #d97706);
      color: #000;
      font-weight: 700;
      font-size: 16px;
      cursor: pointer;
      transition: transform 0.15s, opacity 0.15s;
    }

    .btn-primary:hover {
      opacity: 0.92;
      transform: translateY(-1px);
    }

    .auth-note {
      margin-top: 14px;
      font-size: 12px;
      color: var(--gold-light);
    }

    /* Giao diện chính */
    #game-screen {
      display: none;
      width: 100%;
      max-width: 1120px;
      padding: 16px;
    }

    header {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 12px;
      background: var(--bg-card);
      padding: 14px 20px;
      border-radius: 14px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      margin-bottom: 20px;
    }

    .brand {
      font-size: 20px;
      font-weight: 800;
      color: var(--gold-light);
    }

    .user-info {
      display: flex;
      align-items: center;
      gap: 12px;
      flex-wrap: wrap;
    }

    .coin-badge {
      background: rgba(245, 158, 11, 0.15);
      border: 1px solid var(--gold);
      color: var(--gold-light);
      padding: 6px 14px;
      border-radius: 999px;
      font-weight: 700;
      font-size: 15px;
    }

    .btn-sm {
      padding: 7px 12px;
      border-radius: 8px;
      border: 1px solid #475569;
      background: #0f172a;
      color: #fff;
      cursor: pointer;
      font-size: 13px;
    }

    .btn-sm:hover {
      background: #334155;
    }

    .main-grid {
      display: grid;
      grid-template-columns: 1fr 1.2fr;
      gap: 20px;
      align-items: start;
    }

    @media (max-width: 880px) {
      .main-grid {
        grid-template-columns: 1fr;
      }
    }

    /* Khu vực vòng quay */
    .wheel-card {
      background: var(--bg-card);
      border-radius: 16px;
      padding: 20px;
      border: 1px solid rgba(255, 255, 255, 0.08);
      display: flex;
      flex-direction: column;
      align-items: center;
    }

    .wheel-wrapper {
      position: relative;
      width: 340px;
      height: 340px;
      max-width: 82vw;
      max-height: 82vw;
      margin: 10px 0 18px;
    }

    canvas#wheelCanvas {
      width: 100%;
      height: 100%;
      display: block;
      filter: drop-shadow(0 10px 20px rgba(0, 0, 0, 0.5));
    }

    .pointer {
      position: absolute;
      top: -12px;
      left: 50%;
      transform: translateX(-50%);
      width: 0;
      height: 0;
      border-left: 16px solid transparent;
      border-right: 16px solid transparent;
      border-top: 30px solid #ef4444;
      filter: drop-shadow(0 3px 6px rgba(0, 0, 0, 0.6));
      z-index: 10;
    }

    .spin-btn {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 78px;
      height: 78px;
      border-radius: 50%;
      border: 4px solid #fff;
      background: radial-gradient(circle, #fde047, #d97706);
      color: #000;
      font-weight: 900;
      font-size: 16px;
      cursor: pointer;
      box-shadow: 0 0 20px rgba(245, 158, 11, 0.8);
      z-index: 5;
      transition: transform 0.15s;
    }

    .spin-btn:hover:not(:disabled) {
      transform: translate(-50%, -50%) scale(1.06);
    }

    .spin-btn:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }

    .status-banner {
      width: 100%;
      text-align: center;
      padding: 12px;
      border-radius: 10px;
      background: #0f172a;
      font-weight: 600;
      font-size: 15px;
      min-height: 46px;
      display: flex;
      align-items: center;
      justify-content: center;
      border: 1px solid #334155;
    }

    .history-bar {
      width: 100%;
      margin-top: 14px;
    }

    .history-title {
      font-size: 12px;
      color: var(--text-muted);
      margin-bottom: 6px;
    }

    .history-list {
      display: flex;
      gap: 8px;
      overflow-x: auto;
      padding-bottom: 4px;
    }

    .history-item {
      background: #0f172a;
      border: 1px solid #334155;
      border-radius: 8px;
      padding: 5px 10px;
      font-size: 13px;
      white-space: nowrap;
      display: flex;
      align-items: center;
      gap: 4px;
    }

    /* Bảng chọn biểu tượng */
    .board-card {
      background: var(--bg-card);
      border-radius: 16px;
      padding: 20px;
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .chip-selector {
      display: flex;
      flex-direction: column;
      gap: 8px;
      margin-bottom: 16px;
      background: #0f172a;
      padding: 12px 14px;
      border-radius: 12px;
    }

    .chips {
      display: flex;
      gap: 6px;
      flex-wrap: wrap;
    }

    .chip {
      padding: 6px 11px;
      border-radius: 999px;
      border: 2px solid #475569;
      background: #1e293b;
      color: #fff;
      font-weight: 700;
      font-size: 12px;
      cursor: pointer;
    }

    .chip.active {
      border-color: var(--gold-light);
      background: var(--gold);
      color: #000;
    }

    .symbols-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 10px;
    }

    @media (max-width: 480px) {
      .symbols-grid {
        grid-template-columns: 1fr;
      }
    }

    .symbol-card {
      background: #0f172a;
      border: 2px solid #334155;
      border-radius: 12px;
      padding: 11px 12px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      cursor: pointer;
      transition: border-color 0.15s, transform 0.1s;
      user-select: none;
    }

    .symbol-card:hover {
      border-color: #64748b;
    }

    .symbol-card.has-bet {
      border-color: var(--gold);
      background: rgba(245, 158, 11, 0.08);
    }

    .symbol-card.winner {
      border-color: var(--success);
      box-shadow: 0 0 15px rgba(16, 185, 129, 0.45);
      background: rgba(16, 185, 129, 0.15);
    }

    .sym-left {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .sym-icon {
      font-size: 26px;
      width: 40px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 10px;
      background: rgba(255, 255, 255, 0.05);
    }

    .sym-name {
      font-weight: 700;
      font-size: 14px;
    }

    .sym-mult {
      font-size: 13px;
      color: var(--gold-light);
      font-weight: 700;
    }

    .sym-bet {
      background: #1e293b;
      padding: 5px 9px;
      border-radius: 8px;
      font-weight: 700;
      font-size: 12px;
      color: #38bdf8;
      min-width: 78px;
      text-align: right;
    }

    .board-actions {
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 16px;
      padding-top: 14px;
      border-top: 1px solid #334155;
    }

    .total-bet-text {
      font-size: 14px;
      color: var(--text-muted);
    }

    .total-bet-text span {
      color: #fff;
      font-weight: 700;
    }

    .action-btns {
      display: flex;
      gap: 8px;
    }
  </style>
</head>
<body>

  <!-- MÀN HÌNH ĐĂNG NHẬP -->
  <div id="auth-screen">
    <div class="auth-box">
      <h1>🎡 Vòng Đu Quay Hoàng Gia</h1>
      <p>Đăng nhập hoặc tạo tài khoản mới để bắt đầu trải nghiệm</p>
      <form id="login-form">
        <div class="input-group">
          <label for="username">Tên tài khoản</label>
          <input type="text" id="username" placeholder="Nhập tên của bạn..." required minlength="3" maxlength="20" />
        </div>
        <div class="input-group">
          <label for="password">Mật khẩu</label>
          <input type="password" id="password" placeholder="Nhập mật khẩu..." required minlength="3" />
        </div>
        <button type="submit" class="btn-primary">Vào Chơi Ngay</button>
