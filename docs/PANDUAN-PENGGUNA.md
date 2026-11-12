# Panduan Pengguna: G-TACR MS ISO/IEC 17025 LIMS

Dokumen ini menerangkan cara menggunakan Sistem Pengurusan Maklumat Makmal (*Laboratory Information Management System* - LIMS) langkah demi langkah. Panduan ini ditulis dalam bahasa mudah agar sesiapa sahaja—termasuk mereka yang tiada latar belakang teknikal atau pengaturcaraan—boleh mengendalikan sistem ini dengan lancar.

---

## 🎛️ Memahami Bar Navigasi & Suis Peranan (*Role Switcher*)

Di bahagian atas skrin aplikasi, terdapat bar navigasi utama yang mengandungi:
1. **Lambang Rasmi:** Logo Lembaga Getah Malaysia (LGM) dan lambang akreditasi **G-TACR SAMM No. 008**.
2. **Penukar Peranan (*Role Switcher*):** Butang pintas untuk bertukar antara empat (4) peranan teras:
   * `1. Admin/CS` (Ungu)
   * `2. SRO (Intake)` (Jingga/Kuning)
   * `3. Chemist` (Biru)
   * `4. Tech Manager` (Hijau)
3. **Butang Matriks Kuasa (*Role Matrix*):** Memaparkan jadual perbandingan hak akses mengikut standard ISO 17025.
4. **Butang Tetap Semula Data (*Reset QA Demo Data*):** Ikon putaran bulat untuk memulihkan semula data ujian asal sekiranya anda ingin memulakan demonstrasi dari awal.
5. **Bar Aliran Pintas (*Quick Live Flow*):** Memaparkan laluan langkah demi langkah berserta lencana bilangan tugasan yang menunggu tindakan.

---

## 🧭 Aliran Kerja Langkah Demi Langkah Mengikut Peranan

Sistem ini mempunyai empat fasa utama yang saling bersambung:

```
[Fasa 1: Admin/CS]          [Fasa 2: SRO]               [Fasa 3: Jurukimia]         [Fasa 4: Pengurus Teknikal]
Sebut Harga & Invois  --->  Pemeriksaan Fizikal   --->  Ujian Makmal & Draf   --->  Semakan QA/QC & Kelulusan
(Bayaran Disahkan)          (Pendaftaran Kod ID)        (Kemasukan Keputusan)       (Tandatangan Digital Kripto)
                                                                                            |
                                                                                            v
                                                                                    [Serahan Akhir: Admin/CS]
                                                                                    Muat Turun & Serah COA
```

---

### Fasa 1: Modul Kewangan & Kawalan Bayaran (Peranan: Admin / CS)

Tujuan fasa ini adalah memastikan perkhidmatan pengujian mempunyai kontrak yang jelas dan bayaran telah diterima sebelum sebarang kerja makmal dimulakan.

#### Langkah 1.1: Membina Sebut Harga (*Quotation*)
1. Pastikan peranan aktif di bar atas adalah **Admin / CS**.
2. Klik tab **Finance (Quotes & Invoices)** di menu sebelah kiri.
3. Klik butang **+ Create Quotation** di bahagian atas kanan.
4. Masukkan maklumat pelanggan:
   * **Nama Pelanggan & Syarikat:** Contohnya, *Encik Razman (Apex Rubber Industries Sdn Bhd)*.
   * **Emel & Nombor Telefon:** Contohnya, *razman@apexrubber.com.my* / *+6012-3456789*.
   * **Jenis Sampel & Matriks:** Contohnya, *Lateks Pekat Terpelihara* / *Lateks Asli*.
   * **Pilihan Parameter Ujian:** Tandakan ujian yang diperlukan (cth: Kandungan Pepejal Jumlah, Ujian Ammonia, Ujian Kestabilan Mekanikal). Harga dan cukai SST 6% akan dikira secara automatik.
5. Klik **Generate Quotation**. Sistem akan menghasilkan nombor rujukan seperti `QT-2026-0045`.

