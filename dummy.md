**Pengembangan Sistem *Smart Waste Bin* Berbasis *Internet of Things*
untuk Analisis Pola Pembuangan Sampah**

**Laporan Tugas Akhir**

**Disusun sebagai syarat kelulusan tingkat sarjana**

**Oleh**

**Jazmy Izzati Alamsyah**

**NIM : 18221124**

![](./media/media/image1.png){width="1.036745406824147in"
height="1.3779527559055118in"}

**PROGRAM STUDI SISTEM DAN TEKNOLOGI INFORMASI**

**SEKOLAH TEKNIK ELEKTRO DAN INFORMATIKA**

**INSTITUT TEKNOLOGI BANDUNG**

**Maret 2026**

**Pengembangan Sistem *Smart Waste Bin* Berbasis *Internet of Things*
untuk Analisis Pola Pembuangan Sampah**

**Laporan Tugas Akhir**

**Oleh**

**Jazmy Izzati Alamsyah**

**NIM : 18221124**

**Program Studi Sistem dan Teknologi Informasi**

Sekolah Teknik Elektro dan Informatika

Institut Teknologi Bandung

Telah disetujui dan disahkan sebagai Laporan Tugas Akhir

di Bandung, pada tanggal 5 Maret 2026

+------------------------------------------------------------+------------------------------------------------------------+
| Pembimbing I,                                              | Pembimbing II,                                             |
|                                                            |                                                            |
| ![](./media/media/image2.png){width="2.5833333333333335in" | ![](./media/media/image3.png){width="1.4479166666666667in" |
| height="0.7566491688538932in"}                             | height="1.0625in"}                                         |
|                                                            |                                                            |
| Dr. Fadhil Hidayat, S.Kom., M.T.                           | Dr. Ir. Arry Akhmad Arman, M.T.                            |
|                                                            |                                                            |
| NIP 198609252012121002                                     | NIP 196504141991021001                                     |
+============================================================+============================================================+

**LEMBAR PERNYATAAN**

Dengan ini saya menyatakan bahwa:

1.  Pengerjaan dan penulisan Laporan Tugas Akhir ini dilakukan tanpa
    menggunakan bantuan yang tidak dibenarkan.

2.  Segala bentuk kutipan dan acuan terhadap tulisan orang lain yang
    digunakan di dalam penyusunan laporan tugas akhir ini telah
    dituliskan dengan baik dan benar.

3.  Laporan Tugas Akhir ini belum pernah diajukan pada program
    pendidikan di perguruan tinggi mana pun.

Jika terbukti melanggar hal-hal di atas, saya bersedia dikenakan sanksi
sesuai dengan Peraturan Rektor ITB No. 257 tahun 2019 tentang Penegakan
Norma Akademik dan Kemahasiswaan Institut Teknologi Bandung.

Bandung, 5 Maret 2026

![](./media/media/image4.png){width="1.462684820647419in"
height="0.7313429571303587in"}

Jazmy Izzati Alamsyah

NIM 18221124

ABSTRAK

**Pengembangan Sistem *Smart Waste Bin* Berbasis *Internet of Things*
untuk Analisis Pola Pembuangan Sampah**

Oleh

Jazmy Izzati Alamsyah

NIM : 18221124

Pengelolaan sampah di lingkungan kampus menghadapi tantangan berupa
kurangnya data terstruktur mengenai pola pembuangan sampah, sehingga
menyulitkan pengambilan keputusan berbasis data dalam jadwal
pengangkutan dan alokasi sumber daya. Penelitian ini mengembangkan
sistem *Smart Waste Bin* berbasis *Internet of Things* (IoT) yang mampu
mengotomasi pengumpulan data dan menganalisis pola pembuangan sampah di
Gedung Labtek VIII Institut Teknologi Bandung, khususnya pada area depan
Laboratorium IoT Lantai 4. Sistem dirancang menggunakan arsitektur IoT
4-layer yang terdiri dari *Perception Layer* (mikrokontroler ESP32,
sensor jarak VL53L0X, sensor arus INA219, dan modul GSM SIM800L),
*Network Layer* berbasis protokol MQTT, *Middleware Layer* menggunakan
Node-RED untuk pemrosesan aliran data, serta *Application Layer* dengan
basis data Supabase dan *dashboard* Next.js untuk visualisasi dan
analisis. Selama periode observasi 37 hari, tiga unit perangkat sensor
berhasil mengumpulkan 805 *records* data dengan tingkat keberhasilan
pengiriman sebesar 90,7%. Hasil analisis data historis mengidentifikasi
empat pola temporal pembuangan sampah, di antaranya: *peak hour*
konsisten pada pukul 14:00-17:00, seluruh aktivitas pembuangan
terkonsentrasi pada jam kerja (07:00-19:00) di hari kerja, dominasi
sampah anorganik yang menyumbang 13 dari 27 *event* penambahan (48,1%
dari total *event*) dengan kontribusi volume sebesar 51,7% dari total
delta positif, serta penurunan aktivitas pembuangan pada hari libur
nasional. Perangkat bawaan pihak ketiga dioptimasi melalui lima
peningkatan *firmware*, di mana empat di antaranya terbukti efektif
dalam meningkatkan reliabilitas dan konsistensi pengukuran. Seluruh 10
kebutuhan fungsional dan 7 dari 8 kebutuhan nonfungsional sistem
berhasil dipenuhi. Penelitian ini menunjukkan bahwa sistem IoT berbasis
data mampu menghasilkan wawasan yang terstruktur untuk mendukung
pengelolaan sampah kampus.

Kata kunci: *smart waste bin*, *Internet of Things*, ESP32, VL53L0X,
MQTT, pola pembuangan sampah, analisis temporal.

**KATA PENGANTAR**

Puji syukur penulis panjatkan ke hadirat Tuhan Yang Maha Esa atas segala
rahmat dan karunia-Nya sehingga Laporan Tugas Akhir yang berjudul
\"Pengembangan Sistem *Smart Waste Bin* Berbasis *Internet of Things*
untuk Analisis Pola Pembuangan Sampah\" ini dapat diselesaikan dengan
baik. Laporan ini disusun sebagai salah satu syarat kelulusan tingkat
sarjana pada Program Studi Sistem dan Teknologi Informasi, Sekolah
Teknik Elektro dan Informatika, Institut Teknologi Bandung.

Pada kesempatan ini, penulis ingin menyampaikan terima kasih kepada:

1.  Bapak Dr. Fadhil Hidayat, S.Kom., M.T. selaku Pembimbing I dan Bapak
    Dr. Ir. Arry Akhmad Arman, M.T. selaku Pembimbing II, yang telah
    memberikan bimbingan, arahan, serta masukan yang sangat berarti
    selama proses penelitian dan penulisan laporan ini berlangsung.

2.  Seluruh dosen dan staf Program Studi Sistem dan Teknologi Informasi
    ITB yang telah memberikan ilmu dan dukungan selama masa perkuliahan.

3.  Keluarga tercinta, Bapak, Ibu, dan 3 Adik saya yang senantiasa
    memberikan doa, dukungan, dan semangat tanpa henti selama penulis
    menempuh pendidikan hingga menyelesaikan Tugas Akhir ini.

4.  Teman-teman, baik yang menemani secara langsung maupun daring, yang
    turut memberikan dukungan dan semangat selama penulisan Tugas Akhir
    ini.

5.  Mas Fryma dan Mas Farhan dari PT Layanan Cerdas Indonesia, yang
    telah memberikan dukungan teknis dan membantu dalam proses
    maintenance perangkat selama penelitian berlangsung.

6.  Seluruh pihak yang tidak dapat disebutkan satu per satu yang telah
    turut membantu penyelesaian Tugas Akhir ini.

**DAFTAR ISI**

#  {#section .TOC-Heading}

