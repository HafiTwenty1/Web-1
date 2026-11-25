# Laporan Praktikum Pertemuan 10 — Pemrograman Web 1

Nama : Ahmad Hafi Badali
NIM : ...
Kelas : ...

## Percobaan 1 — Navbar Lab

| No | Eksperimen | Pengamatan |
|---|---|---|
| 1 | Class #menuLab dan aria-expanded saat terbuka | Terbuka: `collapse show`, tombol `aria-expanded="true"`. Tertutup: `collapse`, `false`. |
| 2 | Hamburger di 1000 px dengan navbar-expand-lg | Tidak tampil; menu berderet horizontal (1000 px ≥ 992 px). |
| 3 | Perilaku di 800 px | `-md`: menu berderet. `navbar-expand`: selalu berderet, hamburger tak muncul. Tanpa class expand: selalu terlipat, bahkan di desktop. |
| 4 | data-bs-target salah ketik | Tombol tidak membuka apa pun karena tidak ada elemen `id="menu"`; Console belum tentu menampilkan galat, cek manual di HTML. |
| 5 | Tanpa JS bundle | Tampilan (CSS) tetap ada, tetapi hamburger dan dropdown tidak bereaksi (perilaku JS hilang). |
| 6 | bg-dark tanpa/dengan data-bs-theme="dark" | Tanpa: latar gelap, teks menu gelap sehingga hampir tak terbaca. Dengan: teks dan ikon hamburger menjadi terang. |
| 7 | sticky-top vs fixed-top | sticky-top: menempel saat digulir, judul tidak tertutup. fixed-top: keluar dari aliran dokumen sehingga judul "Konten halaman" tertutup. |

## Percobaan 2 — Buttons & Badges

| No | Eksperimen | Pengamatan |
|---|---|---|
| 1 | Batal–Simpan di 375 px dan 1000 px | 375 px: bertumpuk selebar penuh (`d-grid`). 1000 px: sebaris, rata kanan (`d-md-flex justify-content-md-end`). |
| 2 | Elemen nonaktif yang masih bisa difokus | `<button disabled>` dilewati Tab. Tautan hanya ber-class `disabled` (masih ber-href) tetap bisa difokus dan diaktifkan dengan Enter. Tautan tanpa href + `aria-disabled="true"` tidak menerima fokus. |
| 3 | Kontras text-bg-warning vs bg-warning | `text-bg-warning`: teks gelap di atas kuning (kontras AA). `bg-warning` saja: teks putih bawaan badge, kontras rendah. |
| 4 | Nama tombol Notifikasi | Dengan `visually-hidden`: "Notifikasi 3 notifikasi belum dibaca". Tanpa: "Notifikasi 3". |

## Percobaan 3 — Tipografi

| Class lama | Utilitas pengganti | Tampilan sama? |
|---|---|---|
| .judul-besar | `display-5 text-center` | Ya |
| .pembuka | `lead text-body-secondary text-center` | Ya |
| .label | `text-uppercase fw-bold small` | Hampir (letter-spacing hilang, boleh diabaikan) |
| .catatan | `small fst-italic` | Ya |
| .nim | `font-monospace` | Ya |
| Temuan Lighthouse untuk `<h4>` | Heading tidak berurutan menurun (h1 langsung ke h4). Solusi: tetap `<h2 class="h4">`. | — |

![Sebelum](p3-tipografi/sebelum.png) ![Sesudah](p3-tipografi/sesudah.png)


## Jawaban Pertanyaan Analisis

1. Saat hamburger diklik, JavaScript Bootstrap membaca `data-bs-target`, memilih elemen target dengan selector (seperti `querySelector`/`getElementById`), lalu mengubah class-nya (`collapse` ↔ `collapse show`) dan atribut `aria-expanded` tombol. Ini manipulasi DOM yang dipicu event `click`, sama dengan materi pertemuan 6 (seleksi elemen, event listener, ubah class/atribut).
2. CSS Bootstrap (tampilan) dan JS Bootstrap (perilaku) dimuat terpisah. Tanpa bundle JS, class dan gaya tetap berlaku sehingga navbar tampil, tetapi tidak ada event listener yang mengubah DOM, sehingga interaksi hilang.
3. Class `disabled` hanya mengubah tampilan (`pointer-events: none`, warna pudar). Tautan masih ber-`href` tetap bisa difokus dengan Tab dan diaktifkan dengan Enter, dan pembaca layar tidak diberi tahu bahwa tautan nonaktif. Pengguna keyboard bisa mengaksesnya, jadi perlu `aria-disabled="true"`, `tabindex="-1"`, dan idealnya tanpa `href`.
4. (a) Hierarki heading tetap benar (h1 → h2) sehingga lolos audit aksesibilitas dan mudah dinavigasi pembaca layar/SEO; (b) ukuran tampilan tetap diatur terpisah dengan class `h5`, sehingga struktur semantik dan gaya visual tidak saling terikat.
5. Skor Lighthouse Accessibility: ... Temuan yang diperbaiki: ... (isi setelah menjalankan Lighthouse).

## Kesimpulan

Navbar responsif hanya berfungsi bila tiga syarat terpenuhi: class `navbar-expand-*`, `data-bs-target` yang sama dengan `id` area collapse, dan JS bundle termuat. Pemilihan varian tombol, atribut disabled yang benar, dan badge dengan teks `visually-hidden` meningkatkan makna serta aksesibilitas. Utilitas tipografi Bootstrap menggantikan CSS manual tanpa mengubah tampilan, sambil menjaga hierarki heading. Penerapan pada dashboard SIAKAD Mini membuat tampilan lebih konsisten dan mudah dirawat.
