# Analisis Non-Performing Invoice (NPI) Iuran Pemeliharaan Lingkungan (IPL) – Sinarmas Land

## Project Overview

Proyek ini merupakan capstone project Data Analyst yang berfokus pada analisis performa pembayaran Iuran Pemeliharaan Lingkungan (IPL) pada kawasan township yang dikelola oleh Sinarmas Land.

Analisis dilakukan untuk mengidentifikasi faktor-faktor yang berkontribusi terhadap tingginya Non-Performing Invoice (NPI), mengukur potensi pendapatan yang masih tertahan akibat tunggakan, serta mengevaluasi kualitas data yang digunakan dalam proses billing, payment, dan collection.

Proyek ini menggunakan Python (Pandas, NumPy, Matplotlib, dan Seaborn) untuk proses data preparation, data cleaning, dan exploratory data analysis. Tableau digunakan sebagai sarana visualisasi dan penyajian hasil analisis dalam bentuk dashboard.

## Background

Sinarmas Land mengembangkan sejumlah kawasan township berskala besar di Jabodetabek, seperti BSD City, Grand Wisata, Kota Wisata, Deltamas, dan NavaPark.

Salah satu sumber pendapatan berulang dari pengelolaan kawasan tersebut berasal dari Iuran Pemeliharaan Lingkungan (IPL) yang dibayarkan secara rutin oleh pemilik unit. Pendapatan IPL digunakan untuk mendukung kebutuhan operasional kawasan, termasuk keamanan, kebersihan, dan pemeliharaan fasilitas umum.

Namun, tingginya Non-Performing Invoice (NPI) atau tagihan yang belum dibayarkan berpotensi mengganggu arus kas operasional Estate Management. Selain itu, terdapat beberapa tantangan operasional terkait karakteristik unit yang tidak dihuni, pencatatan metode pembayaran, kelengkapan data kontak pemilik, serta akurasi pencatatan penggunaan air.

Oleh karena itu, diperlukan analisis terhadap data billing dan karakteristik unit untuk memahami sumber permasalahan serta merumuskan rekomendasi yang dapat membantu meningkatkan performa penerimaan IPL.

## Problem Statement

Tim Township Management menghadapi tingkat NPI yang cukup tinggi pada portofolio unit yang dikelola. Kondisi ini berpotensi membebani cashflow operasional kawasan dan meningkatkan ketergantungan terhadap dukungan anggaran dari developer untuk memenuhi kebutuhan pemeliharaan kawasan.

Beberapa permasalahan yang menjadi fokus investigasi:

1. Tingginya proporsi invoice dengan status Unpaid dan Overdue.
2. Belum diketahui secara mendalam karakteristik unit dan pemilik yang berkontribusi terhadap tunggakan IPL.
3. Variasi pencatatan payment method menyulitkan proses rekonsiliasi oleh tim Finance.
4. Ketidaklengkapan informasi kontak pemilik berpotensi menghambat aktivitas penagihan.
5. Terdapat indikasi anomali dalam pencatatan penggunaan air dan proses penerbitan tagihan.

## Project Objectives

Analisis ini memiliki empat tujuan utama:

1. **Identifikasi Segmen Tunggakan:** Mengidentifikasi karakteristik dan segmen unit maupun kawasan yang paling berkontribusi terhadap tunggakan IPL sebagai dasar prioritas aktivitas Collection.
2. **Estimasi Financial Exposure:** Mengestimasi potensi pendapatan yang tertahan akibat tunggakan sebagai bahan pertimbangan perencanaan cashflow Estate Management.
3. **Standardisasi Payment Method:** Merumuskan rekomendasi standardisasi pencatatan metode pembayaran untuk mempermudah proses rekonsiliasi Finance.
4. **Evaluasi Data Quality:** Mengevaluasi kelengkapan, konsistensi, dan indikasi kesalahan pencatatan data billing sebagai dasar rekomendasi perbaikan sistem kepada tim IT/ERP.

## Dataset Overview

Proyek ini menggunakan lima dataset utama yang memiliki hubungan satu sama lain.
Dataset yang digunakan dapat diakses dari url berikut: https://drive.google.com/drive/folders/1BdjYFJAwWalQORejl2M8ahOBR7avI7Oj?usp=sharing

| Dataset | Deskripsi |
|---|---|
| `sml_clusters.csv` | Informasi kawasan dan karakteristik cluster/township. |
| `sml_units.csv` | Informasi unit, karakteristik pemilik, status hunian, dan kontak pemilik. |
| `sml_ipl_billings.csv` | Data transaksi tagihan IPL dan air, termasuk status pembayaran. |
| `sml_collection_actions.csv` | Riwayat aktivitas penagihan dan respons pemilik unit. |
| `sml_payment_disputes.csv` | Informasi pengajuan sengketa dan hasil penyelesaian tagihan. |

### Periode Data

