# Laporan Proyek Machine Learning - Ariestio Dava Pratama
## Domain Proyek
### Latar Belakang
Laptop adalah komputer portabel yang dirancang untuk kemudahan mobilitas dan penggunaan di berbagai tempat. Seluruh komponennya sudah terintegrasi dalam satu perangkat, menjadikannya lebih praktis dan nyaman digunakan. Karena sifatnya yang ringkas, efisien, dan mudah digunakan, laptop menjadi pilihan favorit bagi pekerja maupun pelajar. Seiring berjalannya waktu, permintaan terhadap laptop terus meningkat, sehingga dibutuhkan suatu metode yang dapat membantu platform dalam memprediksi harga laptop berdasarkan merek dan spesifikasinya. Pemanfaatan pembelajaran mesin dengan algoritma dapat digunakan untuk membangun model prediksi harga lebih akurat berdasarkan fitur-fitur spesifikasi laptop.

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
  - Random Forest Regressor (RF): Model ensemble yang menggunakan banyak decision tree untuk meningkatkan akurasi dan mengurangi overfitting dengan cara melakukan averaging dari hasil prediksi masing-masing pohon.
  - Extra Trees Regressor (ET): Mirip dengan Random Forest, tetapi membagi node secara lebih acak, sehingga menghasilkan variasi model yang lebih tinggi dan sering kali lebih cepat dalam pelatihan.
  - Gradient Boosting Regressor (GBR): Model boosting yang membangun pohon secara bertahap, di mana setiap pohon baru mencoba memperbaiki kesalahan dari pohon sebelumnya, sehingga lebih fokus pada prediksi yang sulit ditebak.
- Mengevaluasi performa model menggunakan metrik seperti Mean Squared Error (MSE), Root Mean Squared Error (RMSE), Mean Absolute Error (MAE), dan R-Squared (R²).

