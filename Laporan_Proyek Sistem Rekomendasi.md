# Laporan Proyek Machine Learning - Nafa Khairunnisa

## Project Overview

Sejak pandemi COVID-19, banyak aspek kehidupan mengalami perubahan signifikan, salah satunya adalah kebiasaan berbelanja masyarakat. Peralihan dari belanja konvensional ke belanja daring melalui platform e-commerce menjadi semakin masif. Masyarakat kini lebih sering mencari dan membeli produk secara online, dan sering kali memiliki preferensi terhadap kategori produk tertentu.

Dalam konteks ini, sistem rekomendasi berperan penting untuk meningkatkan pengalaman pengguna dengan menyarankan produk yang relevan berdasarkan preferensi dan perilaku mereka. Sistem rekomendasi yang baik tidak hanya meningkatkan kepuasan pengguna, tetapi juga dapat mendorong peningkatan penjualan dan loyalitas pelanggan.

Berbagai penelitian sebelumnya telah mengembangkan sistem rekomendasi menggunakan pendekatan seperti Collaborative Filtering (berbasis kemiripan antar pengguna atau item) dan Content-Based Filtering (berbasis kemiripan fitur). Misalnya, dalam penelitian yang dilakukan oleh Shabrina Z. P. dkk, sistem rekomendasi content-based filtering dengan TF-IDF dan Cosine Similarity terbukti efektif memiliki presisi 85% dan skor kemiripan minimal 0.1 dan maksimal 1[1]. Dataset yang digunakan terbatas pada nama produk, deskripsi produk, kategori produk, dan harga produk berdasarkan produk yang diklik pengguna selama penggunaan sistem ecommerce.

Penelitian lainnya pada tahun 2024 menggunakan Collaborative Filtering untuk e-commerce dengan membandingkan model K-Nearest Neighbour (KNN) dan SVD++[2]. Dataset yang digunakan terbatas pada rating, product_id, dan shop_id. Dengan metrik evaluasi MAE dan RMSE, model SVD++ lebih unggul dengan nilai MAE 0,161176 dan RMSE 0,185252.

Penelitian yang berjudul *Pengembangan Sistem Rekomendasi Thrifting pada E-Commerce Menggunakan Metode Collaborative Filtering* membuat sistem rekomendasi dengan menganalisis interaksi pengguna, seperti melihat produk (view), menambahkan ke keranjang (add to cart), dan melakukan pembelian (purchase), yang masing-masing diberi bobot nilai untuk menentukan relevansi produk[3]. Dari perhitungan cosine similarity diperoleh nilai rekomendasi tertinggi sebesar 8.13, 6.13, dan 3.34, di mana produk dengan nilai similaritas tertinggi menjadi prioritas utama.

Namun, sebagian besar penelitian tersebut masih terbatas pada fitur tertentu, tanpa mempertimbangkan aspek-aspek seperti harga diskon yang juga dapat memengaruhi keputusan pembelian pengguna.

Oleh karena itu, proyek ini bertujuan membangun sistem rekomendasi produk e-commerce dengan pendekatan Content-Based Filtering yang menggabungkan fitur eksplisit produk—termasuk deskripsi produk dan atribut harga—menggunakan TF-IDF dan Cosine Similarity, serta Collaborative Filtering berbasis rating historis dengan algoritma SVD++. Pendekatan ini memungkinkan sistem menyarankan produk yang relevan meskipun tanpa informasi eksplisit tentang profil pengguna, dengan tetap menghasilkan rekomendasi yang kontekstual dan personal.

Proyek ini mengembangkan sistem rekomendasi menggunakan dua pendekatan utama—Content-Based Filtering dan Collaborative Filtering—dengan memanfaatkan dataset "Amazon Sales Dataset" dari Kaggle[4]. Dataset ini dipilih karena mencakup data multi-aspek yang jarang tersedia secara publik, seperti informasi produk yang dibeli, harga, dan penilaian pengguna. Model rekomendasi yang dibangun menggunakan pendekatan yang telah ada, kemudian dituning pada hyperparameternya untuk memperoleh hasil evaluasi terbaik. Hal ini memungkinkan pembangunan sistem rekomendasi yang dipersonalisasi dan efektif sesuai kebutuhan platform e-commerce.

---

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah diuraikan, terdapat dua tantangan utama dalam sistem rekomendasi pada platform e-commerce:

