# G-TACR MS ISO/IEC 17025 LIMS (SAMM No. 008)

> **Sistem Pengurusan Maklumat Makmal (LIMS) patuh standard MS ISO/IEC 17025:2017 untuk Makmal Penyelidikan Getah G-TACR, Lembaga Getah Malaysia (LGM).**

Aplikasi ini mendigitalkan dan mengawal seluruh perjalanan sampel ujian makmal—daripada penerimaan sebut harga, bayaran wajib, pemeriksaan keadaan fizikal sampel, kemasukan keputusan ujian kimia oleh jurukimia, semakan teknikal QA/QC, sehinggalah pengeluaran Sijil Analisis (*Certificate of Analysis* - COA) rasmi yang dimeterai dengan tandatangan digital kriptografi.

---

## 📌 Masalah yang Diselesaikan

Di dalam makmal pengujian yang mendapat akreditasi rasmi seperti **SAMM No. 008** (*Skim Akreditasi Makmal Malaysia*):

1. **Risiko Kehilangan Akreditasi Kerana Pelanggaran Integriti Data:**  
   Jika staf yang sama boleh menerima sampel, memasukkan keputusan ujian, dan meluluskan laporannya sendiri, data mudah diragui. Sistem ini menguatkuasakan **Pengasingan Kuasa (*Segregation of Duties*)** yang ketat mengikut standard ISO/IEC 17025 Fasal 5 dan 6.
2. **Kelewatan Ujian & Tempoh Menunggu (*Turn-Around Time* - TAT) yang Kabur:**  
   Pelanggan sering tertanya-tanya bila laporan mereka akan siap. Sistem ini menyediakan penjejak masa *TAT 7 Hari Bekerja* berasaskan warna trafik (Hijau, Kuning, Merah) supaya kelewatan dapat dicegah lebih awal.
3. **Ujian Dijalankan Sebelum Bayaran Disahkan (*Revenue Leakage*):**  
   Sampel sering diproses di makmal sebelum pelanggan membayar sebut harga. Sistem ini mengunci proses pendaftaran sampel sehingga bayaran invois disahkan sepenuhnya (*Pre-Payment Gating*).
4. **Sampel Rosak Semasa Transit Diterima Tanpa Rekod:**  
   Jika sampel air sisa atau getah tiba dalam keadaan bocor atau suhu melebihi 6.0°C, keputusan ujian tidak lagi sah. Sistem mewajibkan log pemeriksaan fizikal ISO sebelum sampel boleh didaftarkan.

---

## 👥 Untuk Siapa Aplikasi Ini?

Sistem ini direka khas untuk empat (4) kumpulan pengguna di makmal pengujian:

* **Pegawai Pentadbiran & Khidmat Pelanggan (*Admin / CS*):** Menguruskan sebut harga (*Quotation*), invois, semakan resit bayaran, dan menghantar laporan muktamad kepada pelanggan.
* **Pegawai Penerima Sampel (*Sample Receiving Officer* - SRO):** Memeriksa suhu penerimaan, keutuhan bekas/lak keselamatan, mendaftarkan sampel (*Lab ID* unik), dan mencetak label makmal.
* **Jurukimia & Penganalisis (*Chemist / Analyst*):** Menerima tugasan ujian, menjalankan analisis parameter (fizikal/kimia/logam berat), mengesahkan kawalan kualiti (*QC Passed*), dan menjana draf laporan.
* **Pengurus Teknikal & Penandatangan Sah (*Technical Manager / Authorized Signatory*):** Menyemak integriti teknikal ujian, menolak draf jika ada keraguan, meluluskan laporan dengan tandatangan digital kriptografi, serta menguruskan semakan versi (*Revision Control*).

---

## ⚡ Apa yang Boleh Dibuat? (Fungsi Utama)

Berdasarkan aplikasi yang telah siap dibina:

* **Pengasingan Kuasa 4 Peranan Bersepadu:** Suis peranan di bahagian atas membolehkan pengguna melihat dan menguji aliran kerja mengikut hak akses masing-masing tanpa campur aduk kebenaran.
* **Pintu Kawalan Bayaran Awal (*Pre-Payment Gate*):** SRO tidak dibenarkan mendaftarkan sampel sekiranya invois belum bertanda `PAID`.
* **Pemeriksaan Keadaan Sampel (*Sample Condition Log*):** Semakan suhu (wajib $\le$ 6.0°C bagi sampel alam sekitar), keadaan bekas, integriti lak keselamatan, padanan label, dan borang rantai jagaan (*Chain of Custody*).
* **Penjejak TAT 7 Hari Bekerja (*Turn-Around Time Tracker*):** Kiraan hari automatik dengan status berkod warna:
  * 🟢 **Hijau (Selamat):** Baki 4 hingga 7 hari bekerja.
  * 🟡 **Kuning (Amaran):** Baki 2 hingga 3 hari bekerja.
  * 🔴 **Merah (Kritikal/Lewat):** Baki $\le$ 1 hari bekerja atau terlambat.
  * ⚪ **Selesai:** Laporan telah dihantar kepada pelanggan.
* **Borang Kemasukan Keputusan Ujian Makmal:** Input ujian parameter berserta had kawal selia (*regulatory limit*), anggaran ketidakpastian (*measurement uncertainty*), rujukan instrumen, dan semakan QC.
* **Tandatangan Digital Kriptografi:** Penjanaan kod cincangan (*hash*) keselamatan SHA-256 dan ID sijil penandatangan untuk mengunci integriti laporan.
* **Sijil Analisis (COA) Interaktif & Cetakan:** Paparan COA rasmi dengan logo Lembaga Getah Malaysia (LGM) dan lambang G-TACR SAMM No. 008, sedia untuk dicetak (*Print View*) atau dimuat turun.
* **Jejak Audit Automatik (*Audit Trail Log*):** Merekodkan setiap aktiviti penting (siapa, bila, tindakan, dan perubahan data) tanpa boleh diubah secara manual.

---

## 📖 Contoh Aliran Penggunaan Sebenar

Bayangkan satu senario penghantaran sampel getah asli daripada pelanggan industri:

1. **Langkah 1 (Admin/CS):** Syarikat ABC meminta ujian getah. Admin menjana sebut harga bernilai RM 795.00, pelanggan bersetuju, invois dikeluarkan, dan Admin menandakan bayaran telah diterima (*Paid*).
2. **Langkah 2 (SRO):** Sampel dihantar ke kaunter makmal. SRO menyukat suhu (4.2°C) dan memeriksa bekas. Setelah lulus, sampel didaftarkan dengan kod unik `LAB-2026-0142` dan agihan ujian diagihkan ke makmal kimia.
3. **Langkah 3 (Jurukimia):** Jurukimia membuka senarai kerja (*Worklist*), memasukkan nilai bacaan ujian (cth: Kandungan Kotoran, Abu, Nitrogen, Kerapuhan PRI), menandakan semakan QC lulus, dan menekan *Hantar Draf*.
4. **Langkah 4 (Pengurus Teknikal):** Pengurus membuka modul semakan, meneliti data ujian berbanding had piawaian ASTM/ISO, lalu menurunkan tandatangan digital kelulusan.
5. **Langkah 5 (Admin/CS):** Admin memuat turun Sijil Analisis rasmi yang telah diluluskan untuk diserahkan kepada Syarikat ABC. Tempoh masa TAT ditutup dengan jayanya.

---

## 🚀 Cara Mencuba Aplikasi

Aplikasi prototaip ini boleh dicuba terus melalui pelayar web tanpa perlu memasang sebarang perisian:

