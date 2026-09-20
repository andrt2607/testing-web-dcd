## Cara Menjalankan

Buka file `index.html` langsung di browser, atau jalankan lewat live server (opsional) untuk auto-reload saat mengedit.

## Cara Mengganti Foto Profil / Background

**Menggunakan URL eksternal (saat ini):**
Ganti nilai `src` pada tag `<img>` di `index.html` (foto profil) atau nilai `url(...)` pada `.hero` di `css/style.css` (background) dengan URL gambar baru.

**Menggunakan file lokal:**
1. Simpan gambar baru ke folder `assets/`.
2. Ubah `src` pada `<img>` di `index.html` menjadi path lokal, misal `assets/profile.jpg`.
3. Ubah `background-image` pada `.hero` di `css/style.css` menjadi `url("../assets/background.svg")` atau nama file lokal lainnya.