1. **Sistem rekomendasi yang terbatas pada fitur tertentu**, seperti hanya menggunakan nama atau kategori produk, belum mampu sepenuhnya memahami konteks keputusan pembelian, termasuk pengaruh deskripsi produk atau diskon harga terhadap minat pengguna.
2. **Kurangnya pemanfaatan interaksi historis pengguna**, seperti rating atau pola pembelian, menghambat sistem dalam menghasilkan rekomendasi yang personal dan relevan, sehingga dapat berdampak pada kepuasan dan loyalitas pengguna.

### Goals

Untuk menjawab tantangan tersebut, proyek ini memiliki tujuan utama sebagai berikut:

1. Mengembangkan sistem rekomendasi berbasis Content-Based Filtering yang dapat mempertimbangkan fitur produk yang lebih komprehensif, termasuk deskripsi produk dan diskon harga, untuk memberikan rekomendasi yang lebih relevan dan kontekstual bagi pengguna.

2. Menerapkan Collaborative Filtering dengan memanfaatkan interaksi historis pengguna (seperti rating dan pola pembelian) untuk menghasilkan rekomendasi yang lebih personal dan meningkatkan relevansi saran produk, sehingga dapat meningkatkan kepuasan dan loyalitas pengguna.

### Solution Statements

Untuk mencapai tujuan tersebut, digunakan dua pendekatan sistem rekomendasi yang saling melengkapi:

1. **Content-Based Filtering (CBF)**
  Membangun model dengan teknik TF-IDF dan Cosine Similarity untuk mengukur kesamaan antar produk berdasarkan deskripsi dan fitur lainnya. Model ini akan memberikan rekomendasi produk-produk sejenis yang pernah dibeli atau dinilai oleh pengguna, sehingga meningkatkan relevansi pencarian dan efisiensi belanja. Fitur-fitur yang digunakan yaitu nama produk, kategori, deskripsi, harga, rating, dan diskon, agar pengguna dapat menemukan produk relevan dengan lebih efisien.

2. **Collaborative Filtering (CF)**
  Mengimplementasikan algoritma Singular Value Decomposition Plus Plus (SVD++) yang telah di-tuning untuk memprediksi rating produk yang belum diberikan oleh pengguna. Rekomendasi dihasilkan berdasarkan pola perilaku dan preferensi pengguna lain yang serupa, guna memberikan hasil yang lebih personal dan akurat. Sistem rekomendasi yang dibangun berbasis Collaborative Filtering yang memanfaatkan data interaksi pengguna (seperti user_id, product_id, dan rating) untuk memberikan saran produk berdasarkan kesamaan preferensi antar pengguna.

3. **Penyesuaian berdasarkan penelitian terdahulu**
  Menggunakan algoritma dan pendekatan yang telah terbukti berhasil dalam penelitian sebelumnya, dengan penyesuaian pada hyperparameter untuk meningkatkan performa model.

Dengan menggunakan kedua pendekatan ini, sistem rekomendasi yang dikembangkan diharapkan dapat meningkatkan kepuasan pengguna, efisiensi pencarian produk, serta mendorong peningkatan penjualan dan loyalitas pelanggan pada platform e-commerce.

---

## Data Understanding

Data Understanding merupakan proses memahami dataset yang akan digunakan. Di mana di dalamnya terdapat eksplorasi data.

Dataset yang digunakan ada proyek ini diambil dari platform Kaggle berjudul [Amazon Sales Dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset). Dataset ini memiliki 1000+ data penilaian dan ulasan produk di platform Amazon, sebuah aplikasi e-commerce.

Berikut daftar variabel-variabel di dalam data:
- product_id          : ID produk
- product_name        : Nama produk
- category            : Kategori produk
- discounted_price    : Harga produk diskon
- actual_price        : Harga asli produk
- discount_percentage : Persentase diskon produk
- rating              : Rating produk (nilai)
- rating_count        : Jumlah pengguna yang memerikan rating
- about_product       : Deskripsi produk
- user_id             : ID pengguna yang menulis ulasan
- user_name           : Nama pengguna yang menulis ulasan
- review_id           : ID ulasan pengguna
- review_title        : Ulasan pendek
- review_content      : Ulasan panjang
- img_link            : Tautan gambar produk
- product_link        : Tautan website resmi produk                                

