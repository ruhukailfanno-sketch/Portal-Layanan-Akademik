# Portal Layanan Akademik – Pertemuan 5 (Responsive & Accessible Web Client)

Satu halaman web client untuk layanan akademik: 4 kartu layanan dan 1 form permohonan. Tanpa JavaScript.

## Struktur
```
index.html
css/styles.css
img/logo.svg, img/ilustrasi.svg
evidence/   (screenshot bukti pengujian)
README.md
```

## Keputusan desain
- **Semantik:** `header`, `nav` (dengan `aria-label`), `main`, `section` (masing-masing `aria-labelledby`), `article` untuk kartu, `footer`. Heading: satu `h1`, `h2` per section, `h3` per kartu. Level ditentukan oleh struktur, bukan ukuran visual.
- **Mobile-first:** CSS dasar 1 kolom. Breakpoint ditambahkan karena konten, bukan nama perangkat: `40rem` (kartu jadi 2 kolom) dan `64rem` (kartu 4 kolom dan intro 2 kolom) menggunakan CSS Grid; header/nav memakai Flexbox.
- **Form:** 6 field; setiap `label for` terhubung ke `id`. Tipe `email`, `select`, `radio` dalam `fieldset/legend`, `textarea`. Validasi HTML: `required`, `minlength`, `maxlength`, `pattern` (NIM). Tombol memakai `<button type="submit">`. Petunjuk dihubungkan dengan `aria-describedby`.
- **Aksesibilitas:** skip link, `:focus-visible` outline 3px, target klik minimal 44px, warna teks kontras tinggi, `lang="id"`, ARIA hanya seperlunya (elemen native lebih dulu).
- **Gambar:** `logo.svg` dan `ilustrasi.svg` informatif sehingga memiliki `alt` bermakna. Tidak ada gambar dekoratif, jadi tidak ada `alt=""`. Ukuran `width`/`height` diatur untuk mencegah layout shift.

## Hasil pemeriksaan DevTools / uji otomatis
| Viewport | scrollWidth | Horizontal scroll | Kolom kartu |
|---|---|---|---|
| 360 px | 360 | Tidak ada | 1 |
| 768 px | 768 | Tidak ada | 2 |
| 1280 px | 1280 | Tidak ada | 4 |

- **Network:** reload halaman, seluruh resource (HTML, CSS, 2 SVG) berhasil dimuat, tidak ada status 4xx/5xx.
- **Elements/Inspector:** box model kartu dan form diperiksa; `box-sizing: border-box` global mencegah overflow.
- **Keyboard:** Tab pertama menuju skip link, lalu nav, kartu, dan form. Focus indicator terlihat (`evidence/02-focus-skip-link.png`).
- **Validasi form:** kolom nama kosong ditolak (`valueMissing`); email `bukan-email` ditolak browser dengan pesan format (`evidence/03-validasi-form.png`).

> Catatan: pengujian di atas dijalankan dengan Chromium headless (Playwright). Untuk laporan, ulangi langkah yang sama di DevTools browser Anda (Responsive Mode, Network, Accessibility panel) dan tambahkan capture-nya ke `evidence/`.

## Menjalankan
Buka `index.html` di browser, atau jalankan `python3 -m http.server`.