## Data Understanding
Proyek ini menggunakan dataset [Laptop Prices](https://www.kaggle.com/datasets/owm4096/laptop-prices) yang diperoleh dari Kaggle. Dataset ini berisi **1275 baris × 23 kolom**, dengan setiap kolom merepresentasikan berbagai fitur laptop, seperti Name Product, RAM, Touch Screen, CPU, dan lainnya. Fitur utama yang menjadi target analisis adalah **Price_euros**, yang menunjukkan harga laptop dalam Euro. Dataset ini merupakan versi yang telah diproses ulang dari kumpulan data harga laptop yang populer.

Berikut adalah tabel yang merangkum fitur-fitur dalam dataset:  

| Fitur                 | Deskripsi |
|----------------------|-----------|
| Company           | Produsen atau merek laptop. |
| Product           | Nama merek dan model laptop. |
| TypeName          | Jenis laptop (Notebook, Ultrabook, Gaming, dll.). |
| Inches           | Ukuran layar dalam inci. |
| Ram              | Kapasitas RAM dalam GB. |
| OS               | Sistem operasi yang terpasang pada laptop. |
| Weight           | Berat laptop dalam kilogram. |
| Price_euros      | Harga laptop dalam Euro (target prediksi). |
| Screen           | Resolusi layar (Standard, Full HD, 4K Ultra HD, Quad HD+). |
| ScreenW          | Lebar layar dalam piksel. |
| ScreenH          | Tinggi layar dalam piksel. |
| Touchscreen      | Apakah laptop memiliki layar sentuh atau tidak. |
| IPSpanel         | Apakah layar laptop menggunakan panel IPS atau tidak. |
| RetinaDisplay    | Apakah layar laptop memiliki Retina Display atau tidak. |
| CPU_company      | Produsen prosesor laptop. |
| CPU_freq         | Kecepatan prosesor laptop dalam Hz. |
| CPU_model        | Model prosesor yang digunakan. |
| PrimaryStorage   | Kapasitas penyimpanan utama dalam GB. |
| PrimaryStorageType | Jenis penyimpanan utama (HDD, SSD, Flash Storage, Hybrid). |
| SecondaryStorage | Kapasitas penyimpanan tambahan jika tersedia (GB). |
| SecondaryStorageType | Jenis penyimpanan tambahan (HDD, SSD, Hybrid, atau Tidak Ada). |
| GPU_company      | Produsen kartu grafis. |
| GPU_model        | Model kartu grafis yang digunakan. |

### Exploratory Data Analysis (EDA)
Tahapan Exploratory Data Analysis (EDA) merupakan proses penting untuk mengenali struktur dan karakteristik data sebelum melakukan analisis lebih lanjut. Berikut adalah langkah-langkahnya:

#### 1. Memeriksa Struktur Data
  -  Dataset memiliki 1.275 baris, 23 kolom, tipe data numerik dan kategori.
  -  Tidak ada missing value atau duplikasi.

#### 2. Deskripsi Statistik
  -  Variasi besar dalam harga, RAM, berat, dan resolusi layar.
  -  Statistik menunjukkan distribusi dan kemungkinan outlier.

#### 3. Jumlah Kategori Unik
  -  19 merek laptop, 618 model, 791 variasi harga.
  -  Fitur biner: Touchscreen, IPS Panel, Retina Display.
  -  CPU & GPU memiliki banyak variasi, mencerminkan spesifikasi beragam.

#### 4. Univariate Analysis
A. **Analisis Fitur Kategori**  
  1. Fitur dengan lebih dari 10 kategori unik (Company, Product, CPU_model, GPU_model):
      
      ![Categories_Features_Up_10](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/15ef885bac0ed5fd580e76d56179a608ef4ca95a/submission1-predictive-analytics/gambar/Univariate_Analysis.png)
  
      - Merek seperti Dell dan Lenovo mendominasi, sementara Samsung dan Mediacom jarang ditemukan.  
      - Intel Core i5 7200U dan Core i7 7700HQ paling umum sebagai prosesor utama.  
      - Sebagian besar laptop menggunakan GPU terintegrasi seperti Intel HD Graphics.  
  
  2. Fitur dengan kurang dari 10 kategori unik (TypeName, OS, Screen, dll.):
     ![Categories_Features_Under_10](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/15ef885bac0ed5fd580e76d56179a608ef4ca95a/submission1-predictive-analytics/gambar/Univariate_Analysis1.png)
      - Notebook menjadi jenis laptop paling umum dibandingkan Ultrabook dan Gaming Laptop.  
      - Windows 10 adalah sistem operasi dominan, sementara Android hampir tidak digunakan.  
      - Mayoritas laptop menggunakan layar Full HD (1920x1080).  
      - SSD lebih banyak digunakan dibandingkan HDD, sementara penyimpanan sekunder jarang ditemukan.  
  
  3. Fitur biner (Ya/Tidak):
      ![Categories_Features_Binary](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/15ef885bac0ed5fd580e76d56179a608ef4ca95a/submission1-predictive-analytics/gambar/Univariate_Analysis5.png)
      - Layar sentuh, IPS Panel, dan Retina Display masih jarang ditemukan, hanya ada pada model premium.  
  
B. **Analisis Fitur Numerik**  
  1. Distribusi Histogram:
     ![Numeric_Features_Histogram](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/15ef885bac0ed5fd580e76d56179a608ef4ca95a/submission1-predictive-analytics/gambar/Univariate_Analysis2.png)
      - Ukuran layar (Inches): Mayoritas 14-15.6 inci, menunjukkan standar umum.  
      - RAM: 8GB paling umum, dengan 16GB ke atas lebih banyak ditemukan di laptop kelas atas.  
      - CPU Frequency: Berkisar 2-3 GHz, cukup untuk komputasi sehari-hari.  
      - Penyimpanan (SSD/HDD): Sebagian besar laptop memiliki 256GB hingga 512GB penyimpanan utama.  
      - Harga laptop: Berkisar €600 - €1500, menunjukkan dominasi segmen menengah.
  
  3. Boxplot (Outlier Detection):
     ![Numeric_Features_Histogram](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/15ef885bac0ed5fd580e76d56179a608ef4ca95a/submission1-predictive-analytics/gambar/Univariate_Analysis3.png)
      - Terdapat outlier pada ukuran layar, bobot, RAM, CPU_freq, storage, dan harga.  
      - Outlier dihapus menggunakan metode IQR untuk menjaga akurasi analisis.  

#### 5. Multivariate Analysis
