# Pengendalian Data & Privasi

Dokumen ini menjelaskan secara telus jenis data yang diuruskan oleh aplikasi **G-TACR MS ISO/IEC 17025 LIMS**, di mana data tersebut disimpan, sempadan keselamatan, serta cara data tersebut dikendalikan dalam versi semasa.

---

## 📥 1. Jenis Data yang Dikendalikan

Aplikasi ini memproses beberapa kategori data bagi tujuan pengurusan makmal pengujian:

1. **Maklumat Pelanggan & Perniagaan:**
   * Nama wakil pelanggan, nama syarikat/organisasi, alamat emel perniagaan, dan nombor telefon.
   * Butiran sebut harga, nombor rujukan invois, nilai bayaran perkhidmatan, dan nombor rujukan transaksi kewangan.
2. **Maklumat Sampel Makmal:**
   * Nama dan deskripsi sampel fizikal (cth: Lateks Pekat, Getah Standard Malaysia - SMR 20).
   * Matriks bahan, tarikh persampelan, dan tarikh penerimaan.
   * Rekod keadaan fizikal sampel: bacaan suhu penerimaan (°C), status bekas, status lak keselamatan, dan semakan label.
3. **Data Keputusan Eksperimen & Analisis:**
   * Nilai parameter ujian kimia dan fizikal (cth: peratusan abu, kandungan kotoran, paras logam berat, dsb.).
   * Anggaran ketidakpastian pengukuran (*measurement uncertainty*).
   * Rujukan alat/instrumen makmal dan status lulus kawalan kualiti (*QC Passed*).
   * Catatan ulasan jurukimia dan pengurus teknikal.
4. **Log Jejak Audit (*Audit Trail Log*):**
   * Rekod nama staf pelaksana, peranan yang aktif, jenis tindakan yang dibuat, cap tarikh dan masa (*timestamp*), serta cincangan kriptografi tandatangan digital.

---

## 💾 2. Di Mana Data Disimpan?

* **Penyimpanan Setempat Sahaja (*Client-Side Local Storage*):**  
  Dalam pelaksanaan semasa, **semua data disimpan secara setempat di dalam pelayar web pengguna** menggunakan mekanisme piawai HTML5 Web Storage (`localStorage`).
* **Kunci Storan yang Digunakan:**
  * `gtacr_lims_quotes_samm008_v1` (Rekod Sebut Harga)
  * `gtacr_lims_invoices_samm008_v1` (Rekod Invois & Bayaran)
  * `gtacr_lims_samples_samm008_v1` (Rekod Sampel & Keputusan Ujian)
  * `gtacr_lims_audit_logs_samm008_v1` (Rekod Jejak Audit)
  * `gtacr_lims_active_role_samm008_v1` (Status Peranan Semasa)
* **Tiada Pelayan Luaran Disambung:**  
  Data **TIDAK** dipindahkan atau dimuat naik ke mana-mana pangkalan data awan terpusat (*cloud database*), pelayan pihak ketiga, atau sistem storan luaran.

---

## 🤖 3. Adakah Data Dihantar kepada AI atau Perkhidmatan Pihak Ketiga?

* **Tiada Penghantaran Data ke AI:**  
  Walaupun pakej pustaka `@google/genai` terdapat di dalam fail manifes `package.json`, kod sumber aplikasi semasa **TIDAK membuat sebarang panggilan API atau menghantar data kepada model bahasa raya (LLM) atau perkhidmatan AI luaran**.
* **Operasi Sepenuhnya Luar Talian / Terkandung (*Self-Contained*):**  
  Keseluruhan pengiraan harga, penjejakan TAT, dan penjanaan cincangan SHA-256 dilakukan secara langsung oleh enjin JavaScript pelayar web anda tanpa interaksi pelayan luaran.

---

## 🔐 4. Siapa yang Boleh Mengakses Data Ini?

Berdasarkan pelaksanaan semasa:

1. **Akses Fizikal Peranti:**  
   Sesiapa sahaja yang mempunyai akses kepada komputer, profil pelayar web, atau sesi pelayar yang sama boleh melihat dan mengubah data yang tersimpan di dalam `localStorage`.
2. **Kawalan Peranan di Peringkat Antara Muka (*UI-Level Role Control*):**  
   Pengasingan kuasa yang dipaparkan dalam aplikasi (Admin, SRO, Chemist, Tech Manager) adalah kawalan berasaskan antara muka (*front-end logic*) untuk tujuan demonstrasi aliran kerja ISO 17025. Ia belum dilindungi oleh sistem kata laluan peribadi (*User Authentication*) atau token keselamatan sesi (*JWT / OAuth*).

---

## 🗑️ 5. Cara Memadam atau Menetapkan Semula Data

Sekiranya anda ingin membersihkan rekod data yang telah dimasukkan:

1. **Melalui Antara Muka Aplikasi:**  
   Klik butang **Reset QA Demo Data** (ikon putaran bulat di bahagian atas sebelah kanan skrin) dan tekan butang merah *Reset Data*. Ini akan memadam rekod baharu dan mengembalikan sistem ke data demonstrasi asas.
2. **Melalui Tetapan Pelayar Web:**  
   Buka *Developer Tools* (tekan F12 atau Ctrl+Shift+I) $\rightarrow$ tab *Application* $\rightarrow$ *Local Storage* $\rightarrow$ pilih URL aplikasi $\rightarrow$ klik *Clear All*. Sebagai alternatif, bersihkan data laman (*Clear Site Data*) melalui tetapan privasi pelayar anda.

---

## ⚖️ 6. Penafian Pematuhan Privasi Undang-Undang

Sistem ini adalah prototaip sistem makmal fungsian bagi tujuan demonstrasi dan pembangunan produk. Sebelum digunakan untuk operasi rasmi yang melibatkan data peribadi komersial sebenar:
* Sistem perlu menjalani penilaian privasi rasmi mengikut peruntukan Akta Perlindungan Data Peribadi 2010 (PDPA) Malaysia.
* Sistem mesti dilengkapi dengan sistem log masuk berperingkat (*Enterprise Identity & Access Management*), penyulitan data semasa rehat (*Encryption-at-Rest*), dan saluran penghantaran selamat (*HTTPS/TLS*).
