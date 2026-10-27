# 📘 PANDUAN LENGKAP PENGGUNAAN & PENGELOLAAN SISTEM
## SIKAP — BKPSDM KOTA DUMAI
**Sistem Informasi Kepegawaian dan Administrasi Pegawai**  
*Badan Kepegawaian dan Pengembangan Sumber Daya Manusia Kota Dumai*

---

## 📌 1. Ringkasan Aplikasi

**SIKAP BKPSDM Kota Dumai** adalah portal web layanan kepegawaian mandiri dan informasi resmi terpadu bagi Aparatur Sipil Negara (ASN) di lingkungan Pemerintah Kota Dumai.

Aplikasi ini dibangun menggunakan arsitektur modern yang ringan dan responsif:
- **Backend Server**: Node.js dengan framework **Express.js** untuk mengelola server web, REST API, dan penanganan unggah file.
- **Database**: **JSON Flat-File Database (`data/db.json`)** yang memungkinkan aplikasi berjalan cepat tanpa dependensi database berat seperti MySQL/PostgreSQL.
- **Keamanan**: Password terenkripsi dengan **Bcrypt Hashing**, pembatasan jenis file unggahan (*MIME filter*), serta batasan ukuran file maksimal **5 MB**.

---

## 🖥️ 2. Persyaratan Sistem (Prerequisites)

Sebelum menjalankan aplikasi, pastikan perangkat server atau komputer Anda telah memenuhi persyaratan berikut:

| Kebutuhan | Spesifikasi Minimal | Cara Cek di Terminal |
|---|---|---|
| **Node.js** | Versi `v18.0.0` atau lebih baru | `node -v` |
| **NPM (Node Package Manager)** | Versi `v9.0.0` atau lebih baru | `npm -v` |
| **Browser Web** | Chrome, Edge, Firefox, Safari (Versi Terbaru) | — |
| **Ruang Penyimpanan** | Minimal 500 MB (Tergantung jumlah file upload) | — |

---

## 🚀 3. Cara Menjalankan Server Node.js

Berikut adalah panduan langkah demi langkah untuk menjalankan aplikasi di lingkungan lokal atau server production:

### 📥 Langkah 1: Buka Terminal / PowerShell
- **Windows**: Buka folder `SIKAP_BKPSDM_KOTA_DUMAI`, tekan `Shift + Klik Kanan` pada area kosong, lalu pilih **Open PowerShell window here** atau **Open in Terminal**.
- **Linux / macOS**: Buka aplikasi **Terminal**, lalu gunakan perintah `cd` ke lokasi folder proyek:
  ```bash
  cd /path/to/SIKAP_BKPSDM_KOTA_DUMAI
  ```

---

### 📦 Langkah 2: Install Dependensi (Hanya Saat Setup Pertama)
Jalankan perintah berikut di terminal untuk mengunduh modul-modul yang dibutuhkan:
```bash
npm install
```
> [!NOTE]
> Perintah ini mengunduh modul dependensi seperti `express`, `cors`, `multer`, dan `bcryptjs` ke dalam folder `node_modules`.

---

### ⚙️ Langkah 3: Jalankan Node Server
Jalankan perintah berikut di terminal:
```bash
node server.js
```
atau menggunakan skrip npm:
```bash
npm start
```

Setelah server aktif, terminal akan menampilkan respon:
```text
SIPADU Local Backend Server is running at http://localhost:3000
```

