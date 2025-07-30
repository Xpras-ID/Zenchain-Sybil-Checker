# Zenchain-Sybil-Checker
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>x_pras Sybil Checker</title>
  <style>
    body {
      background: linear-gradient(180deg, #1a1a2e, #1c1c1e);
      color: white;
      font-family: Arial, sans-serif;
      display: flex;
      flex-direction: column;
      align-items: center;
      min-height: 100vh;
      padding: 0;
      margin: 0;
    }
    /* ===== Header ===== */
    .header { text-align: center; margin: 40px 0 20px; }
    .header-logo {
      font-size: 20px;
      font-weight: bold;
      color: #f81ce5;
      border: 2px solid #f81ce5;
      padding: 10px 20px;
      border-radius: 25px;
      display: inline-block;
    }
    .header-title { font-size: 28px; margin: 15px 0 10px; }
    .header-subtitle { font-size: 16px; color: #ccc; }
    /* ===== Follow Box ===== */
    .follow-box {
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 12px;
      padding: 20px;
      text-align: center;
      margin-bottom: 40px;
      width: 500px;
    }
    .follow-title { font-size: 18px; font-weight: bold; margin-bottom: 10px; display: flex; align-items: center; justify-content: center; gap: 8px; }
    .follow-desc { font-size: 14px; color: #bbb; margin-bottom: 20px; }
    .follow-btn {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      background: #8b5cf6;
      color: white;
      padding: 10px 20px;
      border-radius: 8px;
      text-decoration: none;
      font-weight: bold;
      transition: background 0.3s;
    }
    .follow-btn:hover { background: #7c3aed; }
    .x-logo { width: 18px; height: 18px; fill: white; }
    /* ===== Main Box ===== */
    .container {
      width: 500px;
      background: #2c2c2e;
      padding: 50px 40px;
      border-radius: 12px;
      text-align: center;
      box-shadow: 0 4px 10px rgba(0,0,0,0.4);
      margin-bottom: 60px;
    }
    .container h3 { margin-bottom: 25px; font-size: 22px; font-weight: bold; }
    input {
      width: 100%;
      padding: 16px;
      margin-bottom: 25px;
      border-radius: 10px;
      border: none;
      font-size: 16px;
      outline: none;
      box-sizing: border-box;
    }
    button {
      width: 100%;
      padding: 14px;
      background: #8b5cf6;
      border: none;
      border-radius: 10px;
      font-size: 16px;
      color: white;
      cursor: pointer;
      transition: background 0.3s;
    }
    button:hover { background: #7c3aed; }
    /* ===== Result Box ===== */
    .result {
      margin-top: 30px;
      background: #3a3a3c;
      padding: 20px;
      border-radius: 12px;
      opacity: 0;
      transform: translateY(10px);
      transition: all 0.5s ease-in-out;
      word-break: break-word;
    }
    .result.show { opacity: 1; transform: translateY(0); }
    .risk-bar { height: 10px; width: 100%; background: #555; border-radius: 5px; margin-top: 10px; }
    .risk-fill { height: 100%; border-radius: 5px; width: 0; transition: width 1s ease-in-out, background 0.5s; }
    .score { font-size: 40px; margin: 10px 0; }
    .icon { font-size: 30px; margin-bottom: 10px; }
    small { display: block; margin-top: 15px; color: #aaa; }
    /* ===== Footer ===== */
    footer {
      text-align: center;
      padding: 20px;
      font-size: 14px;
      color: #888;
      margin-top: auto;
      border-top: 1px solid rgba(255,255,255,0.1);
      width: 100%;
      background: #1c1c1e;
    }
  </style>
</head>
<body>
  <!-- ===== Header ===== -->
  <div class="header">
    <div class="header-logo">@prasislami90</div>
    <div class="header-title">x_pras Sybil Checker</div>
    <div class="header-subtitle">Analyze your EVM or Monad wallet address to check for potential sybil activity patterns</div>
  </div>

  <!-- ===== Follow Box ===== -->
  <div class="follow-box">
    <div class="follow-title">
      <svg class="x-logo" viewBox="0 0 24 24"><path d="M18.9 2H21.9L14.7 10.3L23 22H16.4L11.2 14.7L5.2 22H2.2L9.8 13.2L2 2H8.7L13.3 8.6L18.9 2Z"/></svg>
      Follow for Access
    </div>
    <div class="follow-desc">Follow us for the latest updates and to unlock the sybil checker</div>
    <a class="follow-btn" href="https://x.com/prasislami90" target="_blank">
      <svg class="x-logo" viewBox="0 0 24 24"><path d="M18.9 2H21.9L14.7 10.3L23 22H16.4L11.2 14.7L5.2 22H2.2L9.8 13.2L2 2H8.7L13.3 8.6L18.9 2Z"/></svg>
      Follow @prasislami90 ↗
    </a>
  </div>

  <!-- ===== Main Container ===== -->
  <div class="container">
    <h3>Wallet Address</h3>
    <input type="text" id="wallet" placeholder="0x...">
    <button onclick="checkSybil()">Check Sybil Score</button>
    
    <div class="result" id="result">
      <div class="icon" id="icon">⚠</div>
      <h4>Analysis Complete</h4>
      <p id="address"></p>
      <h2 class="score" id="scoreText">0%</h2>
      <div class="risk-bar"><div class="risk-fill" id="riskFill"></div></div>
      <p id="riskLabel"></p>
      <small>* This analysis is for educational purposes only and should not be considered as financial advice.</small>
    </div>
  </div>

  <!-- ===== Footer ===== -->
  <footer>
    © 2025 x_pras Sybil Checker. Built for the Zenchain ecosystem.
  </footer>

  <script>
    function animateCount(element, target) {
      let count = 0;
      const step = Math.ceil(target / 50);
      const timer = setInterval(() => {
        count += step;
        if (count >= target) {
          count = target;
          clearInterval(timer);
        }
        element.innerText = count + "%";
      }, 20);
    }

    function checkSybil() {
      const wallet = document.getElementById('wallet').value;
      if (!wallet) return alert("Masukkan alamat wallet!");

      const fakeScore = Math.floor(Math.random() * 100);
      document.getElementById('address').innerText = wallet;
      animateCount(document.getElementById('scoreText'), fakeScore);

      const fill = document.getElementById('riskFill');
      fill.style.width = fakeScore + "%";

      const icon = document.getElementById('icon');
      const riskLabel = document.getElementById('riskLabel');

      if (fakeScore > 70) {
        fill.style.background = "#ef4444";
        icon.innerText = "⚠";
        riskLabel.innerText = "High Risk - This wallet shows high risk patterns for sybil activity.";
      } else if (fakeScore > 40) {
        fill.style.background = "#f59e0b";
        icon.innerText = "⚠";
        riskLabel.innerText = "Medium Risk - This wallet shows moderate risk patterns.";
      } else {
        fill.style.background = "#22c55e";
        icon.innerText = "✔";
        riskLabel.innerText = "Low Risk - This wallet shows low risk patterns.";
      }

      document.getElementById('result').classList.add('show');
    }
  </script>
</body>
</html>

# version of using Dummy API
Endpoint dummy:
https://dummyapi.io/sybil-score?address=0x123...
# Respon JSON
{
  "address": "0x123...",
  "score": 75,
  "risk": "High"
}
# Script
<script>
  async function checkSybil() {
    const wallet = document.getElementById('wallet').value;
    if (!wallet) return alert("Masukkan alamat wallet!");

    try {
      // ==== Panggil Dummy API ====
      const response = await fetch(`https://dummyapi.io/sybil-score?address=${wallet}`);
      if (!response.ok) throw new Error("API error");
      const data = await response.json();

      const fakeScore = data.score || 0;  // Ambil score dari API
      document.getElementById('address').innerText = data.address || wallet;
      animateCount(document.getElementById('scoreText'), fakeScore);

      const fill = document.getElementById('riskFill');
      fill.style.width = fakeScore + "%";

      const icon = document.getElementById('icon');
      const riskLabel = document.getElementById('riskLabel');

      if (fakeScore > 70) {
        fill.style.background = "#ef4444";
        icon.innerText = "⚠";
        riskLabel.innerText = "High Risk - This wallet shows high risk patterns for sybil activity.";
      } else if (fakeScore > 40) {
        fill.style.background = "#f59e0b";
        icon.innerText = "⚠";
        riskLabel.innerText = "Medium Risk - This wallet shows moderate risk patterns.";
      } else {
        fill.style.background = "#22c55e";
        icon.innerText = "✔";
        riskLabel.innerText = "Low Risk - This wallet shows low risk patterns.";
      }

      document.getElementById('result').classList.add('show');

    } catch (e) {
      alert("Gagal mengambil data Sybil Score dari API");
      console.error(e);
    }
  }
</script>

# Notes
You can replace Dummy API with your own server.
If you don't have a server, you can use a mock server like Mocki.io or My-json-sider.typicode.com.
