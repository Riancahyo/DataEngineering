# DATA-ENGINEERING  
# Prediksi Jumlah Kecelakaan Lalu Lintas Berdasarkan Kondisi Jalan, Curah Hujan, dan Jumlah Kendaraan Menggunakan Regresi

## Deskripsi Proyek
Proyek ini bertujuan untuk membangun pipeline ETL (Extract, Transform, Load) untuk menganalisis keterkaitan antara curah hujan, kondisi jalan, dan jumlah kendaraan bermotor terhadap jumlah kecelakaan lalu lintas di Provinsi Jawa Tengah. Data dikumpulkan dari berbagai sumber terpercaya, dibersihkan, diintegrasikan, dan dipersiapkan untuk analisis lebih lanjut serta pelatihan model machine learning berbasis regresi. Hasil akhir proyek berupa dataset terintegrasi yang digunakan untuk memprediksi jumlah kecelakaan lalu lintas di tiap Kabupaten/Kota.

## Manfaat Data / Use Case
- **Tujuan Proyek:** Menyediakan dataset terintegrasi untuk membangun model prediktif jumlah kecelakaan lalu lintas.
- **Manfaat:**
  - Menunjukkan hubungan antara curah hujan, kondisi jalan, jumlah kendaraan, dan jumlah kecelakaan.
  - Menjadi dasar untuk model prediksi jumlah kecelakaan per Kabupaten/Kota.
  - Memberikan rekomendasi berbasis data untuk pemerintah dan instansi terkait.

## Serving Analisis
Data hasil ETL disimpan dalam PostgreSQL dan digunakan untuk analisis eksploratif serta visualisasi interaktif menggunakan Looker Studio dan Plotly.

## Serving Machine Learning
Dataset bersih dan terstandarisasi digunakan untuk melatih model machine learning berbasis regresi. Model terbaik dipilih menggunakan PyCaret, dan **Random Forest Regressor** terpilih sebagai model dengan performa terbaik.

## Pipeline
### Extract (Pengambilan Data)
**Sumber Data:**
- Jumlah Kecelakaan - BPS Jawa Tengah
  https://jateng.bps.go.id/id/statistics-table/2/NTYzIzI=/jumlah-korban-kecelakaan-lalu-lintas-di-wilayah-polda-jawa-tengah-tahun.html 
- Jumlah Kendaraan - BPS Jawa Tengah
  https://jateng.bps.go.id/id/statistics-table/2/MTAwNiMy/jumlah-kendaraan-bermotor-menurut-kabupaten-kota-dan-jenis-kendaraan-di-provinsi-jawa-tengah
- Kondisi Jalan - BPS Jawa Tengah
  https://jateng.bps.go.id/id/statistics-table/1/MjQ1NSMx/panjang-jalan-menurut-kabupaten-kota-dan-kondisi-jalan--di-provinsi-jawa-tengah--km---2020.html
- Curah Hujan - Google Earth Engine (CHIRPS)
  https://code.earthengine.google.com/?project=silken-facet-436013-f9

**Metode Pengambilan:**
- Scraping HTML dengan Selenium untuk data BPS
- API Google Earth Engine untuk curah hujan
- Penyimpanan awal dalam format CSV atau langsung ke PostgreSQL

### Transform (Pembersihan & Transformasi)
- Menghapus duplikat dan baris kosong
- Standardisasi nama kolom dan Kabupaten/Kota
- Penggabungan berdasarkan `Kabupaten_Kota`
- Membuat kolom baru `Total_Kecelakaan` (meninggal + luka berat + luka ringan)

### Load (Pemindahan ke Target)
- Dataset akhir dimuat ke PostgreSQL (Aiven)
- Verifikasi menggunakan `read_sql()` dan `head()`

## Arsitektur / Workflow ETL
- **Alur Modular:** Dibagi menjadi fungsi terpisah di Google Colab
- **Tools:** Python 3.x, pandas, numpy, sqlalchemy, selenium, geemap, pycaret, plotly

## Kode Program
- **Struktur:**
  - Kode ETL dan Machine Learning dipisahkan
  - Variabel deskriptif
- **Machine Learning:**
  - PyCaret `setup()`, `compare_models()` → Random Forest Regressor
  - Visualisasi prediksi vs aktual

## Link Proyek
- ETL Pipeline:
  https://colab.research.google.com/drive/1joB553qDmrkY4ns0zV89T6dznoOPzj5u?usp=sharing 
- Machine Learning:
  https://colab.research.google.com/drive/1c0yRAkOIxntQeLclG-2yiBmG9oWw4Th-?usp=sharing

## Kontributor

| Nama Lengkap                       | NIM         | Peran                |
|------------------------------------|-------------|----------------------|
| RIAN CAHYO ANGGORO                 | 234311052   | Data Engineer        |
| AFIF DZAKI ZAIN                    | 234311029   | Data Analyst         |
| ICON PRIAGAMIS                     | 234311042   | Data Analyst         |
| RAHMAD RISKIAWAN H                 | 234311048   | Project Manager      |
