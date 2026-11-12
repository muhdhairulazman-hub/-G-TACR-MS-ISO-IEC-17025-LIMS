# Status Projek & Pelan Hala Tuju (Roadmap)

Dokumen ini merekodkan status sebenar pembangunan aplikasi **G-TACR MS ISO/IEC 17025 LIMS** setakat versi semasa. Untuk mengekalkan ketelusan, dokumen ini membezakan secara jelas antara fungsi yang telah dibina, fungsi yang telah disahkan melalui ujian, batasan sedia ada, dan perancangan masa hadapan.

---

## 🛠️ 1. Fungsi yang Sudah Dibina

Komponen dan aliran kerja berikut telah lengkap dibina di dalam kod sumber:

* **Sistem Navigasi & Suis Peranan (*Role Switcher*):**
  * Suis pantas 4 peranan: `Admin / CS`, `Sample Receiving Officer (SRO)`, `Chemist / Analyst`, dan `Technical Manager`.
  * Penyekatan akses butang tindakan berdasarkan peranan aktif.
  * Modal visual Matriks Pengasingan Kuasa (*Segregation of Duties Matrix*).
* **Papan Pemuka (*Dashboard*) & Penjejak TAT:**
  * Penjejak masa *TAT 7 Hari Bekerja* dengan pengiraan baki hari dan petunjuk warna trafik (Hijau, Kuning, Merah, Selesai).
  * Penapis pantas sampel mengikut warna amaran TAT dan carian teks masa nyata.
  * Kad ringkasan metrik status (Sampel Aktif, Invois Menunggu Bayaran, Dalam Analisis, Menunggu Kelulusan).
* **Modul Kewangan & Pintu Kawalan Bayaran (*Pre-Payment Gate*):**
  * Borang pembinaan Sebut Harga (*Quotation*) dengan pengiraan automatik SST 6%.
  * Penukaran sebut harga kepada Invois rasmi.
  * Pengesahan penerimaan bayaran (*Mark as Paid*) dengan rekod kaedah bayaran dan nombor rujukan.
* **Modul Penerimaan Sampel (*Sample Registration*):**
  * Senarai semak keadaan sampel fizikal (suhu penerimaan, integriti bekas, lak keselamatan, label, dan borang rantai jagaan).
  * Penjanaan automatik nombor makmal unik format `LAB-2026-XXXX`.
  * Simulasi paparan cetakan pelekat makmal / kod bar botol sampel.
* **Modul Pengujian Makmal (*Lab Testing*):**
  * Senarai tugasan sampel (*Worklist*) untuk jurukimia.
  * Borang kemasukan keputusan ujian multi-parameter berasaskan kaedah piawai (APHA / ASTM / ISO).
  * Tandatangan semakan kawalan kualiti (*QC Passed*) dan pemilihan instrumen makmal.
  * Penyerahan draf laporan ke meja semakan pengurus.
* **Modul Semakan Teknikal & Kelulusan (*Technical Review*):**
  * Papan semakan draf ujian untuk Pengurus Teknikal.
  * Fungsi penolakan draf (*Reject & Return to Analyst*) berserta ulasan pembetulan.
  * Pengesahan kelulusan bertandatangan digital kriptografi (penjanaan cincangan SHA-256).
  * Pengurusan semakan versi (*Revision Control*) sekiranya laporan memerlukan pindaan.
* **Modul Sijil Analisis (COA) & Cetakan:**
  * Paparan modal rasmi COA berformat SAMM No. 008.
  * Lembaran gaya cetakan khas (`@media print`) yang menyembunyikan navigasi web untuk hasil cetakan dokumen kemas.
  * Simulasi muat turun fail laporan teks/mentah.
  * Tindakan serahan laporan kepada pelanggan (*Deliver to Client*) yang menamatkan pemantauan masa TAT.
* **Modul Jejak Audit (*Audit Trail Log*):**
  * Rekod kronologi automatik bagi setiap penciptaan sebut harga, bayaran, pendaftaran sampel, kemasukan data ujian, kelulusan, dan serahan laporan.
* **Fungsi Pemulihan Data (*Reset QA Demo Data*):**
  * Butang memulihkan keseluruhan pangkalan data pelayar kepada set demonstrasi asal.

---

## 🧪 2. Fungsi yang Telah Diuji

Fungsi berikut telah disahkan berfungsi melalui ujian kod dan pengesahan interaktif dalam persekitaran pembangunan:

