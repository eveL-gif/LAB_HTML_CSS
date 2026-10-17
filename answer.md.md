# Jawaban Praktikum: Nadia (10224007 )

## Bagian 1: Pemanasan
1. - Selector: `nav a.active:hover`
   - Deklarasi: `{ color: red; }`
   - Property: `color`
   - Value: `red`
   - Pseudo-class: `:hover` (serta `.active` sebagai class selector)
2. - Block: `p`, `li`, `h2`
   - Inline: `span`, `a`, `strong`
3. Paragraf A dan B. Karena `.box p` menyeleksi semua elemen `<p>` yang berada di dalam elemen ber-class `.box` (descent selector).
4. Warnanya **merah (red)**. Karena ID Selector (`#title`) memiliki nilai spesifisitas (*specificity*) paling tinggi dibanding Class Selector (`.heading`) dan Element/Type Selector (`h1`).
5. Tag tidak ditutup secara berurutan (*improper nesting*). Tag `<strong>` dibuka di dalam `<p>`, sehingga harus ditutup sebelum `</p>`. Perbaikan: `<p>Hello <strong>world</strong></p>`.

## Bagian 3: Prediksi Selector Golf
P1. (a) green  (b) orange  (c) blue
P2. Spesifisitas tertinggi ke terendah: `#tech p` > `.club p` > `main section p` > `p`

Setelah diuji (hasil sebenarnya):
P1:
- (a) "Weekly hack nights." -> **green** (Aturan `section p` [0,0,0,2] lebih spesifik dibanding `p` [0,0,0,1])
- (b) "Bring your own laptop." -> **orange** (Aturan `.note` [0,0,1,0] memenangi spesifisitas atas `section p` [0,0,0,2])
- (c) "© 2026 Student Affairs" -> **blue** (Hanya cocok dengan selector `p` [0,0,0,1])

P2:
1. `#tech p` (0,1,0,1)
2. `.club p` (0,0,1,1)
3. `main section p` (0,0,0,3)
4. `p` (0,0,0,1)

## Bagian 4: Box model
Q1 (content-box):
- Lebar Total Tampak = Width + Padding (Kiri + Kanan) + Border (Kiri + Kanan)
- Perhitungan: 300px + 16px + 16px + 1px + 1px = **334px**

Q2 (border-box):
- Lebar Total Tampak tetap **300px**. Browser menyesuaikan lebar konten menjadi 300px - (32px + 2px) = **266px**.

Pengecekan DevTools:
- Content: 926px × 180px
- Padding: 16px (semua sisi)
- Border: 1px (semua sisi)
- Margin: 0px (top/bottom: 0px, left/right: auto untuk centering)

## Bagian 5: Tabel debug
| # | Baris | Bug | Perbaikan | Cara menemukannya |
|---|-------|-----|-----------|-------------------|
| 1 | 10 | Penulisan properti `colour` (ejaaan UK) | Ubah menjadi `color` | DevTools (property diabaikan/invalid) |
| 2 | 13 | Titik koma `;` hilang pada `background: #dbe7f3` | Tambahkan `;` di akhir baris | Membaca kode / DevTools |
| 3 | 17 | Class `.Card` diawali huruf kapital (tidak cocok dengan `.card`) | Ubah menjadi `.card` | Membaca kode (case-sensitivity CSS) |
| 4 | 21 | Terdapat spasi pada nilai unit `18 px` | Ubah menjadi `18px` | DevTools (invalid property value) |
| 5 | 24 | Ejaan nilai properti `centre` (UK) | Ubah menjadi `center` | DevTools |
| 6 | 30 | Mismatch tag penutup `<h1>Campus News</h2>` | Ubah `</h2>` menjadi `</h1>` | W3C Validator |
| 7 | 33 | Kutip penutup hilang pada `href="about.html>` | Ubah menjadi `href="about.html">` | W3C Validator / Syntax Highlighting |
| 8 | 40 | Tag `<img>` tidak ditutup / tidak memiliki atribut `alt` | Tambahkan atribut `alt="Gambar Berita Kampus"` | W3C Validator |
| 9 | 41 | ID di HTML `newsList` (camelCase) tidak cocok dengan CSS `#news-list` (kebab-case) | Ubah ID HTML menjadi `id="news-list"` | Membaca kode & DevTools |

