# Dokumen Keperluan Produk (PRD): G-TACR MS ISO/IEC 17025 LIMS

Dokumen ini mendokumentasikan objektif, skop fungsian, peraturan perniagaan (*business rules*), serta keperluan pematuhan standard antarabangsa **MS ISO/IEC 17025:2017** (*General requirements for the competence of testing and calibration laboratories*) bagi aplikasi ini.

---

## 📌 Rujukan Dokumen Asal

Projek ini dibangunkan berdasarkan spesifikasi keperluan rasmi yang disertakan di dalam repositori:
* **Fail Asal:** `public/assets/aistudio/Dokumen_Keperluan_Produk__PRD__LIMS_ISO_17025_a7509c4d.pdf`
* **Tajuk Dokumen:** *Product Requirements Document: Laboratory Information Management System (LIMS) — ISO/IEC 17025 MVP Ready*
* **Institusi Sasaran:** Global Testing & Analytical Chemistry Research (G-TACR), Lembaga Getah Malaysia (LGM).
* **Nombor Akreditasi Kebangsaan:** Skim Akreditasi Makmal Malaysia (**SAMM No. 008**).

---

## 🎯 Tujuan Produk & Pernyataan Masalah

Makmal pengujian kimia getah dan lateks berakreditasi menghadapi cabaran pengurusan yang kritikal:
1. **Pematuhan Audit SAMM / ISO 17025:** Audit berkala oleh Jabatan Standard Malaysia meneliti integriti data, rantaian jagaan sampel, dan kawalan akses. Kegagalan membuktikan pengasingan kuasa boleh mengakibatkan penggantungan sijil akreditasi.
2. **Kekangan Masa (TAT 7 Hari):** Pelanggan komersial getah memerlukan keputusan cepat untuk kelulusan eksport kontena. Tanpa sistem pemantauan automatik, kelewatan sampel sukar dikesan lebih awal.
3. **Kawalan Hasil Kewangan:** Ujian kimia menggunakan reagen mahal dan instrumen canggih (AAS, Titrator, ICP-OES). Sampel tidak wajar dianalisis sebelum komitmen bayaran disahkan oleh pihak pelanggan.

Sistem ini dibina sebagai prototaip fungsian penuh (*Minimum Viable Product* - MVP) untuk mendigitalkan seluruh kitaran hayat pengujian makmal secara telus, selamat, dan berintegriti.

---

## 👥 Pengguna Sasaran & Matriks Pengasingan Kuasa (*Segregation of Duties*)

Bagi mematuhi syarat Fasal 5.2 (Struktur Organisasi) dan Fasal 6.2 (Kakitangan) ISO/IEC 17025, sistem menguatkuasakan pengasingan kuasa kepada 4 peranan utama:

| Peranan | Penerangan Tanggungjawab | Hak Akses Modul | Fasal Berkaitan |
| :--- | :--- | :--- | :--- |
| **Admin / Customer Service (CS)** | Hubungan pelanggan, sebut harga, penerimaan bayaran, dan serahan laporan muktamad. | Modul Kewangan, Pengesahan Bayaran, Paparan COA Muktamad, Serahan Pelanggan. | ISO 17025: 7.1 |
| **Sample Receiving Officer (SRO)** | Pemeriksaan integriti fizikal sampel tiba, pendaftaran ID makmal, dan cetakan label. | Modul Pendaftaran Sampel, Log Keadaan Sampel (*Condition Checklist*), Cetakan Pelekat. | ISO 17025: 7.4 |
| **Chemist / Analyst** | Menjalankan ujian kimia/fizikal, merekod bacaan instrumen, dan mengesahkan QC. | Senarai Kerja Makmal (*Worklist*), Input Keputusan Ujian, Penjanaan Draf COA. | ISO 17025: 7.2 & 7.7 |
| **Technical Manager (Signatory)** | Semakan teknikal bebas, kawalan kualiti (QA), kelulusan laporan rasmi, dan kawalan semakan. | Modul Semakan Teknikal, Kelulusan Tandatangan Digital Kripto, Tolakan Draf, Pindaan Versi. | ISO 17025: 7.8 & 8.5 |

---

## 📋 Skop MVP & Ciri-Ciri Teras

Aplikasi ini merangkumi modul teras berikut:

### 1. Papan Pemuka & Pemantauan TAT (*Dashboard & TAT Countdown*)
* **Sasaran Standard:** 7 Hari Bekerja dari tarikh pendaftaran sampel sehingga serahan laporan.
* **Petunjuk Visual Berkod Warna:**
  * 🟢 **Hijau (*Safe*):** Baki 4 hingga 7 hari bekerja.
  * 🟡 **Kuning (*Warning*):** Baki 2 hingga 3 hari bekerja.
  * 🔴 **Merah (*Critical / Overdue*):** Baki $\le$ 1 hari atau terlambat.
  * ⚪ **Kelabu (*Concluded*):** Proses selesai dan dihantar kepada pelanggan.
* **Penapis Pantas:** Keupayaan menapis sampel mengikut status kecemasan warna dan carian segera berdasarkan kod sampel, nama syarikat, atau nombor invois.

### 2. Modul Kewangan & Pintu Kawalan Bayaran (*Finance & Pre-Payment Gating*)
* **Penjanaan Sebut Harga (*Quotation*):** Pengiraan harga modular mengikut senarai parameter ujian, cukai SST 6%, tempoh sah laku, dan komitmen masa TAT.
* **Invois Rasmi:** Penukaran sebut harga kepada invois dengan kod unik `INV-2026-XXXX`.
* **Pintu Kawalan Wajib (*Mandatory Gate*):** Invois wajib disahkan bertanda `PAID` sebelum modul pendaftaran membenarkan sampel didaftarkan.