#### Langkah 1.2: Menukar Sebut Harga kepada Invois
1. Pada senarai sebut harga, cari sebut harga yang berstatus `Sent` atau `Accepted`.
2. Klik butang **Convert to Invoice**.
3. Sistem akan menjana Invois rasmi dengan nombor seperti `INV-2026-0092`. Status invois baharu ini adalah **UNPAID** (Belum Dibayar).

#### Langkah 1.3: Mengesahkan Penerimaan Bayaran (*Pre-Payment Gating*)
1. Pada senarai invois di bahagian bawah tab Kewangan, cari invois yang berkenaan.
2. Klik butang **Mark as Paid**.
3. Pilih kaedah pembayaran (cth: *Online Banking FPX* atau *Cheque*) dan masukkan nombor rujukan transaksi (cth: `FPX-8839210`).
4. Klik **Confirm Payment**.
5. Status invois kini bertukar menjadi **PAID** (Berwarna Hijau). Sampel kini telah dibenarkan untuk didaftarkan oleh SRO.

---

### Fasa 2: Penerimaan & Pendaftaran Sampel (Peranan: SRO)

Tujuan fasa ini adalah menyemak integriti sampel fizikal yang dihantar ke kaunter makmal agar mematuhi piawaian ISO/IEC 17025 Fasal 7.4.

#### Langkah 2.1: Menukar Peranan kepada SRO
1. Di bar atas, klik butang peranan **2. SRO (Intake)**.
2. Klik tab **Sample Registration** di menu sebelah kiri.

#### Langkah 2.2: Memilih Invois yang Telah Dibayar
1. Di dalam borang pendaftaran, cari menu lungsur (*dropdown*) **Select Paid Invoice**.
2. Pilih invois yang telah berstatus `PAID`.  
   *(Perhatian: Invois yang belum dibayar tidak akan membenarkan pendaftaran lengkap).*

#### Langkah 2.3: Mengisi Log Pemeriksaan Keadaan Sampel (*Sample Condition Log*)
SRO mesti mengisi semakan fizikal berikut:
* **Suhu Penerimaan (°C):** Masukkan bacaan termometer inframerah/kuar. Bagi sampel air sisa atau bahan organik, suhu mesti $\le$ 6.0°C. Sistem akan memberi amaran sekiranya suhu terlalu tinggi.
* **Keadaan Bekas (*Container Intact*):** Tandakan sama ada bekas elok atau bocor.
* **Lak Keselamatan (*Security Seal*):** Tandakan sama ada lak keselamatan masih kemas.
* **Label Sampel (*Label Matched*):** Sahkan nama pada label fizikal sama dengan maklumat permohonan.
* **Borang Rantai Jagaan (*Chain of Custody*):** Pastikan borang serahan fizikal telah ditandatangani oleh penghantar.
* **Keputusan SRO:** Pilih **Accept Sample** jika semua kriteria dipenuhi, atau **Reject Sample** berserta alasan jika rosak.

#### Langkah 2.4: Mengesahkan Pendaftaran & Mencetak Label
1. Sahkan senarai parameter ujian makmal yang dipautkan daripada sebut harga.
2. Klik butang **Register Sample & Generate Lab ID**.
3. Sistem akan menjana kod makmal unik rasmi (cth: `LAB-2026-0145`) dan memulakan kiraan masa **TAT 7 Hari Bekerja**.
4. Anda boleh menekan butang **Print Barcode / Specimen Label** untuk mencetak pelekat makmal.

---

### Fasa 3: Pengujian Makmal & Penyediaan Draf (Peranan: Chemist / Analyst)

Tujuan fasa ini adalah merekodkan keputusan eksperimen sebenar yang dijalankan di meja makmal.

#### Langkah 3.1: Menukar Peranan kepada Jurukimia
1. Di bar atas, klik butang peranan **3. Chemist**.
2. Klik tab **Lab Analysis** di menu sebelah kiri.

