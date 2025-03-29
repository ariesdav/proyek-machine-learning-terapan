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
A. **Analisis Fitur Kategori**
  1. Fitur dengan lebih dari 10 kategori unik:
     ![Categories_Features_Up_10](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/5253638de0868b14b5274ac8f6eabb7309850d67/submission1-predictive-analytics/gambar/Multivariate_Analysis.png)
     - Merek, model, prosesor (CPU), dan kartu grafis (GPU) berpengaruh besar terhadap harga.
     - Laptop gaming dan merek premium cenderung lebih mahal.

  2. Fitur dengan kurang dari 10 kategori unik:
     ![Categories_Features_Under_10](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/5253638de0868b14b5274ac8f6eabb7309850d67/submission1-predictive-analytics/gambar/Multivariate_Analysis1.png)
     - Tipe laptop, sistem operasi, jenis layar, dan spesifikasi hardware utama memengaruhi harga.
     - Workstation, gaming laptop, macOS, layar 4K, SSD, dan GPU Nvidia lebih mahal dibanding laptop standar.
 
 4. Fitur biner (Ya/Tidak):
    <!--![Categories_Features_Binary]()-->
    - Layar sentuh, panel IPS, dan Retina Display meningkatkan harga, menunjukkan bahwa kualitas layar berperan penting.

B. Analisis Fitur Numerik
 1. Heatmap Korelasi:
    ![Heatmap_Correlation](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/5253638de0868b14b5274ac8f6eabb7309850d67/submission1-predictive-analytics/gambar/Multivariate_Analysis2.png)
    - RAM memiliki korelasi tertinggi dengan harga, diikuti oleh resolusi layar, CPU, dan penyimpanan tambahan.
    - Primary storage (SSD/HDD) memiliki korelasi negatif, artinya kehadiran SSD tidak selalu meningkatkan harga secara signifikan.
    - Ukuran layar (Inches) memiliki korelasi rendah, sehingga fitur ini dihapus dari analisis lebih lanjut untuk meningkatkan fokus pada variabel yang lebih berpengaruh.

## **Data Preparation**  

Tahap **Data Preparation** merupakan langkah penting dalam proyek ini untuk memastikan bahwa data siap digunakan dalam proses pemodelan. Data preparation dilakukan dengan berbagai teknik, termasuk **penghapusan fitur yang tidak relevan**, **pengelompokan kategori**, **encoding fitur kategori**, **reduksi dimensi dengan PCA**, **pembagian dataset menjadi train dan test**, serta **standarisasi fitur numerik**.  

### **1. Menghapus Fitur yang Tidak Relevan**  
```python
df.drop('Product', inplace=True, axis=1)
```
Pada tahap awal, fitur **Product** dihapus dari dataset. Hal ini dikarenakan fitur tersebut memiliki **618 kategori unik**, sehingga terlalu granular dan sulit untuk diolah. Jika tetap digunakan, fitur ini bisa menambah kompleksitas model tanpa memberikan informasi yang signifikan.  

### **2. Pengelompokan Fitur dengan Banyak Kategori (CPU_model & GPU_model)**  
Beberapa fitur dalam dataset memiliki terlalu banyak kategori unik, seperti **CPU_model dan GPU_model**. Jika dibiarkan dalam bentuk aslinya, fitur ini akan menyebabkan model menjadi terlalu kompleks dan bisa meningkatkan risiko overfitting. Oleh karena itu, dilakukan pengelompokan sebagai berikut:  

- **CPU_model** dikelompokkan berdasarkan tingkat performanya:  
  - **Low**: Intel i3, Ryzen 3  
  - **Mid**: Intel i5, Ryzen 5  
  - **High**: Intel i7, i9, Ryzen 7, Ryzen 9  

```python
def categorize_cpu(cpu):
    cpu = cpu.lower()
    if 'i3' in cpu or 'ryzen 3' in cpu:
        return 'Low'
    if 'i5' in cpu or 'ryzen 5' in cpu:
        return 'Mid'
    if 'i7' in cpu or 'i9' in cpu or 'ryzen 7' in cpu or 'ryzen 9' in cpu:
        return 'High'
    return 'Other'

df['CPU_performance'] = df['CPU_model'].apply(categorize_cpu)
df.drop(columns=['CPU_model'], inplace=True)
```

Setelah dikategorikan, fitur CPU_model yang asli dihapus, dan kategori baru dikonversi ke variabel **dummy** menggunakan **One-Hot Encoding (OHE)** agar bisa digunakan dalam model.  

