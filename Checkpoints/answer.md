# Jawaban Praktikum: Nadia Saidatunnufus (10224007)

## Bagian 1: Pemanasan
1. Pada aturan `nav a.active:hover { color: red; }`:
   - Selector: `nav a.active:hover`
   - Deklarasi: `{ color: red; }`
   - Property: `color`
   - Value: `red`
   - Pseudo-class: `:hover` (dan `:active` jika ditulis dalam bentuk elemen `.active`)
2. Elemen Default:
   - Block: `p`, `li`, `h2`
   - Inline: `span`, `a`, `strong`
3. Paragraf A dan B. Selector `.box p` memilih semua elemen `<p>` yang merupakan keturunan (descendant) dari elemen bermuatan class `box`.
4. Warna teks menjadi merah (`red`). Hal ini terjadi karena selector ID (`#title`) memiliki nilai spesifisitas (specificity) paling tinggi dibandingkan class selector (`.heading`) maupun element/type selector (`h1`).
5. Kesalahan terletak pada urutan penutupan tag HTML yang tumpang tindih (nesting tag yang salah). Tag `<strong>` dibuka di dalam `<p>`, sehingga seharusnya tag `</strong>` ditutup terlebih dahulu sebelum tag `</p>`.

## Bagian 3: Prediksi Selector Golf
P1. Prediksi awal:
(a) green
(b) orange
(c) blue

P2. Urutan specificity dari tertinggi ke terendah:
1. `#tech p` (Specificity: 1,0,1)
2. `.club p` (Specificity: 0,1,1)
3. `main section p` (Specificity: 0,0,3)
4. `p` (Specificity: 0,0,1)

Setelah diuji (hasil sebenarnya):
(a) Green: Terpengaruh oleh `section p` (specificity 0,0,2 vs `p` 0,0,1).
(b) Orange: Terpengaruh oleh `.note` (specificity 0,1,0 vs `section p` 0,0,2).
(c) Blue: Terpengaruh oleh aturan general `p` (specificity 0,0,1).

## Bagian 4: Box model
Q1 (content-box):
- Perhitungan: Lebar elemen = width + padding-left + padding-right + border-left + border-right
- Hitungan: 300px + 16px + 16px + 1px + 1px = 334px.
- Lebar yang terlihat (border-to-border) adalah 334px.

Q2 (border-box):
- Jika menggunakan `box-sizing: border-box`, total lebar yang terlihat tetap 300px. Lebar area konten internal akan otomatis berkurang menjadi 266px (300px - 32px padding - 2px border) untuk mempertahankan total ukuran elemen.

Pengecekan DevTools:
- Content: 926px x 240px (tergantung isi teks/layar)
- Padding: 16px (atas, kanan, bawah, kiri)
- Border: 1px (atas, kanan, bawah, kiri)
- Margin: 0px (samping), 0px 0px 24px 0px (bawah)

## Bagian 5: Tabel debug
| # | Baris | Bug | Perbaikan | Cara menemukannya |
|---|-------|-----|-----------|-------------------|
| 1 | 9 | Penulisan property CSS `colour` (ejaan Inggris UK) | Ubah menjadi `color: #333;` | DevTools menunjukkan property bernilai tidak valid / membaca kode |
| 2 | 12 | Kurang titik koma `;` pada `background: #dbe7f3` | Tambahkan `;` di akhir baris | Membaca kode / DevTools CSS error |
| 3 | 20 | Terdapat spasi pada nilai unit `18 px` | Ubah menjadi `18px` | DevTools mencoret property css |
| 4 | 23 | Penulisan nilai property `text-align: centre;` | Ubah menjadi `text-align: center;` | DevTools CSS error |
| 5 | 29 | Penutup tag tidak cocok `<h1>Campus News</h2>` | Ubah menjadi `<h1>Campus News</h1>` | W3C Validator |
| 6 | 32 | Tanda petik penutup atribut hilang `href="about.html>` | Ubah menjadi `href="about.html"` | W3C Validator / Syntax highlighting |
| 7 | 36 | Atribut `src` pada elemen `<img>` tidak memiliki atribut `alt` | Tambahkan `alt="Gambar Berita Kampus"` | W3C Validator |
| 8 | 36 | Elemen `<img>` tidak ditutup / dibiarkan tanpa penutup yang sesuai standar | Biarkan sebagai void element yang valid dengan alt lengkap | W3C Validator |
| 9 | 19 | Selector CSS `#news-list` tidak cocok dengan ID di HTML (`id="newsList"`) | Ubah selector CSS menjadi `#newsList` | DevTools elemen tidak mendapatkan gaya CSS |

