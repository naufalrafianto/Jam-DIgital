### 1. **Tag `<head>`**

- **Pustaka Google Fonts**: Diimpor font `'Roboto Mono'` dari Google Fonts agar tampilan teks menggunakan jenis font monospace.
- **Elemen CSS**: Ada beberapa aturan yang diterapkan:

  - **`body`**: Menentukan gaya dasar untuk halaman (font, layout tengah dengan `flex`, warna latar belakang hitam, dan warna teks putih).
  - **`.clock-container`**: Ini adalah kontainer utama untuk menampilkan jam. Tata letak menggunakan `flex` untuk pengaturan elemen secara vertikal.
  - **`.main-time`**: Menampilkan jam utama dalam zona WIB (dengan ukuran font yang besar, hingga 12% dari lebar viewport).
  - **`.date`**: Menampilkan tanggal di bawah jam utama.
  - **`.timezones`**: Ini adalah tata letak untuk menampilkan tiga zona waktu (WIB, WITA, WIT), ditampilkan secara horizontal.
  - **`.timezone`**: Mengatur tata letak teks di setiap zona waktu agar di tengah dan menyesuaikan ukuran font untuk masing-masing bagian waktu.
  - **`.blinking`**: Animasi berkedip pada titik dua (:) yang memisahkan jam, menit, dan detik.

- **Pustaka jQuery**: Ditambahkan pustaka jQuery versi 3.6.0 melalui CDN di dalam tag `<script>`. Ini memungkinkan kita menggunakan jQuery untuk memanipulasi elemen HTML dengan lebih efisien.

### 2. **Tag `<body>`**

- **Div `.clock-container`**: Merupakan kontainer utama yang menampung elemen-elemen jam, tanggal, dan tiga zona waktu.

  - **`<div id="wib-time">`**: Elemen ini menampilkan waktu WIB besar di bagian atas.
  - **`<div id="local-date">`**: Menampilkan tanggal saat ini dalam format yang disesuaikan dengan lokal Indonesia (`id-ID`).
  - **`<div class="timezones">`**: Menampilkan waktu di tiga zona waktu Indonesia (WIB, WITA, WIT). Setiap zona memiliki elemen dengan class `timezone` yang menampilkan nama zona waktu (WIB, WITA, WIT) dan waktu dalam elemen `<div>` masing-masing.

### 3. **JavaScript (Menggunakan jQuery)**

Kode JavaScript ini melakukan pembaruan waktu secara otomatis setiap detik menggunakan fungsi `setInterval`.

#### Fungsi Utama: `updateClock()`

- **Mendapatkan waktu saat ini**:
  `const now = new Date();`
- **Memperbarui waktu WIB utama (elemen `#wib-time`)**:

  - Waktu disusun dari jam, menit, dan detik.
  - Titik dua (`:`) yang memisahkan jam, menit, dan detik memiliki class `blinking` untuk membuatnya berkedip.
  - Menggunakan jQuery (`$('#wib-time')`) untuk memasukkan waktu ke dalam elemen HTML:

    `` wibTimeElement.html(`${hours}<span class="blinking">:</span>${minutes}<span class="blinking">:</span>${seconds}`); ``

- **Memperbarui tanggal lokal**:

  - Menggunakan fungsi `toLocaleDateString()` untuk mendapatkan tanggal dengan format lokal bahasa Indonesia (`id-ID`) dengan format yang sesuai (`long` untuk hari, bulan, dan tahun).
  - Diperbarui ke dalam elemen `#local-date` menggunakan jQuery:

    `localDateElement.text(now.toLocaleDateString('id-ID', options));`

- **Memperbarui waktu untuk tiga zona waktu (WIB, WITA, WIT)**:

  - Fungsi `updateTimezone()` digunakan untuk setiap zona waktu, yaitu Asia/Jakarta (WIB), Asia/Makassar (WITA), dan Asia/Jayapura (WIT).
  - `toLocaleTimeString()` digunakan untuk mendapatkan waktu dalam setiap zona waktu yang ditentukan.
  - Waktu kemudian diperbarui ke elemen terkait menggunakan jQuery:

    `function updateTimezone(timezone, elementId) {
    const timeString = now.toLocaleTimeString('id-ID', { timeZone: timezone, hour12: false, hour: '2-digit', minute:'2-digit' });
    $(elementId).text(timeString);
}`

#### Timer `setInterval()`

- Fungsi `setInterval(updateClock, 1000)` dipanggil untuk memperbarui waktu setiap detik. Fungsi `updateClock()` dijalankan setiap 1000 milidetik (1 detik).