- **GPU_model** juga dikelompokkan berdasarkan performa:  
  - **Integrated**: GPU bawaan Intel/AMD  
  - **Mid**: MX series, Radeon R, Quadro  
  - **High**: GTX, RTX, Radeon RX  

```python
def categorize_gpu(gpu):
    gpu = gpu.lower()
    if ('intel' in gpu or 'uhd' in gpu or 'hd' in gpu or 'iris' in gpu or 'integrated' in gpu):
        return 'Integrated'
    elif ('gtx' in gpu or 'rtx' in gpu or 'radeon rx' in gpu):
        return 'High'
    elif ('mx' in gpu or 'radeon r' in gpu or 'quadro' in gpu):
        return 'Mid'
    return 'Other'

df['GPU_performance'] = df['GPU_model'].apply(categorize_gpu)
df.drop(columns=['GPU_model'], inplace=True)
```

### **3. Encoding Fitur Kategori**  
Dataset memiliki beberapa fitur kategori yang perlu dikonversi ke format numerik agar bisa digunakan oleh model. Teknik encoding yang digunakan meliputi **One-Hot Encoding (OHE) dan Label Encoding**.  

#### **One-Hot Encoding (OHE)**  
```python
ohe_feat = ['Company', 'TypeName', 'OS', 'CPU_company', 'PrimaryStorageType', 'SecondaryStorageType', 'GPU_company']
df = pd.get_dummies(df, columns=ohe_feat, drop_first=True, dtype='int')
```
Fitur dengan banyak kategori, seperti **Company, TypeName, OS, CPU_company, PrimaryStorageType, SecondaryStorageType, dan GPU_company**, dikonversi menggunakan **One-Hot Encoding**.  

#### **Label Encoding**  
```python
binary_cat_col = ["Touchscreen", "IPSpanel", "RetinaDisplay"]
le = LabelEncoder()

for col in binary_cat_col:
    df[col] = le.fit_transform(df[col])
```
Fitur biner yang hanya memiliki dua kategori (Ya/Tidak), seperti **Touchscreen, IPSpanel, dan RetinaDisplay**, dikonversi menggunakan **Label Encoding** untuk menyederhanakan representasi datanya.  