Untuk mengetahui informasi dalam dataset, dilakukan Exploratory Data Analysis (EDA) melalui deskripsi variabel dan univariate data analysis menggunakan bar plot. Dengan begitu dapat diketahui informasi seperti jumlah pasti data, jumlah missing value, jumlah data duplikat, jumlah nilai unik dalam setiap variabel, dan mengetahui nilai dengan jumlah terbanyak pada variabel-variabel seperti category, discount_percentage, dan rating.

Dengan melakukan Exploratory Data Analysis (EDA) melalui deskripsi variabel dan univariate data analysis, didapatkan informasi mengenai dataset sebagai berikut:
- Dataset memiliki total 1465 sampel.
- Memiliki 16 fitur.
- Semua fitur bertipe data object.
- Nilai unique setiap fitur bervariasi.
- Hanya fitur rating_count yang memiliki missing value.
- Dataset tidak memiliki data duplikat.
- Kategori di setiap transaksi bertingkat (memilik hierarki).
- 'Computers&Accessories|Accessories&Peripherals|Cables&Accessories|Cables|USBCables' merupakan category yang paling banyak muncul.
- Persentase diskon yang paling banyak muncul yaitu 50%, 60%, 0%, 80%, dan 55%. Top 5 distribusi persentase diskon dapat dilihat pada gambar 1.
![Top 5 distribusi persentase diskon](img\discount_percentage.png)
Gambar 1. Top 5 distribusi persentase diskon
- Rating yang diberikan paling banyak berada pada rating 4.1, 4.3, 4.2, 4.0, dan 3.9. Artinya kualitas produk baik. Top 5 distribusi rating dapat dilihat pada gambar 2.
![Top 5 distribusi rating](img\distribusi_rating.png)
Gambar 2. Top 5 distribusi rating

Hasil eksplorasi awal menunjukkan bahwa dataset memiliki struktur hierarkis pada kategori, distribusi diskon yang bervariasi, dan kecenderungan rating yang tinggi, sehingga cocok digunakan untuk membangun sistem rekomendasi berbasis konten maupun interaksi pengguna.

---

## Data Preparation

Data preparation merupakan proses membersihkan dan mengolah data agar siap digunakan pada model. Pada penelitian ini, melakukan content-based filtering dan collaborative filtering di mana kedua pendekatan tersebut membutuhkan pendekatan data preparation yang berbeda. Sehingga data preparation pada penelitian ini dilakukan dua kali.

### Data Preparation untuk Content-Based Filtering

Sesuai dengan namanya, content-based filtering menggunakan informasi produk untuk membentuk model rekomendasi. Maka dari itu, hanya ada beberapa fitur yang digunakan untuk pendekatan ini yaitu yang berkaitan dengan informasi produk dan rating produk. Berikut tahapan lengkap data preparation:

- Menyalin fitur-fitur yang akan digunakan ke dalam dataframe baru bernama preparation_df.
Dataframe awal yaitu df disalin ke dalam dataframe baru yaitu preparation_df yang berisi: 'product_name', 'category', 'about_product', 'discounted_price', 'actual_price', 'discount_percentage', 'rating', 'rating_count'.
- Menghapus data duplikat.
Setelah membuat dataframe baru, muncul data duplikat karena kini fitur terbatas sehingga perlu dihapus. Data duplikat yang muncul ada 84 dan kemudian dihapus sehingga jumlah data dalam preparation_df menjadi 1381 sampel.
- Kolom rating_count yang bertipe object dibersihkan dari tanda koma, diisi nilai kosongnya dengan nol, lalu dikonversi menjadi integer.
- Mengganti simbol '|' dengan nilai NaN dan mengonversi tipe data dari object ke float untuk kolom 'rating'.
Kolom rating memiliki nilai desimal di dalamnya dan ada juga yang memiliki simbol '|'. Simbol tersebut diganti menjadi nilai NaN. Nilai NaN pada rating diisi dengan nilai rata-rata dari rating yang valid kemudian kolom rating dikonversi menjadi float.
- Menghapus simbol '₹' dan mengonversi tipe data dari object ke float pada kolom 'discounted_price' dan 'actual_price'.
- Menghilangkan tanda % dan konversi ke tipe float pada kolom 'discount_percentage'.
- Melakukan text processing untuk kolom 'product_name', 'category', dan 'about_product'.
Fitur category pada setiap produk terdiri dari beberapa tingkatan (misalnya: Electronics | Computers | Cables). Oleh karena itu, category, product_name, dan about_product digabungkan ke dalam satu kolom teks gabungan (content_text) sebagai representasi deskriptif dari setiap produk. Selain itu, kategori yang paling spesifik (bagian paling kanan setelah simbol "|") juga diekstrak secara terpisah untuk eksplorasi.
- Normalisasi fitur numerik dengan MinMaxScaler.
Normalisasi dilakukan untuk menyamakan skala antar fitur numerik agar tidak mendominasi perhitungan similarity.
Berikut snippet codenya:
```
scaler = MinMaxScaler()
```
- Menyalin fitur numerik yang sudah dibersihkan ke dataframe baru.
- Ekstraksi fitur teks menggunakan TF-IDF Vectorizer dengan max_features=5000 untuk merepresentasikan teks dari kolom content_clean ke dalam bentuk vektor numerik. TF-IDF menangkap kata-kata penting yang mewakili karakteristik tiap produk. max_features = 5000 pada TfidfVectorizer dipilih untuk membatasi kompleksitas vektor dan mengurangi noise dari kata yang terlalu jarang muncul.

