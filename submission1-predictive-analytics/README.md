# Laporan Proyek Machine Learning - Ariestio Dava Pratama
## Domain Proyek
### Latar Belakang
Laptop adalah komputer portabel yang dirancang untuk kemudahan mobilitas dan penggunaan di berbagai tempat. Seluruh komponennya sudah terintegrasi dalam satu perangkat, menjadikannya lebih praktis dan nyaman digunakan. Karena sifatnya yang ringkas, efisien, dan mudah digunakan, laptop menjadi pilihan favorit bagi pekerja maupun pelajar. Seiring berjalannya waktu, permintaan terhadap laptop terus meningkat, sehingga dibutuhkan suatu metode yang dapat membantu platform dalam memprediksi harga laptop berdasarkan merek dan spesifikasinya. Pemanfaatan pembelajaran mesin dengan algoritma seperti Support Vector Regression, K-Nearest Neighbors Regression, dan Random Forest Regression dapat digunakan untuk membangun model prediksi harga lebih akurat berdasarkan fitur-fitur spesifikasi laptop.

Berdasarkan laporan International Data Corporation [IDC](https://www.idc.com/getdoc.jsp?containerId=prAP52599624), pasar PC di Indonesia mencatat 953 ribu unit pada kuartal kedua 2024, mencakup desktop, notebook, dan workstation. Selain itu menurut survei Kurious [KIC](https://databoks.katadata.co.id/-/statistik/3b8142e85a411d7/kurious-kic-asus-jadi-merek-laptop-yang-paling-banyak-digunakan-konsumen-indonesia?utm_source=chatgpt.com) menunjukkan bahwa Asus menjadi merek laptop paling populer di Indonesia dengan 23,3% pengguna, diikuti Acer (23%), Lenovo (16,2%), dan HP (13,7%). Merek merupakan faktor utama dalam penjualan, meskipun data spesifik terkait spesifikasi laptop masih terbatas. Dengan demikian, perusahaan berupaya meningkatkan penjualan laptop dengan fokus pada fitur-fitur yang memengaruhi keputusan pembelian. Proyek ini dapat membantu perusahaan dalam mengembangkan platform pemasaran dengan model prediksi harga yang lebih akurat menggunakan beberapa teknik pembelajaran mesin.

## Business Understanding
### Problem Statements 
Mengacu pada penjelasan dari latar belakang, muncul beberapa permasalahan yang memengaruhi proyek ini:
- Fitur atau komponen apa saja yang paling berpengaruh terhadap harga sebuah laptop?
- Bagaimana perusahaan dapat memprediksi harga laptop lebih akurat?
### Goals
Untuk mencapai tujuan proyek, beberapa hal yang harus dicapai adalah: 
- Menjelaskan fitur atau komponen utama yang paling berpengaruh terhadap harga laptop.
- Membangun model prediksi harga laptop yang akurat dengan berbagai teknik pembelajaran mesin.
### Solution Statement
Selain dari tujuan proyek, tentu diperlukan solusi agar proyek ini dapat berhasil. Beberapa solusi diantaranya adalah:
- Melakukan analisis eksplorasi data untuk memahami korelasi antara fitur-fitur laptop dan harga.  
- Menerapkan model pembelajaran mesin untuk meningkatkan akurasi prediksi harga, termasuk:  
  - Support Vector Regression (SVR): Model regresi berbasis Support Vector Machine (SVM) yang mencari fungsi terbaik untuk memprediksi nilai output kontinu.  
  - K-Nearest Neighbors Regression (KNN): Metode non-parametrik yang memprediksi nilai berdasarkan rata-rata dari K tetangga terdekat.  
  - Random Forest Regression: Algoritma ensemble yang menggabungkan banyak decision tree untuk prediksi yang lebih stabil dan akurat.  
- Mengevaluasi performa model menggunakan metrik seperti Mean Squared Error (MSE), Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), dan R-Squared (R²).

## Data Understanding
## Pemahaman Data  
Dataset yang digunakan dalam proyek ini adalah [Laptops Price Dataset](https://www.kaggle.com/datasets/juanmerinobermejo/laptops-price-dataset). Dataset ini berisi kumpulan informasi mengenai berbagai jenis laptop, memungkinkan analisis mendalam terkait spesifikasi dan harganya. Data mencakup berbagai merek, model, serta konfigurasi laptop yang beragam.  

Beberapa fitur utama dalam dataset ini meliputi:  
- Laptop Name: Identitas unik atau model dari masing-masing laptop.
- Status: Status laptop termasuk kategori baru atau bekas.
- Brand: Merek laptop yang tersedia dalam dataset.  
- Model: Model spesifik dari setiap merek laptop.  
- CPU (Central Processing Unit): Informasi mengenai prosesor, termasuk merek, model, dan spesifikasi terkait.  
- GPU (Graphics Processing Unit): Detail tentang kartu grafis yang digunakan, termasuk merek dan modelnya.  
- RAM (Random Access Memory): Kapasitas memori yang tersedia untuk menjalankan berbagai tugas secara bersamaan.  
- Storage: Jenis penyimpanan yang digunakan (HDD atau SSD) beserta kapasitasnya.  
- Final Price: Harga laptop dalam mata uang yang digunakan dalam dataset.  
