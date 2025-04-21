# Python-Data-Analytics-Customer-loyality

# Laporan Proyek Data Analytics - Cara Florist

## Domain Proyek

Proyek ini bertujuan untuk melakukan analisis peringkat pelanggan berdasarkan total pembelian tertinggi di Cara Florist. Tujuannya adalah untuk mengidentifikasi pelanggan-pelanggan paling loyal atau dengan nilai transaksi tertinggi agar dapat menjadi target utama dalam kampanye promosi, khususnya dalam rangka Anniversary (ulang tahun) Cara Florist.

---

## Mengapa Masalah Ini Harus Diselesaikan

- Cara Florist ingin membangun relasi yang lebih dekat dengan pelanggan paling aktif.
- Menyusun strategi kampanye loyalitas pelanggan secara tepat sasaran membutuhkan data pelanggan yang valid dan terstruktur.
- Data transaksi yang tersedia sebelumnya tidak tersusun dalam format database standar, sehingga menyulitkan proses analisis dan visualisasi.

---

## Business Understanding

### Problem Statements

1. Bagaimana cara mengolah data transaksi pelanggan yang tidak terstruktur menjadi bentuk yang bersih dan dapat dianalisis?
2. Siapa saja pelanggan yang memiliki total pembelian tertinggi selama periode tertentu?
3. Bagaimana hasil peringkat pelanggan dapat digunakan untuk kampanye bisnis?

### Goals

- Membersihkan dan menyusun ulang data transaksi pelanggan agar dapat diproses menggunakan Python/pandas.
- Menghitung total pembelian untuk setiap pelanggan berdasarkan data transaksi historis.
- Menghasilkan daftar peringkat pelanggan berdasarkan jumlah pembelian terbanyak.

### Solution Statements

- Menggunakan pustaka Python `pandas` untuk melakukan data wrangling dan agregasi data transaksi.
- Melakukan grup data berdasarkan nama pelanggan dan menjumlahkan nilai pembelian (unit price) untuk setiap pelanggan.
- Menyortir data dari pembelian tertinggi ke terendah untuk menghasilkan peringkat pelanggan yang valid.

---

## Data Understanding

### Bentuk Data Asli

Data transaksi pelanggan yang diberikan memiliki format yang tidak standar, contohnya:

| Customer / Date         | Transaction   | No    | Product                       | Qty | Unit | Unit Price | Amount | Total        |
|-------------------------|---------------|-------|-------------------------------|-----|------|-------------|--------|--------------|
| A Radityo Whisnu        | NaN           | NaN   | NaN                           | ... | ...  | ...         | ...    | ...          |
| 27/12/2023              | Sales Invoice | 50416 | Medium Bouquet                | 1.0 | Pcs  | 435000.0    | 435000 | 435000.0     |
| 27/12/2023              | Sales Invoice | 50416 | KL of Frame Rose Gold White  | 3.0 | Pcs  | 10000.0     | 30000  | 465000.0     |
| 27/12/2023              | Sales Invoice | 50416 | KL Korean YY White           | 1.0 | Pcs  | 10000.0     | 10000  | 475000.0     |
| (A Radityo Whisnu) ...  | ...           | ...   | ...                           | ... | ...  | ...         | ...    | 475000.0     |

Masalah utama pada data ini:
- Nama pelanggan tidak berada dalam kolom khusus, melainkan tercampur dalam baris yang kosong pada bagian transaksi.
- Struktur data tidak mendukung pemrosesan langsung seperti pada format database normal (baris = 1 transaksi).
- Kolom dan informasi tidak konsisten antar baris.

---

## Data Preparation

### 1. Pembersihan Data

- Langkah awal adalah membaca data dan menyusun ulang struktur data agar nama pelanggan dapat ditetapkan untuk setiap baris transaksi yang terkait.
- Menyaring hanya baris transaksi nyata (yang memiliki harga/unit) dan mengaitkannya dengan nama pelanggan yang terdeteksi sebelumnya.

### 2. Ekstraksi dan Agregasi

Setelah struktur diperbaiki, dilakukan proses berikut:

```python
# Mengelompokkan berdasarkan nama pelanggan dan menjumlahkan nilai pembelian
df_new = df.groupby('Customer')['Unit Price'].sum().reset_index()


```

### 3. Penyortiran Data
Untuk menentukan pelanggan dengan pembelian tertinggi, data diurutkan berdasarkan total pembelian:



```python
df_new = df_new.sort_values(by='Unit Price', ascending=False)

```

## Hasil dan Implementasi
- Hasil dari peringkat pelanggan ini digunakan sebagai dasar untuk membuat kampanye loyalitas pelanggan.
- Pada momen spesial seperti Anniversary Cara Florist, pelanggan-pelanggan top akan diberikan penawaran khusus, hadiah loyalitas, atau voucher diskon eksklusif.
- Analisis ini dapat diulang secara berkala (bulanan atau triwulanan) untuk mengevaluasi pelanggan aktif.

## Kesimpulan
Proyek ini berhasil mengubah data transaksi yang tidak terstruktur menjadi informasi yang bermakna melalui pendekatan analitik berbasis Python. Analisis pelanggan berdasarkan total pembelian memberikan dampak nyata pada strategi pemasaran dan retensi pelanggan Cara Florist.