### Data Preparation untuk Collaborative Filtering

Berikut tahapan data preparation untuk collaborative filtering:
- Memilih fitur relevan untuk user-based collaborative filtering
 Hanya beberapa fitur yang dipilih untuk digunakan dalam modeling yaitu 'user_id', 'product_id', 'rating'. Fitur-fitur tersebut dimasukkan ke dalam dataframe baru bernama cf_preparation.
- Menangani data duplikat
Data duplikat muncul setelah pemilihan fitur. Sebanyak 104 data duplikat dihapus dari dataframe menyisakan 1361 sampel data.
- Mengganti nilai non-numerik (seperti '|') dengan NaN, mengisi nilai NaN tersebut dengan nilai rata-rata rating, dan mengonversi kolom rating menjadi float
Tahapan ini sama seperti pada data preparation untuk content-based filtering dimana kolom rating memiliki simbol '|' dan masih berupa tipe data object. Sehingga perlu penanganan seperti mengganti simbol dengan nilai NaN, mengganti nilai NaN dengan rata-rata rating, dan mengonversinya ke tipe data float.
-  Encoding fitur product_id dan user_id
Encoding dilakukan dengan memetakan setiap nilai user_id dan product_id menjadi bilangan bulat unik menggunakan dictionary mapping.
- Menghitung nilai minimum dan maximum rating dan menghitung jumlah nilai pada kolom product_id dan user_id.
- Mengacak data dalam dataframe.
Hal ini dilakukan agar data yang digunakan dalam sistem rekomendasi bisa lebih general.
- Menyimpan dataset ke dalam dataframe baru bernama data untuk kemudian digunakan pada library surprise.
- Splitting data menjadi train data 80% dan test data 20%.


---

## Modeling and Result

Modeling merupakan proses pembuatan model. Results merupakan hasil rekomendasi menggunakan model yang telah dibuat. Pada bagian ini dibagi menjadi dua yaitu modeling untuk content-based filtering dan collaborative filtering.

### Modeling dan Results untuk Content-Based Filtering (CBF)

#### Modeling
Pada pendekatan Content-Based Filtering, model dibangun berdasarkan informasi konten produk. Berikut langkah-langkah modeling yang dilakukan:

1. Penggabungan Fitur:
  - Vektor TF-IDF digabung dengan fitur numerik tambahan menggunakan hstack() untuk membentuk satu matriks fitur gabungan.
2. Penghitungan Cosine Similarity:
  - Cosine similarity dihitung antar semua produk untuk mengukur kemiripan antar item.
  - Hasilnya dikonversi ke dalam bentuk DataFrame agar mudah diakses saat proses rekomendasi.

#### Results
Untuk mendapatkan hasil rekomendasi, digunakan fungsi content_based_recommendation() yang menerima indeks produk, matriks kesamaan (cosine similarity), dan data produk. Fungsi ini menyaring produk yang memiliki skor kemiripan di atas ambang batas (threshold), kemudian memilih Top-10 produk paling mirip.

Sebagai contoh, sistem memberikan rekomendasi untuk produk ke-10 (indeks ke-10) dengan threshold kemiripan sebesar 0.2.

Produk ke-10:
| product_name | category | discounted_price |
|--------------|----------|------------------|
| B08CF3D7QR | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹154 |

Berikut adalah output 10 produk yang direkomendasikan beserta skor kemiripannya:

