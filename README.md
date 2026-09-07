<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Absensi Online</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 30px auto; padding: 20px; background: #f4f7f6; }
        .card { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); margin-bottom: 20px; }
        h2 { margin-top: 0; color: #333; }
        input, select, button { width: 100%; padding: 10px; margin: 8px 0; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        button { background-color: #28a745; color: white; border: none; font-weight: bold; cursor: pointer; }
        button:hover { background-color: #218838; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
        th { background-color: #007bff; color: white; }
    </style>
</head>
<body>

<div class="card">
    <h2>Form Absensi</h2>
    <form id="absensiForm">
        <label>Nama Lengkap</label>
        <input type="text" id="nama" placeholder="Masukkan nama..." required>
        
        <label>Keterangan</label>
        <select id="keterangan">
            <option value="Hadir">Hadir</option>
            <option value="Izin">Izin</option>
            <option value="Sakit">Sakit</option>
        </select>
        
        <button type="submit">Kirim Absen</button>
    </form>
</div>

<div class="card">
    <h2>Daftar Kehadiran</h2>
    <table>
        <thead>
            <tr>
                <th>Waktu</th>
                <th>Nama</th>
                <th>Status</th>
            </tr>
        </thead>
        <tbody id="tabelAbsen"></tbody>
    </table>
</div>

<script>
    const form = document.getElementById('absensiForm');
    const tabel = document.getElementById('tabelAbsen');

    function muatData() {
        tabel.innerHTML = '';
        const data = JSON.parse(localStorage.getItem('dataAbsensi')) || [];
        data.forEach(item => {
            const row = `<tr>
                <td>${item.waktu}</td>
                <td>${item.nama}</td>
                <td>${item.keterangan}</td>
            </tr>`;
            tabel.innerHTML += row;
        });
    }

    form.addEventListener('submit', function(e) {
        e.preventDefault();
        const nama = document.getElementById('nama').value;
        const keterangan = document.getElementById('keterangan').value;
        const waktu = new Date().toLocaleString('id-ID');

        const dataLama = JSON.parse(localStorage.getItem('dataAbsensi')) || [];
        dataLama.push({ nama, keterangan, waktu });
        localStorage.setItem('dataAbsensi', JSON.stringify(dataLama));

        form.reset();
        muatData();
    });

    muatData();
</script>

</body>
</html>
