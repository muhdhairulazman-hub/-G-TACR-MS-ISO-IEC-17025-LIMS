# Log Perubahan (Changelog)

Semua perubahan dan evolusi pembangunan aplikasi **G-TACR MS ISO/IEC 17025 LIMS** direkodkan di sini berasaskan komitmen dan binaan sebenar. Format dokumen ini berpandukan prinsip [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [1.0.0] - 2026-11-12

### Ditambah (Added)
* **Pengasingan Kuasa 4 Peranan (*Segregation of Duties*):**
  * Pelaksanaan kawalan peranan: Admin/CS, Pegawai Penerima Sampel (SRO), Jurukimia (Analyst), dan Pengurus Teknikal (Technical Manager).
  * Modal panduan Matriks Kuasa ISO 17025 Fasal 5.2 dan 6.2.
* **Pintu Kawalan Bayaran Awal (*Pre-Payment Gating*):**
  * Modul Sebut Harga (*Quotation*) dengan pengiraan SST 6%.
  * Penjanaan Invois rasmi dan pengesahan status `PAID`.
  * Sekatan automatik pendaftaran sampel sekiranya invois belum dibayar.
* **Log Pemeriksaan Keadaan Sampel (*Sample Condition Log*):**
  * Semakan suhu penerimaan dengan had amaran $\le$ 6.0°C bagi sampel organik/alam sekitar mengikut Fasal 7.4.
  * Semakan keutuhan bekas, lak keselamatan, padanan label, dan borang rantai jagaan.
  * Penjanaan kod sampel makmal automatik berformat `LAB-2026-XXXX`.
* **Modul Pengujian Makmal (*Lab Testing*):**
  * Paparan senarai kerja (*Worklist*) jurukimia mengikut sampel berdaftar.
  * Input keputusan multi-parameter (fizikal, kimia, logam berat) berpandukan kaedah ASTM/APHA/ISO.
  * Semakan kawalan kualiti (*QC Passed*) dan rekod instrumen makmal.
* **Modul Kelulusan & Semakan Teknikal:**
  * Semakan teknikal bebas oleh Pengurus Teknikal.
  * Fungsi penolakan draf (*Reject & Return*) berserta ulasan pembetulan.
  * Kelulusan rasmi dengan penjanaan tandatangan digital kriptografi (cincangan SHA-256).
  * Pengurusan semakan versi laporan (*Revision Control*).
* **Penjejak Masa TAT 7 Hari Bekerja (*Turn-Around Time Countdown*):**
  * Kiraan automatik baki hari bekerja dari tarikh pendaftaran sampel.
  * Penunjuk status berkod warna: Hijau (Selamat), Kuning (Amaran), Merah (Kritikal/Lewat), dan Kelabu (Selesai).
* **Sijil Analisis (COA) & Cetakan:**
  * Reka bentuk Sijil Analisis berformat piawai G-TACR SAMM No. 008.
  * Lembaran gaya `@media print` untuk cetakan kemas terus ke kertas A4 tanpa butang menu.
  * Simulasi muat turun laporan teks/mentah dan status serahan pelanggan.
* **Jejak Audit Automatik (*Audit Trail Log*):**
  * Perekodan peristiwa secara automatik bagi setiap aktiviti utama dengan cap masa dan identiti pelaksana.
* **Dokumentasi Lengkap Repositori:**
  * Penulisan `README.md`, `docs/PANDUAN-PENGGUNA.md`, `docs/KEPERLUAN-PRODUK.md`, `docs/STATUS-DAN-ROADMAP.md`, `docs/DATA-DAN-PRIVASI.md`, `docs/SETUP-DAN-PENYELENGGARAAN.md`, dan `CHANGELOG.md` dalam Bahasa Melayu yang jelas dan berintegriti.
