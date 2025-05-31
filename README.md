<!DOCTYPE html><html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Uaycha Top Up</title>
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-800">
  <div class="max-w-2xl mx-auto p-6">
    <div class="flex justify-between items-center mb-4">
      <h1 class="text-3xl font-bold">Uaycha Top Up 💎</h1>
      <button onclick="toggleLanguage()" class="bg-blue-500 text-white px-4 py-1 rounded">EN/ID</button>
    </div><form id="topup-form" class="bg-white p-6 rounded-xl shadow-md mb-6">
  <label class="block mb-2 font-semibold" data-en="Select Country" data-id="Pilih Negara">Pilih Negara</label>
  <select class="w-full mb-4 p-2 border rounded" id="country">
    <option value="Indonesia">Indonesia 🇮🇩</option>
    <option value="Singapore">Singapore 🇸🇬</option>
    <option value="Philippines">Philippines 🇵🇭</option>
    <option value="Malaysia">Malaysia 🇲🇾</option>
  </select>

  <label class="block mb-2 font-semibold" data-en="Select Game" data-id="Pilih Game">Pilih Game</label>
  <select class="w-full mb-4 p-2 border rounded" id="game">
    <option value="Mobile Legends">Mobile Legends</option>
    <option value="Free Fire">Free Fire</option>
    <option value="Higgs Domino">Higgs Domino</option>
  </select>

  <label class="block mb-2 font-semibold" data-en="Player ID" data-id="ID Pemain">ID Pemain</label>
  <input type="text" id="player-id" class="w-full mb-4 p-2 border rounded" placeholder="Masukkan ID game kamu" required />

  <label class="block mb-2 font-semibold" data-en="Diamond Amount" data-id="Jumlah Diamond">Jumlah Diamond</label>
  <select class="w-full mb-4 p-2 border rounded" id="amount">
    <option value="86">86 Diamond - Rp20.000</option>
    <option value="172">172 Diamond - Rp38.000</option>
    <option value="257">257 Diamond - Rp55.000</option>
    <option value="344">344 Diamond - Rp70.000</option>
    <option value="514">514 Diamond - Rp95.000</option>
    <option value="706">706 Diamond - Rp120.000</option>
    <option value="878">878 Diamond - Rp150.000</option>
  </select>

  <label class="block mb-2 font-semibold" data-en="Payment Method" data-id="Metode Pembayaran">Metode Pembayaran</label>
  <select class="w-full mb-4 p-2 border rounded" id="payment">
    <option value="Dana">Dana</option>
    <option value="OVO">OVO</option>
    <option value="Bank">Transfer Bank</option>
  </select>

  <button type="button" onclick="sendWhatsApp()" class="w-full bg-green-500 text-white font-bold py-2 rounded hover:bg-green-600" data-en="Send Order" data-id="Kirim Pesanan">Kirim Pesanan</button>
</form>

<div class="bg-white p-4 rounded shadow">
  <h2 class="text-xl font-semibold mb-3" data-en="Order History" data-id="Riwayat Pesanan">Riwayat Pesanan</h2>
  <ul id="order-history" class="text-sm space-y-2"></ul>
</div>

  </div>  <script>
    function sendWhatsApp() {
      const game = document.getElementById('game').value;
      const id = document.getElementById('player-id').value;
      const amount = document.getElementById('amount').value;
      const payment = document.getElementById('payment').value;
      const country = document.getElementById('country').value;

      const message = `Halo! Saya ingin top up:\nNegara: ${country}\nGame: ${game}\nID: ${id}\nDiamond: ${amount}\nPembayaran: ${payment}`;
      const encodedMsg = encodeURIComponent(message);
      const waNumber = '6285852931074';
      window.open(`https://wa.me/${waNumber}?text=${encodedMsg}`, '_blank');

      const history = JSON.parse(localStorage.getItem('orders') || '[]');
      history.push({ country, game, id, amount, payment, time: new Date().toLocaleString() });
      localStorage.setItem('orders', JSON.stringify(history));
      loadHistory();
    }

    function loadHistory() {
      const history = JSON.parse(localStorage.getItem('orders') || '[]');
      const list = document.getElementById('order-history');
      list.innerHTML = history.reverse().slice(0, 10).map(h => `<li>📌 [${h.time}] ${h.country} - ${h.game} - ${h.amount} (${h.payment})</li>`).join('');
    }

    function toggleLanguage() {
      const elements = document.querySelectorAll('[data-en]');
      const current = elements[0].textContent.trim() === elements[0].dataset.id ? 'en' : 'id';
      elements.forEach(el => el.textContent = el.dataset[current]);
    }

    window.onload = loadHistory;
  </script></body>
</html>
