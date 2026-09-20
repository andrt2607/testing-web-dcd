# Website Profile - Alif

Website profil sederhana yang dibuat hanya menggunakan HTML dan CSS (CSS ditulis inline di dalam `<style>` pada `index.html`), tanpa JavaScript, sesuai ketentuan submission Dicoding (menghindari Client-Side Rendering untuk konten dan aset).

## Struktur Proyek

```
website-profile-alif/
├── index.html          # Halaman utama (struktur konten + CSS inline)
├── assets/
│   ├── background.svg          # Aset gambar background (fallback lokal)
│   └── avatar-placeholder.svg  # Aset placeholder foto profil (fallback lokal)
├── Dockerfile           # Container nginx untuk deploy ke Cloud Run
├── .dockerignore
└── README.md
```

## Fitur

- Halaman profil dengan bagian hero, tentang saya, keahlian, dan kontak.
- Frame foto profil berbentuk lingkaran yang menampilkan foto dari URL eksternal.
- Gambar background full-page yang diambil dari URL eksternal.
- Desain responsif untuk tampilan mobile.
- Murni HTML & CSS (CSS inline di `index.html`), tidak ada JavaScript.

## Sumber Aset

Foto profil dan gambar background saat ini diambil dari Google Cloud Storage:

- Foto profil: `https://storage.googleapis.com/bucket-testing-dicoding/WhatsApp%20Image%202026-09-19%20at%2021.04.10.jpeg`
- Background: `https://storage.googleapis.com/bucket-testing-dicoding/background.svg`

Referensi ke aset ini ada di `index.html`:
- Tag `<img>` di dalam `.profile-frame` — foto profil
- Properti `background-image` pada `.hero` di dalam blok `<style>` — background

Aset lokal di folder `assets/` tetap disimpan sebagai cadangan/fallback bila ingin kembali menggunakan aset lokal.

## Cara Menjalankan

Buka file `index.html` langsung di browser, atau jalankan lewat live server (opsional) untuk auto-reload saat mengedit.

## Cara Mengganti Foto Profil / Background

**Menggunakan URL eksternal (saat ini):**
Ganti nilai `src` pada tag `<img>` di `index.html` (foto profil) atau nilai `url(...)` pada `.hero` di dalam blok `<style>` (background) dengan URL gambar baru.

**Menggunakan file lokal:**
1. Simpan gambar baru ke folder `assets/`.
2. Ubah `src` pada `<img>` di `index.html` menjadi path lokal, misal `assets/profile.jpg`.
3. Ubah `background-image` pada `.hero` di dalam blok `<style>` menjadi `url("assets/background.svg")` atau nama file lokal lainnya.

## Deploy ke Cloud Run (GCP)

Website ini disajikan lewat container nginx (`Dockerfile`) yang listen di port 8080, sesuai kontrak port Cloud Run.

Build & deploy pakai Cloud Build + Cloud Run:

```bash
gcloud builds submit --tag gcr.io/PROJECT_ID/website-profile-alif

gcloud run deploy website-profile-alif \
  --image gcr.io/PROJECT_ID/website-profile-alif \
  --platform managed \
  --region REGION \
  --allow-unauthenticated
```

Ganti `PROJECT_ID` dengan ID project GCP dan `REGION` dengan region tujuan (misal `asia-southeast2`).

Uji coba container secara lokal:

```bash
docker build -t website-profile-alif .
docker run -p 8080:8080 website-profile-alif
```

Lalu buka `http://localhost:8080`.