> [!TIP]
> **Akses Portal Web**:
> - **Portal Utama Publik**: [http://localhost:3000](http://localhost:3000)
> - **Dashboard Admin Web**: [http://localhost:3000/admin.html](http://localhost:3000/admin.html)

---

### 🛑 Langkah 4: Menghentikan Server
Untuk mematikan Node server, tekan **`Ctrl + C`** pada jendela terminal. Ketik `Y` jika diminta konfirmasi penghentian.

---

### 🔄 Menjalankan Server Otomatis 24/7 (Menggunakan PM2 di VPS / Server Production)
Agar aplikasi tetap aktif di latar belakang meskipun terminal ditutup atau komputer di-restart:

1. **Install PM2 secara Global**:
   ```bash
   npm install -g pm2
   ```
2. **Jalankan Aplikasi dengan PM2**:
   ```bash
   pm2 start server.js --name "sikap-bkpsdm"
   ```
3. **Perintah Pengelolaan PM2**:
   - 📊 **Cek Status**: `pm2 status`
   - 📜 **Lihat Log Sistem**: `pm2 logs sikap-bkpsdm`
   - 🔄 **Restart Server**: `pm2 restart sikap-bkpsdm`
   - 🛑 **Stop Server**: `pm2 stop sikap-bkpsdm`

---

## 🔐 4. Akun Akses Administrator Default

> [!IMPORTANT]
> Untuk alasan keamanan, segera ubah Username & Password default setelah login pertama kali melalui menu **"Ubah Username & Password"** di Dashboard Administrator.

| Peran (Role) | Username Default | Password Default | Hak Akses & Tanggung Jawab |
|---|---|---|---|
| **Admin Web (Super Admin)** | `adminweb` | `sikap2026` | Pengelolaan penuh seluruh konten portal (Pengumuman, Kegiatan, Layanan, Hero Banner, Aplikasi ASN, Kontak, & Profil) |
| **Admin Staf** | `adminstaf` | `staf2026` | Pengelolaan Direktori Staf & Status Kehadiran Pejabat |

---

## 💡 5. Fitur Utama & Cara Penggunaan

### 📢 A. Pengumuman Kepegawaian (`pengumuman.html`)
- **Pencarian Real-Time & Filter Kategori**: Cari pengumuman berdasarkan judul, nomor surat, atau kata kunci isi. Filter berdasarkan kategori (*CPNS/PPPK, Kepangkatan, Diklat, Mutasi, Pensiun*).
- **Tombol Reset Pencarian (X)**: Klik ikon **(X)** atau hapus teks pencarian untuk mereset dan menampilkan kembali seluruh pengumuman sesuai kategori pill yang aktif.
- **Status & Prioritas**: Pengumuman dengan status `Urgent / Penting` akan diberi penanda khusus berwarna merah berkilau di bagian atas kartu.

---

### 📋 B. Layanan Kepegawaian & Persyaratan (`layanan.html`)
- **Penulisan Sub-Judul Kelompok Persyaratan**:
  Dalam pengisian daftar persyaratan layanan di Admin Web, gunakan tanda **`-`** di awal baris atau akhiri baris dengan tanda **`:`** untuk membuat **Judul Sub-Kelompok**.
  
  *Contoh format penulisan di form Admin:*
  ```text
  - Mutasi Masuk Pemerintah Kota Dumai :
  1. Asli Surat Permohonan diatas materai
  2. FC Legalisir SK Pangkat Terakhir
  
  - Syarat Mutasi Keluar :
  1. Asli Surat Permohonan diatas materai
  2. FC Legalisir SKP 2 Tahun Terakhir
  ```
  Sistem akan otomatis merender judul sub-kelompok dengan desain banner elegan dan mereset penomoran item di bawahnya mulai dari `01`, `02`, dst.

- **Tautan Akses External / Google Drive (Opsional)**:
  Setiap layanan mendukung tautan tambahan (seperti folder Google Drive atau form online). Jika diisi, tombol **`🔗 Buka Link / Drive`** akan muncul di kartu layanan serta di dalam modal detail.

---

### 👁️ C. Widget Counter Pengunjung Website
- Menampilkan jumlah total kunjungan ke portal secara live dengan desain *glassmorphism neon gold glowing*.
- Tampilan widget counter ini dapat diaktifkan atau disembunyikan melalui Admin Web (Tab Home Stats).

---

### 📁 D. Ketentuan & Batasan Unggah File (File Upload)

> [!WARNING]
> Batas maksimal ukuran file yang diunggah adalah **5 MB** per file.

| Jenis File | Ekstensi Diizinkan | Keterangan |
|---|---|---|
| **Dokumen Lampiran / SK** | `.pdf` | Lampiran pengumuman atau formulir persyaratan layanan |
| **Foto / Gambar / Logo** | `.jpg`, `.jpeg`, `.png`, `.webp`, `.svg`, `.gif` | Foto thumbnail pengumuman, banner hero, foto kegiatan, dan logo aplikasi |

Jika file melebihi 5 MB atau format tidak sesuai, sistem akan secara otomatis membatalkan unggahan dan menampilkan notifikasi pesan kesalahan di layar.

---

## 📂 6. Struktur Folder & File Proyek

```text
SIKAP_BKPSDM_KOTA_DUMAI/
├── server.js                   # Entry point server Express.js & REST API
├── package.json                # Dependensi modul & konfigurasi skrip Node
├── PANDUAN.md                  # Dokumentasi panduan penggunaan & deployment
│
├── data/
│   └── db.json                 # Flat-file Database (Pengumuman, Layanan, Staf, Slides, dll)
│
├── uploads/                    # Folder penyimpanan gambar slider, foto staf, & dokumen PDF
│
├── admin.html                  # Dashboard Pengelolaan Administrator
├── index.html                  # Halaman Beranda Utama Portal SIKAP
├── pengumuman.html             # Halaman Daftar Pengumuman & Berita
├── pengumuman-detail.html      # Halaman Detail Pengumuman & Lampiran PDF
├── kegiatan.html               # Halaman Berita Dokumentasi Kegiatan
├── layanan.html                # Halaman Informasi Layanan & Persyaratan Mandiri
├── aplikasi.html               # Portal Layanan Aplikasi ASN (SIASN, E-Kinerja, SIMPEG, dll)
├── profil.html                 # Halaman Visi Misi, Sejarah, & Pimpinan Instansi
├── staf.html                   # Halaman Direktori Staf & Status Kehadiran
├── alur.html                   # Halaman Alur Prosedur Pelayanan Mandiri
└── kontak.html                 # Halaman Alamat Kantor & Peta Lokasi
```

---

## 🛠️ 7. Pemecahan Masalah (Troubleshooting)

### ❓ 1. Error `EADDRINUSE: address already in use :::3000`
- **Penyebab**: Port 3000 sedang digunakan oleh aplikasi lain atau instance Node server yang belum dihentikan.
- **Solusi**:
  Jalankan server pada port alternatif (misal Port 3001):
  - **Windows PowerShell**:
    ```powershell
    $env:PORT=3001; node server.js
    ```
  - **Linux / macOS**:
    ```bash
    PORT=3001 node server.js
    ```

### ❓ 2. Error `Cannot find module 'express'`
- **Penyebab**: Folder `node_modules` belum diinstall.
- **Solusi**: Jalankan perintah `npm install` pada terminal hingga selesai.

### ❓ 3. Cara Backup Data Sistem
- **Solusi**: Untuk mencadangkan data portal, cukup salin file `data/db.json` dan folder `uploads/` ke lokasi cadangan yang aman.

---

*© 2026 BKPSDM Kota Dumai — Sistem Informasi Kepegawaian dan Administrasi Pegawai*