## Bagian 6: Tabel Code Review
| # | Baris | Masalah | Mengapa penting | Perbaikan saya |
|---|-------|---------|-----------------|----------------|
| 1 | 1 | Tag `<!DOCTYPE html>` dan atribut `lang` hilang | Browser masuk ke Quirks Mode dan membahayakan aksesibilitas. | Tambahkan `<!DOCTYPE html><html lang="id">` |
| 2 | 4 | Penggunaan `width: 1200px` secara fixed | Merusak tampilan di layar HP/tablet (tidak responsif). | Gunakan `max-width: 1200px; width: 100%;` |
| 3 | 5 | Menggunakan `!important` pada selector biasa | Merusak hierarki spesifisitas dan menyulitkan maintenance CSS. | Hapus `!important`, perbaiki selector |
| 4 | 6, 7 | Kontras warna teks sangat rendah (`#bbbbbb` di atas putih) | Sulit dibaca oleh pengguna biasa maupun penderita gangguan penglihatan (WCAG). | Ubah warna ke yang lebih gelap seperti `#333333` |
| 5 | 12-28 | Menggunakan `<div>` secara berlebihan (*divsoup*) tanpa tag semantik | Buruk untuk SEO dan screen reader pembaca disabilitas. | Ganti dengan `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>` |
| 6 | 13, 20, 26 | Menggunakan `<div>` untuk heading dan styling font langsung | Tidak memiliki struktur outline dokumen yang sah secara WCAG/SEO. | Gunakan tag `<h1>`, `<h2>`, dst. |
| 7 | 20, 26 | Menggunakan Inline CSS (`style="..."`) | Menyulitkan pengelolaan gaya secara terpusat (*separation of concerns*). | Pindahkan seluruh style ke file CSS terpisah |
| 8 | 21, 23, 25 | Penggunaan tag `<br>` bertumpuk untuk jarak layout | Tag `<br>` untuk pemisah baris teks, bukan pengatur spasi visual. | Gunakan properti `margin` atau `padding` di CSS |
| 9 | 27-29 | Form tidak memiliki tag `<form>`, `<label>`, dan atribut pendukung | Aksesibilitas buruk (screen reader tidak bisa membaca konteks input). | Bungkus dengan `<form>`, tambahkan `<label for="...">` |

Refleksi:
1. Masalah kontras warna dan ketidakberadaan tag semantik (penggunaan `div` sebagai heading) adalah yang paling sulit disadari hanya dari visual browser. Secara visual teks terlihat besar dan tebal, namun secara struktur dokumen dan aksesibilitas screen reader hal itu cacat.
2. Halaman asli "berfungsi" hanya di perangkat penguji saat itu. Masalah ini tetap penting karena mempengaruhi responsivitas di layar kecil, performa SEO Google, aksesibilitas penderita disabilitas, serta keterbacaan kode saat dikembangkan dalam tim.
3. Saya akan selalu menjalankan W3C Validator dan melakukan pemeriksaan kontras serta responsivitas menggunakan DevTools browser sebelum melakukan pengumpulan/commit kode.

## Bagian 7: Exit ticket
1. Aturan CSS terdiri dari **Selector** (penunjuk elemen HTML mana yang diberi gaya) dan **Blok Deklarasi** yang dibungkus kurung kurawal `{}`. Di dalam deklarasi terdapat pasang **Property** (aspek yang diatur) dan **Value** (nilai pengaturan), yang dipisahkan dengan titik dua `:` dan diakhiri titik koma `;`.
2. Penerapan kalkulasi spesifisitas CSS gabungan (*combinators*) saat selector semakin panjang.
3. Membuat tabel semantik HTML dengan `<thead>`, `<tbody>`, `<th>`, dan `<td>`.