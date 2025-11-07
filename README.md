kodingan html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Daftar Film dan Pemesanan Tiket</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>

  <!-- Container card film -->
  <div class="cards-container">

    <div class="card">
      <img src="/img/asasin.jpeg" alt="Sniper: Assassin's End" />
      <strong>Card title</strong>
      <p>
        ini menceritakan tentang seorang mantan prajurit pasukan khusus yang di jebak oleh petinggi negara sebagai kambing hitam.
      </p>
      <small>Last updated 3 mins ago</small>
    </div>

    <div class="card">
      <img src="/img/petaka.jpeg" alt="Petaka Gunung Gede" />
      <strong>Card title</strong>
      <p>
        Ini adalah film yang menceritakan tentang hal mistis di gunung.
      </p>
      <small>Last updated 3 mins ago</small>
    </div>

    <div class="card">
      <img src="/img/sniper.1.jpeg" alt="Sniper Ghost Shooter" />
      <strong>Card title</strong>
      <p>
        Ini menceritakan tentang duel sengit antara mantan pasukan elit global dengan pasukan khusus amerika.
      </p>
      <small>Last updated 3 mins ago</small>
    </div>
    
  </div>

  <!-- Form pemesanan tiket -->
  <div class="form-container">
    <h2>Sistem Pemesanan Tiket Film</h2>
    <form id="formPemesanan">
      <label for="film"><b>Pilih Film yang Akan Ditonton:</b></label>
      <select id="film" name="film" required>
        <option value="">-- Pilih Film --</option>
        <option value="Sniper Assassin's End">Sniper Assassin's End</option>
        <option value="Petaka Gunung Gede">Petaka Gunung Gede</option>
        <option value="Sniper Ghost Shooter">Sniper Ghost Shooter</option>
      </select>

      <label for="jumlah-tiket"><b>Jumlah Tiket:</b></label>
      <input type="text" id="jumlah-tiket" name="jumlah-tiket" placeholder="Masukkan jumlah tiket" required>

      <label for="jenis-kursi"><b>Jenis Kursi:</b></label>
      <select id="jenis-kursi" name="jenis-kursi" required>
        <option value="reguler">Reguler (Rp 50.000)</option>
        <option value="vip">VIP (Reguler + Rp 25.000)</option>
      </select>

      <button type="submit">Pesan & Hitung Total</button>
    </form>
    
    <div id="hasilPemesanan"></div>
  </div>

  <script src="script.js"></script>
</body>
</html>
#kodingan css#
body {
  background-color: #7ec0ee; /* warna biru muda */
  font-family: Arial, sans-serif;
  margin: 20px;
  color: black;
}

/* Container utama untuk ketiga card */
.cards-container {
  display: flex;
  justify-content: center;
  gap: 80px;
  margin-bottom: 40px;
  flex-wrap: wrap;
}

/* Satu card */
.card {
  max-width: 220px;
  background-color: transparent;
  text-align: left;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.card img {
  width: 150px;
  height: auto;
  border-radius: 6px;
  margin-bottom: 12px;
  object-fit: cover;
}

.card strong {
  margin-bottom: 10px;
  display: block;
}

.card p {
  margin: 0 0 12px 0;
  font-size: 14px;
  text-align: justify;
}

.card small {
  font-size: 12px;
  color: #222;
  align-self: flex-start;
}

/* Container form pemesanan */
.form-container {
  max-width: 320px;
  background-color: #155ED1; /* biru gelap */
  padding: 20px;
  border-radius: 8px;
  color: white;
  margin: 0 auto;
  font-size: 14px;
  box-sizing: border-box;
}

.form-container h2 {
  color: white;
  text-align: center;
  margin-top: 0;
  margin-bottom: 20px;
  font-weight: normal;
}

.form-container label {
  font-weight: bold;
  display: block;
  margin-top: 10px;
  margin-bottom: 6px;
}

.form-container input[type="text"],
.form-container select {
  width: 100%;
  padding: 8px 6px;
  font-size: 14px;
  border-radius: 4px;
  border: none;
  box-sizing: border-box;
}

.form-container button {
  margin-top: 16px;
  width: 100%;
  padding: 10px;
  background-color: #2596f4;
  border: none;
  color: white;
  border-radius: 6px;
  font-size: 16px;
  cursor: pointer;
}

.form-container button:hover {
  background-color: #1a67c7;
}

/* Area hasil pemesanan */
#hasilPemesanan {
  margin-top: 30px;
  background-color: #ececec;
  color: #000;
  border-radius: 8px;
  padding: 15px;
  font-weight: bold;
  white-space: pre-line; /* agar \n berfungsi */
}
#kodingan js#
document.addEventListener("DOMContentLoaded", function() {
  const form = document.getElementById("formPemesanan");
  const hasilDiv = document.getElementById("hasilPemesanan");

  form.addEventListener("submit", function(e) {
    e.preventDefault();

    const film = form.film.value;
    const jumlahTiketStr = form["jumlah-tiket"].value.trim();
    const jenisKursi = form["jenis-kursi"].value;

    if (film === "") {
      hasilDiv.textContent = "Silakan pilih film yang akan ditonton.";
      return;
    }

    const jumlahTiket = parseInt(jumlahTiketStr, 10);
    if (isNaN(jumlahTiket) || jumlahTiket < 1) {
      hasilDiv.textContent = "Jumlah tiket harus diisi dengan angka lebih besar dari 0.";
      return;
    }

    let hargaPerTiket = 0;
    switch(jenisKursi) {
      case "reguler":
        hargaPerTiket = 50000;
        break;
      case "vip":
        hargaPerTiket = 100000;
        break;
      case "vvip":
        hargaPerTiket = 150000;
        break;
      default:
        hargaPerTiket = 0;
    }

    const totalHarga = hargaPerTiket * jumlahTiket;

    hasilDiv.textContent =
      `Film yang dipilih: ${film}
Jumlah tiket: ${jumlahTiket}
Jenis kursi: ${jenisKursi.toUpperCase()}
Total harga yang harus dibayar: Rp ${totalHarga.toLocaleString('id-ID')}`;
  });
});
`