### **4. Reduksi Dimensi dengan PCA**  
![PCA](https://github.com/ariesdav/proyek-machine-learning-terapan/blob/5253638de0868b14b5274ac8f6eabb7309850d67/submission1-predictive-analytics/gambar/PCA.png)
```python
pca = PCA(n_components=1, random_state=123)
pca.fit(df[['ScreenW', 'ScreenH']])
df['ScreenSize'] = pca.transform(df[['ScreenW', 'ScreenH']]).flatten()
df.drop(['ScreenW', 'ScreenH'], axis=1, inplace=True)
```
Beberapa fitur numerik dalam dataset memiliki korelasi tinggi, sehingga bisa menyebabkan **redundansi informasi**. Salah satu contoh adalah fitur **ScreenW dan ScreenH**, yang sama-sama menggambarkan resolusi layar. Untuk mengatasi ini, dilakukan **Principal Component Analysis (PCA)** untuk menggabungkan kedua fitur tersebut menjadi satu fitur baru bernama **ScreenSize**.  

### **5. Membagi Data (Train-Test Split)**  
```python
X = df.drop(["Price_euros"], axis=1)
y = df["Price_euros"]
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=123)
```
Setelah data dikonversi ke bentuk numerik dan dimensi dikurangi, dataset dibagi menjadi **training set (80%) dan test set (20%)**. Training set digunakan untuk melatih model, sedangkan test set digunakan untuk mengevaluasi performa model.  

### **6. Standarisasi Fitur Numerik**  
```python
numerical_features = ['Ram', 'Weight', 'ScreenSize', 'SecondaryStorage']
scaler = StandardScaler()
scaler.fit(X_train[numerical_features])
X_train[numerical_features] = scaler.transform(X_train.loc[:, numerical_features])
```
Fitur numerik dalam dataset memiliki skala yang berbeda-beda, misalnya **RAM dalam GB**, **berat dalam kg**, dan **ScreenSize dalam ukuran relatif**. Jika tidak disesuaikan, perbedaan skala ini bisa menyebabkan model lebih berat ke fitur dengan nilai besar. Oleh karena itu, dilakukan **standardisasi** menggunakan **StandardScaler**, yang mengubah semua fitur numerik menjadi skala dengan rata-rata **0** dan standar deviasi **1**.  

## Pengembangan Model
### 1. Modeling
Proses ini bertujuan untuk membangun model machine learning yang mampu memprediksi harga dengan tingkat akurasi yang tinggi. Beberapa algoritma yang digunakan dalam proyek ini meliputi:

- **Random Forest Regressor (RF)**: Model ensemble berbasis pohon keputusan yang meningkatkan akurasi dengan menggabungkan banyak pohon dan mengurangi overfitting.
- **Extra Trees Regressor (ET)**: Mirip dengan RF, tetapi menggunakan lebih banyak elemen acak dalam pemilihan fitur dan pemotongan pohon, yang membuatnya lebih cepat dalam pelatihan.
- **Gradient Boosting Regressor (GBR)**: Model boosting yang membangun pohon secara bertahap untuk memperbaiki kesalahan dari pohon sebelumnya, sehingga lebih fokus pada prediksi yang sulit.

### 2. Implementasi Model
Pertama, dibuat sebuah DataFrame kosong untuk menyimpan nilai error dari setiap model.
```python
models = pd.DataFrame(index=['train_mse', 'test_mse'], columns=['RF', 'ET', 'GBR'])
```

#### a. Random Forest Regressor (RF)
Model RF dilatih menggunakan 50 pohon keputusan (**n_estimators=50**) dengan kedalaman maksimal 15 (**max_depth=15**).
```python
rf = RandomForestRegressor(n_estimators=50, max_depth=15, random_state=55, n_jobs=-1)
```
**Kelebihan RF:**
- Mengurangi overfitting dibandingkan model pohon keputusan tunggal.
- Mampu menangani data dengan banyak fitur.

**Kekurangan RF:**
- Kurang optimal untuk dataset yang sangat besar karena membutuhkan banyak pohon.
- Interpretasi model lebih sulit dibandingkan model pohon tunggal.

#### b. Extra Trees Regressor (ET)
ET dilatih dengan parameter yang sama seperti RF, yaitu 50 pohon dengan kedalaman maksimal 15.
```python
et = ExtraTreesRegressor(n_estimators=50, max_depth=15, random_state=55, n_jobs=-1)
```
**Kelebihan ET:**
- Lebih cepat dalam pelatihan dibandingkan RF karena lebih banyak elemen acak.
- Menghasilkan variasi model yang lebih luas, sehingga lebih tahan terhadap overfitting.

**Kekurangan ET:**
- Akurasi bisa lebih rendah dibandingkan RF pada dataset dengan pola yang sangat jelas.
- Lebih sulit untuk dituning dibandingkan model lain.

#### c. Gradient Boosting Regressor (GBR)
GBR dilatih dengan parameter **n_estimators=50**, **max_depth=15**, dan **learning_rate=0.5**.
```python
gbr = GradientBoostingRegressor(n_estimators=50, max_depth=15, learning_rate=0.5, random_state=55)
```
**Kelebihan GBR:**
- Dapat menangani dataset dengan jumlah fitur besar.
- Lebih akurat dibandingkan RF dan ET jika parameter dioptimalkan dengan baik.

**Kekurangan GBR:**
- Proses pelatihan lebih lambat dibandingkan RF dan ET.
- Lebih rentan terhadap overfitting jika parameter tidak dituning dengan benar.

### 3. Pemilihan Model Terbaik3. Pemilihan Model Terbaik
Meskipun model Gradient Boosting Regressor (GBR) memiliki akurasi yang lebih tinggi pada data training, model ini lebih rentan terhadap overfitting, sehingga kurang andal saat digunakan untuk data baru. Oleh karena itu, model Random Forest Regressor (RF) dipilih sebagai model terbaik karena mampu memberikan prediksi yang lebih stabil dan dapat digeneralisasi dengan baik ke data yang belum pernah dilihat sebelumnya.

Beberapa alasan utama memilih RF sebagai model terbaik:
- Keseimbangan antara akurasi dan generalisasi: RF mampu memberikan hasil yang cukup akurat tanpa mengalami overfitting yang berlebihan.
- Robust terhadap variasi data: Dengan teknik bagging, RF dapat menangani berbagai pola data tanpa kehilangan performa secara drastis.
- Lebih mudah diimplementasikan dan dituning: Dibandingkan GBR yang memerlukan tuning parameter lebih kompleks, RF lebih fleksibel dan tidak terlalu sensitif terhadap perubahan parameter.

