# Panduan Pemasangan & Penyelenggaraan Sistem

Dokumen ini ditujukan kepada pembangun perisian atau pentadbir teknikal yang ingin memasang, menjalankan, dan menyelenggara aplikasi **G-TACR MS ISO/IEC 17025 LIMS** pada komputer tempatan (*local machine*) atau pelayan pengeluaran.

---

## 💻 1. Keperluan Sistem Minimum

Sebelum memulakan pemasangan, pastikan persekitaran komputer anda mempunyai:

* **Node.js:** Versi `20.x` atau lebih baharu (disyorkan versi LTS terkini).
* **Pengurus Pakej (*Package Manager*):** `npm` versi `10.x` ke atas (disertakan bersama pemasangan Node.js).
* **Sistem Operasi:** Windows 10/11, macOS, atau Linux (Ubuntu 22.04+ disyorkan).
* **Pelayar Web Moden:** Google Chrome, Microsoft Edge, Mozilla Firefox, atau Safari versi terkini yang menyokong standard ES2022 dan CSS moden.

---

## 📥 2. Langkah Pemasangan Tempatan

Ikuti empat (4) langkah mudah berikut:

### Langkah 2.1: Dapatkan Kod Sumber
Klonkan repositori projek ini ke komputer anda menggunakan Git:
```bash
git clone <URL_REPOSITORI_ANDA>
cd gtacr-iso17025-lims
```

### Langkah 2.2: Pasang Pakej Kebergantungan (*Dependencies*)
Jalankan arahan berikut untuk memuat turun semua pustaka yang diperlukan mengikut fail `package.json`:
```bash
npm install
```
*Tujuan Langkah:* Pakej seperti React 19, Tailwind CSS v4, Lucide Icons, dan Vite akan dimuat turun ke dalam folder `node_modules`.

### Langkah 2.3: Sediakan Fail Konfigurasi Persekitaran (*Environment Variables*)
Salin templat fail `.env.example` kepada `.env`:
```bash
cp .env.example .env
```
*Penerangan Pemboleh Ubah:*
* `GEMINI_API_KEY`: Disediakan sebagai placeholder sekiranya ciri AI berasaskan Gemini diaktifkan pada fasa akan datang. Sistem ini boleh berjalan sepenuhnya tanpa mengisi nilai kunci ini.
* `APP_URL`: URL asas aplikasi (lalai: `http://localhost:3000`).

---

## 🚀 3. Menjalankan Aplikasi

### Mod Pembangunan (*Development Server*)
Untuk memulakan pelayan pembangunan tempatan dengan kemas kini pantas:
```bash
npm run dev
```
* Perkhidmatan akan bermula pada alamat: `http://localhost:3000`
* Buka pelayar web dan layari URL tersebut untuk menggunakan aplikasi.

### Mod Semakan Kod (*Code Linting / Type Checking*)
Untuk memastikan tiada kesilapan jenis data TypeScript:
```bash
npm run lint
```
*Arahan ini menjalankan `tsc --noEmit` bagi mengesahkan ketepatan kod tanpa menghasilkan fail binaan.*

### Mod Binaan Pengeluaran (*Production Build*)
Untuk membina fail statik yang telah dimampatkan dan sedia untuk pelayan pengeluaran:
```bash
npm run build
```
* Hasil binaan yang optimum akan disimpan di dalam folder `/dist`.

### Menguji Binaan Pengeluaran Secara Tempatan (*Preview Build*)
Untuk menguji hasil binaan folder `/dist` sebelum dimuat naik ke pelayan:
```bash
npm run preview
```

---

## 🏗️ 4. Struktur Fail & Folder Utama

Berikut adalah ringkasan susunan struktur projek:

```
├── docs/                       # Dokumentasi lengkap sistem
│   ├── PANDUAN-PENGGUNA.md     # Panduan langkah demi langkah 4 peranan
│   ├── KEPERLUAN-PRODUK.md     # Spesifikasi PRD & standard ISO 17025
│   ├── STATUS-DAN-ROADMAP.md   # Status binaan, ujian & perancangan
│   ├── DATA-DAN-PRIVASI.md     # Ketelusan data & keselamatan
│   └── SETUP-DAN-PENYELENGGARAAN.md # Dokumen teknikal ini
├── public/                     # Fail aset statik awam
│   └── assets/aistudio/        # Logo LGM, lambang G-TACR & salinan PRD PDF
├── src/                        # Kod sumber aplikasi
│   ├── components/             # Komponen antaramuka mengikut modul
│   │   ├── analysis/           # Modul senarai kerja & ujian jurukimia
│   │   ├── audit/              # Modul paparan jejak audit (Audit Trail)
│   │   ├── coa/                # Sijil Analisis & format cetakan
│   │   ├── dashboard/          # Papan pemuka & penjejak masa TAT
│   │   ├── finance/            # Sebut harga, invois & pintu bayaran
│   │   ├── layout/             # Header, bar peranan & menu tepi (Sidebar)
│   │   ├── registration/       # Pemeriksaan fizikal sampel & kod makmal
│   │   └── review/             # Semakan teknikal & tandatangan kripto
│   ├── context/                # Pengurusan keadaan data global (LIMSContext)
│   ├── data/                   # Data rujukan piawai & set demonstrasi asal
│   ├── types/                  # Definisi jenis data TypeScript (lims.ts)
│   ├── App.tsx                 # Titik masuk utama komponen aplikasi
│   ├── index.css               # Konfigurasi Tailwind CSS & gaya cetakan
│   └── main.tsx                # Titik pelancaran React DOM
├── .env.example                # Templat pemboleh ubah persekitaran selamat
├── .gitignore                  # Senarai fail dikecualikan daripada Git
├── CHANGELOG.md                # Rekod sejarah perubahan versi
├── package.json                # Maklumat pakej kebergantungan & skrip
├── README.md                   # Penerangan umum projek untuk orang awam
├── tsconfig.json               # Konfigurasi pengkompil TypeScript
└── vite.config.ts              # Konfigurasi binaan Vite
```

---

## 🛠️ 5. Penyelesaian Masalah Teknikal Biasa

### Isu 1: Ralat Port 3000 Telah Digunakan (*Port 3000 in use*)
* **Punca:** Terdapat aplikasi lain yang sedang berjalan pada port 3000.
* **Penyelesaian:** Hentikan proses lama tersebut, atau ubah konfigurasi port di dalam `package.json` pada bahagian skrip `"dev"` (contoh: `vite --port=3001`).

### Isu 2: Masalah Binaan Selepas Kemas Kini (*Node Modules Corrupted*)
* **Penyelesaian:** Bersihkan fail pemasangan lama dan pasang semula kebergantungan:
  ```bash
  rm -rf node_modules package-lock.json
  npm install
  ```

### Isu 3: Sijil COA Dicetak Bersama Tajuk Laman dan Tarikh Pelayar
* **Penyelesaian:** Pada tetingkap cetakan pelayar (*Print Dialog*), buka bahagian tetapan lanjutan (*More settings*) dan nyah-tandakan (*uncheck*) pilihan **Headers and footers**.