### 3. Modul Penerimaan & Pemeriksaan Sampel (*Intake & Condition Log*)
* **Pemeriksaan Keadaan Fizikal (ISO Fasal 7.4):**
  * Suhu penerimaan (wajib $\le$ 6.0°C untuk sampel alam sekitar/organik).
  * Keadaan bekas (*intact / leaking*).
  * Integriti lak keselamatan (*security seal*).
  * Ketepatan label sampel berbanding dokumen serahan.
  * Padanan borang rantaian jagaan (*Chain of Custody*).
* **Penjanaan Kod Makmal Unik:** Format tersusun seperti `LAB-2026-XXXX`.
* **Simulasi Cetakan Kod Bar / Label Makmal:** Paparan label botol ujian berserta kod bar dan tarikh penerimaan.

### 4. Modul Pengujian & Rekod Keputusan (*Lab Testing & Worklist*)
* **Senarai Kerja Mengikut Sampel:** Paparan sampel yang sedang menunggu analisis kimia.
* **Input Keputusan Multi-Parameter:**
  * Parameter fizikal (cth: Kandungan Kotoran, Abu, Kerapuhan PRI).
  * Parameter kimia (cth: Kandungan Nitrogen, Sebatian Meruap).
  * Logam berat (cth: Plumbum, Kadmium, Kuprum).
* **Anggaran Ketidakpastian Pengukuran (*Uncertainty of Measurement*):** Dipaparkan mengikut standard ISO Fasal 7.6.
* **Semakan Kawalan Kualiti (*QC Check*):** Jurukimia mesti menandakan lulus QC instrumen sebelum draf boleh dihantar.

### 5. Modul Semakan Teknikal & Tandatangan Digital (*QA/QC & Sign-Off*)
* **Semakan Bebas:** Hanya Pengurus Teknikal berdaftar dibenarkan membuat keputusan.
* **Tandatangan Digital Kriptografi:** Penjanaan kod cincangan (*cryptographic hash*) berasaskan algoritma SHA-256 untuk memeteraikan ketulenan dokumen (ISO Fasal 7.8).
* **Kawalan Semakan Versi (*Revision Control*):** Sekiranya laporan perlu dipinda selepas kelulusan, sistem menaikkan versi (cth: daripada `Rev00` kepada `Rev01`) dan mewajibkan rekod justifikasi pindaan.

### 6. Paparan Sijil Analisis (COA) & Jejak Audit (*Audit Trail*)
* **Format Sijil Standard SAMM No. 008:** Memaparkan kepala surat rasmi LGM & G-TACR, perincian sampel, jadual keputusan ujian berbanding had piawaian, dan meterai tandatangan digital.
* **Mesra Cetakan (*Print-Ready*):** Dilengkapi CSS `@media print` yang mengoptimumkan cetakan kertas A4 rasmi tanpa elemen antara muka laman web.
* **Jejak Audit Tanpa Padam (*Immutable Audit Trail*):** Merekodkan cap masa, nama staf, peranan, entiti terlibat, dan butiran tindakan bagi memenuhi syarat Fasal 8.5 ISO 17025.

---

## 📐 Peraturan Perniagaan (*Business Rules*)

1. **Aturan R1 (Pintu Bayaran):** `Sample.register()` HANYA dibenarkan jika `Invoice.status === 'paid'`.
2. **Aturan R2 (Pemisahan Kuasa Ujian & Kelulusan):** Jurukimia (`chemist`) TIDAK BOLEH menandatangani kelulusan akhir COA. Hanya Pengurus Teknikal (`tech_manager`) yang mempunyai kuasa meluluskan.
3. **Aturan R3 (Integriti Sampel Suhu Dingin):** Sekiranya suhu penerimaan sampel melebihi 6.0°C dan SRO memilih untuk menerima dengan pengecualian, status amaran disimpan di dalam log audit.
4. **Aturan R4 (Kunci Draf Selepas Hantar):** Sebaik sahaja draf dihantar oleh jurukimia, keputusan ujian dikunci daripada sebarang suntingan sehingga disemak oleh pengurus.
5. **Aturan R5 (Penutupan TAT):** Pengiraan masa TAT hanya ditamatkan apabila status sampel bertukar kepada `delivered`.

---

## ✅ Kriteria Penerimaan (*Acceptance Criteria*)

* [x] Pengguna boleh bertukar antara 4 peranan dengan paparan visual tema warna yang berbeza.
* [x] Invois boleh dijana dan ditandakan sebagai berbayar (`PAID`).
* [x] Pendaftaran sampel dihalang jika invois masih belum berbayar.
* [x] Senarai semak keadaan sampel ISO 17025 merekodkan suhu dan status bekas.
* [x] Jurukimia boleh mengemaskini nilai ujian multi-parameter dan menghantar draf laporan.
* [x] Pengurus Teknikal boleh meluluskan laporan dengan tandatangan digital cincangan unik atau menolak draf kembali ke meja makmal.
* [x] Sijil Analisis (COA) memaparkan status `FINAL OFFICIAL REPORT` lengkap dengan format cetakan kemas.
* [x] Setiap tindakan kritikal direkodkan ke dalam paparan Jejak Audit (*Audit Trail*).
