# Website Profile - Alif

Website profil sederhana yang dibuat hanya menggunakan HTML dan CSS (CSS ditulis inline di dalam `<style>` pada `index.html`), tanpa JavaScript, sesuai ketentuan submission Dicoding (menghindari Client-Side Rendering untuk konten dan aset).

## Struktur Proyek

```
website-profile-alif/
├── index.html          # Halaman utama (struktur konten + CSS inline)
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

Semua gambar diambil dari Google Cloud Storage (bucket `bucket-testing-dicoding`):

- Foto profil: `WhatsApp%20Image%202026-09-19%20at%2021.04.10.jpeg`
- Background: `background.svg`
- Ikon GitHub: `icon-github.svg`
- Ikon LinkedIn: `icon-linkedin.svg`
- Ikon Email: `icon-email.svg`

**Penting:** upload 3 file ikon (`icon-github.svg`, `icon-linkedin.svg`, `icon-email.svg`) ke bucket dengan nama persis seperti di atas, atau sesuaikan nama file di `index.html` kalau nama filenya beda.

Referensi ke aset ini ada di `index.html`:
- Tag `<img>` di dalam `.profile-frame` — foto profil
- Properti `background-image` pada `.hero` di dalam blok `<style>` — background
- Tag `<img>` di dalam `.social-links` — ikon GitHub, LinkedIn, Email

## Cara Menjalankan

Buka file `index.html` langsung di browser, atau jalankan lewat live server (opsional) untuk auto-reload saat mengedit.

## Cara Mengganti Foto Profil / Background

**Menggunakan URL eksternal (saat ini):**
Ganti nilai `src` pada tag `<img>` di `index.html` (foto profil) atau nilai `url(...)` pada `.hero` di dalam blok `<style>` (background) dengan URL gambar baru.

**Menggunakan file lokal:**
1. Buat folder `assets/` dan simpan gambar baru di dalamnya.
2. Ubah `src` pada `<img>` di `index.html` menjadi path lokal, misal `assets/profile.jpg`.
3. Ubah `background-image` pada `.hero` di dalam blok `<style>` menjadi `url("assets/background.svg")` atau nama file lokal lainnya.
4. Tambahkan `COPY assets/ /usr/share/nginx/html/assets/` di `Dockerfile` supaya folder ikut ke-copy ke image.

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