#### Langkah 3.2: Memilih Sampel daripada Senarai Kerja (*Worklist*)
1. Panel senarai kerja memaparkan semua sampel yang berstatus `Registered` atau `In Analysis`.
2. Klik pada kad sampel yang ingin diuji untuk membuka borang pengujian.

#### Langkah 3.3: Memasukkan Nilai Keputusan & Pengesahan Kualiti (QC)
Bagi setiap parameter yang ditugaskan:
1. Masukkan nilai bacaan ujian pada ruangan **Measured Result Value** (cth: `12.4` atau `0.02`).
2. Sahkan unit ukuran (cth: `mg/L`, `%`, `g/cm³`) dan semak sama ada nilai melepasi had piawaian (*Regulatory Limit*).
3. Pilih rujukan instrumen/alat yang digunakan (cth: *Metrohm 905 Titrando*, *PerkinElmer PinAAcle 900T AAS*).
4. Tandakan kotak **QC Passed** (Kawalan Kualiti Lulus) setelah graf kalibrasi dan sampel kawalan (*Blank/Spike*) disahkan.
5. Klik **Save Parameter Result**.

#### Langkah 3.4: Menghantar Draf Laporan untuk Semakan Teknikal
1. Masukkan sebarang catatan jurukimia jika ada (cth: *Sampel diuji dalam dua ulangan (duplicate) dengan ketepatan RPD < 5%*).
2. Klik butang **Submit Draft for Technical Review**.
3. Status sampel kini berubah kepada **Draft Submitted**. Jurukimia tidak lagi boleh mengubah keputusan ujian tanpa kebenaran pengurus.

---

### Fasa 4: Semakan Teknikal & Kelulusan (Peranan: Technical Manager)

Tujuan fasa ini adalah pengesahan mutu teknikal secara bebas sebelum sijil rasmi dikeluarkan kepada pelanggan.

#### Langkah 4.1: Menukar Peranan kepada Pengurus Teknikal
1. Di bar atas, klik butang peranan **4. Tech Manager**.
2. Klik tab **Technical Review** di menu sebelah kiri.

#### Langkah 4.2: Meneliti Draf Laporan
1. Pilih sampel di bawah senarai **Pending Technical Sign-Off**.
2. Periksa kesemua parameter, nilai ketidakpastian (*measurement uncertainty*), dan rekod QC yang dimasukkan oleh jurukimia.
3. Anda mempunyai dua (2) pilihan tindakan:
   * **Tolak Draf (*Reject & Return to Analyst*):** Jika terdapat keraguan atau salah kiraan, masukkan sebab penolakan dan pulangkan kepada jurukimia untuk ujian semula.
   * **Luluskan dengan Tandatangan Digital (*Approve & Digitally Sign COA*):** Jika semua data mematuhi standard ISO 17025.

#### Langkah 4.3: Menurunkan Tandatangan Digital Kriptografi
1. Masukkan sebarang ulasan teknikal rasmi jika perlu.
2. Klik butang **Sign & Approve Official COA**.
3. Sistem akan menjana tandatangan digital yang mengandungi:
   * Nama dan jawatan Pengurus Teknikal bertauliah.
   * Tarikh dan masa kelulusan yang tepat (*ISO Timestamp*).
   * Kod cincangan unik (*SHA-256 Cryptographic Hash*) sebagai bukti sijil belum diusik.
   * Nombor Sijil Rasmi bertaraf muktamad (cth: `COA-2026-0145-Rev00`).

---

### Fasa 5: Serahan Sijil Analisis (COA) kepada Pelanggan (Peranan: Admin / CS)

1. Tukar peranan kembali kepada **Admin / CS**.
2. Buka tab **Dashboard** atau **Technical Review**.
3. Klik butang **View Final COA** pada sampel yang telah diluluskan.
4. Di dalam paparan sijil:
   * Klik **Print Certificate** untuk mencetak salinan rasmi terus ke pencetak kertas atau PDF pelayar.
   * Klik **Download Text / Raw Report** untuk memuat turun salinan sandaran.
   * Klik **Deliver to Client** untuk menandakan sijil telah selamat diserahkan kepada pihak pelanggan.