[BAB I PENDAHULUAN [1](#pendahuluan)](#pendahuluan)

[I.1 Latar Belakang [1](#latar-belakang)](#latar-belakang)

[I.2 Rumusan Masalah [2](#rumusan-masalah)](#rumusan-masalah)

[I.3 Tujuan [2](#tujuan)](#tujuan)

[I.4 Batasan Masalah [3](#batasan-masalah)](#batasan-masalah)

[I.5 Metodologi [3](#metodologi)](#metodologi)

[I.5.1 Studi Literatur [4](#studi-literatur)](#studi-literatur)

[I.5.2 Pendekatan *Design Thinking*
[5](#pendekatan-design-thinking)](#pendekatan-design-thinking)

[BAB II STUDI LITERATUR [8](#studi-literatur-1)](#studi-literatur-1)

[II.1 Pengelolaan Sampah [8](#pengelolaan-sampah)](#pengelolaan-sampah)

[II.1.1 Konsep Dasar Pengelolaan Sampah
[8](#konsep-dasar-pengelolaan-sampah)](#konsep-dasar-pengelolaan-sampah)

[II.1.2 Tantangan Pengelolaan Sampah pada Lingkungan Kampus
[9](#tantangan-pengelolaan-sampah-pada-lingkungan-kampus)](#tantangan-pengelolaan-sampah-pada-lingkungan-kampus)

[II.1.3 Data dalam Pengelolaan Sampah
[11](#data-dalam-pengelolaan-sampah)](#data-dalam-pengelolaan-sampah)

[II.2 *Internet of Things*
[12](#internet-of-things)](#internet-of-things)

[II.2.1 Arsitektur *Internet of Things*
[14](#arsitektur-internet-of-things)](#arsitektur-internet-of-things)

[II.2.2 Komponen Perangkat Keras pada IoT
[19](#komponen-perangkat-keras-pada-iot)](#komponen-perangkat-keras-pada-iot)

[II.2.3 Protokol Komunikasi IoT
[25](#protokol-komunikasi-iot)](#protokol-komunikasi-iot)

[II.3 Node-RED [28](#node-red)](#node-red)

[II.4 Studi Terkait [29](#studi-terkait)](#studi-terkait)

[II.4.1 Sistem *Smart Waste Bin* Berbasis IoT
[29](#sistem-smart-waste-bin-berbasis-iot)](#sistem-smart-waste-bin-berbasis-iot)

[BAB III ANALISIS MASALAH [31](#analisis-masalah)](#analisis-masalah)

[III.1 Analisis Kondisi Saat Ini
[31](#analisis-kondisi-saat-ini)](#analisis-kondisi-saat-ini)

[III.2 Analisis Kebutuhan
[33](#analisis-kebutuhan)](#analisis-kebutuhan)

[III.2.1 Identifikasi Masalah Pengguna
[33](#identifikasi-pengguna)](#identifikasi-pengguna)

[III.2.2 Kebutuhan Fungsional
[34](#kebutuhan-fungsional)](#kebutuhan-fungsional)

[III.2.3 Kebutuhan Nonfungsional
[36](#kebutuhan-nonfungsional)](#kebutuhan-nonfungsional)

[III.3 Analisis Pemilihan Solusi
[37](#analisis-pemilihan-solusi)](#analisis-pemilihan-solusi)

[III.3.1 Alternatif Solusi [37](#alternatif-solusi)](#alternatif-solusi)

[III.3.2 Analisis Penentuan Solusi Menggunakan Metode AHP
[40](#analisis-penentuan-solusi-menggunakan-metode-ahp)](#analisis-penentuan-solusi-menggunakan-metode-ahp)

[III.3.3 Evaluasi dan Pemilihan Alternatif Solusi
[43](#evaluasi-dan-pemilihan-alternatif-solusi)](#evaluasi-dan-pemilihan-alternatif-solusi)

[BAB IV DESAIN DAN IMPLEMENTASI SISTEM *SMART WASTE BIN*
[45](#desain-dan-implementasi-sistem-smart-waste-bin)](#desain-dan-implementasi-sistem-smart-waste-bin)

[IV.1 Gambaran Umum Sistem
[45](#gambaran-umum-sistem)](#gambaran-umum-sistem)

[IV.1.1 Arsitektur Sistem [45](#arsitektur-sistem)](#arsitektur-sistem)

[IV.1.2 Alur Data Sistem [47](#alur-data-sistem)](#alur-data-sistem)

[IV.1.3 Pemilihan Teknologi
[51](#pemilihan-teknologi)](#pemilihan-teknologi)

[IV.2 Komponen External: Perangkat *Smart Waste Bin*
[52](#komponen-external-perangkat-smart-waste-bin)](#komponen-external-perangkat-smart-waste-bin)

[IV.2.1 Deskripsi Fungsional Perangkat
[53](#deskripsi-fungsional-perangkat)](#deskripsi-fungsional-perangkat)

[IV.2.2 Spesifikasi *Interface* Data
[55](#spesifikasi-interface-data)](#spesifikasi-interface-data)

[IV.3 Peningkatan *Firmware* Perangkat *Smart Waste Bin*
[57](#peningkatan-firmware-perangkat-smart-waste-bin)](#peningkatan-firmware-perangkat-smart-waste-bin)

[IV.3.1 Perubahan Interval Pengambilan Data
[58](#perubahan-interval-pengambilan-data)](#perubahan-interval-pengambilan-data)

[IV.3.2 Implementasi Median *Filter*
[59](#implementasi-median-filter)](#implementasi-median-filter)

[IV.3.3 Mekanisme *Auto-recovery*
[61](#mekanisme-auto-recovery)](#mekanisme-auto-recovery)

[IV.3.4 Warmup Sensor [62](#warmup-sensor)](#warmup-sensor)

[IV.3.5 Optimasi Daya [63](#optimasi-daya)](#optimasi-daya)

[IV.4 *Middleware*: Data Gateway
[65](#middleware-data-gateway)](#middleware-data-gateway)

[IV.4.1 Arsitektur *Flow* Node-RED
[65](#arsitektur-flow-node-red)](#arsitektur-flow-node-red)

[IV.4.2 Konfigurasi *Node* [67](#konfigurasi-node)](#konfigurasi-node)

[IV.4.3 Alur Pemrosesan Data
[70](#alur-pemrosesan-data)](#alur-pemrosesan-data)

[IV.4.4 *Deployment* dan Operasional Node-RED
[71](#deployment-dan-operasional-node-red)](#deployment-dan-operasional-node-red)

[IV.5 *Database* [71](#database)](#database)

[IV.5.1 Spesifikasi *Platform* *Database*
[71](#spesifikasi-platform-database)](#spesifikasi-platform-database)

[IV.5.2 Desain Skema *Database*
[72](#desain-skema-database)](#desain-skema-database)

[IV.6 *Dashboard* [75](#dashboard)](#dashboard)

[IV.6.1 Arsitektur *Dashboard*
[75](#arsitektur-dashboard)](#arsitektur-dashboard)

[IV.6.2 Implementasi API [76](#implementasi-api)](#implementasi-api)

[IV.6.3 Implementasi Antarmuka
[77](#implementasi-antarmuka)](#implementasi-antarmuka)

[IV.6.4 *Dashboard* *Hosting*
[80](#dashboard-hosting)](#dashboard-hosting)

[BAB V HASIL DAN EVALUASI
[82](#hasil-dan-evaluasi)](#hasil-dan-evaluasi)

[V.1 Metode Evaluasi [82](#metode-evaluasi)](#metode-evaluasi)

[V.1.1 Konfigurasi Pengujian Sistem
[82](#konfigurasi-pengujian-sistem)](#konfigurasi-pengujian-sistem)

[V.1.2 Skenario Evaluasi [84](#skenario-evaluasi)](#skenario-evaluasi)

[V.2 Hasil Evaluasi [85](#hasil-evaluasi)](#hasil-evaluasi)

[V.2.1 Hasil Evaluasi Fungsionalitas Sistem (SE-01)
[85](#hasil-evaluasi-fungsionalitas-sistem-se-01)](#hasil-evaluasi-fungsionalitas-sistem-se-01)

[V.2.2 Hasil Evaluasi Pengumpulan Data (SE-02)
[92](#hasil-evaluasi-pengumpulan-data-se-02)](#hasil-evaluasi-pengumpulan-data-se-02)

[V.2.3 Hasil Analisis Pola Pembuangan Sampah (SE-03)
[99](#hasil-analisis-pola-pembuangan-sampah-se-03)](#hasil-analisis-pola-pembuangan-sampah-se-03)

[V.2.4 Hasil Evaluasi Peningkatan Sistem (SE-04)
[111](#hasil-evaluasi-peningkatan-sistem-se-04)](#hasil-evaluasi-peningkatan-sistem-se-04)

[V.3 Pemenuhan Kebutuhan Sistem
[113](#pemenuhan-kebutuhan-sistem)](#pemenuhan-kebutuhan-sistem)

[V.3.1 Pemenuhan Kebutuhan Fungsional
[113](#pemenuhan-kebutuhan-fungsional)](#pemenuhan-kebutuhan-fungsional)

[V.3.2 Pemenuhan Kebutuhan Nonfungsional
[115](#pemenuhan-kebutuhan-nonfungsional)](#pemenuhan-kebutuhan-nonfungsional)

[V.4 Diskusi Hasil Evaluasi
[116](#diskusi-hasil-evaluasi)](#diskusi-hasil-evaluasi)

[V.4.1 Analisis Konsumsi Daya pada Sensor 3
[116](#analisis-konsumsi-daya-pada-sensor-3)](#analisis-konsumsi-daya-pada-sensor-3)

[V.4.2 Validitas Temuan [117](#validitas-temuan)](#validitas-temuan)

[V.4.3 Implikasi Praktis Pengelolaan Sampah
[119](#implikasi-praktis-pengelolaan-sampah)](#implikasi-praktis-pengelolaan-sampah)

[BAB VI KESIMPULAN DAN SARAN
[120](#kesimpulan-dan-saran)](#kesimpulan-dan-saran)

[VI.1 Kesimpulan [120](#kesimpulan)](#kesimpulan)

[VI.2 Saran [122](#saran)](#saran)

\
DAFTAR LAMPIRAN

[LAMPIRAN A TAUTAN PENTING
[131](#lampiran-a-tautan-penting)](#lampiran-a-tautan-penting)

[LAMPIRAN B ANTAR MUKA DASHBOARD
[132](#lampiran-b-antar-muka-dashboard)](#lampiran-b-antar-muka-dashboard)

[LAMPIRAN C BUKTI KESALAHAN PEMILAHAN SAMPAH OLEH PENGGUNA
[135](#lampiran-c-bukti-kesalahan-pemilahan-sampah-oleh-pengguna)](#lampiran-c-bukti-kesalahan-pemilahan-sampah-oleh-pengguna)

[LAMPIRAN D PEMASANGAN TEMPAT SAMPAH
[137](#lampiran-d-pemasangan-tempat-sampah)](#lampiran-d-pemasangan-tempat-sampah)

DAFTAR GAMBAR

[Gambar II.1 IoT Reference Model 3 *Layer* (Sethi dan Sarangi, 2017)
[16](#_Toc223586787)](#_Toc223586787)

[Gambar III.1 Kriteria Evaluasi Alternatif Solusi
[41](#_Toc223586788)](#_Toc223586788)

[Gambar IV.1 Arsitektur Sistem *Smart waste bin*
[46](#_Toc223586789)](#_Toc223586789)

[Gambar IV.2 *Data* *Flow* *Diagram* Level 0
[48](#_Toc223586790)](#_Toc223586790)

[Gambar IV.3 *Data* *Flow* *Diagram* Level 1
[49](#_Toc223586791)](#_Toc223586791)

[Gambar IV.4 Diagram Blok Fungsional Perangkat *Smart waste bin*
[53](#_Toc223586792)](#_Toc223586792)

[Gambar IV.5 *Payload* Data Perangkat
[57](#_Toc223586793)](#_Toc223586793)

[Gambar IV.6 *Flow* Node-RED [67](#_Toc223586794)](#_Toc223586794)

[Gambar IV.7 Tabel sensor_data [74](#_Toc223586795)](#_Toc223586795)

[Gambar IV.8 Contoh *Response* GET [79](#_Toc223586796)](#_Toc223586796)

[Gambar V.1 Statistik *fillLevel* [102](#_Toc223586797)](#_Toc223586797)

[Gambar V.2 Distribusi *fillLevel* per Rentang Jam
[104](#_Toc223586798)](#_Toc223586798)

[Gambar V.3 Rata-rata *fillLevel* per Hari dalam Seminggu
[105](#_Toc223586799)](#_Toc223586799)

[Gambar V.4 Rata-rata *fillLevel* Berdasarkan Kategori Hari
[106](#_Toc223586800)](#_Toc223586800)

[Gambar V.5 Distribusi Kategori Delta dan Delta per Rentang Jam
[108](#_Toc223586801)](#_Toc223586801)

[Gambar V.6 Perbandingan Pola Jenis Sampah
[109](#_Toc223586802)](#_Toc223586802)

DAFTAR TABEL

[Tabel III.1 Kebutuhan Fungsional [34](#_Toc223689758)](#_Toc223689758)

[Tabel III.2 *Mapping* Rumusan Masalah dengan Kebutuhan Fungsional
[35](#_Toc223689759)](#_Toc223689759)

[Tabel III.3 Kebutuhan Nonfungsional
[36](#_Toc223689760)](#_Toc223689760)

[Tabel III.4 Pemenuhan Kebutuhan Fungsional per Alternatif
[39](#_Toc223689761)](#_Toc223689761)

[Tabel III.5 Kriteria Evaluasi Alternatif Solusi
[41](#_Toc223074007)](#_Toc223074007)

[Tabel III.6 Matriks Perbandingan Kriteria Berpasangan
[42](#_Toc223074008)](#_Toc223074008)

[Tabel III.7 Bobot Kriteria Hasil AHP
[42](#_Toc223074009)](#_Toc223074009)

[Tabel III.8 Matriks Perbandingan Berpasangan Alternatif pada Setiap
Kriteria [43](#_Toc223074010)](#_Toc223074010)

[Tabel III.9 Bobot Lokal Alternatif pada Setiap Kriteria
[43](#_Toc223074011)](#_Toc223074011)

[Tabel III.10 Skor Global untuk Setiap Alternatif Solusi
[44](#_Toc223689767)](#_Toc223689767)

[Tabel IV.1 Deskripsi Komponen DFD Level 1
[49](#_Toc223074012)](#_Toc223074012)

[Tabel IV.2 Alur Data DFD Level 1 [50](#_Toc223689769)](#_Toc223689769)

[Tabel IV.3 Pemilihan Teknologi [51](#_Toc223689770)](#_Toc223689770)

[Tabel IV.4 Fungsi setiap Komponen *Smart waste bin*
[53](#_Toc223689771)](#_Toc223689771)

[Tabel IV.5 Spesifikasi Konektivitas MQTT
[55](#_Toc223689772)](#_Toc223689772)

[Tabel IV.6 *Payload* Data Perangkat
[55](#_Toc223689773)](#_Toc223689773)

[Tabel IV.7 Peningkatan *Firmware* [57](#_Toc223689774)](#_Toc223689774)

[Tabel IV.8 Urutan *Shutdown* [64](#_Toc223689775)](#_Toc223689775)

[Tabel IV.9 Konfigurasi MQTT [67](#_Toc223689776)](#_Toc223689776)

[Tabel IV.10 Konfigurasi *Node* JSON
[68](#_Toc223689777)](#_Toc223689777)

[Tabel IV.11 Konfigurasi *Node* HTTP Request
[68](#_Toc223689778)](#_Toc223689778)

[Tabel IV.12 Konfigurasi HTTP *Header*s
[69](#_Toc223689779)](#_Toc223689779)

[Tabel IV.13 Konfigurasi *Node* Debug
[69](#_Toc223689780)](#_Toc223689780)

[Tabel IV.14 Konfigurasi *Node* Inject
[70](#_Toc223689781)](#_Toc223689781)

[Tabel IV.15 Spesifikasi *Deployment* dan Operasional Node-RED
[71](#_Toc223689782)](#_Toc223689782)

[Tabel IV.16 Spesifikasi *Hosting* *Dashboard*
[72](#_Toc223689783)](#_Toc223689783)

[Tabel IV.17 Detil sensor_data [73](#_Toc223689784)](#_Toc223689784)

[Tabel IV.18 Komponen Teknologi *Dashboard*
[75](#_Toc223689785)](#_Toc223689785)

[Tabel IV.19 Spesifikasi API Endpoint
[76](#_Toc223689786)](#_Toc223689786)

[Tabel IV.20 Nilai Parameter *Time* *Range*
[76](#_Toc223689787)](#_Toc223689787)

[Tabel IV.21 *State* *Variable* [78](#_Toc223689788)](#_Toc223689788)

[Tabel IV.22 Spesifikasi Dashboard *Hosting*
[80](#_Toc223689789)](#_Toc223689789)

[Tabel V.1 Detil Unit SWB [83](#_Toc223689790)](#_Toc223689790)

[Tabel V.2 Konfigurasi Lingkungan [83](#_Toc223689791)](#_Toc223689791)

[Tabel V.3 *Mapping* Rumusan Masalah dengan Skenario Evaluasi
[84](#_Toc223689792)](#_Toc223689792)

[Tabel V.4 Pengujian Fungsionalitas Sistem
[86](#_Toc223689793)](#_Toc223689793)

[Tabel V.5 Hasil Pengujian Sensor VL53L0X
[87](#_Toc223689794)](#_Toc223689794)

[Tabel V.6 Hasil Pengujian Sensor INA219
[88](#_Toc223689795)](#_Toc223689795)

[Tabel V.7 Hasil Pengujian Modem GPRS
[88](#_Toc223689796)](#_Toc223689796)

[Tabel V.8 Hasil Pengujian MQTT [89](#_Toc223689797)](#_Toc223689797)

[Tabel V.9 Hasil Pengujian Node-RED
[90](#_Toc223689798)](#_Toc223689798)

[Tabel V.10 Hasil Pengujian API *Dashboard*
[91](#_Toc223689799)](#_Toc223689799)

[Tabel V.11 Hasil Pengujian Komponen *Dashboard*
[91](#_Toc223689800)](#_Toc223689800)

[Tabel V.12 Detil Pengumpulan Data [92](#_Toc223689801)](#_Toc223689801)

[Tabel V.13 Hasil Jumlah Data [93](#_Toc223689802)](#_Toc223689802)

[Tabel V.14 Statistik Interval Pengiriman Data
[94](#_Toc223689803)](#_Toc223689803)

[Tabel V.15 Penyebab *Data loss* dan Kotor
[94](#_Toc223689804)](#_Toc223689804)

[Tabel V.16 Jenis-jenis Data Kotor [96](#_Toc223689805)](#_Toc223689805)

[Tabel V.17 Hasil Kualitas Data [97](#_Toc223689806)](#_Toc223689806)

[Tabel V.18 Jumlah Record per Rentang Jam
[98](#_Toc223689807)](#_Toc223689807)

[Tabel V.19 Jumlah Record per Hari [98](#_Toc223689808)](#_Toc223689808)

[Tabel V.20 Statistik *fillLevel* [99](#_Toc223689809)](#_Toc223689809)

[Tabel V.21 Distribusi *fillLevel*
[101](#_Toc223689810)](#_Toc223689810)

[Tabel V.22 Pola Temporal Harian [101](#_Toc223689811)](#_Toc223689811)

[Tabel V.23 Pola Temporal Mingguan
[102](#_Toc223689812)](#_Toc223689812)

[Tabel V.24 Pola Hari Libur [104](#_Toc223689813)](#_Toc223689813)

[Tabel V.25 Analisis Delta *fillLevel*
[105](#_Toc223689814)](#_Toc223689814)

[Tabel V.26 Delta *fillLevel* per Rentang Jam
[105](#_Toc223689815)](#_Toc223689815)

[Tabel V.27 Pola Setiap Jenis Sampah
[106](#_Toc223689816)](#_Toc223689816)

[Tabel V.28 Perbandingan Jenis Tempat Sampah
[108](#_Toc223689817)](#_Toc223689817)

[Tabel V.29 Perhitungan Estimasi Volume per Orang per Hari
[108](#_Toc223689818)](#_Toc223689818)

[Tabel V.30 Kesesuaian Jenis Sampah
[110](#_Toc223689819)](#_Toc223689819)

[Tabel V.31 Hasil Evaluasi Peningkatan *Firmware*
[111](#_Toc223689820)](#_Toc223689820)

[Tabel V.32 Pemenuhan Kebutuhan Fungsional
[113](#_Toc223689821)](#_Toc223689821)

[Tabel V.33 Pemenuhan Kebutuhan Nonfungsional
[115](#_Toc223689822)](#_Toc223689822)

[Tabel V.34 Validasi Pola dengan Observasi Lapangan
[118](#_Toc223689823)](#_Toc223689823)

DAFTAR KODE

[Kode IV.1 Implementasi Perubahan Interval Pengambilan Data
[59](#_Toc223676163)](#_Toc223676163)

[Kode IV.2 Implementasi *Median* *Filter* pada Pembacaan Sensor
[60](#_Toc223676164)](#_Toc223676164)

[Kode IV.3 Implementasi *Auto-recovery* Sensor
[61](#_Toc223676165)](#_Toc223676165)

[Kode IV.4 Implementasi *Power* *Cycle* Sensor
[62](#_Toc223676166)](#_Toc223676166)

[Kode IV.5 Implementasi Warmup Sensor
[63](#_Toc223676167)](#_Toc223676167)

[Kode IV.6 Implementasi GPIO *Isolation*
[64](#_Toc223676168)](#_Toc223676168)

**DAFTAR PERSAMAAN\**

[Persamaan IV.1 Persentase *Fill Level*
[54](#_Toc223586641)](#_Toc223586641)

[Persamaan IV.2 *State of Charge* Baterai
[54](#_Toc223586642)](#_Toc223586642)

#  PENDAHULUAN

## Latar Belakang

Pertumbuhan populasi global dan urbanisasi yang pesat telah meningkatkan
volume produksi sampah secara signifikan. Menurut World Bank, produksi
sampah global diproyeksikan mencapai 3,4 miliar ton pada tahun 2050,
meningkat dari 2,01 miliar ton pada tahun 2016 (Kaza dkk. 2018).
Peningkatan volume sampah ini menimbulkan tantangan kompleks dalam
pengelolaan limbah yang efisien dan berkelanjutan.

Salah satu tantangan utama dalam pengelolaan sampah adalah ketiadaan
data terstruktur mengenai pola pembuangan. Pertanyaan seperti kapan
terjadi puncak pembuangan, apakah ada perbedaan pola antara hari kerja
dan akhir pekan, serta jenis sampah apa yang mendominasi, menjadi sulit
dijawab tanpa sistem monitoring yang memadai. Metode konvensional
seperti pengecekan visual atau pencatatan manual memiliki keterbatasan
dalam hal konsistensi, akurasi, dan cakupan waktu, sehingga pengambilan
keputusan sering dilakukan tanpa basis data.

Perkembangan teknologi *Internet of Things* (IoT) membuka peluang untuk
mengatasi permasalahan tersebut. Sensor yang dipasang pada tempat sampah
dapat memantau tingkat kepenuhan secara periodik, menyimpan data ke
basis data, dan menghasilkan insight mengenai pola pembuangan. Di
Indonesia, salah satu contoh perangkat *Smart Waste Bin* yang telah
dikembangkan adalah produk dari PT Layanan Cerdas Indonesia (LCI), yang
telah diimplementasikan di beberapa kota untuk pemantauan kapasitas
kontainer sampah (Layanan Cerdas Indonesia, 2024). Namun, perangkat
*Smart Waste Bin* yang tersedia secara komersial umumnya dirancang untuk
skala perkotaan, sehingga konfigurasi perangkat termasuk *firmware*
belum tentu sesuai untuk lingkungan yang lebih kecil seperti kampus, di
mana dinamika pembuangan sampah berubah dalam hitungan jam dan
memerlukan resolusi data yang lebih tinggi.

Berdasarkan permasalahan tersebut, penelitian ini bertujuan untuk
mengembangkan sistem *Smart Waste Bin* berbasis IoT yang disesuaikan
dengan kebutuhan lingkungan kampus, baik dari sisi perangkat lunak
sistem maupun *firmware* perangkat. Sistem yang dibangun kemudian diuji
di Gedung Labtek VIII ITB untuk mengumpulkan data dan menganalisis pola
pembuangan sampah yang dihasilkan.

## Rumusan Masalah

Berdasarkan latar belakang dan permasalahan di atas, penelitian ini
merumuskan pertanyaan penelitian sebagai berikut:

1.  Bagaimana rancangan dan implementasi sistem *Smart Waste Bin*
    berbasis IoT yang mampu mengumpulkan data pembuangan sampah secara
    periodik dan terstruktur?

2.  Pola pembuangan sampah apa yang dapat diidentifikasi berdasarkan
    data yang dikumpulkan oleh sistem, dan seberapa valid pola tersebut
    terhadap observasi lapangan?

3.  Peningkatan *firmware* apa yang diperlukan agar perangkat *Smart
    Waste Bin* yang dirancang untuk skala perkotaan dapat beroperasi
    secara optimal di lingkungan kampus?

## Tujuan

Penelitian ini bertujuan untuk mengimplementasikan dan mengevaluasi
sistem *Smart Waste Bin* berbasis *Internet of Things* untuk memahami
pola pembuangan sampah di Gedung Labtek VIII ITB. Secara detil, tujuan
penelitian ini adalah:

1.  Merancang arsitektur dan mengimplementasikan sistem *Smart Waste
    Bin* berbasis IoT yang mampu mengumpulkan data pembuangan sampah
    secara periodik dan terstruktur.

2.  Mengidentifikasi pola pembuangan sampah berdasarkan data yang
    dikumpulkan oleh sistem dan memvalidasinya melalui observasi
    lapangan.

3.  Mengevaluasi dan mengusulkan peningkatan *firmware* agar perangkat
    *Smart Waste Bin* yang dirancang untuk skala perkotaan dapat
    beroperasi secara optimal di lingkungan kampus.

## Batasan Masalah

Penelitian ini memiliki batasan-batasan berikut:

1.  Pengujian lapangan dari sistem yang dibangun dilakukan di Lantai 4
    area depan Laboratorium IoT, Gedung Labtek VIII Institut Teknologi
    Bandung.

2.  Sistem menggunakan 3 unit perangkat *Smart Waste Bin* yang
    masing-masing ditempatkan berdasarkan jenis sampah: organik,
    anorganik, dan residu.

3.  Perangkat IoT yang digunakan merupakan modifikasi dari perangkat
    *Smart Waste Bin* pihak ketiga yang disesuaikan untuk kebutuhan
    lingkungan kampus.

4.  Interval pengumpulan data ditetapkan ±2,5 jam berdasarkan
    pertimbangan kapasitas daya baterai perangkat.

5.  Klasifikasi jenis sampah mengacu pada penempatan fisik tempat sampah
    (organik, anorganik, residu), bukan melalui sensor klasifikasi
    otomatis.

6.  Analisis pola pembuangan sampah mencakup pola temporal (distribusi
    jam dan hari), tren volume, serta komposisi jenis sampah berdasarkan
    data yang dikumpulkan sistem.

## Metodologi

Pelaksanaan tugas akhir ini didukung oleh studi literatur dan
menggunakan pendekatan *Design* *Thinking* untuk pengembangan sistem.
Studi literatur dilakukan untuk membangun fondasi teoritis dan memahami
teknologi yang relevan, sedangkan *Design Thinking* digunakan sebagai
*framework* pengembangan solusi yang berfokus pada kebutuhan pengguna.

### Studi Literatur

Studi literatur dilakukan untuk mengumpulkan informasi yang relevan
tentang topik yang diangkat, mencakup teori, konsep, teknologi, dan
penelitian terdahulu yang telah dilakukan oleh peneliti lain. Studi
literatur ini menjadi fondasi dalam pengembangan sistem *Smart Waste
Bin* berbasis *Internet of Things*.

Aktivitas yang dilakukan pada tahap studi literatur meliputi:

1.  Pencarian Literatur

> Melakukan pencarian literatur dari berbagai sumber akademik dan
> ilmiah, seperti jurnal internasional, konferensi, artikel ilmiah,
> buku, dan dokumentasi teknis. Pencarian dilakukan menggunakan basis
> data akademik seperti IEEE *Xplore*, *Google* *Scholar*,
> *ScienceDirect*, dan *Springer*. Kata kunci yang digunakan dalam
> pencarian mencakup: \"*smart waste bin*\", \"IoT *waste management*\",
> \"*waste pattern analysis*\", \"*smart waste monitoring*\",
> \"*sensor-based waste management*\", dan kombinasi kata kunci lainnya
> yang relevan.

2.  Pengelompokan Literatur

> Literatur yang diperoleh dikelompokkan berdasarkan kategori-kategori
> seperti, konsep dan teori dasar tentang *Internet of Things* (IoT),
> teknologi sensor dan perangkat keras untuk *monitoring* sampah,
> arsitektur sistem dan integrasi IoT, penelitian terdahulu tentang
> *smart waste bin* dan pengelolaan sampah berbasis teknologi, dan
> metode analisis data temporal.

3.  Penapisan dan Evaluasi Literatur

> Literatur yang telah dikumpulkan disaring berdasarkan relevansi,
> kualitas publikasi, dan kebaruan informasi.

1.  Sintesis dan Dokumentasi

> Hasil studi literatur disintesis untuk mengidentifikasi *gap*
> penelitian, *best practices*, dan pendekatan yang dapat diadopsi atau
> dikembangkan lebih lanjut. Seluruh proses studi literatur
> didokumentasikan dan hasil sintesisnya akan dijelaskan secara
> sistematis di Bab II Studi Literatur.

### Pendekatan *Design Thinking*

Pengembangan sistem *Smart Waste Bin* menggunakan pendekatan Design
Thinking yang mencakup lima tahap utama, yaitu Empati, Definisi, Ideasi,
Prototipe, dan Pengujian. Pendekatan ini dipilih karena berfokus pada
pemahaman kebutuhan pengguna dan pengembangan solusi secara iteratif.
Berikut adalah penjelasan untuk setiap tahapan *Design Thinking* yang
diterapkan secara spesifik pada penelitian ini:

1.  Empati

    Tahap empati bertujuan untuk memahami kondisi aktual pengelolaan
    sampah dan pola pembuangan sampah di Gedung Labtek VIII ITB,
    khususnya di area Lantai 4 yang menjadi lokasi penelitian. Aktivitas
    pada tahap ini meliputi.

<!-- -->

a.  Melakukan pengamatan langsung terhadap kondisi sistem pembuangan
    eksisting yang masih bersifat konvensional tanpa adanya sistem
    *monitoring*.

<!-- -->

2.  Definisi

    Tahap definisi bertujuan untuk merumuskan permasalahan utama yang
    akan diselesaikan berdasarkan hasil analisis dari tahap empati.
    Aktivitas pada tahap ini meliputi:

<!-- -->

a.  Mengolah data dan informasi untuk mengidentifikasi gap atau
    permasalahan inti terkait ketiadaan sistem pengumpulan data yang
    terstruktur dan batasan fungsionalitas sistem vendor.

b.  Merumuskan spesifikasi kebutuhan sistem yang ideal, yang mencakup
    pendefinisian Kebutuhan Fungsional (pengumpulan data, penyimpanan,
    dan visualisasi pola) serta Kebutuhan Nonfungsional (performa dan
    reliabilitas).

<!-- -->

3.  Ideasi

    Setelah masalah terdefinisi, tahap ideasi dilakukan untuk
    mengembangkan berbagai alternatif arsitektur dan solusi teknologi.
    Aktivitas pada tahap ini meliputi:

    a.  Mengeksplorasi berbagai alternatif pendekatan dalam membangun
        sistem.

    b.  Mengeksplorasi ide-ide peningkatan (*enhancement*) pada sisi
        *firmware* perangkat keras bawaan vendor untuk mengoptimalkan
        keandalan dan konsumsi daya.

    c.  Mengevaluasi dan memilih alternatif solusi terbaik menggunakan
        metode pengambilan keputusan yang terukur berdasarkan kriteria
        kelayakan teknis, kesesuaian tujuan, waktu, dan biaya.

4.  Prototipe

    Tahap prototipe bertujuan untuk mewujudkan rancangan arsitektur dan
    solusi yang telah dipilih pada tahap ideasi menjadi sistem *Smart
    Waste Bin* yang fungsional. Aktivitas pada tahap ini meliputi:

    a.  Mengembangkan dan mengimplementasikan penyesuaian pada sisi
        *firmware* perangkat keras bawaan untuk mengoptimalkan keandalan
        operasional sistem.

    b.  Mengembangkan sistem penerimaan, transmisi, dan penyimpanan data
        pembuangan sampah sesuai dengan arsitektur yang terpilih.

    c.  Mengintegrasikan seluruh komponen perangkat keras dan perangkat
        lunak sehingga membentuk satu kesatuan yang dapat beroperasi
        secara otomatis.

    d.  Melakukan pengujian awal terhadap prototipe sistem untuk
        memastikan setiap komponen berfungsi dengan baik, serta
        melakukan perbaikan jika ditemukan kekurangan sebelum
        diimplementasikan di lapangan.

5.  Pengujian

    Tahap pengujian bertujuan untuk mengevaluasi kinerja sistem *Smart
    Waste Bin* yang telah dikembangkan dan mengumpulkan data pembuangan
    sampah dalam periode tertentu di lapangan. Aktivitas pada tahap ini
    meliputi:

    a.  Mengimplementasikan pengumpulan data dengan menempatkan unit
        *smart waste bin* pada lokasi yang telah ditentukan.

    b.  Melakukan *monitoring* terhadap operasional sistem selama
        periode pengumpulan data untuk memastikan sistem merekam dan
        mentransmisikan data dengan konsisten.

    c.  Mengevaluasi hasil pengumpulan data untuk memahami pola
        pembuangan sampah di lokasi penelitian, beserta evaluasi
        terhadap efektivitas peningkatan sistem yang telah dikembangkan.

#  STUDI LITERATUR

Bab ini menyajikan hasil studi literatur sebagaimana ditetapkan pada
Subbab I.5.1. Studi literatur dilakukan untuk membangun fondasi teoritis
yang mendasari perancangan dan implementasi sistem *Smart Waste Bin*
berbasis IoT. Pembahasan mencakup tiga topik utama: pengelolaan sampah
dan tantangannya dalam konteks lingkungan kampus, teknologi *Internet of
Things* beserta arsitektur dan komponen yang relevan, serta studi
terkait sistem *Smart Waste Bin* yang telah dikembangkan sebelumnya.

## Pengelolaan Sampah

Pengelolaan sampah merupakan kegiatan sistematis yang mencakup
pengumpulan, pengangkutan, pemrosesan, daur ulang, dan pembuangan
material sampah yang dihasilkan dari aktivitas manusia. Pengelolaan
sampah yang efektif harus mempertimbangkan aspek teknis, ekonomi,
lingkungan, dan sosial untuk mencapai tujuan keberlanjutan (Giurea dkk.
2024). Sistem pengelolaan sampah yang baik tidak hanya berfokus pada
pembuangan akhir, tetapi juga pada pengurangan volume sampah dari
sumbernya, pemilahan, dan pemanfaatan kembali material yang masih
memiliki nilai.

### Konsep Dasar Pengelolaan Sampah 

Dalam konteks hierarki pengelolaan sampah, terdapat beberapa tingkatan
prioritas yang harus dipertimbangkan berdasarkan *Waste Framework
Directive*. Tingkatan tertinggi adalah pencegahan dan pengurangan sampah
di sumber (*waste prevention and reduction*), diikuti oleh persiapan
untuk penggunaan kembali (*preparing for reuse*), daur ulang
(*recycling*), pemulihan energi (*energy* *recovery*), dan terakhir
adalah pembuangan akhir (*disposal*) (European Commission, 2008).
Pendekatan hierarkis ini menekankan pentingnya upaya pr*event*if dan
pemanfaatan nilai ekonomi dari sampah sebelum melakukan pembuangan.

Pengelolaan sampah modern juga menerapkan prinsip *circular* *economy*
yang bertujuan untuk meminimalkan limbah dan memaksimalkan pemanfaatan
sumber daya melalui sistem yang tertutup. *Circular economy*
didefinisikan sebagai sistem regeneratif di mana *input* sumber daya,
limbah, emisi, dan kebocoran energi diminimalkan melalui strategi
memperlambat, menutup, dan mempersempit aliran material dan energi
(Geissdoerfer dkk. 2017). Dalam konteks institusi pendidikan tinggi,
penerapan *circular economy* mencakup tiga dimensi keberlanjutan:
ekonomi, ekologi, dan sosial, yang bekerja secara sinergis untuk
menciptakan sistem pengelolaan sampah yang tidak hanya ramah lingkungan,
tetapi juga bertanggung jawab secara ekonomi dan sosial (Giurea dkk.
2024).

*Sustainable* *Development* *Goals* (SDGs) yang ditetapkan oleh *United
Nations* juga menekankan pentingnya pengelolaan sampah berkelanjutan
sebagai bagian dari upaya mencapai dunia yang lebih berkelanjutan dan
berkeadilan pada tahun 2030 (United Nations, 2015). Pengelolaan sampah
yang efektif berkontribusi pada beberapa SDGs, termasuk kota dan
komunitas berkelanjutan (SDG 11), konsumsi dan produksi yang bertanggung
jawab (SDG 12), serta aksi iklim (SDG 13).

### Tantangan Pengelolaan Sampah pada Lingkungan Kampus

Lingkungan kampus dan gedung perkuliahan memiliki karakteristik unik
dalam hal pengelolaan sampah yang membedakannya dari lingkungan
perkotaan pada umumnya. Institusi pendidikan tinggi menghadapi tantangan
khusus karena kepadatan populasi yang tinggi, variasi aktivitas yang
beragam, dan pola penggunaan yang dinamis sepanjang hari dan minggu
(Bahçelioğlu dkk. 2020). Karakteristik ini menyebabkan volume dan
komposisi sampah yang dihasilkan sangat bervariasi tergantung pada
waktu, aktivitas akademik, dan kegiatan yang berlangsung di gedung.

Berdasarkan *review* komprehensif terhadap penelitian tentang
pengelolaan sampah di institusi pendidikan tinggi, rata-rata tingkat
produksi sampah adalah 0,19 ± 0,21 kg/hari per orang (median 0,093
kg/hari per orang) (Rodríguez-Guerreiro dkk. 2024). Komposisi sampah
didominasi oleh sampah organik yang mencapai rata-rata 30 ± 19% dari
total sampah, diikuti oleh kertas dan kardus (23 ± 13%), dan plastik (18
± 11%) (Bahçelioğlu dkk. 2020).

Salah satu tantangan utama adalah keterbatasan data mengenai pola
pembuangan sampah. Penelitian menunjukkan bahwa sebagian besar institusi
pendidikan mengalami kesulitan dalam melacak kapan, di mana, dan berapa
banyak sampah yang dihasilkan karena tidak memiliki sistem *monitoring*
yang memadai (Bahçelioğlu dkk. 2020). Tanpa data yang *reliable*,
pengambilan keputusan terkait pengelolaan sampah menjadi tidak akurat,
menghambat perencanaan strategis yang efektif, dan mempersulit pelacakan
*progress* terhadap tujuan pengurangan sampah (Sensoneo, 2024).

Tantangan lain yang dihadapi adalah variasi temporal dalam produksi
sampah. Kampus dapat mengalami fluktuasi volume sampah yang signifikan
antara periode aktif perkuliahan dan periode libur, dengan volume sampah
dapat turun hingga sebagian kecil dari volume normal dalam waktu singkat
(RoadRunner, 2024). Pola pembuangan sampah juga sangat dipengaruhi oleh
jadwal perkuliahan, waktu istirahat, dan aktivitas khusus seperti
seminar atau acara. Tanpa pemahaman yang baik terhadap pola temporal
ini, alokasi sumber daya untuk pengumpulan sampah menjadi tidak efisien.

Tingkat partisipasi pengguna dalam pemilahan sampah juga menjadi
tantangan tersendiri. Meskipun banyak kampus telah menyediakan fasilitas
untuk pemilahan sampah, tingkat kepatuhan dan konsistensi dalam
pemilahan masih rendah. Kontaminasi dalam aliran daur ulang terjadi
ketika material yang tidak dapat didaur ulang tercampur dengan yang
dapat didaur ulang, mengurangi efisiensi program daur ulang dan
meningkatkan biaya pemrosesan (Sensoneo, 2024). Hal ini menunjukkan
perlunya sistem yang tidak hanya menyediakan infrastruktur fisik, tetapi
juga mekanisme untuk meningkatkan kesadaran dan partisipasi pengguna.

Tantangan operasional lainnya mencakup pengumpulan sampah yang tidak
efisien, dengan *pickup* yang sering dilakukan pada tempat sampah yang
masih kosong atau sebagian terisi, mengakibatkan pemborosan bahan bakar,
jam kerja, dan biaya pemeliharaan. Kondisi bin yang meluap tidak hanya
menciptakan lingkungan kampus yang tidak menarik, tetapi juga
berkontribusi pada kontaminasi aliran daur ulang karena orang berhenti
memilah sampah dan membuangnya ke bin kosong terdekat tanpa
memperhatikan jenis bin tersebut (Sensoneo, 2024).

### Data dalam Pengelolaan Sampah

Data merupakan fondasi penting dalam pengambilan keputusan untuk
pengelolaan sampah yang efektif dan efisien. Sistem pengelolaan sampah
berbasis data memungkinkan identifikasi pola, prediksi kebutuhan, dan
optimalisasi operasional yang tidak dapat dicapai melalui pendekatan
konvensional (Vishnu dkk. 2022). Dengan data yang akurat dan
terstruktur, pengelola dapat memahami karakteristik sampah yang
dihasilkan, mengidentifikasi area atau waktu yang memerlukan perhatian
khusus, dan merancang strategi pengelolaan yang lebih responsif.

Keputusan yang diambil berdasarkan data sampah yang tidak *reliable*
dapat mengganggu akurasi pelaporan keberlanjutan dan menghambat
perencanaan strategis yang efektif. Tanpa data yang dapat diandalkan,
sulit untuk melacak kemajuan terhadap tujuan pengurangan sampah,
mengidentifikasi inefisiensi, atau mengoptimalkan jadwal pengumpulan
(Sensoneo, 2024). Data yang tidak konsisten atau tidak akurat juga dapat
menyebabkan pengambilan keputusan yang buruk dalam alokasi sumber daya.

Pengumpulan data secara sistematis memungkinkan analisis tren jangka
panjang yang dapat mengungkapkan perubahan pola pembuangan sampah
seiring waktu. Banyak faktor dapat mempengaruhi pola ini, termasuk
perubahan populasi, kebijakan institusi, kampanye kesadaran lingkungan,
atau perubahan musiman. Integrasi teknologi *Internet of Things* (IoT)
memungkinkan *monitoring* *real-time* terhadap tingkat kepenuhan tempat
sampah, lokasi, dan kondisi lingkungan, yang menghasilkan data berharga
untuk analisis dan visualisasi (Sriaadhibhatla, 2025).

Data juga memainkan peran krusial dalam optimalisasi operasional
pengumpulan sampah. Sistem *Smart* *Bin* yang dilengkapi dengan sensor
*fill-level* menyediakan data *real-time* mengenai tingkat kepenuhan
sampah, memungkinkan kendaraan pengumpul sampah untuk memprioritaskan
rute berdasarkan tingkat kepenuhan bin (Sriaadhibhatla, 2024).
Optimalisasi ini mengurangi konsumsi bahan bakar, biaya tenaga kerja,
dan emisi gas rumah kaca. Pendekatan berbasis data ini mengubah model
pengumpulan dari jadwal tetap (*fixed schedule*) menjadi model
*on-demand* atau prediktif yang lebih efisien.

Pemanfaatan teknologi sensor ultrasonik, *Time-of-Flight* (*ToF*), dan
perangkat IoT lainnya memungkinkan *monitoring* bin secara *real-time*,
yang dapat memberikan *alert* ketika bin mendekati atau mencapai
kapasitas penuh (Pires dkk. 2025). Sistem ini tidak hanya meningkatkan
efisiensi operasional, tetapi juga mencegah kondisi bin yang meluap yang
dapat menciptakan risiko kesehatan dan lingkungan yang tidak menarik.

Selain itu, data pembuangan sampah dapat memberikan *insight* berharga
untuk pengembangan program edukasi dan perubahan perilaku. Dengan
memahami kapan dan di mana sampah paling banyak dihasilkan, serta jenis
sampah yang dominan, institusi dapat merancang intervensi yang lebih
spesifik untuk mengurangi produksi sampah atau meningkatkan tingkat daur
ulang. Dalam konteks institusi pendidikan tinggi, data pengelolaan
sampah juga berkontribusi pada pelaporan keberlanjutan (*sustainability*
*reporting*) yang semakin menjadi standar dalam akreditasi dan *ranking*
universitas internasional. Pengelolaan sampah yang komprehensif
merupakan salah satu komponen utama dalam mencapai keberlanjutan
institusional (Bahçelioğlu dkk. 2020). Oleh karena itu, ketersediaan
data yang akurat dan terverifikasi mengenai pengelolaan sampah menjadi
penting tidak hanya untuk operasional, tetapi juga untuk reputasi dan
akuntabilitas institusi.

## *Internet of Things*

*Internet of Things* (IoT) didefinisikan sebagai konsep yang
menghubungkan benda fisik dan virtual melalui jaringan internet untuk
memungkinkan pertukaran data secara otomatis. Kevin Ashton, yang pertama
kali memperkenalkan istilah IoT pada tahun 1999, menjelaskan bahwa IoT
memungkinkan komputer untuk secara mandiri mengumpulkan informasi tanpa
bantuan manusia. Hal ini dapat mengurangi pemborosan, biaya, serta
meningkatkan efisiensi dengan memberikan kemampuan bagi komputer untuk
\"melihat, mendengar, dan mencium\" dunia di sekitarnya secara mandiri.
Dengan cara ini, IoT memungkinkan pelacakan, penghitungan, dan perawatan
benda secara lebih efektif, termasuk mengetahui kapan benda perlu
diganti atau diperbaiki (Ashton, 2009).

IoT dapat dipahami sebagai keberadaan pervasif dari berbagai objek yang
mampu berinteraksi dan bekerja sama satu sama lain melalui skema
pengalamatan yang unik untuk mencapai tujuan bersama (Atzori dkk. 2010).
Definisi ini memperluas gagasan IoT dengan menekankan kemampuan objek
untuk berkolaborasi secara mandiri dalam ekosistem yang terhubung.

Dokumen dari *International Telecommunication Union Telecommunication
Standardization Sector* (*ITU-T*) menambahkan dimensi yang lebih luas
dengan mendefinisikan IoT sebagai infrastruktur global yang mendukung
layanan canggih melalui konektivitas benda fisik dan virtual menggunakan
teknologi informasi dan komunikasi yang terus berkembang. IoT juga
dianggap sebagai visi dengan implikasi teknologi dan sosial yang
signifikan, di mana keamanan dan privasi menjadi aspek yang tidak
terpisahkan (Telecommunication Union Telecommunication Standardization
Sector, 2012).

Sementara itu, IoT *European Research Cluster* (*IERC*) mendefinisikan
IoT sebagai infrastruktur jaringan global yang dinamis dengan kemampuan
konfigurasi mandiri, menggunakan protokol komunikasi standar dan
interoperabel. Benda fisik dan virtual memiliki identitas, atribut
fisik, dan kepribadian virtual yang terintegrasi secara mulus ke dalam
jaringan informasi (IoT European Research Cluster, 2014). Pendekatan ini
menekankan pada kemampuan IoT untuk mengintegrasikan benda secara cerdas
ke dalam sistem informasi global.

*ISO/IEC* *Joint Technical Committee* *1* (*JTC1*) memberikan pandangan
serupa dengan mendefinisikan IoT sebagai infrastruktur yang
menghubungkan objek, manusia, sistem, dan sumber daya informasi bersama
dengan layanan cerdas untuk memproses informasi dari dunia fisik dan
virtual serta memberikan respons yang relevan (ISO/IEC Joint Technical
Committee 1, 2024).

Dengan berbagai definisi dari berbagai organisasi standar, *Internet of
Things* (IoT) secara umum dapat didefinisikan sebagai infrastruktur
global yang menghubungkan benda fisik dan virtual melalui jaringan
internet, memungkinkan pertukaran data secara otomatis tanpa intervensi
manusia yang signifikan. IoT mengintegrasikan elemen-elemen seperti
sensor, aktuator, dan identitas unik, yang memungkinkan benda
berkomunikasi dan berkolaborasi secara mandiri untuk mencapai tujuan
tertentu. Selain itu, IoT menawarkan layanan canggih dengan memastikan
interoperabilitas teknologi, keamanan, dan privasi, serta memberikan
manfaat signifikan dalam berbagai sektor seperti transportasi,
kesehatan, manufaktur, dan kota pintar.

### Arsitektur *Internet of Things*

Arsitektur *Internet of Things* (IoT) bertujuan untuk menciptakan
sinergi antara berbagai sistem yang memungkinkan perangkat-perangkat IoT
untuk berkomunikasi dan saling beroperasi secara otomatis. Tujuan utama
dari arsitektur IoT adalah menyediakan layanan inovatif dengan
interoperabilitas yang andal. Untuk mencapai ini, standar global
diperlukan agar *platform* IoT dapat mendukung integrasi sistem yang
berbeda secara efisien.

Meskipun IoT diharapkan dapat merevolusi berbagai sektor ekonomi,
keberadaannya juga menghadirkan tantangan besar terkait pengelolaan,
pemrosesan, dan transmisi data. Tantangan ini menimbulkan kebutuhan akan
standar keamanan untuk melindungi individu, bisnis, dan pemerintah yang
menggunakan sistem IoT. Selain itu, arsitektur referensi (*Reference
Architecture/RA*) menjadi penting untuk mendefinisikan pedoman yang
dapat digunakan selama perencanaan dan implementasi sistem IoT (Hasan
dkk. 2017).

Berbagai organisasi standar, industri, dan universitas telah berupaya
untuk mengembangkan arsitektur referensi untuk IoT. Model ini mencakup
arsitektur berlapis yang memungkinkan interoperabilitas antar sistem IoT
yang berbeda. Contoh standar yang telah dikembangkan termasuk
spesifikasi *oneM2M*, yang menciptakan kerangka kerja untuk mendukung
aplikasi seperti *smart grid*, mobil terhubung, otomatisasi rumah,
keselamatan publik, dan kesehatan. Selain itu, IEEE dan ITU juga telah
berkontribusi dengan mengembangkan standar dan arsitektur referensi yang
mencakup domain aplikasi IoT yang luas.

Berbagai arsitektur referensi lain seperti Industrial Internet Reference
Architecture (IIRA) dan Reference Architecture Model for Industrie 4.0
(RAMI 4.0) dirancang untuk meningkatkan efisiensi proses industri dengan
menggunakan teknologi IoT. RAMI 4.0, misalnya, fokus pada pengoptimalan
proses industri seperti penelitian, pengembangan, logistik, dan layanan.
Selain itu, Sensor Network Reference Architecture (SNRA) memberikan
gambaran umum tentang jaringan sensor yang digunakan untuk pengumpulan
data pada sistem IoT.

Salah satu model arsitektur IoT yang paling fundamental dan banyak
diadopsi adalah model tiga *layer* yang terdiri dari *Perception Layer*,
*Network Layer*, dan *Application Layer* (Sethi dan Sarangi, 2017).
Model ini menyediakan kerangka dasar untuk memahami bagaimana
komponen-komponen IoT berinteraksi dari tingkat perangkat fisik hingga
aplikasi pengguna akhir.

![[]{#_Toc223586787 .anchor}Gambar II.1 IoT Reference Model 3 *Layer*
(Sethi dan Sarangi,
2017)](./media/media/image5.png){alt="A screenshot of a phone AI-generated content may be incorrect."
width="2.319410542432196in" height="3.034783464566929in"}

Berikut adalah penjelasan untuk setiap *layer* pada arsitektur IoT:

1.  *Perception Layer*

*Perception Layer* yang juga dikenal sebagai *Physical Layer* atau
*Device Layer*, merupakan lapisan paling bawah dalam arsitektur IoT.
*Layer* ini terdiri dari perangkat fisik seperti sensor, aktuator, *RFID
tags*, dan perangkat IoT lainnya yang berinteraksi langsung dengan
lingkungan fisik (Al-Fuqaha dkk. 2015). Fungsi utama dari *layer* ini
adalah untuk mengumpulkan data dari lingkungan sekitar, seperti suhu,
kelembaban, tekanan, gerak, atau parameter lainnya sesuai dengan jenis
sensor yang digunakan.

> Dalam konteks sistem *Smart Waste Bin*, *Perception Layer* mencakup
> sensor ultrasonik atau *load cell* yang dipasang pada tempat sampah
> untuk mengukur tingkat kepenuhan atau berat sampah. Sensor-sensor ini
> mengubah fenomena fisik menjadi sinyal digital yang dapat diproses
> oleh sistem. *Layer* ini juga dapat mencakup *actuator* yang
> memberikan respons fisik berdasarkan data yang diterima, meskipun
> dalam sistem *monitoring* seperti *smart waste bin*, fokus utamanya
> adalah pada fungsi *sensing*.
>
> Karakteristik penting dari *Perception Layer* adalah kemampuannya
> untuk beroperasi dalam berbagai kondisi lingkungan, efisiensi energi
> (terutama untuk perangkat yang menggunakan baterai), dan akurasi dalam
> pengukuran. Pemilihan sensor yang tepat pada *layer* ini sangat
> menentukan kualitas data yang akan dikumpulkan dan dianalisis pada
> *layer*-*layer* di atasnya.

2.  *Network Layer*

> *Network Layer* berfungsi sebagai jembatan komunikasi yang
> menghubungkan *Perception Layer* dengan *Application Layer*. *Layer*
> ini bertanggung jawab untuk transmisi data yang dikumpulkan oleh
> sensor ke sistem pemrosesan atau *cloud* *server* (Al-Fuqaha dkk.
> 2015). *Network Layer* menggunakan berbagai protokol komunikasi dan
> teknologi jaringan, seperti Wi-Fi, Ethernet, LoRaWAN, NB-IoT, Zigbee,
> Bluetooth, atau protokol komunikasi lainnya, tergantung pada kebutuhan
> jarak, *bandwidth*, dan konsumsi energi dari aplikasi spesifik.
>
> Fungsi utama *Network Layer* mencakup transmisi data dari perangkat
> IoT ke *server* atau *cloud* *platform*, pengelolaan berbagai protokol
> komunikasi untuk memastikan data dapat dikirim dengan format yang
> tepat, pengoperasian *gateway* atau *edge* *devices* yang berfungsi
> sebagai perantara antara sensor dan jaringan internet, serta
> implementasi enkripsi dan mekanisme keamanan untuk melindungi data
> selama transmisi. *Layer* ini memainkan peran krusial dalam memastikan
> data dapat dikirimkan dengan andal, efisien, dan aman dari sumber data
> hingga ke sistem pemrosesan.
>
> Dalam sistem *Smart Waste Bin*, *Network Layer* dapat menggunakan
> koneksi Wi-Fi atau *cellular network* (seperti 4G/5G) untuk
> mengirimkan data tingkat kepenuhan sampah dari lokasi tempat sampah ke
> *server* pusat secara periodik. Pemilihan teknologi komunikasi pada
> *layer* ini harus mempertimbangkan faktor-faktor seperti cakupan area,
> ketersediaan infrastruktur jaringan, biaya operasional, dan kebutuhan
> *bandwidth* untuk memastikan sistem dapat beroperasi secara optimal
> dan berkelanjutan.

3.  *Application Layer*

> *Application Layer* merupakan lapisan tertinggi dalam arsitektur IoT
> yang berfungsi untuk menyediakan layanan dan antarmuka kepada pengguna
> akhir (Al-Fuqaha dkk. 2015). *Layer* ini mencakup aplikasi yang
> memproses, menganalisis, dan memvisualisasikan data yang diterima dari
> *Network Layer*. Pada *layer* ini juga terdapat sistem manajemen data,
> analitik, dan *dashboard* yang memungkinkan pengguna untuk memantau
> kondisi, mengambil keputusan, atau melakukan kontrol terhadap
> perangkat IoT.
>
> Komponen utama dalam *Application Layer* mencakup pemrosesan data
> mentah menjadi informasi yang bermakna, penyimpanan data historis
> dalam *database* atau data *warehouse*, visualisasi informasi melalui
> *dashboard* dan *interface*, penyediaan aplikasi web atau *mobile*
> yang memungkinkan interaksi pengguna dengan sistem, serta sistem
> pendukung keputusan yang memberikan rekomendasi atau *alert*
> berdasarkan analisis data. *Layer* ini bertindak sebagai jembatan
> antara data teknis yang dikumpulkan dari perangkat IoT dengan
> kebutuhan bisnis atau operasional pengguna akhir.
>
> Dalam konteks sistem *Smart Waste Bin*, *Application Layer* mencakup
> sistem *database* untuk menyimpan data pembuangan sampah secara
> terstruktur, serta *dashboard* atau *interface* yang memungkinkan
> pengelola untuk melihat status tempat sampah dan hasil analisis pola
> pembuangan. *Layer* ini memungkinkan transformasi data mentah dari
> sensor menjadi *insight* yang dapat digunakan untuk pengambilan
> keputusan dalam pengelolaan sampah.

### Komponen Perangkat Keras pada IoT

Implementasi sistem *Internet of Things* memerlukan komponen *hardware*
yang berfungsi sebagai jembatan antara dunia fisik dan dunia digital.
Komponen-komponen ini berada pada *Perception Layer* dalam arsitektur
IoT dan berperan dalam pengumpulan data dari lingkungan serta pemrosesan
awal sebelum data dikirimkan ke sistem *backend* (Khanna 2024).
*Hardware* IoT mencakup berbagai perangkat mulai dari *microcontroller*
sebagai unit pemrosesan, sensor untuk pengumpulan data, hingga modul
komunikasi untuk transmisi data.

1.  *Microcontroller*

> *Microcontroller* merupakan komputer kecil dalam satu *chip* yang
> berfungsi sebagai \"otak\" dari perangkat IoT. *Microcontroller*
> bertanggung jawab untuk membaca data dari sensor, memproses data
> tersebut, dan mengirimkannya ke *server* atau *cloud* melalui protokol
> komunikasi tertentu. Berbeda dengan mikroprosesor yang memerlukan
> komponen eksternal seperti memori dan *interface* *I/O*,
> *microcontroller* mengintegrasikan semua komponen ini dalam satu
> *chip*, termasuk *CPU*, *RAM*, *ROM*/*Flash* *memory*, dan berbagai
> *peripheral* seperti *ADC* (*Analog-to-Digital Converter*), *timer*,
> dan *port* komunikasi.
>
> Beberapa *platform* *microcontroller* yang umum digunakan dalam
> pengembangan sistem IoT meliputi Arduino, ESP32, ESP8266, dan
> Raspberry Pi. Arduino merupakan *platform* *open-source* yang populer
> untuk *prototyping* dengan dukungan *library* yang luas dan komunitas
> pengguna yang besar, menjadikannya pilihan yang baik untuk pengembang
> pemula maupun profesional. ESP32 dan ESP8266 adalah *microcontroller*
> berbasis arsitektur Xtensa yang dikembangkan oleh Espressif Systems,
> dilengkapi dengan *Wi-Fi* dan Bluetooth *built-in*, menjadikannya
> pilihan populer untuk aplikasi IoT yang memerlukan konektivitas
> nirkabel tanpa memerlukan modul komunikasi eksternal tambahan.
> Raspberry Pi, meskipun secara teknis merupakan *single-board computer*
> dengan sistem operasi lengkap, sering digunakan dalam proyek IoT yang
> memerlukan daya komputasi lebih tinggi, kemampuan *multitasking*, atau
> *interfacing* dengan berbagai perangkat *peripheral*. Pemilihan
> *microcontroller* dalam implementasi sistem IoT bergantung pada
> beberapa faktor, termasuk kebutuhan daya pemrosesan, konsumsi energi,
> ketersediaan *interface* komunikasi, dukungan *library* dan ekosistem
> pengembangan, serta biaya implementasi. Untuk aplikasi *monitoring*
> sederhana seperti pembacaan sensor secara periodik, *microcontroller*
> dengan spesifikasi rendah hingga menengah umumnya sudah memadai dan
> dapat menghemat konsumsi daya (Ooko 2019).

  --------------------------------------------------------------------------------------------
     **Kriteria**        **Arduino**      **Raspberry       **ESP8266           **ESP32**
                                             Pi**          *Node*MCU**     
  ------------------ ------------------- ------------- ------------------- -------------------
    **Pengembang**         Arduino       Raspberry Pi  ESP8266 Open Source  Espressif Systems
                                          Foundation        Community      

       **Tipe**         Single Board     Mini Computer    Single Board        Single Board
                      *Microcontroller*                 *Microcontroller*   *Microcontroller*

  **Sistem Operasi**        None             Linux            XTOS              FreeRTOS

       **CPU**        Atmel, ARM, Intel   ARM Cortex         LXT106         Dual-Core Xtensa
                                                                               32-bit LX6

     **Kecepatan           16 MHz           1.2 GHz      26 MHz - 52 MHz       160-240 MHz
       Clock**                                                             

      **Memori**            32 KB          1 - 4 GB       Hingga 128 MB        520 KB SRAM

   **Penyimpanan**          1 KB           MicroSDHC       4 MB Flash      Hingga 16 MB Flash
                                             Slot                          

       **Daya**         USB, Baterai,    USB, *Power*          USB         USB, *Power* Supply
                       *Power* Supply       Supply                         

      **Tegangan             5V               5V              3.3V                3.3V
      Operasi**                                                            

   **Konektivitas**          I/O           SPI, I2C,       UART, GPIO      UART, GPIO, Wi-Fi,
                                          UART, GPIO                          BLE, SPI, I2C
  --------------------------------------------------------------------------------------------

  : Table II.1 Perbandingan Arduino, Raspberry Pi, ESP8266 *Node* MCU
  (Ooko, 2019) dan ESP32 (Espressif Systems, 2021)

> Pada Tabel II.1, terlihat perbandingan karakteristik teknis dari empat
> *platform* *microcontroller* yang umum digunakan dalam aplikasi IoT:
> Arduino, Raspberry Pi, ESP8266 *Node*MCU, dan ESP32. Masing-masing
> *platform* memiliki spesifikasi dan fitur yang dirancang untuk
> memenuhi kebutuhan yang berbeda dalam pengembangan sistem IoT, dengan
> kelebihan dan keterbatasan yang perlu dipertimbangkan sesuai dengan
> karakteristik aplikasi yang akan dikembangkan.
>
> Arduino merupakan *microcontroller* sederhana yang ideal untuk
> pengendalian perangkat keras dasar, seperti pembacaan sensor dan
> kontrol *actuator*, tanpa memerlukan sistem operasi. Dengan kecepatan
> *clock* sebesar 16 MHz dan memori 32 KB, Arduino cocok digunakan untuk
> aplikasi dengan kebutuhan komputasi ringan dan konsumsi daya yang
> minimal. Dukungan komunitas yang luas, dokumentasi yang lengkap, dan
> ketersediaan *library* yang matang menjadikannya pilihan yang tepat
> untuk pembelajaran dasar IoT, *prototyping* cepat, atau pengembangan
> aplikasi *monitoring* sederhana (Ooko 2019). Raspberry Pi memiliki
> karakteristik yang berbeda secara fundamental, lebih menyerupai
> komputer mini lengkap dibandingkan *microcontroller* tradisional.
> Dilengkapi dengan CPU ARM Cortex berkecepatan 1,2 GHz dan memori
> hingga 4 GB, Raspberry Pi menjalankan sistem operasi Linux lengkap,
> yang memungkinkannya digunakan untuk aplikasi IoT yang memerlukan
> pemrosesan data kompleks, *multitasking*, atau *interfacing* dengan
> berbagai *peripheral*. Raspberry Pi cocok untuk aplikasi yang
> memerlukan pemrosesan data skala besar, visualisasi *real*-*time*,
> atau integrasi dengan berbagai protokol komunikasi. Namun, konsumsi
> daya yang lebih tinggi dan kompleksitas sistem operasi menjadi
> pertimbangan untuk aplikasi yang memerlukan efisiensi energi tinggi
> atau *deployment* pada perangkat berbasis baterai (Ooko 2019). ESP8266
> *Node*MCU dirancang khusus untuk aplikasi IoT yang memerlukan
> konektivitas jaringan dengan biaya rendah. Modul ini memiliki
> konektivitas Wi-Fi terintegrasi, membuatnya ideal untuk aplikasi yang
> membutuhkan transmisi data ke *server* atau *cloud* *platform* tanpa
> memerlukan modul komunikasi eksternal tambahan. Dengan memori hingga
> 128 MB dan tegangan operasi 3,3V, ESP8266 menawarkan keseimbangan
> antara kapabilitas pemrosesan dan efisiensi daya. Kecepatan *clock*
> antara 26-52 MHz memberikan kapabilitas yang memadai untuk aplikasi
> *monitoring* dan kontrol sederhana hingga menengah. ESP8266 sering
> dipilih untuk sistem pengukuran lingkungan, pengendalian perangkat
> rumah pintar, atau aplikasi telemetri yang memerlukan konektivitas
> nirkabel dengan *budget* terbatas (Ooko 2019). ESP32 merupakan evolusi
> dari ESP8266 yang menawarkan peningkatan signifikan dalam hal performa
> dan fitur.
>
> Dikembangkan oleh *Espressif* *Systems*, ESP32 dilengkapi dengan
> prosesor *dual-core* Xtensa 32-bit LX6 dengan kecepatan *clock* hingga
> 240 MHz, memberikan kapabilitas pemrosesan yang jauh lebih tinggi
> dibandingkan pendahulunya. ESP32 mendukung konektivitas Wi-Fi dan
> *Bluetooth Low Energy* (*BLE*) secara simultan, memberikan
> fleksibilitas komunikasi yang lebih besar untuk aplikasi IoT modern
> yang memerlukan *multiple* *connectivity* *options*. Dengan memori
> SRAM sebesar 520 KB dan penyimpanan *flash* hingga 16 MB, ESP32 dapat
> menangani aplikasi yang lebih kompleks, termasuk pemrosesan data
> tingkat lanjut, pengelolaan *multiple* *sensors*, atau implementasi
> algoritma yang memerlukan komputasi lebih intensif (Ooko 2019).
> Dukungan sistem operasi *FreeRTOS* pada ESP32 memungkinkan pengelolaan
> *multitasking* yang lebih baik, dengan kemampuan menjalankan
> *multiple* *tasks* secara *concurrent*, menjadikannya pilihan ideal
> untuk aplikasi yang memerlukan pemrosesan paralel atau *real*-*time*
> *response*. ESP32 juga menawarkan fitur keamanan terintegrasi seperti
> enkripsi SSL/TLS, sensor sentuh kapasitif, antarmuka kamera, dan
> berbagai *peripheral* lainnya yang memperluas kemungkinan aplikasi.
> Kombinasi antara kinerja tinggi, efisiensi energi yang dapat
> dikonfigurasi melalui berbagai mode daya, fitur komunikasi yang
> komprehensif, dan harga yang kompetitif menjadikan ESP32 salah satu
> pilihan paling populer untuk pengembangan sistem IoT modern, mulai
> dari aplikasi sederhana hingga kompleks seperti *smart* *home*
> *systems*, *environmental monitoring networks*, dan *industrial* IoT
> *applications* (*Espressif Systems* 2021).
>
> Pemilihan *platform* *microcontroller* harus mempertimbangkan
> *trade-off* antara berbagai faktor seperti kompleksitas aplikasi,
> kebutuhan pemrosesan, konsumsi daya, *budget*, dan ekosistem
> pengembangan yang tersedia. Untuk aplikasi *monitoring* sederhana
> dengan pembacaan sensor periodik, Arduino atau ESP8266 dapat menjadi
> pilihan yang ekonomis dan efisien. Untuk aplikasi yang memerlukan
> konektivitas nirkabel dengan performa lebih tinggi, ESP32 menawarkan
> keseimbangan terbaik antara fitur dan biaya. Sementara untuk aplikasi
> yang memerlukan pemrosesan kompleks atau integrasi dengan sistem yang
> lebih besar, Raspberry Pi dapat menjadi pilihan yang lebih sesuai
> meskipun dengan konsumsi daya dan kompleksitas yang lebih tinggi.

2.  *Sensor* dan *actuator*

> Sensor adalah perangkat yang mendeteksi dan merespons *input* dari
> lingkungan fisik, mengubah fenomena fisik seperti suhu, kelembaban,
> tekanan, cahaya, gerakan, atau parameter lainnya menjadi sinyal
> elektrik yang dapat dibaca dan diproses oleh *microcontroller*. Dalam
> sistem IoT, sensor berfungsi sebagai mata dan telinga yang
> memungkinkan sistem untuk \"merasakan\" kondisi lingkungan sekitar dan
> mengumpulkan data yang kemudian dapat dianalisis untuk berbagai tujuan
> aplikasi. Sensor dapat dikategorikan berdasarkan jenis parameter yang
> diukur atau prinsip kerja yang digunakan. Sensor aktif memerlukan
> sumber daya eksternal untuk beroperasi dan menghasilkan sinyal
> *output*, sementara sensor pasif menghasilkan *output* tanpa
> memerlukan sumber daya eksternal (Rayes dan Salam 2017). Dalam konteks
> IoT, sensor juga dapat dikategorikan berdasarkan jenis data yang
> dihasilkan: sensor analog yang menghasilkan sinyal kontinu, dan sensor
> digital yang menghasilkan sinyal diskrit yang dapat langsung dibaca
> oleh *microcontroller*. *Actuator*, di sisi lain, adalah perangkat
> yang melakukan aksi fisik berdasarkan perintah dari sistem kontrol.
> *Actuator* mengubah sinyal elektrik menjadi gerakan mekanis, panas,
> cahaya, atau bentuk energi lainnya (Mohamed 2019). Dalam sistem IoT,
> *actuator* memungkinkan sistem untuk tidak hanya mengamati lingkungan
> tetapi juga berinteraksi dan mengubah kondisi lingkungan berdasarkan
> data yang dikumpulkan dan logika yang diprogram. Meskipun banyak
> sistem IoT berfokus pada *monitoring* melalui sensor, integrasi
> *acuator* memungkinkan sistem untuk menjadi lebih interaktif dan
> responsif terhadap kondisi yang terdeteksi.

### Protokol Komunikasi IoT

Protokol komunikasi dalam sistem *Internet of Things* memainkan peran
krusial dalam memastikan interoperabilitas dan efisiensi pertukaran data
antar perangkat yang terhubung. Protokol-protokol ini dirancang untuk
mengatasi tantangan spesifik yang dihadapi oleh perangkat IoT, seperti
keterbatasan daya, *bandwidth* terbatas, dan kebutuhan akan komunikasi
yang andal dalam berbagai kondisi jaringan.1 Pemilihan protokol yang
tepat sangat bergantung pada karakteristik aplikasi, termasuk frekuensi
transmisi data, volume data, kebutuhan latensi, dan keterbatasan sumber
daya perangkat.

Protokol IoT dapat dikategorikan berdasarkan lapisan dalam model
referensi jaringan, dengan protokol *Application Layer* menjadi yang
paling relevan untuk komunikasi data antara perangkat IoT dan sistem
*backend*. Berbeda dengan protokol internet tradisional yang dirancang
untuk komputer dengan sumber daya yang melimpah, protokol IoT dirancang
khusus untuk beroperasi secara efisien pada perangkat dengan memori
terbatas, daya pemrosesan rendah, dan konsumsi energi yang minimal
(Hassan dkk. 2017).

1.  HTTP/HTTPS (Hypertext Transfer Protocol)

> HTTP merupakan protokol komunikasi berbasis *request-response* yang
> telah lama digunakan dalam komunikasi web dan telah diadopsi secara
> luas dalam aplikasi IoT. Protokol ini beroperasi di atas TCP
> (Transmission *Control* Protocol), yang menyediakan pengiriman data
> yang andal dengan mekanisme konfirmasi dan pengurutan paket.3 HTTPS
> adalah versi aman dari HTTP yang menggunakan enkripsi SSL/TLS untuk
> melindungi data selama transmisi, menjadikannya penting untuk aplikasi
> IoT yang menangani data sensitif.
>
> Kelebihan HTTP/HTTPS dalam konteks IoT meliputi kompatibilitas yang
> luas dengan infrastruktur web yang ada, dukungan *library* yang matang
> di berbagai *platform* pemrograman, dan kemudahan integrasi dengan
> layanan *cloud*. Protokol ini cocok untuk aplikasi IoT yang tidak
> memerlukan komunikasi real-*time* dan memiliki akses ke sumber daya
> komputasi yang memadai. Namun, HTTP memiliki *overhead* yang relatif
> besar dibandingkan protokol IoT lainnya, yang dapat menjadi
> pertimbangan untuk perangkat dengan keterbatasan *bandwidth* atau daya
> (Hassan dkk. 2017).

2.  MQTT (*Message* Queuing Telemetry Transport)

MQTT adalah protokol *messaging* berbasis *publish-subscribe* yang
dirancang khusus untuk perangkat dengan sumber daya terbatas dan
jaringan dengan *bandwidth* rendah atau tidak stabil. Protokol ini
dikembangkan pada tahun 1999 oleh Andy Stanford-Clark dari IBM dan Arlen
Nipper untuk *monitoring* *pipeline* minyak melalui satelit.5 MQTT
beroperasi di atas TCP dan menggunakan model *broker* sentral yang
mengelola komunikasi antara *publisher* (perangkat yang mengirim data)
dan *subscriber* (aplikasi yang menerima data).

Arsitektur *publish-subscribe* MQTT memberikan beberapa keunggulan untuk
aplikasi IoT. Pertama, decoupling antara *publisher* dan *subscriber*
memungkinkan skalabilitas yang lebih baik karena perangkat tidak perlu
mengetahui alamat spesifik penerima data. Kedua, MQTT mendukung tiga
tingkat Quality of Service (QoS): QoS 0 (at most once), QoS 1 (at least
once), dan QoS 2 (exactly once), yang memungkinkan aplikasi untuk
menyeimbangkan antara keandalan dan efisiensi sesuai kebutuhan.6 Ketiga,
MQTT memiliki *overhead* protokol yang sangat kecil, dengan *header*
minimum hanya 2 *bytes*, menjadikannya ideal untuk perangkat dengan
*bandwidth* terbatas.

MQTT juga mendukung fitur retained *message*s, di mana *broker* dapat
menyimpan pesan terakhir pada sebuah *topic* dan mengirimkannya kepada
*subscriber* baru yang bergabung, serta *last will and testament* (LWT)
yang memungkinkan perangkat untuk mengirim pesan otomatis ketika koneksi
terputus secara tidak terduga. Fitur-fitur ini menjadikan MQTT sangat
populer dalam aplikasi *monitoring* dan telemetri IoT (Hassan dkk.
2017).

3.  *CoAP* (*Constrained Application Protocol*)

> *CoAP* adalah protokol aplikasi web yang dirancang khusus untuk
> perangkat terkendali (*constrained devices*) dengan memori, daya
> pemrosesan, dan *bandwidth* yang sangat terbatas. Protokol ini
> dikembangkan oleh *IETF* (*Internet Engineering Task Force*)
> *Constrained RESTful Environments* (*CoRE*) *Working Group* dan
> didefinisikan dalam RFC 7252. *CoAP* dirancang untuk mengikuti prinsip
> *REST* (*Representational State Transfer*) seperti HTTP, namun dengan
> *overhead* yang jauh lebih kecil.
>
> Berbeda dengan HTTP yang menggunakan TCP, CoAP beroperasi di atas UDP
> (User Datagram Protocol), yang mengurangi *overhead* komunikasi dan
> konsumsi memori. CoAP menggunakan model *request-response* yang mirip
> dengan HTTP, dengan metode *GET*, *POST*, *PUT*, dan *DELETE*,
> sehingga memudahkan integrasi dengan sistem web yang ada. Protokol ini
> menggunakan format pesan biner yang ringkas, dengan *header* minimum
> hanya 4 *bytes*, yang secara signifikan lebih efisien dibandingkan
> HTTP.
>
> CoAP mendukung dua mode transmisi: *confirmablemessage*s (CON) yang
> memerlukan acknowledgment dari penerima, dan *non-confirmablemessage*s
> (*NON*) untuk data yang tidak kritis. Protokol ini juga mendukung
> *observe* *pattern*, yang memungkinkan *client* untuk \"*subscribe*\"
> pada sebuah *resource* dan menerima notifikasi ketika *resource*
> tersebut berubah, mirip dengan model *publish-subscribe*. *CoAP* cocok
> untuk aplikasi IoT yang memerlukan komunikasi *RESTful* namun
> beroperasi pada perangkat dengan keterbatasan sumber daya yang
> signifikan (Hassan dkk. 2017).

4.  Perbandingan Protokol

Pemilihan protokol komunikasi dalam implementasi sistem IoT bergantung
pada berbagai faktor, termasuk karakteristik perangkat, kebutuhan
aplikasi, dan kondisi jaringan. HTTP/HTTPS cocok untuk sistem yang
memerlukan integrasi mudah dengan infrastruktur web yang ada dan
memiliki akses ke sumber daya yang memadai. MQTT ideal untuk aplikasi
yang memerlukan komunikasi asinkron dengan *overhead* rendah dan
dukungan QoS yang fleksibel. CoAP merupakan pilihan terbaik untuk
perangkat dengan keterbatasan sumber daya yang ekstrem namun masih
memerlukan pola komunikasi RESTful.

Penelitian komparatif menunjukkan bahwa MQTT memiliki performa terbaik
dalam hal konsumsi *bandwidth* dan latensi untuk aplikasi telemetri,
sementara CoAP unggul dalam efisiensi penggunaan memori dan daya pada
perangkat terkendali. HTTP/HTTPS, meskipun memiliki *overhead* yang
lebih besar, menawarkan keuntungan dalam hal kemudahan implementasi dan
kompatibilitas dengan sistem *legacy* (Hassan dkk. 2017).

## Node-RED

Node-RED adalah *platform* pemrograman visual berbasis aliran
(*flow-based*) yang dikembangkan oleh IBM dan kini merupakan proyek
*open-source* di bawah naungan OpenJS Foundation. *Platform* ini
dirancang untuk menghubungkan perangkat keras, API, dan layanan daring
dengan cara yang mudah dipahami melalui antarmuka berbasis browser.
Node-RED berjalan di atas run*time* *Node*.js dan memungkinkan pengguna
untuk membuat alur pemrosesan data dengan cara menyusun dan
menghubungkan *node*-*node* fungsional tanpa harus menulis kode secara
eksplisit. (OpenJS Foundation, 2024)

Konsep utama Node-RED adalah *flow*, yaitu rangkaian *node* yang saling
terhubung melalui kabel (*wire*). Setiap *node* merepresentasikan satu
fungsi tertentu, seperti menerima pesan MQTT, melakukan transformasi
data, atau meneruskan data ke *database*. Terdapat tiga kategori *node*
utama: *input* *node* yang berfungsi sebagai sumber data (misalnya MQTT
In, HTTP In), *processing* *node* yang memanipulasi data (misalnya
*Function*, *Switch*, *Change*), serta *output* *node* yang mengirimkan
data ke tujuan akhir (misalnya HTTP *Request*, *Debug*, *database*
*node*). Arsitektur ini menjadikan Node-RED sangat fleksibel sebagai
komponen *middleware* dalam ekosistem IoT, karena mampu menjembatani
protokol komunikasi yang berbeda-beda dan mengintegrasikan berbagai
layanan dalam satu alur pemrosesan yang terpusat. (Blackstock dan Lea
2016)

Dalam konteks sistem IoT, Node-RED sering digunakan sebagai lapisan
*middleware* yang menerima data dari perangkat sensor melalui protokol
MQTT atau HTTP, kemudian memvalidasi, mentransformasi, dan meneruskan
data tersebut ke sistem penyimpanan atau layanan lainnya. Keunggulan
Node-RED dibandingkan pendekatan berbasis kode konvensional meliputi
kemudahan konfigurasi melalui antarmuka visual, ekosistem *node* yang
kaya (tersedia lebih dari 4.000 *node* tambahan di repositori publik),
serta kemampuan *deployment* yang cepat tanpa memerlukan proses
kompilasi. Selain itu, Node-RED mendukung pengelolaan alur secara
modular sehingga memudahkan pemeliharaan dan pengembangan sistem di
kemudian hari. (Clerissi dkk. 2018)

## Studi Terkait

Bagian ini mengkaji penelitian-penelitian terdahulu yang relevan dengan
topik pengembangan sistem *Smart Waste Bin*, dengan fokus pada metode
yang digunakan, hasil yang diperoleh, dan gap yang menjadi dasar
penelitian ini.

### Sistem *Smart Waste Bin* Berbasis IoT

Latifah dkk. mengembangkan sistem *Automated* *Trash Volume*
*Monitoring* berbasis *Internet of Things* (IoT) untuk meningkatkan
efisiensi pengelolaan sampah perkotaan. Sistem yang dikembangkan
mengintegrasikan sensor ultrasonik HC-SR04 untuk *monitoring* tingkat
kepenuhan tempat sampah secara real-*time*, mikrokontroler *Node*MCU
ESP8266 sebagai unit pemrosesan, dan *platform* Blynk sebagai
*interface* untuk visualisasi dan notifikasi kepada petugas kebersihan.
Sistem juga dilengkapi dengan servo motor yang mengoperasikan mekanisme
pembukaan dan penutupan tutup tempat sampah secara otomatis ketika
sensor infrared mendeteksi keberadaan pengguna pada jarak 50 cm,
bertujuan untuk mengurangi kontak langsung dengan tempat sampah dan
meminimalkan risiko penyebaran bakteri. Implementasi sistem menggunakan
sensor ultrasonik yang ditempatkan di bagian atas tempat sampah untuk
mengukur jarak antara sensor dan permukaan sampah, yang kemudian
dikonversi menjadi persentase kepenuhan. Data pembacaan sensor
dikirimkan ke *cloud* *platform* Blynk melalui koneksi Wi-Fi setiap
beberapa detik, memungkinkan *monitoring* real-*time* dari perangkat
mobile. Sistem juga mengimplementasikan *threshold-based*
*notification*, di mana *alert* otomatis dikirimkan kepada petugas
kebersihan ketika tingkat kepenuhan mencapai 80% atau lebih.

Hasil pengujian sistem menunjukkan akurasi pengukuran volume sebesar 97%
dengan *margin of error* 3%, menunjukkan reliabilitas tinggi dalam
*monitoring* kondisi tempat sampah. Pengujian dilakukan dengan
membandingkan pembacaan sensor terhadap pengukuran manual *actual* *fill
Level* pada berbagai kondisi. Sistem berhasil mengirimkan notifikasi
secara konsisten ketika threshold tercapai, dengan *average* *response*
*time* kurang dari 5 detik dari deteksi hingga notifikasi diterima.
Penelitian ini berkontribusi dalam demonstrasi *feasibility* sistem IoT
untuk *waste* *management* dengan *implementation* *cost* yang relatif
terjangkau.

#  ANALISIS MASALAH 

Bab ini merupakan pelaksanaan fase *Empathize* dan *Define* dari
pendekatan *Design Thinking* yang telah ditetapkan pada Subbab I.5.2.
Pada fase *Empathize*, dilakukan observasi langsung terhadap kondisi
pengelolaan sampah di Gedung Labtek VIII ITB untuk memahami permasalahan
yang dihadapi. Pada fase *Define*, hasil observasi dirumuskan menjadi
kebutuhan sistem, baik fungsional maupun nonfungsional, serta
dilanjutkan dengan pemilihan solusi menggunakan metode AHP.

Bab ini menguraikan tiga aspek. Pertama, analisis kondisi saat ini yang
mengidentifikasi permasalahan pengelolaan sampah akibat tidak adanya
data terstruktur mengenai pola pembuangan. Kedua, analisis kebutuhan
yang merumuskan spesifikasi sistem berdasarkan permasalahan yang
ditemukan. Ketiga, pemilihan solusi melalui evaluasi alternatif untuk
menentukan pendekatan yang paling sesuai dengan tujuan penelitian.

## Analisis Kondisi Saat Ini

Berdasarkan observasi yang dilakukan di Gedung Labtek VIII, kondisi
pengelolaan sampah saat ini bersifat konvensional. Tempat sampah tidak
dilengkapi sensor atau sistem monitoring, pengecekan dilakukan secara
visual oleh petugas kebersihan, dan pengumpulan sampah dilakukan
berdasarkan jadwal tetap tanpa mempertimbangkan kondisi aktual
kepenuhan.

Dari kondisi tersebut, teridentifikasi tiga permasalahan utama:

1.  Ketiadaan Data Terstruktur Mengenai Pola Pembuangan Sampah.

> Sistem pengelolaan sampah saat ini tidak memiliki mekanisme untuk
> mengumpulkan data mengenai pola pembuangan. Tidak ada informasi
> mengenai kapan puncak pembuangan terjadi, apakah ada perbedaan pola
> antara hari kerja dan akhir pekan, atau jenis sampah apa yang
> mendominasi. Pengambilan keputusan dilakukan tanpa basis data yang
> memadai.

2.  Tidak Ada Dokumentasi Data Historis.

> Sistem saat ini tidak mendokumentasikan data pembuangan sampah dalam
> format yang terstruktur. Akibatnya, analisis tren jangka panjang,
> identifikasi perubahan pola seiring waktu, dan evaluasi efektivitas
> strategi pengelolaan tidak dapat dilakukan.

3.  Pengelolaan Berdasarkan Jadwal Tetap tanpa Umpan Balik Data dan
    Pengecekan Visual Manual.

> Pengumpulan sampah dilakukan berdasarkan jadwal tetap dan pengecekan
> visual secara manual tanpa mempertimbangkan kondisi aktual kepenuhan
> sebelum pengecekan. Pendekatan ini berpotensi menyebabkan inefisiensi,
> di mana pengumpulan dilakukan terlalu cepat saat tempat sampah masih
> kosong atau terlambat saat sudah penuh.

Di sisi lain, perangkat *Smart Waste Bin* berbasis IoT yang tersedia
secara komersial umumnya dirancang untuk skala perkotaan. Konfigurasi
bawaan perangkat, termasuk interval pengiriman data dan mekanisme
pembacaan sensor pada *firmware*, belum tentu sesuai untuk lingkungan
yang lebih kecil seperti kampus, di mana dinamika pembuangan sampah
berubah dalam hitungan jam dan memerlukan titik data yang lebih tinggi.
Hal ini menunjukkan bahwa selain membangun sistem pengumpulan data,
diperlukan juga penyesuaian pada sisi *firmware* perangkat agar dapat
beroperasi secara optimal di lingkungan kampus.

Permasalahan tersebut menunjukkan bahwa pengelolaan sampah di lokasi
pengujian masih berfungsi untuk keperluan dasar, namun tidak dilengkapi
kemampuan untuk mengumpulkan dan menganalisis data mengenai pola
pembuangan sampah. Kebutuhan akan sistem *Smart Waste Bin* yang
disesuaikan, baik dari sisi perangkat lunak maupun firmware, menjadi
dasar analisis kebutuhan pada subbab berikutnya.

## Analisis Kebutuhan 

Analisis kebutuhan terbagi menjadi tiga bagian utama. Pertama,
identifikasi masalah dan kebutuhan dari perspektif pengguna sistem untuk
memahami *stakeholder* yang terlibat dan ekspektasi mereka terhadap
sistem. Kedua, perumusan kebutuhan fungsional yang mendeskripsikan
fungsi-fungsi spesifik yang harus dimiliki sistem untuk memenuhi tujuan
penelitian. Ketiga, spesifikasi kebutuhan nonfungsional yang
mendefinisikan karakteristik kualitas sistem.

### Identifikasi Pengguna

Sistem *Smart Waste Bin* yang akan dikembangkan memiliki beberapa
pengguna dengan kebutuhan yang berbeda-beda, yaitu:

1.  Pengurus Lantai/Pengelola Gedung

Pengelola gedung bertanggung jawab untuk pengawasan pengelolaan sampah
dan pengambilan keputusan terkait strategi pengelolaan. Kebutuhan utama
pengelola gedung adalah akses terhadap informasi mengenai pola
pembuangan sampah, tren volume sampah, dan *insight* yang dapat
mendukung perencanaan dan optimalisasi pengelolaan sampah.

2.  Peneliti/Developer Sistem

Peneliti bertanggung jawab untuk pengembangan, implementasi, dan
*maintenance* sistem. Kebutuhan peneliti meliputi akses terhadap *raw*
data untuk analisis, kemampuan untuk konfigurasi sistem (seperti
Interval pembacaan sensor atau *threshold*), dan *interface* untuk
*monitoring* status operasional sistem.

3.  Pengguna Gedung (*Indirect User*)

Meskipun pengguna gedung (mahasiswa, dosen, *staff*) tidak berinteraksi
langsung dengan sistem, mereka adalah sumber data pembuangan sampah.
Keberadaan *smart waste bin* tidak boleh mengubah atau mempersulit
proses pembuangan sampah bagi pengguna gedung.

### Kebutuhan Fungsional

Kebutuhan fungsional menjelaskan fungsi-fungsi dan fitur-fitur yang
harus tersedia pada sistem. Berdasarkan identifikasi masalah dan
kebutuhan pengguna, kebutuhan fungsional sistem *Smart Waste Bin* adalah
sebagai berikut:

  ---------------------------------------------------------------------------
  **ID**   **Komponen**   **Kebutuhan**          **Penjelasan**
  -------- -------------- ---------------------- ----------------------------
  KF-01    IoT *Device*   Pembacaan Sensor       Sistem harus dapat membaca
                                                 tingkat kepenuhan *waste
                                                 bin* menggunakan sensor
                                                 dengan Interval yang
                                                 ditentukan

  KF-02    IoT *Device*   Transmisi Data         Sistem harus dapat
                                                 mengirimkan data ke *server*
                                                 melalui protokol komunikasi
                                                 secara otomatis

  KF-03    IoT *Device*   *Time Stamping*        Setiap data harus dilengkapi
                                                 *Timestamp* dan identifier
                                                 *waste bin*

  KF-04    IoT *Device*   Konversi Data          Sistem harus dapat
                                                 mengkonversi jarak hasil
                                                 pembacaan sensor menjadi
                                                 persentase kepenuhan
                                                 (0-100%)

  KF-05    *Database*     Penyimpanan Data       Sistem harus dapat menyimpan
                                                 data sensor secara
                                                 terstruktur dan historis

  KF-06    *Database*     Pengambilan Data       Sistem dapat menyediakan
                                                 *query* untuk mengambil data
                                                 secara spesifik

  KF-07    Analisis       Analisis Pola Temporal Sistem harus dapat
                                                 mengidentifikasi pola
                                                 pembuangan berdasarkan waktu
                                                 (*hour*ly, daily, weekly)

  KF-08    Analisis       Statistik Deskriptif   Sistem harus dapat
                                                 menghasilkan statistik
                                                 deskriptif (*mean*, median,
                                                 std) untuk setiap pola

  KF-09    *Dashboard*    Visualisasi Data       *Dashboard* harus
                                                 menampilkan status kepenuhan
                                                 *waste bin* terbaru

  KF-10    *Dashboard*    Grafik Pola Temporal   *Dashboard* harus
                                                 menampilkan grafik pola
                                                 pembuangan per jam, per
                                                 hari, dan per minggu
  ---------------------------------------------------------------------------

  : []{#_Toc223689758 .anchor}Tabel III.1 Kebutuhan Fungsional

Berikut adalah *mapping* untuk setiap kebutuhan fungsional dengan
rumusan masalah pada Bab I.3 Rumusan Masalah.

  -----------------------------------------------------------------------
  Rumusan Masalah                     Kebutuhan Fungsional
  ----------------------------------- -----------------------------------
  RM-1: Rancangan dan implementasi    KF-01, KF-02, KF-03, KF-04, KF-05,
  sistem *Smart Waste Bin* berbasis   KF-06
  IoT yang mampu mengumpulkan data    
  secara periodik dan terstruktur     

  RM-2: Pola pembuangan sampah yang   KF-07, KF-08, KF-09, KF-10
  dapat diidentifikasi berdasarkan    
  data sistem dan validasinya         
  terhadap observasi lapangan         

  RM-3: Peningkatan *firmware* agar   KF-01, KF-02, KF-04 (evaluasi dan
  perangkat *Smart Waste Bin* skala   peningkatan)
  perkotaan dapat beroperasi optimal  
  di lingkungan kampus                
  -----------------------------------------------------------------------

  : []{#_Toc223689759 .anchor}Tabel III.2 *Mapping* Rumusan Masalah
  dengan Kebutuhan Fungsional

### Kebutuhan Nonfungsional

Kebutuhan nonfungsional mendeskripsikan karakteristik kualitas sistem
yang harus dipenuhi, mencakup aspek performa, keandalan, dan akurasi.
Berikut adalah tabel kebutuhan non-fungsional:

  --------------------------------------------------------------------------
  ID        Kategori        Kebutuhan           Penjelasan
  --------- --------------- ------------------- ----------------------------
  KNF-01    *Performance*   Waktu Pembacaan     Sensor harus dapat melakukan
                            Sensor              pembacaan dalam waktu
                                                maksimal 1 menit

  KNF-02    *Performance*   Latensi Transmisi   Data harus dikirim ke
                            Data                *server* dalam waktu
                                                maksimal 10 detik setelah
                                                pembacaan

  KNF-03    *Performance*   *Response* *Time*   *Dashboard* harus merespons
                            *Dashboard*         interaksi user dalam waktu
                                                maksimal 3 detik

  KNF-04    *Performance*   Waktu *Query*       *Query* data dari *database*
                                                harus selesai dalam waktu
                                                maksimal 5 detik

  KNF-05    *Reliability*   Up*time* Sistem IoT Sistem IoT harus beroperasi
                                                dengan availability minimal
                                                95%

  KNF-06    *Reliability*   Konsistensi         Pembacaan setiap 3 jam
                            Pembacaan           dengan toleransi
                                                keterlambatan maksimal ±15
                                                menit

  KNF-07    *Reliability*   Kelengkapan Data    Minimal 90% data harus
                                                berhasil dikumpulkan selama
                                                periode penelitian

  KNF-08    *Accuracy*      Akurasi Sensor      Pembacaan sensor harus
                                                memiliki galat maksimal 10%
                                                dari volume aktual
  --------------------------------------------------------------------------

  : []{#_Toc223689760 .anchor}Tabel III.3 Kebutuhan Nonfungsional

## Analisis Pemilihan Solusi 

Berdasarkan analisis kondisi saat ini dan kebutuhan sistem yang telah
diidentifikasi, terdapat beberapa alternatif pendekatan dalam
pengembangan sistem *Smart Waste Bin* berbasis IoT. Bagian ini akan
menguraikan alternatif-alternatif solusi yang dapat diterapkan serta
analisis pemilihan solusi menggunakan metode *Analytical Hierarchy
Process* (AHP).

### Alternatif Solusi

Berdasarkan analisis kebutuhan, seluruh alternatif solusi menggunakan
perangkat *Smart Waste Bin* yang tersedia dari pihak ketiga sebagai
basis perangkat keras. Perbedaan antar alternatif terletak pada
pendekatan *software stack* untuk pengumpulan data, *monitoring*, dan
kemudahan *maintenance* sistem. Analisis pola pembuangan (KF-07, KF-08)
pada seluruh alternatif dilakukan melalui *pipeline* analisis data
terpisah menggunakan *script* pengolahan data.

Terdapat tiga alternatif solusi yang dapat diimplementasikan:

1.  Alternatif 1: Perangkat *Smart Waste Bin* + *Platform Cloud*
    (ThingSpeak/Blynk)

> Menggunakan perangkat *Smart Waste Bin* dan mengintegrasikannya dengan
> platform IoT *cloud* untuk penyimpanan data dan visualisasi.

Karakteristik alternatif ini:

a.  Perangkat keras *Smart Waste Bin* dari pihak ketiga

b.  Platform *cloud* menyediakan *backend* dan *dashboard* siap pakai

c.  *Deployment* cepat dengan konfigurasi minimal

d.  Fitur analisis terbatas pada yang disediakan platform (grafik
    standar, *threshold alert*)

e.  Keterbatasan dalam *custom query* untuk analisis pola temporal yang
    kompleks

<!-- -->

2.  Alternatif 2: Perangkat *Smart Waste Bin* + *Backend Custom* +
    *Dashboard*

> Menggunakan perangkat *Smart Waste Bin*, mengembangkan *middleware*
> dan *backend custom* (Supabase PostgreSQL), serta membangun
> *dashboard* untuk *monitoring*.

Karakteristik alternatif ini:

a.  Perangkat keras *Smart Waste Bin* dari pihak ketiga

b.  *Backend custom* memungkinkan *query* fleksibel untuk analisis pola
    temporal

c.  *Dashboard custom* untuk *monitoring* status terkini dan visualisasi
    historis

d.  Dapat diintegrasikan dengan sistem lain di kemudian hari

e.  Memerlukan *effort* pengembangan *middleware* dan *dashboard*

<!-- -->

3.  Alternatif 3: Perangkat *Smart Waste Bin* + *Backend Custom* saja
    (Tanpa Dashboard)

Menggunakan perangkat *Smart Waste Bin* dan mengembangkan *backend*
*custom* untuk penyimpanan data, tanpa *dashboard* visual. *Monitoring*
dilakukan melalui *query database.*

Karakteristik alternatif ini:

a.  Perangkat keras *Smart Waste Bin* dari pihak ketiga

b.  *Backend custom* memungkinkan *query* fleksibel untuk analisis

c.  Tidak ada *interface* visual untuk *monitoring*

d.  *Maintenance* dan *monitoring* harus dilakukan manual via *query*
    *database*

e.  *Effort* pengembangan lebih rendah (tidak perlu *dashboard*)

Tabel berikut menyajikan pemenuhan kebutuhan fungsional untuk setiap
alternatif solusi.

  ------------------------------------------------------------------------
  Kebutuhan         Alt-1 (Platform  Alt-2 (Backend +    Alt-3 (Backend
                    Cloud)           Dashboard)          saja)
  ----------------- ---------------- ------------------- -----------------
  KF-01 s.d. KF-04  Terpenuhi        Terpenuhi           Terpenuhi
  (IoT *Device*)                                         

  KF-05, KF-06      Terbatas fitur   Terpenuhi           Terpenuhi
  (Database)        platform                             

  KF-07, KF-08      Terbatas fitur   Terpenuhi (pipeline Terpenuhi
  (Analisis Pola)   platform         analisis terpisah)  (pipeline
                                                         analisis
                                                         terpisah)

  KF-09 (Monitoring Terpenuhi        Terpenuhi           Tidak terpenuhi
  Terkini)          (template        (dashboard custom)  
                    platform)                            

  KF-10             Terbatas         Terpenuhi           Parsial (hasil
  (Visualisasi      template         (dashboard + hasil  analisis saja)
  Historis)                          analisis)           
  ------------------------------------------------------------------------

  : []{#_Toc223689761 .anchor}Tabel III.4 Pemenuhan Kebutuhan Fungsional
  per Alternatif

Seluruh alternatif memenuhi kebutuhan pada sisi perangkat IoT (KF-01
s.d. KF-04) karena menggunakan perangkat keras yang sama. Analisis pola
(KF-07, KF-08) pada Alternatif 2 dan 3 dilakukan melalui *pipeline*
analisis terpisah, sedangkan Alternatif 1 terbatas pada fitur bawaan
*platform*. Perbedaan utama terletak pada monitoring: Alternatif 3 tidak
memenuhi KF-09 karena tidak memiliki *dashboard*, dan hanya memenuhi
KF-10 secara parsial.

### Analisis Penentuan Solusi Menggunakan Metode AHP

Untuk menentukan alternatif solusi yang paling sesuai, digunakan metode
Analytical Hierarchy Process (AHP). Metode ini dipilih karena dapat
mengakomodasi kriteria-kriteria dengan bobot yang berbeda serta
memberikan hasil yang terukur dan terstruktur.

![[]{#_Toc223586788 .anchor}Gambar III.1 Kriteria Evaluasi Alternatif
Solusi](./media/media/image6.png){alt="A diagram of a company AI-generated content may be incorrect."
width="5.363043525809274in" height="2.9819444444444443in"}

Berikut kriteria yang digunakan untuk evaluasi alternatif solusi.

  ------------------------------------------------------------------------
  ID        Kriteria        Deskripsi
  --------- --------------- ----------------------------------------------
  C-1       Kelayakan       Kemudahan implementasi dengan kemampuan dan
            Teknis          *resource* yang tersedia

  C-2       Kesesuaian      Seberapa baik solusi mendukung pencapaian
            Tujuan          tujuan penelitian (implementasi sistem,
                            analisis pola, dan evaluasi *firmware*)

  C-3       Waktu           Durasi waktu yang dibutuhkan untuk
            Pengembangan    menyelesaikan pengembangan sistem

  C-4       Biaya           Total biaya implementasi yang dikeluarkan
  ------------------------------------------------------------------------

  : []{#_Toc223074007 .anchor}Tabel III.5 Kriteria Evaluasi Alternatif
  Solusi

Penentuan bobot kriteria dilakukan melalui *pairwise* *comparison*
*matrix* menggunakan skala Saaty. C-2 (Kesesuaian dengan tujuan
penelitian) merupakan prioritas tertinggi karena sistem harus mendukung
analisis pola dan evaluasi firmware. C-1 (Kelayakan teknis) lebih
penting dari C-3 (Waktu pengembangan). C-4 (Biaya) mendapat bobot
terendah karena semua alternatif berada dalam *range* biaya yang
*comparable*.

  --------------------------------------------------------------------------
                 **C-1**        **C-2**        **C-3**        **C-4**
  -------------- -------------- -------------- -------------- --------------
  **C-1**        1              0.5            2              5

  **C-2**        2              1              3              7

  **C-3**        0.5            0.333          1              3

  **C-4**        0.2            0.143          0.333          1

  **Jumlah**     3.7            1.976          6.333          16
  --------------------------------------------------------------------------

  : []{#_Toc223074008 .anchor}Tabel III.6 Matriks Perbandingan Kriteria
  Berpasangan

Setelah proses normalisasi matriks dan perhitungan rata-rata baris,
diperoleh bobot untuk setiap kriteria.

  -----------------------------------------------------------------------
  Kriteria                      Bobot          Persentase
  ----------------------------- -------------- --------------------------
  C-1 (Kelayakan Teknis)        0.288          28.8%

  C-2 (Kesesuaian Tujuan)       0.490          49.0%

  C-3 (Waktu Pengembangan)      0.163          16.3%

  C-4 (Biaya)                   0.061          6.1%
  -----------------------------------------------------------------------

  : []{#_Toc223074009 .anchor}Tabel III.7 Bobot Kriteria Hasil AHP

Selanjutnya, nilai Consistency Ratio (CR) dihitung untuk memastikan
konsistensi penilaian. Dengan λmax = 4.019, CI = 0.0063, dan RI = 0.90,
diperoleh CR = 0.7% yang berada di bawah batas 10%, menunjukkan
konsistensi yang baik.

### Evaluasi dan Pemilihan Alternatif Solusi

Evaluasi dilakukan dengan membuat matriks perbandingan berpasangan untuk
setiap kriteria terhadap tiga alternatif solusi:

  -----------------------------------------------------------------------
  **Kriteria**   **Justifikasi Perbandingan**
  -------------- --------------------------------------------------------
  C-1            Alt-1 paling mudah (*platform* siap pakai). Alt-2
  (Kelayakan)    moderat (perlu develop *middleware*+*dashboard*). Alt-3
                 mudah tapi *maintenance* sulit tanpa visual.

  C-2            Alt-2 paling sesuai: memenuhi seluruh KF termasuk
  (Kesesuaian)   *dashboard* custom untuk *monitoring*. Alt-1 memenuhi
                 KF-09/KF-10 tapi analisis terbatas fitur *platform*.
                 Alt-3 tidak memenuhi KF-09.

  C-3 (Waktu)    Alt-1 tercepat (*plug-and-play*). Alt-3 cukup cepat
                 (tanpa *dashboard*). Alt-2 perlu waktu develop
                 *dashboard*.

  C-4 (Biaya)    Alt-3 termurah (tanpa *dashboard*). Alt-2 moderat
                 (Supabase *free* tier + *hosting* *dashboard*). Alt-1
                 tergantung *pricing* *platform* *cloud*.
  -----------------------------------------------------------------------

  : []{#_Toc223074010 .anchor}Tabel III.8 Matriks Perbandingan
  Berpasangan Alternatif pada Setiap Kriteria

Dari setiap matriks perbandingan, dilakukan proses normalisasi dan
perhitungan bobot lokal. Hasil perhitungan bobot lokal untuk setiap
alternatif.

  ------------------------------------------------------------------
  Alternatif                         C-1     C-2     C-3     C-4
  ---------------------------------- ------- ------- ------- -------
  Alt-1: SWB + *Platform* *Cloud*    0.539   0.110   0.581   0.250

  Alt-2: SWB + *Backend* +           0.297   0.581   0.110   0.250
  *Dashboard*                                                

  Alt-3: SWB + *Backend* saja        0.164   0.309   0.309   0.500
  ------------------------------------------------------------------

  : []{#_Toc223074011 .anchor}Tabel III.9 Bobot Lokal Alternatif pada
  Setiap Kriteria

Skor global dihitung dengan mengalikan bobot lokal dengan bobot
kriteria.

  ---------------------------------------------------------------------------
  Alternatif                       Perhitungan                Skor    \%
  -------------------------------- -------------------------- ------- -------
  Alt-1: SWB + *Platform* *Cloud*  Σ(bobot lokal × bobot      0.319   31.9%
                                   kriteria)                          

  Alt-2: SWB + *Backend* +         Σ(bobot lokal × bobot      0.404   40.4%
  *Dashboard*                      kriteria)                          

  Alt-3: SWB + *Backend* saja      Σ(bobot lokal × bobot      0.279   27.9%
                                   kriteria)                          
  ---------------------------------------------------------------------------

  : []{#_Toc223689767 .anchor}Tabel III.10 Skor Global untuk Setiap
  Alternatif Solusi

Berdasarkan Tabel III.9, Alternatif 2 terpilih sebagai solusi terbaik
dengan skor 0.404 (40.4%), unggul dibandingkan Alternatif 1 (31.9%) dan
Alternatif 3 (27.9%). Keunggulan Alternatif 2 berasal dari dominasi pada
kriteria C-2 (Kesesuaian dengan tujuan penelitian) yang memiliki bobot
tertinggi (49%). Meskipun Alternatif 1 unggul pada kelayakan (C-1) dan
waktu (C-3), keterbatasan fitur analisis dan *query* pada *platform*
*cloud* menyebabkan skor C-2 yang rendah. Alternatif 3 memiliki
fleksibilitas *query* yang sama dengan Alternatif 2, namun tidak
memenuhi KF-09 (*monitoring* data terkini) karena tidak memiliki
*dashboard*.

Dengan demikian, sistem *Smart Waste Bin* akan diimplementasikan
menggunakan Alternatif 2, yaitu perangkat *Smart Waste Bin* dari pihak
ketiga dengan *backend* *custom* (Supabase) dan *dashboard* untuk
*monitoring*. Analisis pola pembuangan dilakukan melalui *pipeline*
analisis data terpisah. Selain pengembangan *software* *stack*,
peningkatan pada sisi *firmware* perangkat juga akan dilakukan untuk
menyesuaikan konfigurasi bawaan yang dirancang untuk skala perkotaan
agar optimal di lingkungan kampus, sebagaimana telah diidentifikasi pada
Subbab III.1.

#  DESAIN DAN IMPLEMENTASI SISTEM *SMART WASTE BIN*

Bab ini merupakan realisasi dari tahap Prototipe dalam metodologi
*Design Thinking* yang telah diuraikan pada Subbab I.5.2. Berdasarkan
hasil analisis kebutuhan dan pemilihan solusi pada Bab III, dikembangkan
sistem *Smart Waste Bin* yang terdiri dari perangkat IoT, *middleware*,
*database*, dan *dashboard*.

Komponen sistem dibedakan menjadi dua kategori: komponen eksternal
berupa perangkat IoT *Smart Waste Bin* dari pihak ketiga, serta komponen
internal yang dikembangkan oleh peneliti meliputi *middleware*,
*database*, dan *dashboard*. Karena konfigurasi *firmware* bawaan
perangkat dirancang untuk skala perkotaan sebagaimana diidentifikasi
pada Subbab III.1, bab ini juga menjelaskan peningkatan *firmware* yang
dilakukan agar perangkat dapat beroperasi optimal di lingkungan kampus.

## Gambaran Umum Sistem 

Subbab ini menyajikan gambaran umum sistem *Smart Waste Bin* yang
dikembangkan, mencakup arsitektur sistem secara keseluruhan dan alur
data dari pengumpulan hingga analisis. Gambaran umum ini bertujuan untuk
memberikan pemahaman holistik mengenai struktur dan cara kerja sistem
secara konseptual sebelum membahas pemilihan teknologi dan detil
implementasi pada subbab-subbab selanjutnya.

### Arsitektur Sistem

Sistem *Smart Waste Bin* dirancang menggunakan arsitektur berlapis
(*layered* *architecture*) yang mengacu pada model arsitektur IoT.
Berbeda dengan model *three*-*layer* *architecture* standar, sistem ini
mengadopsi *four*-*layer* *architecture* dengan penambahan *Middleware*
*Layer*. Pemilihan arsitektur empat *layer* didasarkan pada kebutuhan
untuk memisahkan fungsi transmisi data dengan fungsi pemrosesan dan
*routing* data untuk memberikan modularitas yang lebih baik dalam
pengembangan dan pemeliharaan sistem.

Gambar IV.1 menunjukkan arsitektur keseluruhan sistem *Smart Waste Bin*
yang terdiri dari empat *layer* utama beserta pembagian komponen
berdasarkan tanggung jawab pengembangan.

![[]{#_Toc223586789 .anchor}Gambar IV.1 Arsitektur Sistem *Smart Waste
Bin*](./media/media/image7.png){width="4.385416666666667in"
height="6.6129297900262465in"}

Berdasarkan Gambar IV.1, sistem terdiri dari empat *layer* dengan fungsi
sebagai berikut. *Perception Layer* terdiri dari tiga unit perangkat
*Smart Waste Bin* yang berfungsi mengumpulkan data tingkat kepenuhan
tempat sampah secara periodik. *Network Layer* menyediakan infrastruktur
komunikasi nirkabel untuk mentransmisikan data dari perangkat ke sistem
penerima. *Middleware* *Layer* merupakan penambahan dari arsitektur
standar, berfungsi sebagai data *gateway* yang menerima, memvalidasi,
dan meneruskan data ke *layer* di atasnya. *Application Layer* terdiri
dari dua komponen utama yaitu sistem *database* untuk penyimpanan data
dan *dashboard* untuk visualisasi serta analisis pola pembuangan sampah.

Arsitektur sistem juga membedakan komponen berdasarkan tanggung jawab
pengembangan sebagaimana ditunjukkan pada Gambar IV.1. Komponen
eksternal (garis putus-putus) mencakup perangkat IoT pada *Perception
Layer* yang disediakan oleh vendor. Komponen internal (garis solid)
mencakup data *gateway* pada *Middleware* *Layer* serta seluruh komponen
pada *Application Layer* yang dikembangkan oleh peneliti. Komponen
*shared* mencakup infrastruktur *Network Layer* yang digunakan bersama.
Pembagian ini memastikan fokus penelitian tetap pada domain Sistem dan
Teknologi Informasi tanpa membahas aspek teknis perangkat keras secara
mendalam.

### Alur Data Sistem

Sistem *Smart Waste Bin* mengimplementasikan alur data yang terstruktur
dari pengumpulan data di perangkat IoT hingga penyajian informasi kepada
pengguna dan analisis pola pembuangan sampah. Untuk menggambarkan alur
data secara sistematis, digunakan *Data* *Flow* *Diagram* (DFD) yang
terdiri dari dua level, yaitu DFD Level 0 (*Context Diagram*) yang
menunjukkan sistem secara keseluruhan beserta entitas eksternal, dan DFD
Level 1 yang menunjukkan detil proses-proses utama dalam sistem.

DFD Level 0 atau *Context Diagram* menggambarkan sistem *Smart Waste
Bin* sebagai satu kesatuan proses yang berinteraksi dengan entitas
eksternal. Gambar IV.2 menunjukkan *Context Diagram* sistem *Smart Waste
Bin*.

![[]{#_Toc223586790 .anchor}Gambar IV.2 *Data* *Flow* *Diagram* Level
0](./media/media/image8.png){width="5.354166666666667in"
height="4.731589020122485in"}

Berdasarkan Gambar IV.2, terdapat dua entitas eksternal yang
berinteraksi dengan sistem. Entitas pertama adalah *Smart Waste Bin*
yang merupakan perangkat IoT sebagai sumber data. Perangkat ini
mengirimkan data tingkat kepenuhan, identifier perangkat, dan
*Timestamp* pembacaan ke sistem secara periodik. Entitas kedua adalah
Pengguna yang dalam konteks ini mencakup pengelola gedung dan peneliti.
Pengguna mengirimkan request data dan *filter* ke sistem, kemudian
menerima visualisasi status, grafik historis, dan hasil analisis pola
sebagai *output*.

DFD Level 1 menunjukkan dekomposisi proses tunggal pada DFD Level 0
menjadi tiga proses utama beserta data store yang digunakan. Gambar IV.3
menunjukkan DFD Level 1 sistem *Smart Waste Bin*.

![[]{#_Toc223586791 .anchor}Gambar IV.3 Data *Flow* Diagram Level
1](./media/media/image9.png){width="4.695652887139108in"
height="3.224349300087489in"}

Berdasarkan Gambar IV.3, sistem terdiri dari tiga proses utama dan satu
data store. Tabel IV.1 menyajikan deskripsi setiap komponen dalam DFD
Level 1.

  -------------------------------------------------------------------------
  ID    Komponen      Tipe     Deskripsi
  ----- ------------- -------- --------------------------------------------
  1.0   Terima &      Proses   Menerima data dari perangkat IoT, melakukan
        Validasi Data          parsing dan validasi format serta nilai data

  2.0   Simpan Data   Proses   Menyimpan data yang telah tervalidasi ke
                               dalam *database* secara persisten melalui
                               *middleware*

  3.0   Visualisasi   Proses   Mengambil data dari *database*, menyajikan
        Data                   dalam bentuk *dashboard* dan grafik, serta
                               memberikan status perangkat untuk kebutuhan
                               pemeliharaan

  D1    *Database*    Data     Menyimpan seluruh data pembacaan sensor
                      Store    secara historis
  -------------------------------------------------------------------------

  : []{#_Toc223074012 .anchor}Tabel IV.1 Deskripsi Komponen DFD Level 1

Data sensor dari *smart waste bin* mengalir ke Proses 1.0 (Terima &
Validasi Data) yang melakukan parsing dan validasi. Data yang lolos
validasi diteruskan ke Proses 2.0 (Simpan Data) untuk disimpan ke
*Database* melalui *middleware*. Dari *database*, data dapat diakses
oleh Proses 3.0 (Visualisasi) yang mengambil data untuk ditampilkan
kepada Pengguna dalam bentuk *dashboard*, grafik interaktif, dan status
setiap perangkat untuk kebutuhan pemeliharaan.

Tabel IV.2 dibawah menjelaskan setiap alur data yang dilalui.

  --------------------------------------------------------------------------
  **No**   **Dari**     **Ke**       **Data yang Mengalir**
  -------- ------------ ------------ ---------------------------------------
  1        *Smart Waste Proses 1.0   Data sensor (fill_level, sensor_id,
           Bin*                      *Timestamp*, *Battery*, dll)

  2        Proses 1.0   Proses 2.0   Data tervalidasi

  3        Proses 2.0   *Database*   Record data pembacaan

  4        *Database*   Proses 3.0   *Query* result (data sesuai *filter*)

  5        Proses 3.0   Peneliti     *Dashboard*, grafik historis, status
                                     perangkat

  6        Pengguna     Proses 3.0   Request data, parameter *filter*,
                                     rentang waktu
  --------------------------------------------------------------------------

  : []{#_Toc223689769 .anchor}Tabel IV.2 Alur Data DFD Level 1

### Pemilihan Teknologi

Implementasi sistem *Smart Waste Bin* memerlukan pemilihan teknologi
yang tepat untuk setiap komponen agar sistem dapat beroperasi secara
optimal dan terintegrasi. Pemilihan teknologi didasarkan pada beberapa
pertimbangan, yaitu kesesuaian dengan kebutuhan fungsional dan
nonfungsional yang telah diidentifikasi pada Bab III, kemudahan
integrasi antar komponen, ketersediaan dokumentasi dan dukungan
komunitas, serta pengalaman pengembang.

Tabel IV.3 menyajikan teknologi yang digunakan pada setiap *layer*
sistem beserta justifikasinya.

  -----------------------------------------------------------------------------
  ***Layer***    **Komponen**     **Teknologi**   **Justifikasi**
  -------------- ---------------- --------------- -----------------------------
  Perception     Mikrokontroler   ESP32           Dual-core processor, konsumsi
                                                  daya rendah dengan *deep
                                                  sleep* mode

  Perception     Sensor Jarak     VL53L0X V2      Sensor *Time*-of-Flight
                                                  dengan akurasi tinggi,
                                                  jangkauan hingga 2 meter,
                                                  *interface* I2C

  Perception     Sensor Daya      INA219          Mengukur tegangan, arus, dan
                                                  daya untuk *monitoring*
                                                  status baterai

  Perception     Konektivitas     SIM800L         Pengiriman data via GPRS di
                                                  lokasi tanpa Wi-Fi

  Perception     Sumber Daya      18650 Li-Ion    Baterai 3000mAh yang dapat
                                                  diisi ulang

  Network        Protokol         MQTT            *Overhead* rendah (*header* 2
                                                  *bytes*), arsitektur
                                                  *publish-subscribe*

  Network        *Broker*         MQTT *Broker*   Disediakan oleh vendor

  *Middleware*   Data Gateway     Node-RED        Visual *programming*,
                                                  dukungan MQTT *built-in*,
                                                  integrasi mudah dengan
                                                  *database*

  Application    *Database*       Supabase        PostgreSQL dengan REST API
                                                  *built-in*, free tier
                                                  tersedia

  Application    *Dashboard*      Next.js         *Server*-side rendering,
                                                  React-based, integrasi dengan
                                                  Supabase

  Application    Charting         Recharts        *Library* visualisasi data
                                                  untuk React
  -----------------------------------------------------------------------------

  : []{#_Toc223689770 .anchor}Tabel IV.3 Pemilihan Teknologi

Berdasarkan Tabel IV.3, komponen pada *Perception Layer* dan *Network
Layer* merupakan komponen eksternal yang disediakan oleh pihak ketiga,
sedangkan komponen pada *Middleware Layer* dan *Application Layer*
merupakan komponen internal yang dikembangkan oleh peneliti. Pemilihan
protokol MQTT sebagai mekanisme komunikasi telah dibahas pada Bab II, di
mana karakteristik *lightweight* dan arsitektur *publish-subscribe*
menjadikannya sesuai untuk aplikasi IoT dengan keterbatasan *bandwidth*.

## Komponen External: Perangkat *Smart Waste Bin*

Perangkat IoT *Smart Waste Bin* merupakan komponen eksternal yang
disediakan oleh pihak ketiga dan berperan sebagai sumber data dalam
sistem. Pada konteks penelitian ini, perangkat IoT diperlakukan sebagai
\"*black box*\" yang menghasilkan *output* berupa data tingkat kepenuhan
tempat sampah. Subbab ini menjelaskan deskripsi fungsional perangkat,
spesifikasi *interface* data, serta asumsi dan batasan yang berlaku.

### Deskripsi Fungsional Perangkat

Perangkat *Smart Waste Bin* berfungsi untuk mengukur tingkat kepenuhan
tempat sampah dan mengirimkan data tersebut ke sistem secara periodik.
Gambar IV.5 menunjukkan diagram blok fungsional perangkat *Smart Waste
Bin*.

![[]{#_Toc223586792 .anchor}Gambar IV.4 Diagram Blok Fungsional
Perangkat *Smart Waste
Bin*](./media/media/image10.png){width="5.485141076115486in"
height="2.9583333333333335in"}

Berdasarkan Gambar IV.5, perangkat *Smart Waste Bin* terdiri dari lima
komponen utama dengan fungsi masing-masing. Tabel IV.4 menyajikan
deskripsi fungsional setiap komponen.

  -------------------------------------------------------
  Komponen             Fungsi
  -------------------- ----------------------------------
  Sensor VL53L0X V2    Mengukur jarak antara sensor
                       dengan permukaan sampah

  Sensor INA219        Mengukur tegangan dan arus baterai
                       untuk *monitoring* daya

  Mikrokontroler ESP32 Memproses data sensor dan mengatur
                       jadwal pengiriman

  Modul GSM SIM800L    Mengirimkan data ke MQTT *broker*
                       melalui jaringan seluler

  Baterai 18650 Li-Ion Menyediakan sumber daya untuk
                       seluruh komponen
  -------------------------------------------------------

  : []{#_Toc223689771 .anchor}Tabel IV.4 Fungsi setiap Komponen *Smart
  Waste Bin*

Mekanisme kerja perangkat secara fungsional adalah sebagai berikut.
Setiap 8 jam, mikrokontroler terbangun dari mode *deep sleep* dan
mengaktifkan seluruh komponen. Sensor VL53L0X V2 melakukan 5 kali
pembacaan jarak, kemudian mikrokontroler mengambil nilai median untuk
mengurangi *noise*. Jika sensor mengalami *timeout* lebih dari 3 kali,
mikrokontroler melakukan *auto-recovery* dengan *power* *cycle* pada
sensor. Nilai jarak kemudian dikonversi menjadi persentase tingkat
kepenuhan menggunakan persamaan IV.1.

$$Fill\ Level\ (\%) = \frac{Kedalaman\ Bin - Jarak\ Terukur}{Kedalaman\ Bin} \times 100$$

> []{#_Toc223586641 .anchor}(IV.1)

dengan kedalaman bin sebesar 1000mm.

Secara bersamaan, sensor INA219 mengukur tegangan dan arus baterai
sebanyak 3 kali dan mengambil rata-rata. Mikrokontroler kemudian
menghitung *State of Charge* (SoC) baterai menggunakan persamaan IV.2.

$$Battery\ Percent\ (\%) = \frac{Tegangan\ Terukur - 5.60}{0.028}$$

> []{#_Toc223586642 .anchor}(IV.2)

Jika tegangan baterai di bawah 5.6V atau persentase di bawah 30%,
perangkat akan memasuki mode \"sleep *forever*\" untuk mencegah
kerusakan baterai akibat *over-discharge*. Data yang telah diproses
dikirimkan ke MQTT *broker*, kemudian mikrokontroler kembali ke mode
*deep sleep*.

### Spesifikasi *Interface* Data

*Interface* antara perangkat IoT dengan sistem internal didefinisikan
melalui format data yang dikirimkan via protokol MQTT. Tabel IV.5
menyajikan spesifikasi koneksi MQTT yang digunakan.

  -------------------------------------------------------
  Aspek                Fungsi
  -------------------- ----------------------------------
  *Broker*             Disediakan oleh vendor

  *Topic* *Pattern*    wp2/basic_01; wp2/basic_02;
                       wp2/basic_03;

  QoS *level*          0 (default)

  *Authentication*     Username dan password (disediakan
                       vendor)
  -------------------------------------------------------

  : []{#_Toc223689772 .anchor}Tabel IV.5 Spesifikasi Konektivitas MQTT

Data dikirimkan dalam format JSON dengan struktur sebagaimana
ditunjukkan pada Tabel IV.6.

  -------------------------------------------------------------------
  *Field*         Tipe Data Deskripsi                Contoh
  --------------- --------- ------------------------ ----------------
  sensor_id       String    Identifier unik          "1"
                            perangkat                

  tegangan        Float     Tegangan baterai (Volt)  7.25

  arus            Float     Arus perangkat (mA)      100

  daya            Float     Daya terpakai (mW)       727.4

  battPercent     Float     Persentase baterai       58.3
                            (0-100)                  

  Ina219_avail    Boolean   Status ketersediaan      true
                            sensor INA219            

  *fillLevel*     Integer   Tingkat kepenuhan        65
                            (0-100, atau -1 jika     
                            error)                   

  dist            Integer   Jarak terukur (mm, atau  490
                            -1 jika error)           

  vol             Integer   Volume sampah (dm³)      38

  sensor_status   String    Status sensor jarak      \"online\"

  vl53l0x_avail   Integer   Ketersediaan sensor      1
                            (1=*available*, 0=not)   

  *event*         String    Tipe *event*             \"DataUpdate\"
  -------------------------------------------------------------------

  : []{#_Toc223689773 .anchor}Tabel IV.6 *Payload* Data Perangkat

Berikut adalah contoh *payload* data yang dikirimkan oleh perangkat:

![[]{#_Toc223586793 .anchor}Gambar IV.5 *Payload* Data
Perangkat](./media/media/image11.png){width="2.698292869641295in"
height="2.7608016185476814in"}

## Peningkatan *Firmware* Perangkat *Smart Waste Bin*

Sebagaimana diidentifikasi pada Subbab III.1, perangkat *Smart Waste
Bin* yang tersedia memiliki konfigurasi *firmware* yang dirancang untuk
skala perkotaan. Untuk menyesuaikan dengan kebutuhan lingkungan kampus
yang memerlukan titik data lebih tinggi dan keandalan operasi jangka
panjang, dilakukan lima peningkatan firmware. Tabel IV.7 menyajikan
ringkasan peningkatan yang dilakukan.

  -----------------------------------------------------------------------
  Aspek                Sebelum               Sesudah
  -------------------- --------------------- ----------------------------
  Interval Pengambilan 8 jam                 2 jam 30 menit
  Data                                       

  Pembacaan Sensor     Single *reading*      5 *readings* dengan median
                                             *filter*

  *Error Handling*     Tidak ada mekanisme   *Auto-recovery* dengan
                       *recovery*            *power* *cycle*

  *Warm-up* Sensor     Langsung pembacaan    3x *warm-up* *readings*
                                             sebelum pengukuran

  GPIO *Management*    Standard              GPIO *isolation* untuk
                                             pr*event* *floating*
  -----------------------------------------------------------------------

  : []{#_Toc223689774 .anchor}Tabel IV.7 Peningkatan *Firmware*

Berikut adalah penjelasan detil untuk setiap peningkatan *firmware* yang
dilakukan.

### Perubahan Interval Pengambilan Data

Perangkat *Smart Waste Bin* yang tersedia pada awalnya dirancang secara
*default* untuk implementasi skala kota. Pada *use case* perkotaan
tersebut, Interval pengiriman data diatur setiap 8 jam sekali. Hal ini
dinilai cukup karena laju penumpukan sampah di kontainer relatif lambat.

Namun, ketika perangkat keras ini diadaptasi untuk lingkungan kampus
khususnya area koridor Laboratorium IoT, konfigurasi waktu tersebut
menjadi tidak relevan. Oleh karena itu, modifikasi pertama yang
dilakukan pada *firmware* adalah memangkas Interval *deep sleep* (waktu
jeda pengambilan data) dari 8 jam menjadi 2 jam 30 menit (mendekati 3
jam).

Perubahan Interval ini didasari oleh dua alasan utama:

1.  Dinamika Pembuangan Sampah Kampus

> Aktivitas mahasiswa dan staf di lingkungan kampus sangat dinamis dan
> terkonsentrasi pada jam-jam tertentu, seperti saat istirahat makan
> siang. Selain itu, jadwal pengosongan tempat sampah oleh petugas
> kebersihan juga dilakukan secara tidak menentu. Jika Interval
> dibiarkan 8 jam, sistem berisiko kehilangan momen kritis pelaporan
> status.

2.  Kebutuhan Resolusi Data untuk Analisis Pola

> Mengacu pada tujuan penelitian untuk mengekstraksi dan
> mengidentifikasi pola temporal harian (*hourly trends*) pembuangan
> sampah, Interval 8 jam hanya akan menghasilkan sekitar 3 titik data
> (*data points*) per hari. Resolusi data ini terlalu rendah untuk bisa
> menangkap fluktuasi aktivitas kampus yang detil. Dengan memendekkan
> Interval menjadi sekitar 3 jam, sistem dapat mengumpulkan hingga 8-9
> titik data per hari per perangkat, sehingga memberikan resolusi
> temporal yang cukup tajam untuk analisis tren waktu sibuk (*peak
> hours*).

Berikut adalah potongan kode perubahan Interval pengambilan data:

+------------------------------------------------------------------+
| // ===== SLEEP CONFIG =====                                      |
|                                                                  |
| // 2.5 jam = 150 menit                                           |
|                                                                  |
| uint64_t *TIME*\_TO_SLEEP = 150ULL \* 60ULL \* 1000000ULL;       |
+==================================================================+

: []{#_Toc223676163 .anchor}Kode IV.1 Implementasi Perubahan Interval
Pengambilan Data

### Implementasi Median *Filter*

Pembacaan sensor VL53L0X ditingkatkan dari *single* *reading* menjadi 5
kali pembacaan dengan pengambilan nilai median. Pendekatan ini dipilih
karena median lebih *robust* terhadap *outlier* dibandingkan rata-rata
(*mean*).

Mekanisme pembacaan sensor yang diimplementasikan adalah sebagai
berikut:

> 1\. Sensor melakukan 5 kali pembacaan dengan Interval 100ms
>
> 2\. Setiap pembacaan dicek validitasnya (*timeout* dan *range*
> 0-1400mm)
>
> 3\. Nilai-nilai valid diurutkan (bubble sort)
>
> 4\. Nilai median (tengah) diambil sebagai hasil akhir
>
> 5\. Jika valid count \< 3, digunakan rata-rata sebagai *fallback*

Implementasi ini mengurangi *noise* pada data. Pengujian menunjukkan
bahwa perbedaan 1 unit raw (misal 899 vs 900 mm) dapat menyebabkan
lompatan 10% pada fillLevel akibat truncation integer. Median dari 5
pembacaan mencegah pembacaan outlier tunggal mempengaruhi hasil. Berikut
adalah potongan kode implementasi median filter:

+------------------------------------------------------------------+
| const int num*Readings* = 5;                                     |
|                                                                  |
| int *readings*\[num*Readings*\];                                 |
|                                                                  |
| int validCount = 0;                                              |
|                                                                  |
| // Take multiple *readings*                                      |
|                                                                  |
| for (int i = 0; i \< num*Readings*; i++) {                       |
|                                                                  |
| int *reading* = sensor.read*Range*ContinuousMillimeters();       |
|                                                                  |
| if (!sensor.*timeout*Occurred() && *reading* \> 0 && *reading*   |
| \<= 1400) {                                                      |
|                                                                  |
| *readings*\[validCount\] = *reading*;                            |
|                                                                  |
| validCount++;                                                    |
|                                                                  |
| }                                                                |
|                                                                  |
| }                                                                |
|                                                                  |
| // Bubble sort for median                                        |
|                                                                  |
| for (int i = 0; i \< validCount - 1; i++) {                      |
|                                                                  |
| for (int j = i + 1; j \< validCount; j++) {                      |
|                                                                  |
| if (*readings*\[i\] \> *readings*\[j\]) {                        |
|                                                                  |
| int temp = *readings*\[i\];                                      |
|                                                                  |
| *readings*\[i\] = *readings*\[j\];                               |
|                                                                  |
| *readings*\[j\] = temp;                                          |
|                                                                  |
| }                                                                |
|                                                                  |
| }                                                                |
|                                                                  |
| }                                                                |
|                                                                  |
| a = *readings*\[validCount / 2\]; // Get median                  |
+==================================================================+

: []{#_Toc223676164 .anchor}Kode IV.2 Implementasi *Median* *Filter*
pada Pembacaan Sensor

### Mekanisme *Auto-recovery*

Sensor VL53L0X dapat mengalami kondisi *hang* yang menyebabkan *timeout*
berulang. Kondisi *trigger* *recovery* bisa diartikan sebagai *timeout*
yang terjadi ≥ 3 kali dari 5 pembacaan, atau tidak ada pembacaan valid
sama sekali. Untuk mengatasi hal ini, diimplementasikan mekanisme
*auto-recovery* dengan alur sebagai berikut.

Langkah *recovery* yang dilakukan:

> 1\. *Stop* continuous mode pada sensor
>
> 2\. Coba *soft* *reset* dengan re-inisialisasi sensor
>
> 3\. Jika *soft* *reset* gagal, lakukan *power* *cycle* (matikan
> *power* sensor 500ms, hidupkan kembali)
>
> 4\. Re-inisialisasi I2C dan sensor
>
> 5\. Jika masih gagal, tandai sensor sebagai *offline*

Mekanisme ini berhasil mencegah *data loss* yang disebabkan oleh sensor
*hang*, di mana sebelumnya kondisi ini memerlukan *reset* manual pada
perangkat. Berikut adalah potongan kode implementasi *auto-recovery*:

+-----------------------------------------------+
| // *Auto-recovery* if sensor *hang*s          |
|                                               |
| if (*timeout*Count \>= 3 \|\| validCount ==   |
| 0) {                                          |
|                                               |
| sensor.*stop*Continuous();                    |
|                                               |
| delay(100);                                   |
|                                               |
| // Try *soft* *reset* first                   |
|                                               |
| if (sensor.init(true)) {                      |
|                                               |
| sensor.setMeasurementTimingBudget(200000);    |
|                                               |
| sensor.startContinuous(200);                  |
|                                               |
| return; // *Soft* *reset* OK                  |
|                                               |
| }                                             |
|                                               |
| // *Soft* *reset* failed, *power* *cycle*     |
|                                               |
| *powerCycle*Sensor();                         |
|                                               |
| if (!sensor.init(true)) {                     |
|                                               |
| readSensor = false; // Sensor *offline*       |
|                                               |
| }                                             |
|                                               |
| }                                             |
+===============================================+

: []{#_Toc223676165 .anchor}Kode IV.3 Implementasi *Auto-recovery*
Sensor

Fungsi *powerCycle*Sensor() mematikan daya sensor selama 500ms kemudian
menghidupkan kembali dan melakukan re-inisialisasi I2C:

+------------------------------------------------------------------+
| void *powerCycle*Sensor() {                                      |
|                                                                  |
| digitalWrite(TRIG_SENSOR, LOW); // Turn off sensor *power*       |
|                                                                  |
| delay(500); // Wait for capacitor discharge                      |
|                                                                  |
| digitalWrite(TRIG_SENSOR, HIGH); // Turn on again                |
|                                                                  |
| delay(300); // Wait for sensor boot                              |
|                                                                  |
| Wire.end(); // Re-init I2C                                       |
|                                                                  |
| delay(50);                                                       |
|                                                                  |
| Wire.begin();                                                    |
|                                                                  |
| }                                                                |
+==================================================================+

: []{#_Toc223676166 .anchor}Kode IV.4 Implementasi *Power* *Cycle*
Sensor

### Warmup Sensor

Sensor VL53L0X memerlukan beberapa pembacaan awal sebelum menghasilkan
nilai yang stabil. Pembacaan pertama setelah inisialisasi cenderung
tidak representatif karena sensor masih dalam proses kalibrasi internal.
Untuk mengatasi hal ini, diimplementasikan mekanisme *warm-up* dengan
melakukan 3 kali pembacaan *dummy* setelah inisialisasi sensor berhasil,
sebelum pembacaan data aktual dilakukan.

Mekanisme *warm-up* diimplementasikan sebagai bagian dari fungsi
initVL53L0X() dengan alur sebagai berikut:

1.  Sensor diinisialisasi dan dikonfigurasi dengan timing budget 200ms

2.  Mode continuous measurement diaktifkan dengan Interval 200ms

3.  Tiga pembacaan *dummy* dilakukan dengan jeda 200ms per pembacaan,
    nilai tidak digunakan

4.  Setelah *warm-up* selesai, sensor dinyatakan siap untuk pengukuran
    aktual

Berikut adalah potongan kode implementasi *warm-up* sensor:

+------------------------------------------------------------------+
| // Inisialisasi sensor berhasil                                  |
|                                                                  |
| sensor.setMeasurementTimingBudget(200000);                       |
|                                                                  |
| delay(100);                                                      |
|                                                                  |
| sensor.startContinuous(200);                                     |
|                                                                  |
| // *Warm-up* *readings* --- nilai dibuang, hanya untuk           |
| stabilisasi                                                      |
|                                                                  |
| SerialMon.println(F(\"Warming up sensor\...\"));                 |
|                                                                  |
| for (int i = 0; i \< 3; i++) {                                   |
|                                                                  |
| sensor.read*Range*ContinuousMillimeters();                       |
|                                                                  |
| delay(200);                                                      |
|                                                                  |
| }                                                                |
|                                                                  |
| SerialMon.println(F(\"Sensor ready!\"));                         |
+==================================================================+

: []{#_Toc223676167 .anchor}Kode IV.5 Implementasi Warmup Sensor

Pendekatan ini memastikan pembacaan pertama yang masuk ke data aktual
sudah dalam kondisi sensor yang stabil, mengurangi risiko nilai anomali
pada awal setiap siklus pengukuran.

### Optimasi Daya

Beberapa optimasi dilakukan untuk memperpanjang masa operasi baterai:

1.  GPIO *Isolation*: Sebelum *deep sleep*, seluruh GPIO yang digunakan
    di-hold pada kondisi LOW untuk mencegah *floating* *state* yang
    dapat menyebabkan konsumsi daya tidak perlu.

2.  *Proper* *shutdown* *sequence*: Urutan mematikan komponen
    dioptimalkan (sensor → MQTT → GPRS → modem → GPIO) untuk memastikan
    tidak ada komponen yang tertinggal dalam kondisi aktif.

Berikut adalah potongan kode implementasi GPIO *isolation*:

+--------------------------------------------------------+
| // Turn off all GPIO                                   |
|                                                        |
| digitalWrite(TRIG, LOW);                               |
|                                                        |
| digitalWrite(TRIG_SENSOR, LOW);                        |
|                                                        |
| digitalWrite(LED_READ, LOW);                           |
|                                                        |
| digitalWrite(LED_NET, LOW);                            |
|                                                        |
| // Isolate GPIO (pr*event* *floating* during sleep)    |
|                                                        |
| gpio_hold_en(GPIO_NUM_13); // TRIG (modem *power*)     |
|                                                        |
| gpio_hold_en(GPIO_NUM_23); // TRIG_SENSOR              |
|                                                        |
| gpio_hold_en(GPIO_NUM_18); // LED_NET                  |
|                                                        |
| gpio_hold_en(GPIO_NUM_19); // LED_READ                 |
|                                                        |
| gpio_deep_sleep_hold_en();                             |
+========================================================+

: []{#_Toc223676168 .anchor}Kode IV.6 Implementasi GPIO *Isolation*

Tabel IV.8 menyajikan urutan *shutdown* yang diimplementasikan.

  ------------------------------------------------------------------------
  Step   Aksi                Keterangan
  ------ ------------------- ---------------------------------------------
  1      *Stop* sensor       Menghentikan mode pembacaan kontinyu VL53L0X
         continuous          

  2      Disconnect MQTT     Menutup koneksi MQTT dengan *broker*

  3      GPRS disconnect     Memutus koneksi data seluler

  4      Modem *power*off    Mematikan modem SIM800L

  5      GPIO LOW            Set semua GPIO ke LOW (TRIG, TRIG_SENSOR,
                             LED)

  6      GPIO hold enable    Isolasi GPIO untuk mencegah *floating* saat
                             sleep

  7      I2C end             Menonaktifkan bus I2C

  8      Serial flush & end  Flush buffer serial dan nonaktifkan

  9      *Deep sleep*        Masuk mode *deep sleep* selama 2.5 jam
  ------------------------------------------------------------------------

  : []{#_Toc223689775 .anchor}Tabel IV.8 Urutan *Shutdown*

## *Middleware*: Data Gateway

*Middleware* merupakan komponen internal yang berfungsi sebagai jembatan
antara perangkat IoT pada *Network Layer* dengan komponen penyimpanan
pada *Application Layer*. Pada sistem ini, *middleware*
diimplementasikan menggunakan Node-RED yang beroperasi pada *server*
lokal. Subbab ini menjelaskan arsitektur *flow*, konfigurasi *node*,
serta mekanisme pemrosesan data.

### Arsitektur *Flow* Node-RED

Node-RED dipilih sebagai *platform* *middleware* karena menyediakan
pendekatan visual *programming* yang memudahkan konfigurasi alur
pemrosesan data. *Flow* Node-RED untuk sistem *smart waste bin*
dirancang untuk menerima data dari tiga perangkat sensor secara paralel
dan meneruskannya ke *database* Supabase. Gambar IV.6 menunjukkan
arsitektur *flow* Node-RED secara keseluruhan.

![[]{#_Toc223586794 .anchor}Gambar IV.6 *Flow*
Node-RED](./media/media/image12.png){width="5.511805555555555in"
height="2.3534722222222224in"}

Berdasarkan Gambar IV.6, *flow* terdiri dari beberapa kelompok *node*.
Pada bagian kiri terdapat *node* inject untuk pengujian dan *node* MQTT
In sebagai *subscriber*. Data yang diterima diproses melalui *node* JSON
untuk parsing, *node* function untuk transformasi, dan *node* HTTP
Request untuk pengiriman ke *database*. *Node* debug digunakan untuk
*monitoring* di setiap tahap. Tabel IV.8 menyajikan ringkasan tipe
*node* yang digunakan dalam *flow*.

  ------------------------------------------------------------------
  Tipe *Node*   Jumlah        Fungsi
  ------------- ------------- --------------------------------------
  Inject        7             Simulasi data untuk pengujian

  MQTT In       3             Menerima data dari MQTT *broker*

  JSON          3             Parsing string JSON ke objek

  Function      3             Transformasi dan penambahan metadata

  HTTP Request  3             Pengiriman data ke *Database*

  Debug         6             *Monitoring* data dan *response*
  ------------------------------------------------------------------

### Konfigurasi *Node*

Setiap tipe *node* pada *flow* memiliki konfigurasi spesifik yang
menentukan perilakunya. Berikut adalah penjelasan dan konfigurasi untuk
setiap tipe *node* yang digunakan.

#### Konfigurasi MQTT In

*Node* MQTT In berfungsi sebagai *subscriber* yang menerima data dari
MQTT *broker*. Terdapat tiga *node* MQTT In yang masing-masing subscribe
ke *topic* berbeda untuk setiap sensor. Tabel IV.9 menyajikan
konfigurasi *node* MQTT In.

  --------------------------------------------------------------------
  Parameter     Nilai           Keterangan
  ------------- --------------- --------------------------------------
  *Server*      (IP *Broker*)   Alamat MQTT *broker*

  Port          1883            Port default MQTT

  *Topic*       wp2/basic_01,   Satu *topic* per sensor
                wp2/basic_02,   
                wp2/basic_03    

  *Output*      Auto-detect     Otomatis deteksi tipe data
  --------------------------------------------------------------------

  : []{#_Toc223689776 .anchor}Tabel IV.9 Konfigurasi MQTT

#### Konfigurasi *Node* JSON

*Node* JSON berfungsi untuk mengkonversi *payload* dari format string
JSON menjadi objek JavaScript yang dapat diproses lebih lanjut. Tabel
IV.10 menyajikan konfigurasi *node* JSON.

  ------------------------------------------------------------------
  Parameter     Nilai                      Keterangan
  ------------- -------------------------- -------------------------
  Action        Convert between JSON       Mengubah string ke objek
                String & Object            

  *Proper*ty    msg.*payload*              Lokasi data yang
                                           dikonversi

  Format JSON   Tidak dicentang            *Output* berupa objek,
  String                                   bukan string
  ------------------------------------------------------------------

  : []{#_Toc223689777 .anchor}Tabel IV.10 Konfigurasi *Node* JSON

#### Konfigurasi *Node* HTTP Request

*Node* HTTP Request berfungsi untuk mengirimkan data ke *database*
Supabase menggunakan REST API. Tabel IV.13 menyajikan konfigurasi *node*
HTTP Request.

  -----------------------------------------------------------------------
  Parameter     Nilai
  ------------- ---------------------------------------------------------
  Method        POST

  URL           https://\[project-ref\].supabase.co/rest/v1/sensor_data

  *Payload*     Dikirim sebagai request body

  Return        UTF-8 String
  -----------------------------------------------------------------------

  : []{#_Toc223689778 .anchor}Tabel IV.11 Konfigurasi *Node* HTTP
  Request

Tabel IV.14 menyajikan konfigurasi HTTP *header*s yang digunakan.

  --------------------------------------------------------------------
  *Header*        Nilai                      Keterangan
  --------------- -------------------------- -------------------------
  apikey          \[Supabase anon key\]      API key untuk autentikasi

  Authorization   Bearer \[anon key\]        Token autentikasi

  Content-Type    application/json           Format data yang dikirim

  Prefer          return=representation      Mengembalikan data yang
                                             berhasil disimpan
  --------------------------------------------------------------------

  : []{#_Toc223689779 .anchor}Tabel IV.12 Konfigurasi HTTP *Header*s

#### Konfigurasi *Node* Debug

*Node* Debug digunakan untuk menampilkan data pada sidebar Node-RED
untuk keperluan *monitoring* dan debugging. Terdapat dua kelompok *node*
debug dalam *flow*. Tabel IV.15 menyajikan konfigurasi *node* Debug.

  -----------------------------------------------------------------------
  Nama *Node*         *Output*                  Fungsi
  ------------------- ------------------------- -------------------------
  *Raw data* 01/02/03 msg.*payload*             Menampilkan data mentah
                                                setelah parsing JSON

  Authorization       msg.*payload*             Menampilkan *response*
                                                dari Supabase
  -----------------------------------------------------------------------

  : []{#_Toc223689780 .anchor}Tabel IV.13 Konfigurasi *Node* Debug

#### Konfigurasi *Node* Inject

*Node* Inject digunakan untuk keperluan pengujian *flow* tanpa harus
menunggu data dari perangkat IoT. Tabel IV.16 menyajikan daftar *node*
Inject beserta skenario pengujiannya.

  -----------------------------------------------------------------------
  Nama *Node*         Skenario                  Karakteristik Data
  ------------------- ------------------------- -------------------------
  Test Sensor         Data normal sensor 1,     Semua nilai dalam rentang
  01/02/03            sensor 2, atau sensor 3   normal

  Test Low *Battery*  Baterai rendah            battPercent \< 30%,
                                                *event*: \"Low*Battery*\"

  Test Sensor Error   Sensor tidak tersedia     Nilai 999, ina219_avail:
                                                false

  Test Bin Full       Tempat sampah penuh       *fillLevel*: 100, dist: 0

  Test Bin Empty      Tempat sampah kosong      *fillLevel*: 0, dist:
                                                tinggi
  -----------------------------------------------------------------------

  : []{#_Toc223689781 .anchor}Tabel IV.14 Konfigurasi *Node* Inject

### Alur Pemrosesan Data

Berdasarkan konfigurasi *node* yang telah dijelaskan dan Gambar IV.4,
alur pemrosesan data pada *middleware* dapat dirangkum sebagai berikut.
Pertama, *node* MQTT In menerima pesan dari *broker* dengan QoS level 0
sesuai konfigurasi *publisher*, sementara *node* dikonfigurasi dengan
maksimum QoS level 2 pada sisi subscribe. Kedua, *node* JSON
mengkonversi string *payload* menjadi objek JavaScript. Ketiga, *node*
*Function* melakukan *mapping* *field* dan menambahkan metadata berupa
*Timestamp* *server* dan *device*\_*topic*. Keempat, *node* HTTP Request
mengirimkan data ke Supabase via REST API dengan *header* autentikasi
yang sesuai. *Response* dari *database* ditampilkan pada *node* Debug
untuk *monitoring*.

### *Deployment* dan Operasional Node-RED

Node-RED dijalankan pada *server* lokal (Personal Computer) yang
beroperasi selama 24 jam untuk memastikan ketersediaan layanan
penerimaan data. Tabel IV.17 menyajikan spesifikasi *deployment*
*middleware*.

  ---------------------------------------------------
  Aspek               Spesifikasi
  ------------------- -------------------------------
  *Platform*          Node-RED v4.1.3

  Run*time*           Node.js v24.12.0

  *Hosting*           *Server* lokal menggunakan
                      komputer peneliti yang
                      dinyalakan selama penelitian

  *Auto-connect*      *Enabled* (reconnect otomatis
                      ke MQTT *broker*)

  *Flow* Name         MQTT to Supabase *Flow*
  ---------------------------------------------------

  : []{#_Toc223689782 .anchor}Tabel IV.15 Spesifikasi *Deployment* dan
  Operasional Node-RED

## *Database*

*Database* merupakan komponen pada *Application Layer* yang berfungsi
untuk menyimpan seluruh data pembacaan sensor secara persisten dan
terstruktur. Pada sistem ini, *database* diimplementasikan menggunakan
Supabase yang merupakan *platform* *Backend*-*as-a-Service* berbasis
PostgreSQL. Subbab ini menjelaskan desain skema *database*, struktur
tabel, serta contoh data yang tersimpan.

### Spesifikasi *Platform* *Database*

Supabase dipilih sebagai *platform* *database* karena menyediakan
beberapa keunggulan yang sesuai dengan kebutuhan sistem. Pertama,
Supabase berbasis PostgreSQL yang merupakan *database* relasional open
source dengan fitur lengkap. Kedua, Supabase menyediakan REST API
*built-in* yang memungkinkan akses data tanpa perlu mengembangkan
*backend* terpisah. Ketiga, Supabase menyediakan *dashboard* web untuk
manajemen *database* yang memudahkan *monitoring* dan administrasi.
Tabel IV.18 menyajikan spesifikasi *platform* *database* yang digunakan.

  --------------------------------------------
  Aspek            Spesifikasi
  ---------------- ---------------------------
  *Platform*       Supabase

  *Database*       PostgreSQL
  Engine           

  *Hosting*        Supabase *Cloud* (Free
                   Tier)

  Akses Data       REST API (PostgREST)

  Autentikasi API  API Key (anon key)

  *Dashboard*      Web-based
  --------------------------------------------

  : []{#_Toc223689783 .anchor}Tabel IV.16 Spesifikasi *Hosting*
  *Dashboard*

### Desain Skema *Database*

Sistem *Smart Waste Bin* menggunakan satu tabel utama bernama
sensor_data untuk menyimpan seluruh data pembacaan sensor. Desain ini
dipilih karena data yang dikumpulkan bersifat *time*-series dengan
struktur yang seragam dari semua perangkat sensor. Gambar IV.7
menunjukkan struktur tabel sensor_data pada Supabase.

![[]{#_Toc223586795 .anchor}Gambar IV.7 Tabel
sensor_data](./media/media/image13.png){width="3.136188757655293in"
height="4.386007217847769in"}

Berdasarkan Gambar IV.7, tabel sensor_data terdiri dari 15 kolom dengan
spesifikasi sebagaimana ditunjukkan pada Tabel IV.19.

  ----------------------------------------------------------------------------------
  Kolom               Tipe Data       Constraint       Deskripsi
  ------------------- --------------- ---------------- -----------------------------
  id                  int8            Primary Key,     Identifier unik record
                                      Auto-increment   

  sensor_id           text            Not Null         Identifier perangkat sensor

  tegangan            Numeric         Nullable         Tegangan baterai (Volt)

  arus                Numeric         Nullable         Arus baterai (mA)

  daya                Numeric         Nullable         Daya terpakai (mW)

  batt_percent        Numeric         Nullable         Persentase baterai (%)

  ina219_avail        Bool            Nullable         Status ketersediaan sensor
                                                       INA219

  *fillLevel*         Int4            Nullable         Tingkat kepenuhan (0-100%)

  *Distance*          Int4            Nullable         Jarak terukur (mm)

  volume              Int4            Nullable         Volume sampah (dm³)

  vl53l0x_avail       Int4            Nullable         Ketersediaan sensor VL53L0X
                                                       (1/0)

  *event*             text            Nullable         Tipe *event* (DataUpdate,
                                                       Low*Battery*, dll)

  *device*\_*topic*   Text            Nullable         *Topic* MQTT sumber data

  *Timestamp*         *Timestamp*tz   Nullable         Waktu pembacaan sensor (dari
                                                       perangkat)

  created_at          *Timestamp*tz   Nullable         Waktu data disimpan di
                                                       *database*
  ----------------------------------------------------------------------------------

  : []{#_Toc223689784 .anchor}Tabel IV.17 Detil sensor_data

Data yang tersimpan dalam tabel sensor_data mengikuti format yang telah
ditransformasi oleh *middleware*. Setiap record merepresentasikan satu
kali pembacaan sensor pada waktu tertentu. *Field* *Timestamp* mencatat
waktu pembacaan di perangkat IoT, sedangkan created_at mencatat waktu
data diterima dan disimpan di *database*. Selisih antara kedua
*Timestamp* tersebut menunjukkan latensi transmisi data dari perangkat
ke *database*.

## *Dashboard*

*Dashboard* merupakan komponen pada *Application Layer* yang berfungsi
sebagai antarmuka pengguna untuk memvisualisasikan data sensor secara
real-*time*. Pada sistem ini, *dashboard* diimplementasikan menggunakan
Next.js yang merupakan framework React untuk pengembangan aplikasi web.
Subbab ini menjelaskan arsitektur *dashboard*, fitur-fitur yang
tersedia, serta implementasi visualisasi data.

###  Arsitektur *Dashboard*

*Dashboard* dibangun menggunakan arsitektur *client*-*server* dengan
Next.js sebagai framework utama. Komponen *frontend* mengambil data dari
*backend* melalui API Routes yang terhubung ke *database* Supabase
menggunakan Drizzle ORM. Tabel IV.22 menyajikan teknologi yang digunakan
dalam pengembangan *dashboard*.

  ---------------------------------------------------------
  Komponen      Teknologi     Fungsi
  ------------- ------------- -----------------------------
  Framework     Next.js       *Server*-side rendering dan
                              routing

  UI *Library*  React         Komponen antarmuka pengguna

  Styling       Tailwind CSS  CSS framework

  Charting      Recharts      *Library* visualisasi data

  ORM           Drizzle ORM   Object-Relational *Mapping*
                              untuk akses *database*

  *Database*    Supabase      Penyimpanan data
                PostgreSQL    
  ---------------------------------------------------------

  : []{#_Toc223689785 .anchor}Tabel IV.18 Komponen Teknologi *Dashboard*

### Implementasi API

*Dashboard* berkomunikasi dengan *database* melalui API Routes yang
disediakan oleh Next.js. API endpoint /api/sensor-data diimplementasikan
pada file src/app/api/sensor-data/route.ts dan mendukung operasi CRUD
untuk manajemen data sensor. Tabel IV.21 menyajikan spesifikasi API
endpoint.

  ---------------------------------------------------------------
  Metode        Parameter                Fungsi
  ------------- ------------------------ ------------------------
  GET           sensorId, *timerange*,   Mengambil data sensor
                limit                    dengan *filter*

  POST          Body: sensor data object Menyimpan data sensor
                                         baru

  PUT           Body: id, update         Memperbarui data sensor
                *field*s                 

  DELETE        id, sensorId, olderThan  Menghapus data sensor
  ---------------------------------------------------------------

  : []{#_Toc223689786 .anchor}Tabel IV.19 Spesifikasi API Endpoint

API GET mendukung parameter *timerange* untuk mem*filter* data
berdasarkan rentang waktu. Tabel IV.22 menyajikan nilai parameter
*timerange* yang tersedia.

  ---------------------------------
  Nilai    Rentang Waktu
  -------- ------------------------
  1h       1 jam terakhir

  24h      24 jam terakhir
           (*default*)

  7d       7 hari terakhir

  30d      30 hari terakhir
  ---------------------------------

  : []{#_Toc223689787 .anchor}Tabel IV.20 Nilai Parameter *Time* *Range*

Gambar IV.7 berikut merupakan contoh *response* dari API GET.

![[]{#_Toc223586796 .anchor}Gambar IV.8 Contoh *Response*
GET](./media/media/image14.png){width="3.7296872265966754in"
height="3.500488845144357in"}

*Response* API mencakup data sensor, jumlah record, serta statistik
agregat yang dihitung langsung di *database* menggunakan fungsi SQL
AVG() dan COUNT().

### Implementasi Antarmuka

Antarmuka *dashboard* diimplementasikan sebagai komponen React pada file
src/components/*Dashboard*.tsx. Komponen ini menggunakan React Hooks
untuk manajemen *state* dan side effects. Tabel IV.23 menyajikan *state*
yang digunakan pada komponen *dashboard*.

  ------------------------------------------------------------------------------
  *State* Variable     Tipe                  Deskripsi
  -------------------- --------------------- -----------------------------------
  selectedSensor       string                Menyimpan ID sensor yang dipilih
                                             atau \"all\" untuk semua sensor

  *timerange*          string                Rentang waktu data yang ditampilkan
                                             (24h, 7d, 30d)

  sensorData           SensorDataPoint\[\]   *Array* data mentah dari sensor
                                             yang diterima dari API

  processedData        any\[\]               Data yang telah diproses untuk
                                             visualisasi chart

  sensorStats          object                Statistik agregat untuk setiap
                                             sensor

  loading              boolean               Status *loading* saat *fetching*
                                             data

  lastUpdate           Date \| null          *Timestamp* pembaruan data terakhir

  *available*Sensors   Number\[\]            Daftar sensor IDE yang tersedia
                                             dari *database* untuk opsi
                                             *Dropdown*
  ------------------------------------------------------------------------------

  : []{#_Toc223689788 .anchor}Tabel IV.21 *State* *Variable*

*Dashboard* terdiri dari enam komponen utama yaitu *Header* *Section*,
*Sensor Status* *Cards*, *Control* *Panel*, Visualisasi Data, Recent
Sensor *Readings*, dan *System* *Analytics*. Tampilan lengkap antarmuka
*dashboard* disajikan pada Lampiran B.

1.  *Header* *Section*

Bagian ini menampilkan judul aplikasi dengan ikon, tombol *refresh*
manual untuk memperbarui data secara eksplisit, dan informasi
*Timestamp* pembaruan terakhir yang menunjukkan kapan data terakhir kali
diambil dari *server*.

2.  *Sensor Status Cards*

Menampilkan kartu status untuk setiap sensor aktif dalam sistem. Setiap
kartu menyajikan:

- ID sensor dan status operasional (NORMAL, WARNING, atau CRITICAL)
  berdasarkan tingkat kepenuhan

- *Fill Level* dengan *progress bar* visual yang menggunakan skema
  warna: hijau (≤70%), kuning (71-85%), dan merah (\>85%)

- Persentase *Battery* dan konsumsi daya (*power consumption*) dalam
  satuan mW untuk *monitoring* efisiensi energi

- MQTT *topic* dan *Timestamp* terakhir untuk identifikasi perangkat dan
  verifikasi konektivitas

3.  *Control* *Panel*

Menyediakan kontrol interaktif untuk mem*filter* data yang ditampilkan,
terdiri dari:

- *Dropdown* pemilihan sensor yang di-populate secara dinamis dari
  *field* *available*Sensors pada *response* API, untuk menampilkan data
  sensor spesifik atau semua sensor secara agregat

- *Dropdown* rentang waktu dengan opsi: *Last 24 Hours*, *Last 7 Days*,
  dan *Last 30 Days*

- Informasi jumlah *data points* yang sedang ditampilkan dan jumlah
  *active sensors* dalam sistem

4.  Visualisasi Data

Dua chart interaktif yang diimplementasikan menggunakan *library*
Recharts dalam layout grid 1×2:

- *Waste* *Fill Level* *Trend*: *Line* *chart* yang menampilkan tren
  tingkat kepenuhan sampah dari waktu ke waktu dengan sumbu X
  menunjukkan waktu dan sumbu Y menunjukkan persentase kepenuhan
  (0-100%)

- *Battery* & *Power* *Consumption*: *Dual-axis line chart* yang
  menampilkan persentase *Battery* dan konsumsi daya secara bersamaan
  untuk *monitoring* efisiensi energi sistem

5.  *Recent* Sensor *Readings*

Tabel yang menampilkan 10 pembacaan sensor terbaru dengan kolom: Sensor,
*Fill Level*, *Battery*, *Power*, *Distance*, Volume, *Timestamp*, dan
Status. Setiap baris dilengkapi dengan progress bar mini pada kolom
*fill Level* dan status indicator dengan warna yang sesuai
(hijau/kuning/merah).

6.  System Analytics

Menampilkan 5 metrik agregat sistem dalam bentuk card visual: Total
Records (jumlah total data), Active Sensors (jumlah sensor aktif), Avg
*Battery* (rata-rata persentase baterai), Avg *Power* (rata-rata
konsumsi daya), dan Critical *Alert*s (jumlah sensor dengan status
kritis). Setiap metrik ditampilkan dengan warna berbeda untuk kemudahan
identifikasi visual.

*Dashboard* mengimplementasikan auto-refresh setiap 30 detik menggunakan
useEffect Hook dengan setInterval dan cleanup function untuk mencegah
memory leak. Konfigurasi threshold status sensor (Normal ≤70%, Warning
71-85%, Critical \>85%) diimplementasikan dalam fungsi
getStatusFrom*fillLevel*() yang menentukan warna visual pada seluruh
antarmuka.

### *Dashboard* *Hosting*

*Dashboard* di-deploy menggunakan *platform* Vercel yang merupakan
*platform* *hosting* resmi untuk aplikasi Next.js. Tabel IV.24
menyajikan spesifikasi *hosting* *dashboard*.

  -----------------------------------------------------------------------
  Aspek                     Spesifikasi
  ------------------------- ---------------------------------------------
  *Platform*                Vercel (free tier)

  Framework P*reset*        Next.js

  Build Command             next build

  *Output* Directory        .next

  *Deployment* Method       Git Integration (Continuous *Deployment*)

  Domain                    Subdomain Vercel (\*vercel.app)
  -----------------------------------------------------------------------

  : []{#_Toc223689789 .anchor}Tabel IV.22 Spesifikasi Dashboard
  *Hosting*

*Deployment* dilakukan secara otomatis melalui integrasi dengan
repository Git. Setiap push ke branch utama akan memicu proses build dan
*deployment* secara otomatis (Continuous *Deployment*).

[\
]{.mark}

#  HASIL DAN EVALUASI

Bab ini merupakan realisasi dari tahap Pengujian dalam metodologi Design
Thinking yang telah diuraikan pada Bab I. Setelah sistem *Smart Waste
Bin* didesain dan diimplementasikan pada Bab IV, tahap selanjutnya
adalah mengevaluasi kinerja sistem secara menyeluruh dan menganalisis
data yang dikumpulkan untuk menjawab rumusan masalah penelitian.

## Metode Evaluasi

Evaluasi sistem *Smart Waste Bin* dilakukan secara sistematis melalui
beberapa skenario yang masing-masing dirancang untuk menjawab rumusan
masalah yang telah ditetapkan pada Bab I. Sebelum menjelaskan skenario
evaluasi, subbab ini terlebih dahulu mendeskripsikan konfigurasi sistem
dan lingkungan pengujian yang digunakan selama periode evaluasi.

### Konfigurasi Pengujian Sistem

Pengujian sistem dilakukan dengan mengoperasikan tiga unit perangkat
*Smart Waste Bin* di Lantai 4 Gedung Labtek VIII Institut Teknologi
Bandung. Perangkat ditempatkan di area koridor depan Laboratorium IoT
yang berada di ujung lantai. Pemilihan lokasi ini didasarkan pada
beberapa pertimbangan sebagai berikut.

1.  Penempatan tiga unit tempat sampah berukuran besar di area umum
    gedung memerlukan proses perizinan dan birokrasi yang panjang. Area
    depan Laboratorium IoT yang berada di ujung lantai memungkinkan
    proses perizinan yang lebih sederhana dengan dukungan dari pengelola
    laboratorium.

2.  Peneliti sering beraktivitas di Laboratorium IoT, sehingga
    memudahkan *monitoring* rutin dan *maintenance* perangkat jika
    diperlukan.

3.  Meskipun berada di ujung lantai, area ini tetap dilalui oleh
    pengguna gedung dan memiliki aktivitas pembuangan sampah yang dapat
    diobservasi.

Setiap unit *smart waste bin* diberi kode warna sesuai dengan jenis
sampah yang ditampung sebagaimana disajikan pada Tabel V.1.

  ------------------------------------------------------------------------
  **Sensor    **Kode Warna**       **Jenis Sampah**    **MQTT *Topic***
  ID**                                                 
  ----------- -------------------- ------------------- -------------------
  1           Hijau                Organik             wp2/basic_01

  2           Kuning               Anorganik           wp2/basic_02

  3           Hitam                Residu              wp2/basic_03
  ------------------------------------------------------------------------

  : []{#_Toc223689790 .anchor}Tabel V.1 Detil Unit SWB

Pemberian kode warna mengikuti standar pemilahan sampah yang umum
diterapkan di lokasi umum, di mana warna hijau untuk sampah organik,
kuning untuk sampah anorganik, dan hitam untuk sampah residu. Analisis
per jenis sampah dilakukan berdasarkan label tempat sampah dengan asumsi
pengguna membuang sampah sesuai label.

Konfigurasi pengujian mencakup seluruh komponen sistem dari *Perception
Layer* hingga *Application Layer* sebagaimana telah dirancang pada Bab
IV. Tabel V.2 menyajikan konfigurasi lingkungan pengujian secara
keseluruhan.

  -----------------------------------------------------------------------
  Aspek                 Spesifikasi
  --------------------- -------------------------------------------------
  Lokasi                Lantai 4, Gedung Labtek VIII ITB

  Area Penempatan       Koridor depan Laboratorium IoT

  Jumlah Perangkat      3 unit

  Periode Pengumpulan   24 Desember 2025 - 29 Januari 2026
  Data                  

  Interval Pengiriman   \~2.5 jam
  Data                  

  Konektivitas          GSM/GPRS (SIM800L)

  *Database*            Supabase PostgreSQL

  *Dashboard*           Next.js pada Vercel
  -----------------------------------------------------------------------

  : []{#_Toc223689791 .anchor}Tabel V.2 Konfigurasi Lingkungan

### Skenario Evaluasi 

Skenario evaluasi dirancang untuk menjawab setiap rumusan masalah yang
telah ditetapkan pada Bab I. Tabel V.3 menyajikan *mapping* antara
rumusan masalah, skenario evaluasi, dan tujuan evaluasi.

[]{#_Toc223689792 .anchor}Tabel V.3 *Mapping* Rumusan Masalah dengan
Skenario Evaluasi

  ------------------------------------------------------------------------
  ID      Rumusan Masalah       Skenario         Tujuan Evaluasi
                                Evaluasi         
  ------- --------------------- ---------------- -------------------------
  RM-1    Rancangan dan         SE-01: Evaluasi  Memverifikasi fungsi
          implementasi sistem   Fungsionalitas   sistem berjalan sesuai
          *Smart Waste Bin*     Sistem           dengan rancangan dan
          berbasis IoT yang                      implementasi yang telah
          mampu mengumpulkan                     dilakukan
          data secara periodik                   
          dan terstruktur                        

  RM-1                          SE-02: Evaluasi  Mengukur keberhasilan
                                Pengumpulan Data pengumpulan data periodik

  RM-2    Pola pembuangan       SE-03: Analisis  Mengidentifikasi pola
          sampah yang dapat     Pola Pembuangan  temporal dan validasi
          diidentifikasi                         lapangan
          berdasarkan data                       
          sistem dan                             
          validasinya terhadap                   
          observasi lapangan                     

  RM-3    Peningkatan           SE-04: Evaluasi  Mengevaluasi efektivitas
          *firmware* agar       Peningkatan      peningkatan *firmware*
          perangkat *Smart      Sistem           secara kualitatif
          Waste Bin* skala                       
          perkotaan dapat                        
          beroperasi optimal di                  
          lingkungan kampus                      
  ------------------------------------------------------------------------

## Hasil Evaluasi 

Bagian ini menyajikan hasil evaluasi untuk setiap skenario yang telah
dirancang pada subbab V.1.2. Setiap skenario dilengkapi dengan
metodologi pengujian, hasil pengujian, dan kesimpulan yang menjawab
rumusan masalah terkait.

### Hasil Evaluasi Fungsionalitas Sistem (SE-01)

Skenario SE-01 mengevaluasi fungsionalitas seluruh komponen sistem
*Smart Waste Bin* untuk memverifikasi bahwa arsitektur dan mekanisme
berfungsi sesuai dengan desain pada Bab IV. Pengujian fungsionalitas
dilakukan dengan metode *black-box* testing pada setiap *layer*
arsitektur IoT.

+---------------+------------------+---------------+------------------+
| *Layer*       | Komponen         | Aspek         | Kriteria         |
|               |                  | Pengujian     | Keberhasilan     |
+===============+==================+===============+==================+
| Perception    | VL53L0X          | Pengukuran    | Persentase       |
|               |                  | jarak objek   | *fillLevel*      |
|               |                  |               | sensor sesuai    |
|               |                  |               | dengan           |
|               |                  |               | persentase       |
|               |                  |               | aktual           |
+---------------+------------------+---------------+------------------+
| Perception    | INA219           | *Monitoring*  | Nilai dalam      |
|               |                  | tegangan dan  | *range*          |
|               |                  | arus          | operasional      |
|               |                  |               | normal dan       |
|               |                  |               | kegagalan        |
|               |                  |               | pembacaan tidak  |
|               |                  |               | lebih dari 1     |
|               |                  |               | hari             |
+---------------+------------------+---------------+------------------+
| Network       | SIM800L          | Koneksi       | Berhasil         |
|               |                  |               | terhubung ke APN |
|               |                  | GPRS ke       | *operator*       |
|               |                  | jaringan      |                  |
+---------------+------------------+---------------+------------------+
| Network       | MQTT             | *Publish*     | Data terkirim    |
|               |                  | data ke       | dengan format    |
|               |                  | *broker*      | valid            |
+---------------+------------------+---------------+------------------+
| *Middleware*  | API              | *Response*    | Status 200       |
|               |                  | *endpoint*    | dengan data      |
|               |                  |               | valid            |
+---------------+------------------+---------------+------------------+
| *Application* | *Dashboard*      | *Rendering*   | Data ditampilkan |
|               |                  | komponen UI   | dengan benar dan |
|               |                  |               | lengkap          |
+---------------+------------------+---------------+------------------+
| *Application* | Supabase         | *Insert* dan  | Data tersimpan   |
|               |                  | *query* data  | dengan benar     |
+---------------+------------------+---------------+------------------+

: []{#_Toc223689793 .anchor}Tabel V.4 Pengujian Fungsionalitas Sistem

#### Hasil Pengujian *Perception Layer*

Pengujian *Perception Layer* mencakup sensor VL53L0X untuk pengukuran
jarak dan sensor INA219 untuk *monitoring* daya.

Pengujian sensor VL53L0X dilakukan dengan membandingkan pembacaan sensor
dengan pengukuran manual menggunakan meteran pada berbagai jarak.
Pengujian dilakukan sebanyak 5 kali untuk setiap titik jarak.

  ---------------------------------------------------------
  Jarak Aktual (cm,  Pembacaan Sensor     Pembacaan Sensor
  *fillLevel* %)     (raw)                (*fillLevel*)
  ------------------ -------------------- -----------------
  100 (\~0%)         Sensor 1-3: \>900    Sensor 1-3: 0%

  80 (\~20%)         Sensor 1-3: 700 -    Sensor 1-3: 20%
                     799                  

  60 (\~40%)         Sensor 1-3: 500 -    Sensor 1-3: 40%
                     599                  

  20 (\~80%)         Sensor 1-3: 100 -199 Sensor 1-3: 80%

  0 (\~100%)         Sensor 1-3: 0 - 99   Sensor 1-3: 100%
  ---------------------------------------------------------

  : []{#_Toc223689794 .anchor}Tabel V.5 Hasil Pengujian Sensor VL53L0X

Mekanisme penentuan *fillLevel* pada *firmware* bekerja sebagai berikut.
Sistem membaca data raw dalam milimeter, kemudian menghitung selisih
ketinggian menggunakan rumus heightDiff = (1000 - height) / 100. Nilai
tersebut kemudian dipetakan ke persentase 0-100% menggunakan fungsi
map(). Penggunaan tipe data integer menyebabkan pembulatan (truncation)
yang memberikan efek stabilisasi pada indikator *dashboard* agar tidak
terlalu fluktuatif. Hasil pengujian menunjukkan kesesuaian yang tinggi
antara pengukuran manual dengan *output* sistem.

Setelah pengujian sensor VL53L0X, pengujian sensor INA219 dilakukan
selama periode pengumpulan data untuk memverifikasi keandalan pembacaan
tegangan, arus, dan daya. Kriteria keberhasilan adalah kegagalan
pembacaan tidak lebih dari 1 hari berturut-turut.

  ------------------------------------------------------------------
  Sensor   Jenis       Tegangan (V)  Arus (mA)  Daya (mW)   Status
  -------- ----------- ------------- ---------- ----------- --------
  1        Organik     7.30 - 7.50   110 - 140  803 - 1050  OK

  2        Anorganik   7.10 - 7.45   110 - 135  781 - 1006  OK

  3        Residu      6.90 - 7.50   210 - 235  1449 - 1763 FAILED
  ------------------------------------------------------------------

  : []{#_Toc223689795 .anchor}Tabel V.6 Hasil Pengujian Sensor INA219

Sensor 3 (Residu) menunjukkan konsumsi arus yang lebih tinggi (210-235
mA) dibandingkan sensor lainnya (110-140 mA). Hal ini disebabkan oleh
karakteristik *hardware* yang berbeda pada unit tersebut. Sensor 3
(Residu) juga mengalami kegagalan INA219 selama 4 hari berturut-turut
(11-14 Januari 2026), melebihi batas kriteria 1 hari berturut-turut.
Kegagalan ini bertepatan dengan periode gangguan kabel I2C yang juga
menyebabkan kegagalan VL53L0X secara bersamaan. Setelah perbaikan kabel,
pembacaan kembali normal. Sensor 1 dan 2 tidak mengalami kegagalan
INA219 sama sekali sehingga kriteria terpenuhi untuk kedua sensor
tersebut.

#### Hasil Pengujian *Network Layer*

Pengujian *Network Layer* dilakukan sebelum pemasangan perangkat di
tempat sampah dengan memverifikasi *output* *debug* pada *Serial*
*Monitor*. Pengujian mencakup konektivitas GPRS dan komunikasi MQTT.
Pengujian modul GPRS dilakukan dengan mengamati *output* Serial Monitor
saat modul SIM800L melakukan inisialisasi dan koneksi ke jaringan GPRS.

  -----------------------------------------------------------------------
  Tahap              *Output* Serial Monitor                     Status
  ------------------ ------------------------------------------- --------
  Inisialisasi Modem Initializing modem\...                      OK

  Info Modem         Modem Info: SIM800 R14.18                   OK

  Registrasi         Waiting for network\... success             OK
  Jaringan                                                       

  Status Jaringan    Network connected                           OK

  Koneksi APN        Connecting to M2MINTERNET\... success       OK

  Status GPRS        GPRS connected                              OK
  -----------------------------------------------------------------------

  : []{#_Toc223689796 .anchor}Tabel V.7 Hasil Pengujian Modem GPRS

Seluruh tahap koneksi GPRS berhasil dengan *output* sesuai yang
diharapkan. Modul SIM800L dinyatakan lulus pengujian.

Setelah itu**,** pengujian MQTT dilakukan dalam dua tahap: pertama
menggunakan listener lokal (MQTT *client*) untuk memverifikasi data
terkirim, kemudian menggunakan Node-RED sebagai *subscriber* untuk
memproses data ke *database*.

  --------------------------------------------------------------------------
  Tahap            Hasil                                            Status
  ---------------- ------------------------------------------------ --------
  Koneksi ke       Connecting to 38.47.176.109\... success          OK
  *Broker*                                                          

  Test Listener    Data JSON diterima oleh MQTT *client* pada       OK
  Lokal            *topic* wp2/basic_01, 02, 03                     

  Test ke Node-RED Node-RED menerima dan mem-parse data JSON dengan OK
                   benar                                            

  Format *Payload* JSON valid: sensor_id, tegangan, arus, daya,     OK
                   battPercent, capacity, dist, vol, vl53l0x_avail, 
                   ina219_avail                                     
  --------------------------------------------------------------------------

  : []{#_Toc223689797 .anchor}Tabel V.8 Hasil Pengujian MQTT

Pengujian *Network Layer* menunjukkan bahwa modul SIM800L berhasil
terhubung ke jaringan GPRS dan komunikasi MQTT ke *broker* berfungsi
dengan baik.

#### Hasil Pengujian *Middleware* *Layer* dan *Application Layer*

Pengujian pada tahap ini berfokus pada pusat pengolahan, penyimpanan,
dan visualisasi data. *Middleware* *Layer* yang terdiri dari Node-RED
dan *database* Supabase bertugas untuk menjembatani aliran data dari
perangkat keras menuju antarmuka pengguna. Pengujian pada *layer* ini
bertujuan untuk memastikan bahwa setiap *payload* MQTT yang dikirimkan
oleh sensor berhasil ditangkap, diproses (parsing), dan disimpan ke
dalam *database* relasional tanpa ada data yang hilang (*data loss*)
atau rusak (corrupt). Tabel V.9 menyajikan hasil pengujian
fungsionalitas *Middleware* *Layer*.

  --------------------------------------------------------------------------
  Aspek Pengujian  Hasil                                            Status
  ---------------- ------------------------------------------------ --------
  Subscribe MQTT   Berhasil subscribe ke wp2/basic_01,              OK
                   wp2/basic_02, wp2/basic_03                       

  Parsing JSON     Data JSON di-parse dengan benar menggunakan JSON OK
                   *node*                                           

  Insert ke        Data diteruskan ke Supabase melalui HTTP request OK
  Supabase         *node*                                           

  Data Integrity   Tidak ada data corrupt atau duplikat             OK

  *Query*          *Response* *time* \< 500ms untuk *query* 1       OK
  Performance      minggu                                           
  --------------------------------------------------------------------------

  : []{#_Toc223689798 .anchor}Tabel V.9 Hasil Pengujian Node-RED

Setelah data dipastikan tersimpan dengan aman di Supabase, pengujian
dilanjutkan ke *Application Layer*, yang diawali dengan pengujian pada
Application *Programming* *Interface* (API) endpoint. Pengujian
dilakukan dengan melakukan request HTTP GET menggunakan parameter yang
berbeda untuk memverifikasi apakah *filter* data berdasarkan ID sensor
dan rentang waktu beroperasi secara presisi. Hasil pengujian endpoint
dirangkum pada Tabel V.10.

  ----------------------------------------------------------------------------
  Endpoint                           Method   Expected     *Actual*   Status
  ---------------------------------- -------- ------------ ---------- --------
  /api/sensor-data                   GET      200, array   200        OK

  /api/sensor-data?sensorId=1        GET      200,         200        OK
                                              *filter*ed              

  /api/sensor-data?sensorId=2        GET      200,         200        OK
                                              *filter*ed              

  /api/sensor-data?sensorId=3        GET      200,         200        OK
                                              *filter*ed              

  /api/sensor-data?*timerange*=24h   GET      200, 24h     200        OK
                                              data                    

  /api/sensor-data?*timerange*=7d    GET      200, 7d data 200        OK
  ----------------------------------------------------------------------------

  : []{#_Toc223689799 .anchor}Tabel V.10 Hasil Pengujian API *Dashboard*

pengujian User *Interface* (UI) pada komponen *dashboard* Next.js.
Pengujian ini dilakukan secara end-to-end untuk memastikan bahwa data
yang ditarik dari API berhasil dirender ke dalam bentuk visualisasi
grafik dan indikator yang mudah dipahami oleh pengguna. Selain itu,
fitur-fitur interaktif seperti panel kontrol dan mekanisme pembaruan
data otomatis (auto-refresh) juga divalidasi kinerjanya. Detil pengujian
antarmuka disajikan pada Tabel V.11.

  ------------------------------------------------------------------------
  Komponen        Aspek Pengujian                                 Hasil
  --------------- ----------------------------------------------- --------
  *Header*        Menampilkan judul, tombol refresh, last update  Sesuai
  Section                                                         

  Sensor Cards    Menampilkan status 3 sensor dengan warna        Sesuai
                  threshold                                       

  *Fill Level*    Progress bar sesuai persentase *fillLevel*      Sesuai
  Bar                                                             

  *Control* Panel *Filter* sensor dan *time* *range* berfungsi    Sesuai

  Chart: *Fill    Line chart menampilkan tren *fillLevel*         Sesuai
  Level*                                                          

  Chart:          Dual-axis chart *Battery* dan *power*           Sesuai
  *Battery*       consumption                                     

  Auto-refresh    Data ter-update setiap 30 detik                 Sesuai
  ------------------------------------------------------------------------

  : []{#_Toc223689800 .anchor}Tabel V.11 Hasil Pengujian Komponen
  *Dashboard*

Seluruh komponen sistem dari *Perception Layer* hingga *Application
Layer* berfungsi sesuai dengan desain. Hasil pengujian ini menjawab RM-1
terkait komponen, arsitektur, dan mekanisme sistem *Smart Waste Bin*
berbasis IoT.

### Hasil Evaluasi Pengumpulan Data (SE-02)

Skenario SE-02 mengevaluasi keberhasilan dan konsistensi pengumpulan
data secara periodik selama periode observasi. Evaluasi ini melengkapi
jawaban RM-1 terkait mekanisme sistem.

#### Periode Pengumpulan Data

Data dikumpulkan selama periode 24 Desember 2025 hingga 29 Januari 2026.
Tabel V.12 menyajikan detil periode pengumpulan data.

  ---------------------------------------------------------------
  Aspek                    Nilai
  ------------------------ --------------------------------------
  Tanggal mulai            24 Desember 2025

  Tanggal selesai          29 Januari 2026

  Total durasi             37 hari

  Hari kerja (Senin-Jumat) 24 hari

  *Weekend* (Sabtu-Minggu) 10 hari

  Hari libur nasional      3 hari

  Target Interval          ± 2.5 jam (*TIME*\_TO_SLEEP = 150
  pengiriman               menit)
  ---------------------------------------------------------------

  : []{#_Toc223689801 .anchor}Tabel V.12 Detil Pengumpulan Data

Hari libur nasional yang tercatat selama periode pengumpulan data
meliputi: 25-26 Desember 2025 (Natal dan Cuti Bersama) dan 1 Januari
2026 (Tahun Baru).

#### Volume Data Terkumpul

Tabel V.13 menyajikan jumlah data yang berhasil dikumpulkan dari setiap
sensor selama periode observasi.

  ------------------------------------------------------------------
  Sensor   Jenis Sampah Records   Target   Pencapaian   Status
  -------- ------------ --------- -------- ------------ ------------
  1        Organik      289       296      97.6%        OK

  2        Anorganik    290       296      98.0%        OK

  3        Residu       226       296      76.4%        Sebagian OK

  Total    \-           805       888      90.7%        \-
  ------------------------------------------------------------------

  : []{#_Toc223689802 .anchor}Tabel V.13 Hasil Jumlah Data

Target 296 *records* per sensor diperoleh dari total durasi observasi 37
hari dengan asumsi interval pengiriman terburuk 3 jam, sehingga dalam
satu hari diharapkan terkumpul minimal 8 *records* per sensor (24 jam ÷
3 jam = 8 records/hari × 37 hari = 296 records). Sensor 1 (Organik) dan
Sensor 2 (Anorganik) mencapai target mendekati 100%. Sensor 3 (Residu)
mencapai 76.4% yang lebih rendah karena konsumsi daya yang lebih tinggi
(210-235 mA vs 110-140 mA), menyebabkan baterai lebih cepat habis.

#### Konsistensi Interval Pengiriman

Tabel V.14 menyajikan statistik Interval pengiriman data untuk setiap
sensor.

  ---------------------------------------------------------
  Sensor   Rata-rata      Minimum   Maximum        Std Dev
  -------- -------------- --------- -------------- --------
  1        2 jam 24 menit 35 menit  4 jam 58 menit 25 menit

  2        2 jam 24 menit 22 menit  5 jam 22 menit 31 menit

  3        2 jam 21 menit 2 menit\* 4 jam 57 menit 38 menit
  ---------------------------------------------------------

  : []{#_Toc223689803 .anchor}Tabel V.14 Statistik Interval Pengiriman
  Data

\*Nilai minimum sangat kecil merupakan indikasi retry pengiriman setelah
koneksi gagal, bukan Interval reguler. Rata-rata Interval ±144 menit (≈2
jam 24 menit) mendekati target *TIME*\_TO_SLEEP = 150 menit.

#### Analisis *Data loss* dan Data Kotor

Selama periode pengumpulan data, terdapat data yang hilang (*loss*)
maupun data yang tidak valid (kotor). Tabel V.15 menyajikan analisis
penyebab *data loss* dan data kotor.

  ---------------------------------------------------------------------------
  Kategori        Jumlah   Persentase   Penyebab / Keterangan
  --------------- -------- ------------ -------------------------------------
  Data sukses     805      90.7%        \-
  terkirim                              

  Kabel           35       3.9%         Saat penggantian baterai, kabel
  I2C/sensor                            terganggu dan perlu kalibrasi ulang
  terganggu                             

  Baterai habis / 25       2.8%         *Deep sleep* karena baterai habis; 4
  bocor                                 baterai bocor (mati total)

  Gagal koneksi   10       1.1%         SIM card expired atau modul tidak
  GPRS                                  terbaca karena kabel terganggu

  MQTT *broker*   8        0.9%         *Broker* tidak aktif; pengumpulan
  down                                  dihentikan 29 Januari 2026 karena
                                        *broker* dimatikan vendor

  Total expected  888      100%         \-

  Total *data     78       8.8%         Dalam batas toleransi (\<10%)
  loss*                                 
  ---------------------------------------------------------------------------

  : []{#_Toc223689804 .anchor}Tabel V.15 Penyebab *Data loss* dan Kotor

Penyebab utama data loss adalah gangguan pada kabel I2C atau kabel
sensor saat penggantian baterai. Proses penggantian baterai memerlukan
pembukaan casing yang dapat menggeser posisi kabel, sehingga diperlukan
kalibrasi ulang setelahnya. Kalibrasi tersebut dapat menghasilkan data
yang tidak valid (data kotor). Selain itu, 4 unit baterai mengalami
kebocoran dan mati total karena tidak mampu menahan beban konsumsi daya,
terutama pada Sensor 3 yang memiliki konsumsi lebih tinggi.

Pengumpulan data dihentikan pada tanggal 29 Januari 2026 karena MQTT
broker dimatikan oleh vendor penyedia layanan. Meskipun terdapat
berbagai kendala teknis, total data loss sebesar 8.8% masih dalam batas
toleransi yang ditetapkan (\<10%).

Selain data loss, ada pula data yang berhasil terkirim namun memiliki
nilai yang tidak valid atau anomali. Tabel V.16 menyajikan jenis-jenis
data kotor yang teridentifikasi beserta penyebabnya.

  ----------------------------------------------------------------------------
  Jenis Anomali Jumlah   Indikator             Penyebab
  ------------- -------- --------------------- -------------------------------
  *Battery*     7        tegangan = arus =     Kabel I2C putus total
  999%                   batt = 999,           menyebabkan INA219 dan VL53L0X
                         *fillLevel* = -1,     gagal sekaligus (ina219_avail =
                         ina219_avail = 0,     0, vl53l0x_avail = 0);
                         vl53l0x_avail = 0     seluruhnya berasal dari Sensor
                                               3

  *fillLevel* = 3        *fillLevel* di luar   VL53L0X *timeout* atau *error*
  -1 atau 101+           0-100%                karena kabel sensor terganggu
  ----------------------------------------------------------------------------

  : []{#_Toc223689805 .anchor}Tabel V.16 Jenis-jenis Data Kotor

Berdasarkan dirty_data_log (Lampiran A, tautan No.4), terdapat 11 record
kotor yang seluruhnya berasal dari Sensor 3 (Residu). Sebanyak 7 record
mengalami kegagalan ganda pada INA219 dan VL53L0X secara bersamaan,
ditandai dengan nilai tegangan, arus, baterai, dan fillLevel yang
bernilai 999 atau -1 (ina219_avail = 0, vl53l0x_avail = 0). Sebanyak 3
record mengalami kegagalan VL53L0X saja (fillLevel = -1) sementara
INA219 masih berfungsi, dan 1 record borderline dengan fillLevel = 0
meskipun vl53l0x_avail = 0. Seluruh data kotor disebabkan oleh masalah
kabel I2C pada Sensor 3, konsisten dengan anomali konsumsi daya tinggi
yang teridentifikasi pada unit tersebut. Data kotor ini dapat
diidentifikasi melalui kolom vl53l0x_avail dan ina219_avail pada
dataset, serta validasi range nilai fillLevel dan battPercent.

#### Kualitas Data Setelah *Filtering*

Setelah data kotor di-*filter* berdasarkan kolom availability sensor,
Tabel V.17 menyajikan hasil analisis kualitas data yang valid.

  -------------------------------------------------------------
  Metrik Kualitas                                       Hasil
  ----------------------------------------------------- -------
  Data dengan vl53l0x_avail = 1 (sensor jarak aktif)    100%

  Data dengan ina219_avail = 1 (sensor daya aktif)      100%

  *fillLevel* dalam *range* valid (0-100%) setelah      100%
  *filter*                                              

  *Timestamp* valid (format ISO 8601, *time*zone        100%
  Asia/Jakarta)                                         

  Tidak ada duplikat (unique *Timestamp* + sensor_id)   100%

  *Battery* percentage dalam *range* valid (0-100%)     100%
  setelah *filter*                                      

  Sensor ID valid (1, 2, atau 3)                        100%
  -------------------------------------------------------------

  : []{#_Toc223689806 .anchor}Tabel V.17 Hasil Kualitas Data

Kualitas data yang terkumpul sangat baik dengan rata-rata validitas di
atas 100% untuk semua metrik yang diukur. Data dengan vl53l0x_avail = 0
atau ina219_avail = 0 di*filter* pada tahap *preprocessing* sebelum
analisis pola, sehingga hanya data valid yang digunakan untuk
identifikasi pola pembuangan sampah.

#### Distribusi Temporal Data

Tabel V.18 dan V.19 menyajikan distribusi data berdasarkan waktu untuk
memastikan data terdistribusi merata.

  ----------------------------------------
  Rentang Jam  Jumlah Records Persentase
  ------------ -------------- ------------
  07:00 -      56             7.0%
  09:00                       

  09:00 -      81             10.1%
  12:00                       

  12:00 -      53             6.6%
  14:00                       

  14:00 -      119            14.8%
  17:00                       

  17:00 -      73             9.1%
  19:00                       

  19:00 -      423            52.5%
  07:00                       

  Total        805            100%
  ----------------------------------------

  : []{#_Toc223689807 .anchor}Tabel V.18 Jumlah Record per Rentang Jam

  ------------------------------------
  Hari     Jumlah Records Persentase
  -------- -------------- ------------
  Senin    102            12.7%

  Selasa   127            15.8%

  Rabu     153            19.0%

  Kamis    135            16.8%

  Jumat    108            13.4%

  Sabtu    91             11.3%

  Minggu   89             11.1%

  Total    805            100%
  ------------------------------------

  : []{#_Toc223689808 .anchor}Tabel V.19 Jumlah Record per Hari

Rentang 19:00-07:00 mendominasi distribusi jam (52.5%) karena sensor
mengirim data setiap ±2.5 jam selama 24 jam penuh, termasuk sepanjang
malam. Dari 805 records, sebanyak 382 records (47.5%) berasal dari jam
aktif kampus (07:00-19:00). Distribusi per hari relatif merata dengan
sedikit variasi --- hari kerja (Senin-Jumat) masing-masing berkontribusi
12-19%, sedangkan Sabtu dan Minggu masing-masing 11.3% dan 11.1%.

### Hasil Analisis Pola Pembuangan Sampah (SE-03)

Skenario SE-03 mengidentifikasi pola temporal pembuangan sampah
berdasarkan data yang dikumpulkan dan memvalidasinya dengan observasi
lapangan untuk menjawab RM-2. Analisis dilakukan menggunakan *script*
Python yang mencakup data cleaning, perhitungan statistik deskriptif,
dan visualisasi pola (kode sumber tersedia pada Lampiran A, Tautan No.
4).

#### Statistik Deskriptif fillLevel pada Setiap Sensor

Tabel V.20 menyajikan statistik deskriptif *fillLevel* untuk setiap
sensor.

  -------------------------------------------------------
  Statistik       Organik (S1) Anorganik (S2) Residu (S3)
  --------------- ------------ -------------- -----------
  Jumlah data (n) 289          290            226

  *Mean*          5.3%         14.4%          6.4%

  Median          0%           10%            10%

  Modus           0%           0%             10%

  Std Deviasi     5.7%         13.0%          6.0%

  Minimum         0%           0%             0%

  Maximum         20%          40%            20%
  -------------------------------------------------------

  : []{#_Toc223689809 .anchor}Tabel V.20 Statistik *fillLevel*

![[]{#_Toc223586797 .anchor}Gambar V.1 Statistik
*fillLevel*](./media/media/image15.png){width="5.511805555555555in"
height="2.2222222222222223in"}

Sensor 2 (Anorganik) memiliki rata-rata *fillLevel* tertinggi (14.4%)
dengan variasi terbesar (std 13.0%), menunjukkan aktivitas pembuangan
sampah anorganik paling tinggi di lokasi pengujian. Median Organik (S1)
bernilai 0% karena lebih dari separuh records memiliki *fillLevel* 0%,
mencerminkan frekuensi pengosongan yang tinggi.

#### Distribusi *fillLevel*

Tabel V.21 menyajikan distribusi frekuensi nilai *fillLevel* pada setiap
sensor.

  ---------------------------------------------------------------------
  *fillLevel*   Organik (S1)       Anorganik (S2)    Residu (S3)
  ------------- ------------------ ----------------- ------------------
  0%            145 records        93 records        96 records (42.5%)
                (50.2%)            (32.1%)           

  10%           134 records        66 records        116 records
                (46.4%)            (22.8%)           (51.3%)

  20%           10 records (3.5%)  69 records        14 records (6.2%)
                                   (23.8%)           

  30%           0 records (0%)     35 records        0 records (0%)
                                   (12.1%)           

  40%           0 records (0%)     27 records (9.3%) 0 records (0%)
  ---------------------------------------------------------------------

  : []{#_Toc223689810 .anchor}Tabel V.21 Distribusi *fillLevel*

Sampah Anorganik memiliki distribusi *fillLevel* paling bervariasi
dengan nilai mencapai 40%, sedangkan Organik dan Residu didominasi oleh
*fillLevel* rendah (0-10%) yang menunjukkan tempat sampah dikosongkan
secara rutin.

#### Pola Temporal Harian

Analisis pola harian dilakukan dengan mengelompokkan rata-rata
*fillLevel* berdasarkan rentang jam. Nilai yang ditampilkan merupakan
rata-rata *fillLevel* kumulatif per slot waktu, bukan laju penambahan.

  -----------------------------------------------------------------
  Rentang Jam   Organik   Anorganik   Residu   Keterangan
  ------------- --------- ----------- -------- --------------------
  07:00 - 09:00 6.5%      11.4%       5.7%     Awal aktivitas
                                               kampus

  09:00 - 12:00 5.9%      14.8%       8.8%     Jam kerja/kuliah
                                               pagi

  12:00 - 14:00 7.8%      13.2%       10.0%    Jam makan siang

  14:00 - 17:00 5.6%      13.4%       5.7%     Jam kerja/kuliah
                                               sore

  17:00 - 19:00 5.6%      15.7%       5.5%     Akhir aktivitas

  19:00 - 07:00 4.7%      14.9%       5.8%     Non-aktif (malam)
  -----------------------------------------------------------------

  : []{#_Toc223689811 .anchor}Tabel V.22 Pola Temporal Harian

![[]{#_Toc223586798 .anchor}Gambar V.2 Distribusi *fillLevel* per
Rentang Jam](./media/media/image16.png){width="5.511805555555555in"
height="2.44375in"}

Nilai *fillLevel* tertinggi pada S1 (Organik) dan S3 (Residu) terjadi
pada rentang 12:00-14:00, konsisten dengan aktivitas makan siang. S2
(Anorganik) menunjukkan *fillLevel* relatif tinggi dan merata sepanjang
hari.

#### Pola Temporal Mingguan

Analisis pola mingguan dilakukan dengan mengelompokkan rata-rata
*fillLevel* berdasarkan hari. Nilai *fillLevel* bersifat kumulatif antar
pengosongan sehingga pola dipengaruhi jadwal pengosongan aktual, bukan
semata aktivitas pengguna.

  ---------------------------------------------------
  Hari     Organik   Anorganik   Residu   Kategori
  -------- --------- ----------- -------- -----------
  Senin    5.0%      10.8%       8.9%     Hari kerja

  Selasa   7.2%      13.0%       8.0%     Hari kerja

  Rabu     4.7%      14.1%       8.9%     Hari kerja

  Kamis    4.0%      15.3%       5.3%     Hari kerja

  Jumat    5.0%      16.7%       0.6%     Hari kerja

  Sabtu    5.6%      18.5%       3.9%     *Weekend*

  Minggu   6.2%      12.5%       7.6%     *Weekend*
  ---------------------------------------------------

  : []{#_Toc223689812 .anchor}Tabel V.23 Pola Temporal Mingguan

![[]{#_Toc223586799 .anchor}Gambar V.3 Rata-rata *fillLevel* per Hari
dalam Seminggu](./media/media/image17.png){width="5.511805555555555in"
height="2.4458333333333333in"}

Rata-rata hari kerja (Senin-Jumat): 5.2% (Organik), 14.0% (Anorganik),
6.3% (Residu). Rata-rata *weekend* (Sabtu-Minggu): 5.9% (Organik), 15.6%
(Anorganik), 5.8% (Residu). Perbedaan antar hari kerja dan *weekend*
tidak signifikan karena *fillLevel* bersifat kumulatif. Nilai yang
tinggi pada hari tertentu dapat mencerminkan akumulasi dari hari-hari
sebelumnya sebelum terjadi pengosongan, bukan cerminan langsung
aktivitas pembuangan pada hari tersebut.

#### Pola Hari Libur

  -------------------------------------------------------------------
  Kategori Hari            Organik   Anorganik   Residu   Jumlah Hari
  ------------------------ --------- ----------- -------- -----------
  Hari kerja (Senin-Jumat) 5.1%      13.6%       6.9%     24 hari

  *Weekend* (Sabtu-Minggu) 5.9%      15.6%       5.8%     10 hari

  Hari libur nasional      5.5%      18.0%       3.5%     3 hari
  -------------------------------------------------------------------

  : []{#_Toc223689813 .anchor}Tabel V.24 Pola Hari Libur

![[]{#_Toc223586800 .anchor}Gambar V.4 Rata-rata *fillLevel* Berdasarkan
Kategori Hari](./media/media/image18.png){width="5.511805555555555in"
height="3.05625in"}

Hari libur nasional yang memiliki data dalam periode pengumpulan
meliputi 25-26 Desember 2025 (Natal) dan 1 Januari 2026 (Tahun Baru).
Tingginya rata-rata *fillLevel* Anorganik pada hari libur (18.0%)
merupakan efek akumulasi kumulatif. Tempat sampah yang tidak dikosongkan
saat libur membawa nilai *fillLevel* dari hari-hari sebelumnya, bukan
mencerminkan aktivitas pembuangan yang lebih tinggi.

#### Analisis Penambahan (Delta)

Analisis delta mengidentifikasi frekuensi dan waktu terjadinya
penambahan sampah.

  -----------------------------------------------------------------
  Jenis Perubahan                    Organik   Anorganik   Residu
  ---------------------------------- --------- ----------- --------
  Tidak ada perubahan (δ = 0)        95.5%     93.4%       94.2%

  Penambahan kecil (+10%)            2.4%      3.8%        3.1%

  Penambahan besar (+20% atau lebih) 0%        0.7%        0%

  Pengurangan / dikosongkan (δ \< 0) 2.1%      2.1%        2.7%
  -----------------------------------------------------------------

  : []{#_Toc223689814 .anchor}Tabel V.25 Analisis Delta *fillLevel*

  -----------------------------------------------------------------------
  Rentang Jam   Organik (S1) Anorganik (S2) Residu (S3) Total   \% dari
                                                                27
  ------------- ------------ -------------- ----------- ------- ---------
  07:00 - 09:00 2            2              1           5       18.5%

  09:00 - 12:00 1            2              3           6       22.2%

  12:00 - 14:00 0            3              2           5       18.5%

  14:00 - 17:00 3            4              1           8       29.6%

  17:00 - 19:00 1            2              0           3       11.1%

  19:00 - 07:00 0            0              0           0       0%

  Total         7            13             7           27      100%
  -----------------------------------------------------------------------

  : []{#_Toc223689815 .anchor}Tabel V.26 Delta *fillLevel* per Rentang
  Jam

![[]{#_Toc223586801 .anchor}Gambar V.5 Distribusi Kategori Delta dan
Delta per Rentang
Jam](./media/media/image19.png){width="5.511805555555555in"
height="1.8763888888888889in"}

Total 27 *event* penambahan terdeteksi selama periode observasi.
Penambahan terbanyak terjadi pada rentang 14:00-17:00 (29.6%), diikuti
09:00-12:00 (22.2%). Rentang 12:00-14:00 dan 07:00-09:00 masing-masing
berkontribusi 18.5%. Tidak ada penambahan yang terdeteksi pada malam
hari (19:00-07:00), konsisten dengan tidak adanya aktivitas kampus.

#### Pola Jenis Sampah

  -------------------------------------------------------------------------
  Aspek                    Organik        Anorganik (Kuning) Residu (Hitam)
                           (Hijau)                           
  ------------------------ -------------- ------------------ --------------
  Rata-rata *fillLevel*    5.3%           14.4%              6.4%

  Max *fillLevel* tercatat 20%            40%                20%

  Frekuensi penambahan     2.4%           4.5%               3.1%

  Jumlah *event*           7 *event*s     13 *event*s        7 *event*s
  penambahan                                                 

  Total delta positif      +70%           +150%              +70%

  Korelasi dengan hari     Tinggi         Sangat Tinggi      Tinggi
  kerja                                                      
  -------------------------------------------------------------------------

  : []{#_Toc223689816 .anchor}Tabel V.27 Pola Setiap Jenis Sampah

![[]{#_Toc223586802 .anchor}Gambar V.6 Perbandingan Pola Jenis
Sampah](./media/media/image20.png){width="5.511805555555555in"
height="1.8993055555555556in"}

Sampah Anorganik memiliki volume dan frekuensi penambahan tertinggi
(51.7% dari total delta). Organik dan Residu masing-masing berkontribusi
24.1%, berbeda dari estimasi sebelumnya yang meremehkan kontribusi
Residu karena kesalahan perhitungan delta. Hal ini sesuai dengan
karakteristik lokasi sebagai area perkantoran/laboratorium yang
menghasilkan lebih banyak sampah plastik, kertas, dan kemasan.

#### Estimasi Sampah per Pengguna

Berdasarkan data delta dan observasi lapangan, dilakukan estimasi volume
sampah yang dihasilkan per pengguna laboratorium. Labtek VIII Lantai 4
merupakan area laboratorium yang biasanya digunakan oleh 3-6 orang per
hari, dan dapat mencapai lebih dari 8 orang pada hari-hari tertentu.

Estimasi menggunakan pendekatan berbasis siklus: akumulasi delta positif
dalam setiap periode antar pengosongan dibagi dengan jumlah hari kerja
dalam periode tersebut, menghasilkan laju penambahan per siklus. Nilai
median dari seluruh siklus digunakan untuk mengurangi bias dari siklus
dengan periode sangat pendek yang menghasilkan laju tinggi.

  ------------------------------------------------------------------------
  Parameter                      Organik       Anorganik     Residu
  ------------------------------ ------------- ------------- -------------
  Dimensi tempat sampah (P×L×T)  40×60×100 cm  40×60×100 cm  40×60×100 cm

  Kapasitas geometris (100%)     240 liter     240 liter     240 liter

  Jumlah *event* penambahan      7 *event*s    13 *event*s   7 *event*s
  terdeteksi                                                 

  Total delta positif terdeteksi +70%          +150%         +70%

  Laju median per hari kerja     2.7%/hari     5.8%/hari     2.5%/hari
  (per siklus)                                               
  ------------------------------------------------------------------------

  : []{#_Toc223689817 .anchor}Tabel V.28 Perbandingan Jenis Tempat
  Sampah

Total 27 *event* penambahan terdeteksi dengan akumulasi +290%
*fillLevel* pada ketiga tempat sampah. Laju penambahan dihitung sebagai
median laju per siklus (delta siklus dibagi hari kerja dalam siklus).
Pendekatan median dipilih karena beberapa siklus dengan periode sangat
pendek (1-2 hari kerja) menghasilkan laju yang tidak representatif.

  -----------------------------------------------------------------------
  Parameter                              Nilai / Perhitungan
  -------------------------------------- --------------------------------
  Laju penambahan median gabungan (3     2.7% + 5.8% + 2.5% = 11.0%/hari
  sensor)                                kerja

  Volume geometris per hari kerja        11.0% x 240 L = 26.4 liter/hari

  Faktor profil kerucut                  1/3 = 0.33

  Volume aktual                          26.4 x 0.33 = 8.7 liter/hari

  Jumlah pengguna laboratorium           4-5 orang/hari

  Estimasi volume per orang per hari     8.7 / 4.5 = \~2 liter/orang/hari
  -----------------------------------------------------------------------

  : []{#_Toc223689818 .anchor}Tabel V.29 Perhitungan Estimasi Volume per
  Orang per Hari

Penjumlahan laju median per sensor dapat dilakukan secara langsung
karena ketiga tempat sampah memiliki kapasitas geometris yang sama (240
liter), sehingga 1% *fillLevel* merepresentasikan volume yang sama pada
setiap bin.

Jumlah pengguna laboratorium diestimasi sebesar 4-5 orang per hari
berdasarkan observasi peneliti selama periode pengumpulan data. Labtek
VIII Lantai 4 merupakan area laboratorium dengan akses terbatas yang
umumnya digunakan oleh mahasiswa peneliti dan asisten laboratorium,
bukan area publik dengan lalu lintas tinggi. Estimasi ini bersifat
perkiraan dan menjadi salah satu sumber ketidakpastian dalam perhitungan
volume per orang.

Faktor profil kerucut (1/3) digunakan sebagai pendekatan koreksi karena
sensor VL53L0X yang dipasang di titik tunggal mengukur puncak gundukan
sampah, bukan distribusi merata. Nilai 1/3 mengacu pada rumus volume
kerucut ideal (V = 1/3 x A x h), namun geometri sampah aktual tidak
selalu berbentuk kerucut sempurna, bisa lebih datar (mendekati 1/2) atau
lebih lancip (mendekati 1/4) tergantung jenis sampah. Oleh karena itu,
estimasi volume yang dihasilkan bersifat perkiraan dengan rentang
ketidakpastian yang perlu diakui sebagai keterbatasan penelitian.

#### Analisis Ketepatan Klasifikasi Sampah

Selain analisis volume, dilakukan juga observasi terhadap ketepatan
klasifikasi sampah oleh pengguna. Observasi visual dilakukan pada
beberapa waktu sampling untuk mengidentifikasi sampah yang dibuang pada
kategori yang tidak sesuai peruntukannya (lihat Lampiran C).

Berdasarkan dokumentasi foto yang tersedia, berikut temuan observasi
ketepatan klasifikasi.

  ------------------------------------------------------------------------
  Tempat Sampah   Temuan                            Validasi Lapangan
  --------------- --------------------------------- ----------------------
  Organik (Hijau) Ditemukan kantong plastik dan     Terdokumentasi foto
                  sisa bungkus makanan              (Lampiran C)

  Anorganik       Ditemukan beberapa sisa tisu      Terdokumentasi foto
  (Kuning)        basah yang seharusnya masuk ke    (Lampiran C)
                  residu                            

  Residu (Hitam)  Ditemukan sisa makanan dalam      Terdokumentasi foto
                  wadah dan tisu bekas              (Lampiran C)
  ------------------------------------------------------------------------

  : []{#_Toc223689819 .anchor}Tabel V.30 Kesesuaian Jenis Sampah

Temuan utama dari observasi ketepatan klasifikasi:

1.  Plastik di Tempat Sampah Organik

> Ditemukan plastik kemasan makanan di tempat sampah organik. Pengguna
> cenderung membuang kemasan makanan beserta sisa makanannya sekaligus
> karena dianggap satu kesatuan.

2.  Residu di Tempat Sampah Anorganik

> Ditemukan sampah yang seharusnya masuk kategori residu seperti tisu
> kotor dan styrofoam di tempat sampah anorganik, kemungkinan karena
> kurangnya pemahaman tentang definisi sampah residu.

3.  Campuran di Tempat Sampah Residu

> Tempat sampah residu ditemukan mengandung sisa makanan yang seharusnya
> masuk kategori organik. Hal ini mengindikasikan bahwa pengguna
> mengalami kebingungan dalam mengidentifikasi kategori residu, yang
> memang memiliki definisi paling tidak intuitif dibandingkan kategori
> organik dan anorganik.

Temuan ini menunjukkan perlunya sosialisasi berkala tentang jenis sampah
dan penyediaan infografis panduan singkat di dekat lokasi tempat sampah
untuk meningkatkan ketepatan klasifikasi oleh pengguna.

### Hasil Evaluasi Peningkatan Sistem (SE-04)

Skenario SE-04 mengevaluasi efektivitas peningkatan *firmware* yang
dilakukan terhadap perangkat *Smart Waste Bin* untuk menjawab RM-3.

#### Evaluasi Peningkatan *Firmware*

Peningkatan *firmware* dievaluasi berdasarkan efektivitasnya dalam
mengatasi masalah yang ditargetkan. Tabel V.31 menyajikan hasil evaluasi
untuk setiap peningkatan.

  -------------------------------------------------------------------------
  Peningkatan           Masalah yang        Hasil Evaluasi        Status
                        Diatasi                                   
  --------------------- ------------------- --------------------- ---------
  Perubahan Interval    Resolusi data       8-9 data points per   Efektif
  pengambilan data (8   terlalu rendah      hari per sensor, pola 
  jam menjadi 2,5 jam)  untuk analisis pola harian berhasil       
                        temporal            teridentifikasi       

  Median *filter* (5    *Noise* pada        fillLevel stabil      Efektif
  *readings*)           pembacaan sensor    tanpa lompatan acak   

  *Auto-recovery*       Sensor *hang*       Tidak ada kejadian    Efektif
  mechanism             menyebabkan *data   *hang* setelah        
                        loss*               implementasi          

  *Warm-up* *readings*  Pembacaan awal      Pembacaan pertama     Efektif
                        tidak stabil/*null* lebih konsisten       

  GPIO *isolation*      *Floating* *state*  Konsumsi daya tidak   Tidak
                        saat sleep          berubah signifikan    Efektif
  -------------------------------------------------------------------------

  : []{#_Toc223689820 .anchor}Tabel V.31 Hasil Evaluasi Peningkatan
  *Firmware*

Dari lima peningkatan *firmware* yang diimplementasikan, empat
peningkatan menunjukkan efektivitas dalam mengatasi masalah yang
ditargetkan. Perubahan Interval pengambilan data dari 8 jam menjadi 2,5
jam berhasil meningkatkan resolusi temporal dari \~3 menjadi 8 - 9 data
points per hari, yang menjadi fondasi keberhasilan analisis pola
pembuangan sampah pada SE-03. Median *filter* berhasil mereduksi *noise*
pada data pembacaan sensor selama periode pengujian. Mekanisme
*auto-recovery* terbukti efektif karena sebelum implementasi *firmware*
baru, sensor pernah mengalami kondisi *hang* dan tidak mengirim data
meskipun baterai masih dalam kondisi baik. Setelah *firmware* dengan
*auto-recovery* di-*upload*, tidak terjadi lagi kejadian sensor *hang*
selama periode pengujian. *Warm-up* *readings* menghasilkan pembacaan
awal yang lebih konsisten dengan membuang 3 pembacaan *dummy* setelah
inisialisasi.

Satu peningkatan yang tidak menunjukkan efektivitas adalah GPIO
*isolation*. Meskipun secara teori isolasi GPIO dapat mencegah
*floating* *state* yang menyebabkan konsumsi daya tidak perlu saat *deep
sleep*, hasil pengukuran menunjukkan konsumsi daya tidak berubah secara
signifikan sebelum dan sesudah implementasi. Hal ini kemungkinan
disebabkan karena konsumsi daya utama berasal dari komponen lain seperti
modul GSM SIM800L yang tidak terpengaruh oleh isolasi GPIO, serta ESP32
yang sudah memiliki mekanisme internal penanganan GPIO saat *deep
sleep*.

#### Dampak keseluruhan Peningkatan

Secara keseluruhan, peningkatan *firmware* memberikan dampak positif
terhadap kinerja sistem dalam empat aspek utama. Pertama, keandalan data
meningkat karena kombinasi median *filter* dan *warm-up* *readings*
menghasilkan pembacaan sensor yang lebih bersih dan konsisten, terbukti
dari tingkat validitas data sebesar 98,2% (vl53l0x_avail) dan 97,8%
(ina219_avail). Kedua, *maintenance* menjadi lebih mudah karena *field*
sleep dan *Reason* pada *payload* memungkinkan diagnosis jarak jauh
tanpa harus mengecek fisik perangkat. Ketiga, *data loss* diminimalkan
karena mekanisme *auto-recovery* mencegah sensor *hang* yang sebelumnya
memerlukan *reset* manual, berkontribusi pada total *data loss* yang
terjaga di bawah 10%.

Empat peningkatan yang terbukti efektif ini dapat direkomendasikan untuk
diadopsi pada perangkat *Smart Waste Bin*, khususnya untuk *deployment*
di lingkungan kampus atau area dengan karakteristik aktivitas yang
terkonsentrasi pada jam-jam tertentu.

## Pemenuhan Kebutuhan Sistem

Subbab ini menyajikan evaluasi pemenuhan kebutuhan fungsional dan
non-fungsional yang telah diidentifikasi pada Bab III. Evaluasi
dilakukan berdasarkan hasil pengujian yang telah disajikan pada subbab
V.2.

### Pemenuhan Kebutuhan Fungsional

Tabel V.32 menyajikan evaluasi pemenuhan kebutuhan fungsional
berdasarkan

  ---------------------------------------------------------------------------
  ID      Kebutuhan Fungsional Bukti Pemenuhan                    Status
  ------- -------------------- ---------------------------------- -----------
  KF-01   Pembacaan tingkat    Sensor VL53L0X membaca jarak dan   Terpenuhi
          kepenuhan tempat     mengkonversi ke *fillLevel* (Tabel 
          sampah               V.5)                               

  KF-02   Transmisi data       Data terkirim setiap \~2.5 jam via Terpenuhi
          otomatis secara      MQTT (Tabel V.14)                  
          periodik                                                

  KF-03   *Setiap* data        Setiap record memiliki field       Terpenuhi
          dilengkapi           timestamp (waktu pembacaan) dan    
          *Timestamp* dan      sensor_id (identifier perangkat)   
          *identifier* *waste  yang tercatat pada database (Tabel 
          bin*                 IV.19)                             

  KF-04   Konversi jarak ke    *Firmware* mengkonversi mm ke %    Terpenuhi
          persentase kepenuhan dengan rumus (Tabel V.5)           

  KF-05   Penyimpanan data ke  Data tersimpan di Supabase         Terpenuhi
          *database*           PostgreSQL (Tabel V.9)             

  KF-06   *Query* data         API mendukung *filter* sensorId    Terpenuhi
          berdasarkan *filter* dan *timerange* (Tabel V.10)       

  KF-07   Analisis pola        Pola harian, mingguan, dan libur   Terpenuhi
          temporal             teridentifikasi (Tabel V.17-V.19)  

  KF-08   Statistik deskriptif Mean, median, std dev dihitung per Terpenuhi
          data                 sensor (Tabel V.16)                

  KF-09   Visualisasi data     *Dashboard* menampilkan *chart*    Terpenuhi
          *dashboard*          dan status (Tabel V.11)            

  KF-10   Grafik pola temporal Line chart menampilkan tren        Terpenuhi
                               *fillLevel* (Tabel V.11)           
  ---------------------------------------------------------------------------

  : []{#_Toc223689821 .anchor}Tabel V.32 Pemenuhan Kebutuhan Fungsional

Seluruh kebutuhan fungsional (KF-01 sampai KF-10) berhasil dipenuhi oleh
sistem yang diimplementasikan.

### Pemenuhan Kebutuhan Nonfungsional

Tabel V.33 menyajikan evaluasi pemenuhan kebutuhan nonfungsional
berdasarkan hasil pengujian sistem.

  ----------------------------------------------------------------------------
  ID       Kebutuhan            Target    Aktual     Kategori      Status
           Nonfungsional                                           
  -------- -------------------- --------- ---------- ------------- -----------
  KNF-01   Waktu pembacaan      \< 1      \< 5 detik Performance   Terpenuhi
           sensor               menit                              

  KNF-02   Latensi transmisi    \< 10     \< 3 detik Performance   Terpenuhi
           data                 detik                              

  KNF-03   *Response* *time*    \< 3      \< 1 detik Performance   Terpenuhi
           *dashboard*          detik                              

  KNF-04   Waktu *query*        \< 5      \< 500 ms  Performance   Terpenuhi
           *database*           detik                              

  KNF-05   Up*time* sistem      \> 95%    90.7%      Reliability   Sebagian

  KNF-06   Konsistensi Interval ± 15      ± 12       Reliability   Terpenuhi
                                menit     menit\*                  

  KNF-07   Kelengkapan data     \> 90%    90.7%      Reliability   Terpenuhi

  KNF-08   Akurasi sensor       \< 10%    Sesuai     Accuracy      Terpenuhi
           *fillLevel*          error                              
  ----------------------------------------------------------------------------

  : []{#_Toc223689822 .anchor}Tabel V.33 Pemenuhan Kebutuhan
  Nonfungsional

\*Catatan: KNF-06 dihitung berdasarkan Sensor 1 dan 2 yang memenuhi
kriteria. Sensor 3 memiliki std dev 28 menit yang melebihi toleransi.

KNF-05 dan KNF-07 menggunakan metrik yang sama yaitu persentase data
berhasil terkumpul (90,7%). Perbedaan status terjadi karena *threshold*
yang berbeda. KNF-05 menargetkan 95% sehingga berstatus sebagian,
sedangkan KNF-07 menargetkan 90% sehingga berstatus terpenuhi.

Dari 8 kebutuhan non-fungsional, 7 kebutuhan berhasil dipenuhi
sepenuhnya dan 1 kebutuhan (KNF-05 *Uptime*) dipenuhi sebagian dengan
pencapaian 90.7% dari target 95%. Penyebab tidak tercapainya target
KNF-05 adalah faktor eksternal berupa *broker* MQTT vendor yang
dimatikan dan baterai bocor.

## Diskusi Hasil Evaluasi

Bagian ini membahas hasil evaluasi yang telah disajikan, memberikan
interpretasi terhadap temuan-temuan yang diperoleh, dan menganalisis
faktor-faktor yang mempengaruhi hasil penelitian.

### Analisis Konsumsi Daya pada Sensor 3

Sensor 3 (Residu) menunjukkan anomali berupa konsumsi arus hampir dua
kali lipat (210-235 mA) dibandingkan Sensor 1 dan 2 (110-140 mA),
meskipun ketiga unit menggunakan spesifikasi komponen yang identik dan
*firmware* yang sama. Anomali ini menyebabkan baterai Sensor 3 lebih
cepat habis dan mengakibatkan *data loss* yang lebih tinggi (23.6%)
dibandingkan sensor lainnya (\~2%).

Berbagai upaya optimasi *firmware* telah dilakukan untuk mengatasi
masalah ini, termasuk GPIO *isolation* dan optimasi urutan *shutdown*
komponen. Namun, konsumsi daya tetap tinggi, yang mengindikasikan bahwa
akar masalah bukan pada *software* melainkan pada *hardware*. Beberapa
hipotesis penyebab anomali ini adalah sebagai berikut.

Pertama, kemungkinan terdapat komponen pasif yang rusak atau tidak
terpasang dengan benar. Resistor *pull-up* atau *pull-down* yang tidak
tersolder dengan baik dapat menyebabkan arus bocor pada jalur sinyal.
Kapasitor decoupling yang rusak juga dapat menyebabkan konsumsi daya
tidak stabil. Kedua, kemungkinan terdapat *short* *circuit* ringan pada
PCB akibat solder bridge atau kontaminasi yang menyebabkan arus bocor
antar jalur. Ketiga, variasi karakteristik komponen aktif seperti modul
SIM800L atau regulator tegangan yang memiliki efisiensi lebih rendah
pada unit tersebut. Keempat, kemungkinan terdapat kerusakan pada jalur
*power* akibat proses *assembly* atau *handling* yang menyebabkan
resistansi tambahan dan disipasi daya.

Temuan ini menunjukkan pentingnya *quality control* dan *burn-in*
testing sebelum *deployment* perangkat IoT. Pengukuran konsumsi daya
setiap unit sebelum *deployment* dapat mengidentifikasi unit bermasalah
lebih awal. Untuk produksi massal, disarankan menetapkan batas toleransi
konsumsi daya dan melakukan *reject* pada unit yang melebihi batas
tersebut.

### Validitas Temuan

Untuk memastikan validitas pola yang teridentifikasi, dilakukan
triangulasi dengan observasi kontekstual lapangan berdasarkan
pengetahuan kondisi aktual lokasi penelitian dan dokumentasi foto
(Lampiran C), mengingat observasi lapangan dilakukan secara informal
tanpa pencatatan terstruktur. Berdasarkan hasil analisis pada Subbab
V.2.3, teridentifikasi empat pola utama pembuangan sampah. Tabel V.34
menyajikan validasi masing-masing pola terhadap kondisi aktual di
lapangan.

+----+-----------------+--------------------------+--------------------+
| No | Pola            | Evidensi Data            | Validasi Lapangan  |
|    | Teridentifikasi |                          |                    |
+====+=================+==========================+====================+
| 1  | *Peak hour*     | Delapan *event*          | Konsisten dengan   |
|    | pada pukul      | penambahan (delta        | jadwal aktivitas   |
|    | 14:00-17:00     | positif) terdeteksi pada | lab, warga lab     |
|    |                 | rentang 14:00-17:00,     | umumnya membuang   |
|    |                 | tertinggi dibandingkan   | sampah setelah     |
|    |                 | rentang waktu lainnya    | sesi kerja siang   |
|    |                 | (29,6% dari total 27     |                    |
|    |                 | *event*). (Tabel V.26)   |                    |
+----+-----------------+--------------------------+--------------------+
| 2  | Aktivitas       | Seluruh 27 event         | Dikonfirmasi, Lab  |
|    | pembuangan pada | penambahan (delta        | IoT tidak          |
|    | hari kerja      | positif) terjadi pada    | beroperasi di luar |
|    | lebih tinggi    | jam aktif kampus         | jam kerja dan      |
|    | dibandingkan    | 07:00-19:00 hari kerja,  | akses terbatas     |
|    | *weekend*       | tidak ada penambahan     |                    |
|    |                 | pada malam hari dan      |                    |
|    |                 | *weekend* (Tabel V.26)   |                    |
+----+-----------------+--------------------------+--------------------+
| 3  | Aktivitas       | Tidak ada *event*        | Dikonfirmasi,      |
|    | pembuangan      | penambahan (delta        | gedung tidak       |
|    | turun drastis   | positif) yang terdeteksi | beroperasi pada    |
|    | pada hari libur | pada hari libur.         | 25-26 Des dan 1    |
|    | nasional        | *fillLevel* tinggi pada  | Jan                |
|    |                 | Anorganik (18,0%)        |                    |
|    |                 | merupakan efek akumulasi |                    |
|    |                 | kumulatif karena tempat  |                    |
|    |                 | sampah tidak dikosongkan |                    |
|    |                 | (Tabel V.24)             |                    |
+----+-----------------+--------------------------+--------------------+
| 4  | Dominasi sampah | Anorganik menyumbang     | Konsisten dengan   |
|    | anorganik       | +150% delta positif dari | observasi,         |
|    | (51,7% dari     |                          | pengguna lab       |
|    | total volume)   | total +290%, setara      | menghasilkan       |
|    |                 | 51,7% dari total *event* | kemasan minuman    |
|    |                 | penambahan (13 dari 27   | dan makanan lebih  |
|    |                 | *event*) dengan          | banyak dari sampah |
|    |                 | frekuensi penambahan     | organik            |
|    |                 | tertinggi 4,5% (Tabel    |                    |
|    |                 | V.27 dan Tabel V.30)     |                    |
+----+-----------------+--------------------------+--------------------+

: []{#_Toc223689823 .anchor}Tabel V.34 Validasi Pola dengan Observasi
Lapangan

Seluruh pola utama tervalidasi melalui observasi yang meningkatkan
*confidence* bahwa pola-pola yang teridentifikasi mencerminkan kondisi
aktual, bukan artefak dari keterbatasan sensor atau *noise* data.

### Implikasi Praktis Pengelolaan Sampah

Temuan penelitian ini memiliki beberapa implikasi praktis untuk
pengelolaan sampah di lingkungan kampus:

1.  Berdasarkan pola, jadwal pengosongan dapat difokuskan pada sore hari
    kerja (setelah jam makan siang), bukan pagi atau *weekend*.

2.  Dominasi sampah anorganik (51,7%) menunjukkan potensi program
    *reduce* kemasan sekali pakai atau penyediaan fasilitas *refill*.

3.  Empat dari lima peningkatan yang telah diuji dapat diterapkan untuk
    penyesuaian perangkat *Smart Waste Bin* di lingkungan dengan
    aktivitas terkonsentrasi pada jam tertentu.

4.  Sistem *Smart Waste Bin* memberikan data objektif untuk pengambilan
    keputusan, menggantikan estimasi manual yang subjektif.

#  KESIMPULAN DAN SARAN

Bab ini berisi uraian komprehensif yang merangkum temuan-temuan utama
dari hasil perancangan, implementasi, dan pengujian sistem *Smart Waste
Bin*. Selain itu, bab ini juga menguraikan sejumlah rekomendasi praktis
dan akademis yang diharapkan dapat menjadi acuan bagi pengembangan
penelitian maupun penyempurnaan perangkat di masa mendatang.

## Kesimpulan

Penelitian ini telah berhasil mengembangkan dan mengimplementasikan
sistem *Smart Waste Bin* berbasis *Internet of Things* (IoT) untuk
keperluan otomatisasi pengumpulan data dan analisis pola pembuangan
sampah di Gedung Labtek VIII Institut Teknologi Bandung (ITB), khususnya
pada Lab *Internet of Things* Lantai 4. Selama periode observasi yang
berlangsung selama 37 hari, sistem terbukti mampu beroperasi dan
berhasil mengumpulkan 805 *records* data dari tiga unit perangkat sensor
dengan tingkat keberhasilan pengiriman mencapai 90,7%. Berdasarkan hasil
evaluasi menyeluruh yang telah dipaparkan pada Bab V, seluruh rumusan
masalah dalam penelitian ini telah berhasil dijawab dengan rincian
sebagai berikut:

1.  **Rancangan dan Implementasi Sistem (Menjawab RM-1)**

> Penelitian ini berhasil merancang sistem *Smart Waste Bin*
> terintegrasi dengan arsitektur IoT 4-*layer*. Arsitektur ini mencakup
> *Perception Layer* (ESP32, VL53L0X, INA219, SIM800L) untuk akuisisi
> data fisik, *Network Layer* (MQTT) untuk transmisi nirkabel,
> *Middleware Layer* (Node-RED) untuk pemrosesan aliran data, dan
> *Application Layer* (Supabase, Next.js) untuk penyimpanan dan
> visualisasi antarmuka. Seluruh komponen terbukti berfungsi sesuai
> dengan desain, di mana 10 kebutuhan fungsional dan 7 dari 8 kebutuhan
> nonfungsional telah terpenuhi dengan baik.

2.  **Identifikasi Pola Pembuangan Sampah (Menjawab RM-2)**

> Melalui analisis data historis dan analisis delta (perubahan antar
> pembacaan), sistem berhasil mengidentifikasi empat pola temporal
> pembuangan sampah di lingkungan kampus yang telah divalidasi melalui
> observasi lapangan (Tabel V.34), yaitu:

- Terjadinya peak hour (jam sibuk) secara konsisten pada pukul
  14:00-17:00, ditunjukkan oleh 8 event penambahan (delta positif) pada
  rentang waktu tersebut atau 29,6% dari total 27 event yang terdeteksi.
  Pola ini konsisten dengan perilaku membuang sampah setelah aktivitas
  makan siang.

- Seluruh event penambahan sampah (delta positif) terjadi pada jam aktif
  hari kerja (07:00-19:00), sedangkan tidak terdeteksi adanya penambahan
  pada malam hari maupun akhir pekan (weekend). Dari total 27 event
  penambahan yang terdeteksi selama periode observasi, tidak ada satupun
  yang terjadi pada rentang 19:00-07:00 maupun pada hari Sabtu dan
  Minggu.

- Aktivitas pembuangan sampah turun drastis pada hari libur nasional, di
  mana tidak terdeteksi adanya event penambahan (delta positif) pada
  tanggal 25-26 Desember 2025 dan 1 Januari 2026. Nilai fillLevel yang
  tercatat pada hari libur merupakan efek akumulasi kumulatif karena
  tempat sampah tidak dikosongkan oleh petugas.

- Adanya dominasi sampah anorganik yang menyumbang 13 dari 27 event
  penambahan (48,1%) dengan total delta positif +150% dari akumulasi
  keseluruhan, konsisten dengan karakteristik lokasi sebagai area
  laboratorium yang menghasilkan banyak sampah kemasan sekali pakai.

3.  **Peningkatan *Firmware* *Smart Waste Bin*** **(Menjawab RM-3)**

> Perangkat bawaan dari pihak ketiga telah berhasil dioptimasi melalui
> lima peningkatan *firmware* agar sesuai dengan kebutuhan lingkungan
> kampus. Peningkatan tersebut meliputi perubahan Interval pengambilan
> data, implementasi median *filter*, mekanisme *auto-recovery*,
> *warm-up* *readings*, dan GPIO *isolation*. Empat dari lima
> peningkatan terbukti efektif dalam mengatasi masalah yang ditargetkan,
> sedangkan GPIO *isolation* tidak menunjukkan perubahan signifikan pada
> konsumsi daya karena sumber konsumsi utama berasal dari modul GSM yang
> tidak terpengaruh oleh kondisi GPIO. Peningkatan yang terbukti efektif
> ini dapat direkomendasikan untuk diadopsi pada produk *Smart waste
> bin* standar vendor, khususnya untuk *deployment* di lingkungan dengan
> karakteristik aktivitas yang terkonsentrasi pada jam-jam tertentu.

## Saran

Untuk penelitian selanjutnya, disarankan menggunakan tempat sampah
berukuran lebih kecil agar resolusi pengukuran *fillLevel* lebih tinggi
dari kelipatan 10% saat ini. Periode pengumpulan data juga perlu
diperpanjang minimal satu semester untuk mendapatkan pola yang lebih
representatif dan memvalidasi pola mingguan dengan *confidence* lebih
tinggi. Selain itu, penambahan sensor *multi-point* dapat
dipertimbangkan untuk mendeteksi sampah di pinggir tempat sampah yang
saat ini tidak terdeteksi dengan sensor *single-point*. Program
sosialisasi pemilahan sampah juga dapat dikombinasikan dengan
*deployment* sistem untuk mengurangi tingkat kesalahan klasifikasi
berdasarkan observasi.

Untuk penyedia teknologi perangkat *Smart Waste Bin*, investigasi
terhadap kebocoran daya perlu dilakukan mengingat ditemukan variasi
konsumsi arus hampir dua kali lipat antar unit dengan spesifikasi
identik. Peningkatan *firmware* yang dikembangkan dalam penelitian ini
dapat diadopsi ke produk standar untuk meningkatkan keandalan sistem.
Terakhir, dokumentasi teknis perlu dilengkapi dengan skema rangkaian dan
*source* *code* *firmware* agar mempermudah proses pemeliharaan
(*maintenance*) dan *troubleshooting*.

DAFTAR PUSTAKA

Al-Fuqaha, Ala, Mohsen Guizani, Mehdi Mohammadi, Mohammed Aledhari, dan
Moussa Ayyash. 2015. "*Internet of Things*: A Survey on Enabling
Technologies, Protocols, and Applications." *IEEE Communications Surveys
& Tutorials* 17 (4). https://doi.org/10.1109/COMST.2015.2444095.

Atzori, Luigi, Antonio Iera, dan Giacomo Morabito. 2010. "The *Internet
of Things*: A survey." *Computer Networks* 54 (15).
https://doi.org/10.1016/j.comnet.2010.05.010.

Bahçelioğlu, Ecem, E. Selin Buğdaycı, Nazlı B. Doğan, Naz Şimşek, Sinan
Ö. Kaya, dan Emre Alp. 2020. "Integrated solid *waste* *management*
strategy of a large campus: A comprehensive study on METU campus,
Turkey." *Journal of Cleaner Production* 265 (Agustus).
https://doi.org/10.1016/j.jclepro.2020.121715.

European Commission. 2008. "*Waste* Framework Directive 2008/98/EC ."
*Official Journal of the European Union 312*.

Gayatri S. 2024. "\"Smart *Waste* *Management* Systems Using IoT:
Revolutionize *Waste* Collection." Bridgera.
https://bridgera.com/IoT-based-smart-*waste*-*management*-system/.

Gayatri S. 2025. "IoT *Waste* *Management*: Revolutionizing *Waste*
*Handling* with IoT Solutions." Bridgera.
https://bridgera.com/IoT-*waste*-*management*-renewing-the-face-of-*waste*/.

Geissdoerfer, Martin, Paulo Savaget, Nancy M.P. Bocken, dan Erik Jan
Hultink. 2017. "The Circular Economy - A new sustainability paradigm?"
*Journal of Cleaner Production* 143 (Februari).
https://doi.org/10.1016/J.JCLEPRO.2016.12.048.

Giurea, Ramona, Marco Carnevale Miino, Vincenzo Torretta, dan Elena
Cristina Rada. 2024. "Approaching sustainability and circularity along
*waste* *management* systems in universities: an overview and proposal
of good practices." *Frontiers in Environmental Science* 12 (Maret).
https://doi.org/10.3389/fenvs.2024.1363024.

International Telecommunication Union. 2012. "Overview of the *Internet
of Things*." *ITU-T Y.2060*.

*Internet of Things* European Research Cluster. 2014. IoT *Semantic
Interoperability: Research Challenges, Best Practices, Recommendations
and Next Steps*.

Kaza, Silpa, Lisa C. Yao, Perinaz Bhada-Tata, dan Frank Van Woerden.
2018. *What a Waste 2.0: A Global Snapshot of Solid Waste Management to
2050*. Dalam *What a Waste 2.0: A Global Snapshot of Solid Waste
Management to 2050*. https://doi.org/10.1596/978-1-4648-1329-0.

Kevin Ashton. 2009. "That '*Internet of Things*' Thing." *RFID Journal*.

Pires, Luis Miguel, João Figueiredo, Ricardo Martins, dan José Martins.
2025. "IoT-Enabled Real-*Time* *Monitoring* of Urban Garbage Levels
Using *Time*-of-Flight Sensing Technology." *Sensors* 25 (7).
https://doi.org/10.3390/s25072152.

RoadRunner. 2024. "How Colleges and Universities Can Overcome 3 *Waste*
Challenges."
https://www.roadrunnerwm.com/blog/how-colleges-and-universities-can-overcome-3-*waste*-challenges.

Rodríguez-Guerreiro, María-Jesús, Verónica Torrijos, dan Manuel Soto.
2024. "A Review of *Waste* *Management* in Higher Education
Institutions: The Road to Zero *Waste* and Sustainability."
*Environments* 11 (12). https://doi.org/10.3390/environments11120293.

Sensoneo. 2024. "5 Strategies to Transform *Waste* *Management* on
Campuses."
https://sensoneo.com/*waste*-*library*/*waste*-*management*-campus/.

Sethi, Pallavi, dan Smruti R. Sarangi. 2017. "*Internet of Things*:
Architectures, Protocols, and Applications." *Journal of Electrical and
Computer Engineering* 2017. https://doi.org/10.1155/2017/9324035.

United Nations. 2015. "Transforming our world: the 2030 Agenda for
Sustainable Development." https://sdgs.un.org/2030agenda. 

####### LAMPIRAN A TAUTAN PENTING

  ----------------------------------------------------------------------------------------------
  No   Tautan                                             Deskripsi
  ---- -------------------------------------------------- --------------------------------------
  1    https://github.com/Mipol2/TA-Node-RED              Repositori Node-RED

  2    https://github.com/Mipol2/TA-Firmware-ESP32        Repositori *Firmware* ESP32

  3    https://github.com/Mipol2/TA-Dasboard              Repositori *Dashboard*

  4    https://github.com/Mipol2/TA-Data-Cleaner-Visual   Repositori *Dataset* Pengukuran Sampah
                                                          serta *Data Cleaner* dan *Data
                                                          Visualization*

  5    https://dashboard-ta-mef7.vercel.app/              *Smart Waste Bin* IoT Dashboard yang
                                                          telah di-*deploy*
  ----------------------------------------------------------------------------------------------

####### LAMPIRAN B ANTAR MUKA DASHBOARD

![](./media/media/image21.png){width="4.500755686789152in"
height="7.75152668416448in"}

B.1 *Header Section*

![](./media/media/image22.png){width="5.495833333333334in"
height="0.48680555555555555in"}

B.2 *Sensor Status Cards*

![](./media/media/image23.png){width="5.504166666666666in"
height="1.1131944444444444in"}

B.3 *Control Panel*

![](./media/media/image24.png){width="5.495833333333334in"
height="0.5215277777777778in"}

B.4 Visualisasi Data

![](./media/media/image25.png){width="5.495833333333334in"
height="3.5131944444444443in"}

B.5 *Recent Sensor Readings*

![](./media/media/image26.png){width="5.511805555555555in"
height="3.112410323709536in"}

B.6 *System Analytics*

![](./media/media/image27.png){width="5.511805555555555in"
height="1.5385017497812774in"}

####### LAMPIRAN C BUKTI KESALAHAN PEMILAHAN SAMPAH OLEH PENGGUNA

**C.1 Sampah Anorganik Dibuang ke Tempat Sampah Organik**

![](./media/media/image28.png){width="5.511805555555555in"
height="4.914583333333334in"}

![](./media/media/image29.png){width="5.511805555555555in"
height="4.54375in"}

**C.2 Sampah Residu Dibuang ke Tempat Sampah Anorganik**

![](./media/media/image30.png){width="3.795793963254593in"
height="3.002392825896763in"}

**C.3 Sampah Organik Dibuang ke Tempat Sampah Residu**

![](./media/media/image31.png){width="4.3964468503937in"
height="5.1361329833770775in"}

####### LAMPIRAN D PEMASANGAN TEMPAT SAMPAH

**D.1 Pemasangan Roda Tempat Sampah**

![](./media/media/image32.png){width="4.718160542432196in"
height="5.332666229221347in"}

**D.2 Pemasangan Baterai Perangkat IoT**

![](./media/media/image33.png){width="2.9900010936132984in"
height="2.6462029746281717in"}

**D.3 Pemasangan Perangkat IoT pada Tempat Sampah**

![](./media/media/image34.png){width="2.8962379702537184in"
height="3.2817082239720037in"}

![](./media/media/image35.png){width="2.344076990376203in"
height="2.437840113735783in"}

**D.4 Pemasangan Label Tempat Sampah**

![](./media/media/image36.png){width="4.570333552055993in"
height="3.247659667541557in"}

![](./media/media/image37.png){width="4.542580927384077in"
height="3.735596019247594in"}

![](./media/media/image38.png){width="4.512397200349956in"
height="3.296887576552931in"}