* **Kompilasi Kod Bersih (*TypeScript Compilation*):**
  * Ujian `tsc --noEmit` lulus 100% tanpa sebarang ralat sintaks atau jenis data (*zero type errors*).
* **Binaan Pengeluaran (*Production Build*):**
  * Skrip `vite build` berjaya menghasilkan pakej fail statik yang optimum tanpa sebarang ralat pemalam.
* **Ujian Aliran Kerja Manual (*End-to-End Simulation*):**
  * Pengesahan bahawa pendaftaran sampel tidak membenarkan invois belum berbayar (*pre-payment gate enforcement*).
  * Pengesahan bahawa jurukimia tidak dapat menekan butang tandatangan kelulusan akhir (*role permission guard*).
  * Pengesahan bahawa pertukaran status sampel mengemas kini pengiraan TAT dan mencatatkan jejak audit baharu ke dalam senarai.
  * Pengesahan pengekalan data melalui muat semula pelayar web (*localStorage persistence*).

---

## ⚠️ 3. Fungsi yang Belum Disahkan / Batasan Semasa

Perkara berikut merupakan batasan teknologi versi prototaip semasa dan belum disahkan untuk persekitaran pengeluaran berskala besar:

* **Penyimpanan Berpusat (*Central Cloud Database*):**  
  Data pada masa ini disimpan dalam storan pelayar (`localStorage`). Jika pengguna membuka aplikasi dari peranti atau pelayar lain, data tidak akan disegerakkan secara automatik.
* **Ujian Unit Automatik (*Automated Test Suite*):**  
  Belum ada fail ujian unit automatik (cth: Vitest, Jest, atau Cypress) yang dikonfigurasikan di dalam repositori.
* **Penjanaan PDF Hakiki Pelayan (*Server-side PDF Engine*):**  
  Fungsi eksport PDF semasa bergantung kepada keupayaan fungsi cetak pelayar (*Browser Print to PDF*) melalui CSS khusus serta simulasi fail teks. Enjin penjanaan dokumen berasaskan pelayan (seperti PDFKit atau Puppeteer) belum dipasang.
* **Penyepaduan Perkakasan Makmal (*Instrument IoT / RS232 Integration*):**  
  Nilai bacaan instrumen makmal masih dimasukkan secara manual oleh jurukimia dan belum disambungkan terus kepada port bersiri perkakasan makmal sebenar.
* **Gerbang Pembayaran & Emel Sebenar:**  
  Tindakan pembayaran dan penghantaran emel disimulasikan di peringkat antara muka dan belum dihubungkan ke penyedia gerbang pembayaran (cth: ToyyibPay / Stripe) atau pelayan SMTP.
* **Pustaka AI (@google/genai):**  
  Pustaka SDK AI dipasang dalam `package.json` untuk persediaan masa hadapan, namun aplikasi semasa beroperasi sepenuhnya sebagai sistem LIMS deterministik tanpa memanggil model bahasa raya (LLM).

---

## 🗺️ 4. Pelan Hala Tuju Seterusnya (Roadmap)

Perancangan pembangunan fasa seterusnya disusun mengikut keutamaan teknikal:

### Fasa A: Pengukuhan Kestabilan & Ujian Automasi
- Menambah suite ujian unit automatik untuk menguji logik perniagaan pengasingan kuasa dan kiraan baki hari TAT.
- Mengkonfigurasi saluran integrasi berterusan (*Continuous Integration* - CI) bagi menyemak kualiti kod setiap kali berlaku commit baharu.

### Fasa B: Penyegerakan Pangkalan Data Awan (Cloud Persistence)
- Menyambungkan aplikasi kepada pangkalan data terpusat (seperti PostgreSQL atau Google Cloud Firestore) dengan pengesahan identiti pengguna sebenar (*User Authentication*).
- Menetapkan kawalan keselamatan pangkalan data berasaskan peranan (*Row-Level Security / Firestore Security Rules*).

### Fasa C: Enjin Dokumen & Integrasi Mesin Makmal
- Membina enjin penjanaan fail PDF rasmi beresolusi tinggi dengan kod QR pengesahan ketulenan sijil di bahagian pelayan.
- Menyediakan sokongan import data fail keputusan terus daripada instrumen makmal (cth: fail CSV atau format keluaran AAS/Titrando).
- Menambah sistem notifikasi emel automatik kepada pelanggan apabila status sampel bertukar kepada sedia untuk diambil.