5. Sebaik sahaja diserahkan, status sampel bertukar ke **Delivered**, dan kiraan penjejak masa TAT akan ditamatkan dengan status *TAT Concluded*.

---

## 🏷️ Maksud Status & Label Penting dalam Sistem

### 1. Status Invois
* **UNPAID:** Invois telah dijana tetapi bayaran belum disahkan. Pendaftaran sampel disekat.
* **PAID:** Bayaran telah diterima dan disahkan oleh Admin. Sampel boleh didaftarkan oleh SRO.

### 2. Status Sampel Makmal
* **Received:** Sampel fizikal tiba di kaunter tetapi belum disahkan keadaannya.
* **Rejected:** Sampel ditolak semasa pemeriksaan fizikal (cth: suhu terlalu panas atau botol pecah).
* **Registered:** Sampel berjaya didaftarkan, kod makmal unik telah dijana, dan penjejak TAT bermula.
* **In Analysis:** Jurukimia sedang memproses ujian di makmal.
* **Draft Submitted:** Jurukimia telah menyiapkan ujian dan menghantar draf untuk semakan pengurus.
* **Approved:** Pengurus Teknikal telah menandatangani COA rasmi secara digital.
* **Delivered:** Sijil muktamad telah diserahkan kepada pelanggan dan proses pengujian selesai sepenuhnya.

### 3. Status Penjejak TAT (*Turn-Around Time* - Sasaran 7 Hari Bekerja)
* 🟢 **Hijau (*Safe*):** Baki masa selamat (antara 4 hingga 7 hari bekerja tinggal).
* 🟡 **Kuning (*Warning*):** Baki masa amaran (antara 2 hingga 3 hari bekerja tinggal).
* 🔴 **Merah (*Critical / Overdue*):** Baki masa kritikal ($\le$ 1 hari bekerja atau telah melepasi tempoh janji).
* ⚪ **Kelabu (*Concluded*):** Proses telah selesai dan laporan dihantar.

---

## ❓ Penyelesaian Masalah Biasa (*Troubleshooting*)

### Soalan 1: Mengapa butang "Register Sample" di modul pendaftaran tidak boleh ditekan atau tiada pilihan invois?
* **Punca:** Sistem menguatkuasakan pintu kawalan bayaran (*Pre-payment Gating*). Anda hanya boleh mendaftarkan sampel bagi invois yang telah bertanda **PAID**.
* **Cara Selesai:** Tukar peranan kepada `Admin/CS`, pergi ke tab **Finance**, cari invois berkaitan dan klik **Mark as Paid**. Selepas itu kembali ke modul pendaftaran di bawah peranan `SRO`.

### Soalan 2: Mengapa saya tidak melihat butang "Sign & Approve Official COA"?
* **Punca:** Mengikut peraturan pengasingan kuasa ISO 17025, hanya **Technical Manager** yang mempunyai kuasa meluluskan laporan akhir.
* **Cara Selesai:** Tukar peranan aktif di bahagian atas skrin kepada `4. Tech Manager`.

### Soalan 3: Bagaimanakah cara untuk mencetak Sijil Analisis (COA) dengan kemas tanpa bahagian menu atau butang aplikasi?
* **Cara Selesai:** Buka modul semakan atau klik butang COA pada mana-mana sampel yang telah diluluskan. Klik butang **Print Certificate**. Helaian gaya cetakan khas (*CSS Print Stylesheet*) akan secara automatik menyembunyikan semua menu tepi, butang atas, dan hanya mencetak dokumen sijil rasmi dua muka surat dengan logo LGM dan G-TACR.

### Soalan 4: Saya telah membuat pelbagai perubahan data dan ingin kembali kepada data demonstrasi asal.
* **Cara Selesai:** Klik ikon putaran bulat (**Reset QA Demo Data**) di bahagian atas sebelah kanan skrin. Sahkan tindakan pada tetingkap pengesahan. Semua sebut harga, invois, sampel, dan rekod jejak audit akan dipulihkan kepada set demonstrasi asal.
