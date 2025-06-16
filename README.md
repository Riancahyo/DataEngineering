# DATA-ENGINEERING
# Analisis Dampak Kondisi Jalan, Curah Hujan, dan Kepadatan Kendaraan terhadap Kecelakaan Lalu Lintas di Jawa Tengah

## Deskripsi Proyek
Proyek ini dirancang untuk membangun pipeline ETL (Extract, Transform, Load) yang menyatukan data curah hujan, kondisi jalan, dan jumlah kendaraan bermotor untuk mendukung **analisis dampak ketiga faktor tersebut terhadap jumlah kecelakaan lalu lintas di Provinsi Jawa Tengah**. Dengan pipeline ini, seluruh data dari berbagai sumber diproses, dibersihkan, dan digabungkan menjadi satu dataset utama agar dapat dianalisis secara menyeluruh.

Proses tidak hanya berhenti pada pengolahan data, tetapi juga dilanjutkan dengan penerapan **analisis korelasi** untuk mengetahui seberapa besar pengaruh masing-masing variabel terhadap kecelakaan. Untuk memperkaya analisis, dataset juga digunakan dalam penerapan model machine learning berbasis regresi. Hasil dari proyek ini diharapkan dapat menjadi dasar pengambilan keputusan berbasis data oleh pemerintah atau pihak terkait dalam merumuskan strategi pencegahan kecelakaan lalu lintas.

## 🎯 Manfaat Data / Use Case
- **Tujuan Proyek:** Menyediakan dataset terintegrasi untuk menganalisis dampak curah hujan, kondisi jalan, dan jumlah kendaraan terhadap kecelakaan lalu lintas.
- **Manfaat:**
  - Memberikan gambaran mengenai hubungan antar variabel penyebab kecelakaan lalu lintas.
  - Menjadi dasar bagi pemerintah dan lembaga terkait untuk menyusun strategi mitigasi kecelakaan berbasis data.
  - Menghasilkan insight yang dapat dimanfaatkan untuk perencanaan jangka panjang terkait keselamatan berlalu lintas.

## Serving Analisis
Seluruh data hasil ETL disimpan dalam PostgreSQL, kemudian digunakan untuk **analisis korelasi antar variabel** dengan visualisasi interaktif menggunakan Looker Studio dan Plotly.

## Machine Learning (Pendukung)
Dataset juga digunakan untuk melatih model machine learning berbasis regresi guna mendukung hasil analisis korelasi. Berdasarkan evaluasi model, **Random Forest Regressor** terpilih sebagai model terbaik untuk prediksi jumlah kecelakaan berdasarkan variabel-variabel yang telah dianalisis.

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
- API Google Earth Engine untuk data curah hujan
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
  - Kode ETL dan Analisis dipisahkan
  - Variabel deskriptif
- **Machine Learning (Pendukung):**
  - PyCaret `setup()`, `compare_models()` → Random Forest Regressor
  - Visualisasi korelasi dan scatter plot untuk mendukung analisis

## Link Proyek
- ETL Pipeline:  
  https://colab.research.google.com/drive/1joB553qDmrkY4ns0zV89T6dznoOPzj5u?usp=sharing
- Machine Learning:  
  https://colab.research.google.com/drive/1c0yRAkOIxntQeLclG-2yiBmG9oWw4Th-?usp=sharing

## Kontributor

| Nama Lengkap             | NIM         | Peran           |
|--------------------------|-------------|-----------------|
| RIAN CAHYO ANGGORO       | 234311052   | Data Engineer   |
| AFIF DZAKI ZAIN          | 234311029   | Data Analyst    |
| ICON PRIAGAMIS           | 234311042   | Data Analyst    |
| RAHMAD RISKIAWAN H       | 234311048   | Project Manager |