| product_name | category | discounted_price | Similarity_Score |
|--------------|----------|------------------|------------------|
| Portronics Konnect L 1.2M POR-1401 Fast Charging 3A 8 Pin USB Cable with Charge & Sync Function (White) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹159 | 0.853435 |
| Portronics Konnect L POR-1081 Fast Charging 3A Type-C Cable 1.2Meter with Charge & Sync Function for All Type-C Devices (Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹154 | 0.842072 |
| Portronics Konnect L POR-1403 Fast Charging 3A Type-C Cable 1.2 Meter with Charge & Sync Function for All Type-C Devices (White) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹210 | 0.833218 |
| Portronics Konnect L 1.2M Fast Charging 3A 8 Pin USB Cable with Charge & Sync Function for iPhone, iPad (Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹154 | 0.804674 |
| Portronics Konnect L 1.2Mtr, Fast Charging 3A Micro USB Cable with Charge & Sync Function (Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹154 | 0.786607 |
| Portronics Konnect CL 20W POR-1067 Type-C to 8 Pin USB 1.2M Cable with Power Delivery & 3A Quick Charge Support, Nylon Braided for All Type-C and 8 Pin Devices, Green | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹350 | 0.520841 |
| Portronics Konnect CL 20W POR-1067 Type-C to 8 Pin USB 1.2M Cable with Power Delivery & 3A Quick Charge Support, Nylon Braided for All Type-C and 8 Pin Devices, Green | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹350 | 0.520841 |
| FLiX (Beetel) USB to Type C PVC Data Sync & 2A Smartphone Fast Charging Cable, Made in India, 480Mbps Data Sync, Tough Cable, 1 Meter Long USB Cable for USB Type C Devices Black XCD-C12 | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹139 | 0.462835 |
| Portronics Konnect L 60W PD Type C to Type C Mobile Charging Cable, 1.2M, Fast Data Sync, Tangle Resistant, TPE+Nylon Braided(Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹249 | 0.460198 |
| Flix (Beetel) Usb To Type C Pvc Data Sync And 2A 480Mbps Data Sync, Tough Fast Charging Long Cable For Usb Type C Devices, Charging Adapter (White, 1 Meter) - Xcd-C12 | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables | ₹139 | 0.458636 |

Output akan menampilkan daftar produk yang paling mirip secara konten, dengan informasi nama produk, kategori, dan harga diskon, serta skor kemiripan (Similarity_Score) yang membantu menjelaskan alasan sistem merekomendasikan produk tersebut.

### Collaborative Filtering (CF)

#### Modeling
Untuk pendekatan Collaborative Filtering, digunakan algoritma SVD++ (Singular Value Decomposition++) dari pustaka Surprise, yang mampu menangkap hubungan tersembunyi antara pengguna dan produk berdasarkan interaksi mereka.

Grid Search digunakan untuk menemukan kombinasi parameter terbaik melalui validasi silang (cross-validation) sebanyak 3 fold. Parameter yang di-tuning:
- n_factors: [20, 50, 100, 150, 200] → jumlah latent factors
- lr_all: [0.001, 0.002, 0.005, 0.01, 0.02] → learning rate
- reg_all: [0.005, 0.01, 0.02, 0.05, 0.1] → regularisasi

Hasil tuning:
Best RMSE score: 0.812
Best parameters: {'n_factors': 100, 'lr_all': 0.005, 'reg_all': 0.02}

Evaluasi awal dilakukan melalui cross-validation dengan metrik RMSE (Root Mean Squared Error) untuk memilih model terbaik. Setelah itu, model terbaik difit ulang menggunakan data pelatihan (train_set) dan dievaluasi terhadap data pengujian (test_set).

#### Results
Model memberikan rekomendasi untuk seorang pengguna tertentu (misalnya, pengguna ke-11) berdasarkan produk yang belum pernah mereka nilai sebelumnya. Sistem memprediksi skor rating untuk setiap produk, lalu mengurutkannya dari estimasi tertinggi.

Rekomendasi disajikan sebagai berikut:

Produk dengan rating tertinggi yang pernah dinilai oleh user:

| Produk | Rating |
|--------|--------|
| AmazonBasics Flexible Premium HDMI Cable (Black, 4K@60Hz, 18Gbps), 3-Foot | 4.4 |
| Amazon Basics High-Speed HDMI Cable, 6 Feet - Supports Ethernet, 3D, 4K video, Black | 4.4 |
| Amazon Basics High-Speed HDMI Cable, 6 Feet (2-Pack), Black | 4.4 |
| AmazonBasics Flexible Premium HDMI Cable (Black, 4K@60Hz, 18Gbps), 3-Foot | 4.4 |

Top 10 Produk Rekomendasi:
| Produk | Kategori |
|--------|----------|
| Wayona Nylon Braided USB to Lightning Fast Charging and Data Sync Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini (3 FT Pack of 1, Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| Ambrane Unbreakable 60W / 3A Fast Charging 1.5m Braided Type C Cable for Smartphones, Tablets, Laptops & other Type C devices, PD Technology, 480Mbps Data Sync, Quick Charge 3.0 (RCT15A, Black) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| Sounce Fast Phone Charging Cable & Data Sync USB Cable Compatible for iPhone 13, 12,11, X, 8, 7, 6, 5, iPad Air, Pro, Mini & iOS Devices | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| boAt Deuce USB 300 2 in 1 Type-C & Micro USB Stress Resistant, Tangle-Free, Sturdy Cable with 3A Fast Charging & 480mbps Data Transmission, 10000+ Bends Lifespan and Extended 1.5m Length (Martian Red) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| Portronics Konnect L 1.2M Fast Charging 3A 8 Pin USB Cable with Charge & Sync Function for iPhone, iPad (Grey) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| pTron Solero TB301 3A Type-C Data and Fast Charging Cable, Made in India, 480Mbps Data Sync, Strong and Durable 1.5-Meter Nylon Braided USB Cable for Type-C Devices for Charging Adapter (Black) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| boAt Micro USB 55 Tangle-free, Sturdy Micro USB Cable with 3A Fast Charging & 480mbps Data Transmission (Black) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| MI Usb Type-C Cable Smartphone (Black) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |
| TP-Link USB WiFi Adapter for PC (TL-WN725N), N150 Wireless Network Adapter for Desktop - Nano Size WiFi Dongle Compatible with Windows 11/10/7/8/8.1/XP/ Mac OS 10.9-10.15 Linux Kernel 2.6.18-4.4.3 | Computers&Accessories\|NetworkingDevices\|NetworkAdapters\|WirelessUSBAdapters |
| Ambrane Unbreakable 60W / 3A Fast Charging 1.5m Braided Micro USB Cable for Smartphones, Tablets, Laptops & Other Micro USB Devices, 480Mbps Data Sync, Quick Charge 3.0 (RCM15, Black) | Computers&Accessories\|Accessories&Peripherals\|Cables&Accessories\|Cables\|USBCables |

Rekomendasi ini bersifat personalized karena mempertimbangkan histori perilaku pengguna, bukan hanya isi konten produk.

### Kelebihan dan Kekurangan Model

Berikut adalah Tabel 1 yang merangkum kelebihan dan kekurangan dari dua model rekomendasi yang digunakan:

**Tabel 1. Kelebihan dan Kekurangan Model**

| Model | Kelebihan | Kekurangan |
|:---|:---|:---|
| Content-Based Filtering (CBF) dengan TF-IDF & Cosine Similarity | Cocok untuk cold-start item (produk baru), tidak tergantung pada data pengguna lain, mudah dijelaskan karena berbasis fitur eksplisit | - Rekomendasi cenderung terbatas dan seragam, tidak mempertimbangkan minat pengguna lain, tidak cocok untuk item dengan fitur minim |
| Collaborative Filtering (CF) dengan SVD++ dan Grid Search | - Mampu menangkap pola preferensi pengguna laten, memberikan rekomendasi yang lebih personal, cocok untuk dataset dengan banyak interaksi | - Tidak efektif untuk cold-start user/item, membutuhkan banyak data interaksi pengguna, interpretasi hasil lebih kompleks dan tidak transparan |

---

## Evaluation

Evaluasi dilakukan dengan menggunakan metrik yang sesuai dengan pendekatan sistem rekomendasi yang digunakan, yaitu:

1. Content-Based Filtering (CBF)
Untuk pendekatan Content-Based Filtering, digunakan metrik Precision@K sebagai evaluasi performa sistem rekomendasi. 
Precision@K cocok digunakan dalam konteks sistem rekomendasi top-N, yaitu ketika sistem ditugaskan untuk menyarankan sejumlah item (misalnya 10 item) yang paling relevan kepada pengguna, sebagaimana dijelaskan di situs evidentlyai[5]. Precision@K mengukur seberapa banyak item yang relevan dari total item yang direkomendasikan. 

Rumus Precision@K:
```
Precision@K = Jumlah item relevan dalam top-K rekomendasi / K
```

Produk dianggap relevan jika berasal dari kategori yang sama dengan produk acuan. Fitur yang dijadikan evaluasi di sini Product_Category_Preference. Evaluasi dilakukan terhadap rekomendasi untuk satu produk tertentu (produk dengan indeks ke-10). Maka K = 10, yang berarti sistem dievaluasi berdasarkan 10 produk teratas yang direkomendasikan.

Hasil evaluasi menunjukkan bahwa nilai Precision@10 sebesar 1.0 (100%). Artinya, seluruh produk yang direkomendasikan berada dalam kategori yang sama dengan produk yang sedang dievaluasi. Ini menunjukkan bahwa sistem content-based mampu menangkap kemiripan antar produk berdasarkan fitur konten (teks deskripsi dan fitur numerik) dengan sangat baik.

2. Collaborative Filtering (CF)
Untuk pendekatan Collaborative Filtering menggunakan algoritma SVD++, digunakan dua metrik evaluasi utama yang umum dalam prediksi rating, yaitu RMSE dan MAE. Kedua metrik ini digunakan ketika sistem rekomendasi berfungsi memperkirakan nilai rating yang akan diberikan pengguna terhadap produk yang belum dinilai. Berikut penjelasan metrik evaluasi tersebut:

a. RMSE (Root Mean Squared Error)
Mengukur akar dari rata-rata selisih kuadrat antara rating aktual dan rating yang diprediksi.

b. MAE (Mean Absolute Error)
Mengukur rata-rata selisih absolut antara rating aktual dan prediksi.

Rumus RMSE:
```
RMSE = sqrt( Σ (rating_asli - rating_prediksi)^2 / N )
```

Rumus MAE:
```
MAE = Σ |rating_asli - rating_prediksi| / N
```

Hasil evaluasi menunjukkan bahwa nilai RMSE sebesar 0.2670 dan nilai MAE sebesar 0.2013. Nilai RMSE dan MAE yang rendah menunjukkan bahwa model mampu memberikan prediksi rating yang sangat dekat dengan rating aktual. Hal ini menunjukkan bahwa model collaborative filtering yang dibangun efektif dalam memahami preferensi pengguna berdasarkan interaksi sebelumnya.

### Dampak terhadap Business Understanding

Penelitian ini menjawab seluruh elemen *Business Understanding* sebagai berikut:

#### Problem Statements:
1. **Sistem rekomendasi yang terbatas pada fitur tertentu**
   Masalah ini diatasi dengan pendekatan Content-Based Filtering (CBF) yang memperluas cakupan fitur yang digunakan dalam sistem rekomendasi. Dengan mempertimbangkan fitur seperti nama produk, kategori, deskripsi, harga, dan diskon, model ini dapat memberikan rekomendasi produk yang lebih relevan dan kontekstual, sesuai dengan keputusan pembelian pengguna. Evaluasi model menggunakan Precision@10 yang mencapai 1.0 (100%) membuktikan bahwa sistem mampu menyaring produk yang relevan secara efektif, membantu pengguna menjelajahi produk dengan lebih efisien, dan memastikan bahwa fitur-fitur yang lebih mendalam (seperti deskripsi dan diskon) berdampak signifikan pada relevansi rekomendasi.

2. **Kurangnya pemanfaatan interaksi historis pengguna**
   Masalah ini dijawab dengan pendekatan Collaborative Filtering (CF) yang memanfaatkan data interaksi historis pengguna seperti rating dan pola pembelian. Dengan menggunakan Singular Value Decomposition Plus Plus (SVD++) yang telah di-tuning, model mampu memberikan rekomendasi berdasarkan pola perilaku pengguna lain yang serupa, menghasilkan rekomendasi yang lebih personal dan relevan. Evaluasi model menggunakan RMSE sebesar 0.2670 dan MAE sebesar 0.2013 menunjukkan bahwa model ini dapat memprediksi preferensi pengguna dengan akurat dan relevan, memperkuat personalisasi dalam sistem rekomendasi dan meningkatkan pengalaman pengguna.

#### Goals:

1. **Mengembangkan sistem CBF untuk rekomendasi produk serupa**  
   Model Content-Based berhasil dikembangkan menggunakan **TF-IDF** dan **Cosine Similarity**, dan terbukti akurat dalam menyarankan produk yang relevan dengan produk referensi, seperti dibuktikan oleh precision@10 = 1.0.

2. **Membangun sistem CF berbasis interaksi pengguna**  
   Model Collaborative Filtering dibangun menggunakan **SVD++ dengan hyperparameter tuning**, dan menghasilkan rekomendasi dengan RMSE sebesar 0.2670 dan nilai MAE sebesar 0.2013. Hal ini mendukung sistem rekomendasi yang lebih personal dan meningkatkan pengalaman pengguna.

#### Solution Statements:
1. **Mengembangkan model Content-Based Filtering**  
   Model CBF telah dikembangkan menggunakan fitur nama produk, kategori, deskripsi, harga, dan diskon. Teknik TF-IDF dengan max_features=5000 digunakan untuk representasi teks, lalu Cosine Similarity digunakan untuk mengukur kesamaan antar produk. Evaluasi Precision@10 membuktikan bahwa pendekatan ini efektif untuk memberikan rekomendasi berdasarkan kemiripan produk.

2. **Mengembangkan model Collaborative Filtering**  
   Model CF telah diimplementasikan menggunakan data user_id, product_id, dan rating, serta algoritma SVD++ yang dituning. Evaluasi menggunakan RMSE dan MAE menunjukkan bahwa model mampu memprediksi rating dengan akurat, memungkinkan pemberian rekomendasi yang sesuai dengan preferensi pengguna.

3. **Penyesuaian berdasarkan penelitian terdahulu**  
   Sistem dibangun menggunakan algoritma yang pernah digunakan oleh penelitian terdahulu dengan hyperparameter tuning. Pada pendekatan Content-Based Filtering, digunakan TF-IDF dan Cosine Similarity, dengan tuning hyperparameter pada tahap ekstraksi fitur, yaitu max_features=5000 pada TF-IDF untuk membatasi kompleksitas vektor dan mengurangi noise dari kata-kata yang jarang muncul. Selanjutnya, pendekatan Collaborative Filtering menggunakan algoritma SVD++ dengan hyperparameter terbaik yang diperoleh melalui proses Grid Search, yaitu: jumlah latent factors sebanyak 100, learning rate sebesar 0.005, dan nilai regularisasi sebesar 0.02.

Secara keseluruhan, sistem rekomendasi yang dikembangkan telah berhasil menjawab seluruh problem statements, mencapai setiap goals yang ditetapkan, dan mengimplementasikan solusi dengan dampak nyata terhadap kebutuhan bisnis. Pendekatan gabungan antara Content-Based Filtering dan Collaborative Filtering memungkinkan sistem memberikan rekomendasi yang relevan, efisien, dan personal, yang secara langsung mendukung peningkatan pengalaman pengguna, kepuasan pelanggan, serta potensi peningkatan konversi penjualan pada platform e-commerce.

---

## Referensi:
[1] Shabrina Zhafarina Putri, Mochamad Hariadi, and Reza Fuad Rachmadi, “Rekomendasi Barang pada E-commerce menggunakan Content Based Recommender System berbasis Ethereum Blockchain,” Jurnal Teknik ITS, vol. 12, no. 2, Sep. 2023, doi: https://doi.org/10.12962/j23373539.v12i2.115263.

[2] Chalista Yulia Hazizah and Triyanna Widiyaningtyas, “Analisis Metode Collaborative Filtering menggunakan KNN dan SVD++ untuk Rekomendasi Produk E-commerce Tokopedia,” EDUMATIC Jurnal Pendidikan Informatika, vol. 8, no. 2, pp. 595–604, Dec. 2024, doi: https://doi.org/10.29408/edumatic.v8i2.27793.
‌
[3] Laksono Ridho Cahyo, Angga Lisdiyanto, and Moch Machlul Alamin, "Pengembangan Sistem Rekomendasi Thrifting pada E-Commerce Menggunakan Metode Collaborative Filtering", JATI (Jurnal Mahasiswa Teknik Informatika) - ITN, doi: https://doi.org/10.36040/jati.v9i3.13744

[4] “Amazon Sales Dataset,” www.kaggle.com. https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset
‌
[5] “10 metrics to evaluate recommender and ranking systems,” www.evidentlyai.com. https://www.evidentlyai.com/ranking-metrics/evaluating-recommender-systems