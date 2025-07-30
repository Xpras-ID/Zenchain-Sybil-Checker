# Zenchain-Sybil-Checker
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