Data transaksi billing mencakup periode **Juli 2022 hingga Desember 2024**.

## Project Structure

```text
SML-IPL-Analysis/
│
├── data/
│   └── cleaned/
│       ├── cleaned_sml_clusters.csv
│       ├── cleaned_sml_units.csv
│       ├── cleaned_sml_ipl_billings.csv
│       ├── cleaned_sml_collection_actions.csv
│       └── cleaned_sml_payment_disputes.csv
│
├── notebooks/
│   ├── Data_Understanding_and_Cleaning_Annotated.ipynb
│   ├── 2.0-EDA_SML_IPL_Annotated.ipynb
│   └── 3.0-InDepth_Analysis_SML_IPL_Final.ipynb
│
├── dashboard/
│   └── Tableau Dashboard
│
├── presentation/
│   └── SML_IPL_Analysis_Presentation.pptx
│
└── README.md
```

## Analysis Workflow

### 1. Data Understanding & Cleaning

Tahap awal dilakukan untuk memahami struktur dataset, memeriksa kualitas data, dan memastikan konsistensi antar tabel sebelum analisis lebih lanjut.

Beberapa proses yang dilakukan:

- Memeriksa struktur, tipe data, missing values, dan duplikasi.
- Memeriksa konsistensi hubungan antar tabel berdasarkan key yang tersedia.
- Mengidentifikasi indikasi duplicate billing berdasarkan kombinasi `unit_id` dan `billing_month`.
- Menentukan status invoice `Valid` dan `Invalid` untuk mencegah penggandaan nominal dalam agregasi.
- Menangani anomali penggunaan air negatif dan menghitung ulang `updated_total_amount`.
- Mengidentifikasi potensi kurang bayar pada invoice yang sudah berstatus Paid.
- Menstandarisasi kategori payment method.
- Mengklasifikasikan penggunaan air berdasarkan distribusi data.

Seluruh tahapan ini bertujuan menghasilkan dataset yang lebih konsisten dan dapat digunakan untuk analisis bisnis.

### 2. Exploratory Data Analysis (EDA)

Tahap EDA dilakukan untuk memahami karakteristik dan pola dasar dari masing-masing dataset.

Analisis mencakup:

- Distribusi status pembayaran dan metode pembayaran.
- Distribusi nilai tagihan dan penggunaan air.
- Tren NPI berdasarkan periode bulanan dan kuartalan.
- Perbandingan performa pembayaran antar township.
- Eksplorasi karakteristik unit dan pemilik.
- Distribusi aktivitas Collection dan Payment Disputes.

### 3. In-Depth Analysis

Tahap ini berfokus pada investigasi yang secara langsung menjawab tujuan dan pertanyaan bisnis dalam brief.

Pembahasan utama meliputi:

**A. NPI Performance & Financial Exposure**
- Mengukur NPI rate dan non-performing amount.
- Membandingkan performa pembayaran berdasarkan township dan cluster.
- Mengidentifikasi kawasan yang memberikan kontribusi terbesar terhadap tunggakan IPL.

**B. Customer & Unit Payment Characteristics**
- Membandingkan riwayat pembayaran berdasarkan status vacant.
- Menganalisis perbedaan pembayaran berdasarkan domisili pemilik.
- Mengevaluasi hubungan autodebit dan status verifikasi kontak dengan performa pembayaran.

**C. Collection & Payment Disputes**
- Membandingkan respons pemilik berdasarkan jenis aktivitas penagihan.
- Mengidentifikasi jenis sengketa yang paling sering diajukan.
- Mengevaluasi proporsi sengketa yang berujung pada pembatalan atau penolakan tagihan.

**D. Water Usage & Billing Accuracy**
- Mengidentifikasi pola penggunaan air.
- Mengevaluasi penggunaan air berdasarkan metode pencatatan manual dan otomatis.
- Mengidentifikasi potensi kelemahan pada proses pencatatan dan validasi tagihan.

## Key Performance Indicators (KPIs)

Beberapa indikator utama yang digunakan dalam analisis:

| KPI | Definisi |
|---|---|
| NPI Rate | Jumlah invoice Unpaid dan Overdue dibagi total invoice Valid. |
| Performing Amount | Total `total_amount` dari invoice Paid dan Valid. |
| Non-Performing Amount | Total `updated_total_amount` dari invoice Unpaid dan Overdue, ditambah `kurang_bayar` dari invoice Paid yang Valid. |
| Total Expected IPL Amount | Total `updated_total_amount` dari seluruh invoice Valid. |

### Perhitungan NPI Rate

\[
NPI\ Rate =
\frac{\text{Jumlah Invoice Unpaid + Overdue (Valid)}}
{\text{Total Invoice Valid}}
\times 100\%
\]

Dalam seluruh perhitungan KPI, hanya invoice dengan `invoice_validity = Valid` yang digunakan.

## Key Findings

Beberapa temuan utama dari hasil analisis:

- NPI rate keseluruhan tercatat sebesar **35,44%**, menunjukkan bahwa lebih dari sepertiga invoice valid masih berstatus Unpaid atau Overdue.
- NPI rate menunjukkan peningkatan hingga **37,07% pada Q4 2024**, sehingga perlu mendapat perhatian dalam perencanaan penerimaan IPL.
- Unit vacant memiliki NPI rate lebih tinggi dibandingkan unit non-vacant.
- Pemilik unit yang berdomisili di luar kota dan luar negeri menunjukkan tingkat NPI yang relatif lebih tinggi dibandingkan pemilik yang berdomisili dalam kota.
- Unit yang terdaftar autodebit menunjukkan NPI rate lebih rendah dibandingkan unit yang tidak terdaftar autodebit.
- Sebagian besar respons dalam riwayat Collection masih berupa Tidak Respon, sehingga efektivitas pendekatan penagihan perlu dievaluasi.
- Analisis Payment Disputes menunjukkan adanya sejumlah pengajuan sengketa yang berujung pada pembatalan tagihan, sehingga validasi billing perlu diperkuat.

*Catatan: Temuan tersebut merupakan hasil analisis atas dataset yang tersedia dan menunjukkan pola atau hubungan statistik, bukan bukti hubungan sebab-akibat.*

## Business Recommendations

Berdasarkan hasil analisis, beberapa rekomendasi yang dapat dipertimbangkan:

1. **Collection Prioritization:** Memprioritaskan township, cluster, dan karakteristik unit yang memiliki kontribusi non-performing amount terbesar.
2. **Customer Engagement:** Memperkuat pendekatan kepada pemilik unit vacant dan pemilik yang berdomisili jauh dari kawasan, termasuk melalui pembaruan informasi kontak.
3. **Autodebit Adoption:** Mendorong penggunaan autodebit sebagai alternatif pembayaran untuk membantu meningkatkan konsistensi penerimaan IPL.
4. **Payment Standardization:** Menerapkan master data dan standardisasi kategori payment method untuk mempermudah rekonsiliasi Finance.
5. **Billing Validation:** Memperkuat validasi otomatis atas pencatatan penggunaan air, khususnya nilai negatif dan lonjakan penggunaan yang tidak biasa.
6. **Meter Reading Improvement:** Meningkatkan prosedur verifikasi pencatatan meteran air manual serta mengevaluasi perluasan penggunaan pencatatan otomatis.
7. **System & Data Quality Improvement:** Melengkapi informasi tanggal penerbitan invoice, meningkatkan kelengkapan data kontak pemilik, dan memperkuat mekanisme deteksi duplicate billing.
8. **Dispute Monitoring:** Meningkatkan monitoring penyelesaian sengketa dan melakukan evaluasi terhadap alasan sengketa yang sering berujung pada koreksi atau pembatalan tagihan.

## Tools & Technologies

| Kategori | Tools |
|---|---|
| Programming Language | Python |
| Data Processing | Pandas, NumPy |
| Data Visualization | Matplotlib, Seaborn |
| Notebook Environment | Jupyter Notebook |
| Business Intelligence | Tableau |
| Documentation & Presentation | PowerPoint, GitHub |

## Project Deliverables

- **Data Understanding & Cleaning:** Notebook proses pemeriksaan dan pembersihan data.
- **Exploratory Data Analysis:** Notebook eksplorasi karakteristik dan pola data.
- **In-Depth Analysis:** Notebook investigasi untuk menjawab tujuan bisnis dan menghasilkan rekomendasi.
- **Tableau Dashboard:** Rancangan dashboard untuk memantau performa pembayaran dan eksposur NPI.
- **Final Presentation:** Ringkasan hasil analisis, insight, dan rekomendasi bisnis.

## Limitations

Beberapa keterbatasan yang perlu diperhatikan dalam menginterpretasikan hasil analisis:

- Dataset hanya mencakup periode Juli 2022 hingga Desember 2024, sehingga belum menggambarkan kondisi pembayaran terkini.
- Data riwayat Collection belum menyediakan histori perubahan status invoice secara lengkap setelah tindakan penagihan dilakukan.
- Belum tersedia informasi tanggal penerbitan invoice, sehingga validasi urutan waktu penerbitan dan pembayaran belum dapat dilakukan secara menyeluruh.
- Klasifikasi penggunaan air berdasarkan P99 merupakan pendekatan statistik untuk mendeteksi nilai ekstrem, bukan standar resmi konsumsi air.
- Hubungan antara karakteristik unit dan performa pembayaran tidak selalu menunjukkan hubungan sebab-akibat.

---

**Project Focus:** Meningkatkan transparansi performa penerimaan IPL, mengidentifikasi sumber risiko tunggakan, dan memberikan rekomendasi berbasis data untuk mendukung pengelolaan cashflow Estate Management Sinarmas Land.