* 🌐 **Pautan Aplikasi Sebenar:** [Buka Demo G-TACR LIMS](https://ais-pre-p65qoxoiydacqsgsxgugvv-860662171272.asia-northeast1.run.app)
* 🛠️ **Pautan Persekitaran Pembangunan:** [Buka Pautan Pembangunan](https://ais-dev-p65qoxoiydacqsgsxgugvv-860662171272.asia-northeast1.run.app)

*(Nota: Jika anda menggunakan komputer peribadi dan ingin menjalankan kod sumber secara lokal, rujuk dokumen setup di bawah).*

---

## 📊 Status Projek Semasa

Untuk ketelusan dan integriti dokumentasi:

| Kategori | Status Sebenar | Penerangan |
| :--- | :---: | :--- |
| **Peringkat Projek** | **Prototaip MVP Siap Dibina** | Seluruh aliran kerja 4 fasa (Kewangan, Penerimaan, Ujian, Kelulusan COA) berfungsi sepenuhnya dalam antara muka web. |
| **Fungsi Telah Diuji** | **Telah Disahkan (Manual & Kod)** | Kompilasi TypeScript lulus (`tsc --noEmit`), binaan Vite berjaya (`vite build`), dan interaksi aliran pengguna telah disahkan dalam pelayar. |
| **Penyimpanan Data** | **Tempatan (*In-Browser*)** | Menggunakan simpanan `localStorage` pelayar web. Menutup atau memuat semula pelayar tidak memadam data, dan butang *Reset QA Demo Data* disediakan untuk memulihkan data asal. |
| **Batasan Penting** | **Belum Bersambung Pangkalan Data Awan** | Belum disambungkan ke pangkalan data terpusat seperti PostgreSQL/Firestore atau pelayan emel luaran. Eksport PDF menggunakan format cetakan pelayar (*window.print*) dan simulasi fail teks. |
| **Ujian Automasi** | **Belum Disahkan** | Rangka kerja ujian unit automatik (seperti Vitest atau Playwright) belum dikonfigurasikan. |

---

## 📚 Panduan & Dokumentasi Lanjut

Sila rujuk dokumen terperinci dalam folder `docs/`:

* 📘 [**Panduan Pengguna**](docs/PANDUAN-PENGGUNA.md) — Panduan bergambar langkah demi langkah mengikut peranan pengguna dan penyelesaian masalah biasa.
* 📋 [**Keperluan Produk (PRD)**](docs/KEPERLUAN-PRODUK.md) — Huraian lengkap skop MVP, fasal piawaian ISO 17025, kriteria penerimaan, dan rujukan dokumen asal.
* 🗺️ [**Status Projek & Pelan Hala Tuju**](docs/STATUS-DAN-ROADMAP.md) — Senarai ciri yang telah dibina, batasan semasa, dan cadangan fasa pembangunan seterusnya.
* 🔒 [**Data & Privasi**](docs/DATA-DAN-PRIVASI.md) — Penjelasan mengenai cara data dikendalikan, lokasi penyimpanan, dan sempadan keselamatan maklumat.
* ⚙️ [**Panduan Pemasangan & Penyelenggaraan**](docs/SETUP-DAN-PENYELENGGARAAN.md) — Langkah teknikal untuk memuat turun kod sumber, memasang kebergantungan, dan menjalankan pelayan secara lokal.
* 📝 [**Log Perubahan (Changelog)**](CHANGELOG.md) — Catatan versi dan penambahbaikan sistem.

---

## 💻 Ringkasan Teknologi yang Digunakan

Aplikasi ini dibina dengan menggunakan teknologi moden yang ringan dan pantas:

* **React (v19):** Digunakan untuk membina antara muka pengguna (UI) yang interaktif dan responsif.
* **TypeScript:** Memastikan kod selamat daripada kesilapan jenis data (*type safety*) dan mudah diselenggara.
* **Tailwind CSS (v4):** Digunakan untuk reka bentuk visual yang kemas, profesional, dan mesra paparan cetakan dokumen.
* **Vite (v8):** Alat binaan (*build tool*) pantas untuk pembangunan aplikasi web moden.
* **Lucide React:** Koleksi ikon visual yang konsisten dan mudah difahami.

---

## 💬 Maklum Balas & Bantuan

Sekiranya anda menemui sebarang isu atau ingin mencadangkan penambahbaikan:

1. Buka tab **Issues** di repositori GitHub ini (setelah repositori disambungkan).
2. Terangkan langkah yang dilakukan dan paparan ralat yang dihadapi.
3. Anda juga boleh memulihkan data ujian pada bila-bila masa dengan menekan butang putaran bulat (**Reset QA Demo Data**) di bahagian atas sebelah kanan aplikasi.