## Bagian 6: Tabel Code Review
| # | Baris | Masalah | Mengapa penting | Perbaikan saya |
|---|-------|---------|-----------------|----------------|
| 1 | 1 | Tag `<!DOCTYPE html>` dan atribut `lang` pada `<html>` hilang | Memicu quirks mode browser dan merugikan SEO serta aksesibilitas layar baca | Tambahkan `<!DOCTYPE html>` dan `<html lang="id">` |
| 2 | 8 | Penggunaan `!important` pada `.nav a` | Merusak prinsip cascading CSS dan menyulitkan pemeliharaan kode | Hapus `!important` dan gunakan selector yang lebih spesifik |
| 3 | 14-22 | Penggunaan tag `<div>` tanpa semantik untuk struktur utama (`header`, `nav`, `footer`) | Mengurangi aksesibilitas screen reader dan performa SEO | Ganti dengan tag semantik `<header>`, `<nav>`, `<main>`, `<footer>` |
| 4 | 15 | Menggunakan tag `<b>` di dalam `<div>` alih-alih `<h1>` untuk judul utama | Struktur hirarki dokumen menjadi tidak jelas untuk mesin pencari dan pengguna | Ubah menjadi elemen `<h1>` |
| 5 | 23 | Teks judul bab menggunakan `<div>` berpenerapan inline style | Menyulitkan standarisasi desain dan tidak sesuai aksesibilitas | Gunakan tag `<h2>` dengan pemisahan CSS luar |
| 6 | 24, 27 | Penggunaan tag `<br>` berulang untuk mengatur jarak antar elemen | Mengacaukan struktur markup HTML; tata letak visual harus ditangani oleh CSS | Hapus tag `<br>` dan gunakan `margin` atau `padding` di CSS |
| 7 | 26 | Elemen `<img>` tidak memiliki atribut `alt` | Mempersulit pengguna dengan keterbatasan penglihatan (screen reader) | Tambahkan atribut `alt` yang deskriptif |
| 8 | 29-31 | Elemen formulir `<input>` tidak memiliki `<label>` terkait | Pengguna screen reader tidak dapat mengetahui fungsi kolom isian | Bungkus atau hubungkan dengan tag `<label for="...">` |
| 9 | 31 | Tombol menggunakan event inline `onclick="alert(...)"` | Mencampur logika interaktif JS ke dalam dokumen presentasi HTML | Pindahkan JavaScript ke script eksternal/file terpisah |
| 10 | 6 | Lebar header dikunci dengan nilai piksel statis `width: 1200px` | Membuat tampilan tidak responsif di perangkat seluler / layar kecil | Gunakan `max-width: 100%` atau `width: 100%` |

Refleksi:
1. Masalah ketiadaan atribut `alt` dan penggunaan tag `<div>` tanpa semantik adalah yang paling sulit disadari hanya dari visual browser. Hal ini karena browser tetap merender tampilan secara normal, meskipun secara struktur dokumen dan aksesibilitas sangat buruk.
2. Walaupun halaman terlihat berfungsi, masalah tersebut sangat memengaruhi performa SEO, aksesibilitas bagi penyandang disabilitas, kemudahan perawatan kode (*maintainability*), serta kestabilan tampilan di berbagai ukuran layar.
3. Kebiasaan yang akan saya terapkan adalah selalu menjalankan kode HTML melalui W3C Validator dan melakukan tes responsif melalui DevTools browser sebelum mengunggah pekerjaan.

## Bagian 7: Exit ticket
1. Anatomi aturan CSS terdiri dari **Selector** (penunjuk elemen HTML yang ingin diberi gaya), diikuti oleh **Declaration Block** dalam kurung kurawal `{}`. Di dalam blok deklarasi terdapat **Property** (sifat yang ingin diubah) dan **Value** (nilai perubahan) yang dipisahkan oleh titik dua `:` dan diakhiri titik koma `;`.
2. Konsep perhitungan nilai spesifisitas (specificity) pada kombinasi selector kompleks dan penggunaan pseudo-element kadang masih memerlukan ketelitian ekstra.
3. Saya sekarang dapat membuat struktur dokumen HTML semantik lengkap beserta form yang terhubung dengan `<label>` tanpa harus melihat dokumentasi external.