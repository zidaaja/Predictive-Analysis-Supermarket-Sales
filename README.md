# Laporan Proyek Machine Learning - Amazida

## Latar Belakang

[Pendapatan kotor](https://id.wikipedia.org/wiki/Pendapatan_kotor) merupakan pendapatan dari seluruh total pendapatan yang dikurangi dengan harga pokok penjualan. Pendapatan kotor, atau margin kotor, atau laba kotor merupakan tolak ukur paling sederhana untuk menghasilkan keuntungan atau laba suatu perusahaan atau instansi. Mengetahui laba kotor dapat membantu suatu instansi atau perusahaan dalam hal memahami perkembangan, dapat menentukan kestabilitasan keuangan, dan dapat menjadi bahan evaluasi model serta strategi bisnis.

[Supermarket](https://www.bing.com/ck/a?!&&p=e69cb78ec1aba472JmltdHM9MTY2MzYzMjAwMCZpZ3VpZD0yYmEzZjJjYS1mOWNiLTZjMWYtMjEzYi1lMzdlZjg5ZDZkODcmaW5zaWQ9NTE2MQ&ptn=3&hsh=3&fclid=2ba3f2ca-f9cb-6c1f-213b-e37ef89d6d87&u=a1aHR0cHM6Ly9pZC53aWtpcGVkaWEub3JnL3dpa2kvU3VwZXJtYXJrZXQ&ntb=1) merupakan tempat perbelanjaan modern yang didalamnya terdapat berbagai lini produk yang biasa dibeli untuk kebutuhan sehari-hari. Saat ini pertumbuhan dan persaingan pasar supermarket semakin meningkat. Oleh sebab itu, melihat pendapatan kotor dapat menjadi acuan mengapa persaingan dan pertumbuhannya semakin meningkat.

Melihat pentingnya pendapatan kotor dalam hal perkembangan bisnis, diperlukan adanya suatu model yang dapat memprediksi pendapatan kotor pada umumnya.
  
  Format Referensi: [Judul Referensi](https://scholar.google.com/) 

## Business Understanding


### Problem Statements

Berdasarkan kondisi yang telah diuraikan sebelumnya, supermarket akan mengembangkan sebuah sistem prediksi pendapatan kotor untuk menjawab permasalahan berikut:
- Fitur apa yang paling berpengaruh pada pendapatan kotor supermarket?
- Bagaimana membuat model yang cocok untuk prediksi pendapatan kotor supermarket?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang berkolerasi dengan pendapatan supermarket
- Mengetahui model yang tepat berdasarkan loss yang paling sedikit

    ### Solution statements
    - Dalam menyelesaikan masalah ini, kita dapat mencoba menggunakan model development K-Nearest Neighbor, Random Forest, dan Boosting Algorithm
    - Dari ketiga model tersebut, akan di evaluasi menggunakan Mean Squared Error untuk memilih model terbaik dalam memprediksi pendapatan kotor/gross income

## Data Understanding
Dataset yang digunakan pada proyek ini adalah dataset Penjualan di supermarket yang dapat diunduh pada link berikut ini: [Supermarket Sales](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales).

### Variabel-variabel pada Supermarket sales dataset adalah sebagai berikut:
- Invoice id: Nomor identifikasi faktur penjualan yang dihasilkan komputer
- Branch: Cabang supercenter (3 cabang tersedia diidentifikasi oleh A, B dan C).
- City: Lokasi supercenter
- Customer type: Jenis pelanggan, dicatat oleh Anggota untuk pelanggan yang menggunakan kartu anggota dan Normal untuk tanpa kartu anggota.
- Gender: Jenis kelamin pelanggan
- Product line: Grup kategorisasi barang umum - Aksesori elektronik, Aksesori mode, Makanan dan minuman, Kesehatan dan kecantikan, Rumah dan gaya hidup, Olahraga dan perjalanan
- Unit price: Harga setiap produk dalam $
- Quantity: Jumlah produk yang dibeli oleh pelanggan
- Tax 5%: biaya pajak 5% untuk pembelian pelanggan
- Total: Total harga termasuk pajak
- Date: Tanggal pembelian (Catatan tersedia dari Januari 2019 hingga Maret 2019)
- Time: Waktu pembelian (10 pagi hingga 9 malam)
- Payment: Pembayaran yang digunakan pelanggan untuk pembelian (tersedia 3 metode – Tunai, Kartu kredit, dan Ewallet)
- COGS: Harga pokok penjualan
- Gross margin percentage: Persentase margin kotor
- Gross income: Pendapatan kotor
- Rating: Peringkat stratifikasi pelanggan pada pengalaman berbelanja mereka secara keseluruhan (Pada skala 1 hingga 10)

Saya menggunakan variabel "gross income" sebagai target variabel. Selain itu, untuk memahami seluruh variabel saya melakukan Exploratory Data Analysis.

Saya menggunakan 2 Teknik yaitu teknik Univariate dan Multivariate EDA. 
Pada fitur numerik univariate saya mendapatkan informasi mengenai peningkatan pendapatan kotor sebanding dengan penurunan jumlah sampel.

<img width="212" alt="image" src="https://user-images.githubusercontent.com/102134676/191318514-0c99ebff-0625-4c17-820b-1800cb7738bd.png">

Pada multivariate analysis ketika mengecek rata-rata Pendapatan kotor terhadap masing-masing fitur, saya mendapatkan informasi bahwa rata-rata seluruh fitur tidak memiliki dampak yang besar terhadap gross income atau pendapatan kotor. Kemudian, saya melihat relasi antara semua fitur numerik dengan fitur target ‘gross income’.

<img width="427" alt="image" src="https://user-images.githubusercontent.com/102134676/191319419-190b4676-0760-47aa-a647-edc1c51c1b48.png">


## Data Preparation
Untuk tahapan data preparation yang saya lakukan yaitu:
- Melakukan Encoding fitur dengan menggunakan One-hot-encoding untuk mengubah variabel kategori menjadi numerik.
- Reduksi dimensi dengan Principal Component Analysis (PCA) untuk mengurangi fitur yang sama atau yang memiliki korelasi tinggi.
- Membagi dataset dengan fungsi train_test_split dari library sklearn.
- Melakukan standarisasi dengan standard scaler untuk mengubah nilai mean menjadi 0 dan standar deviasi 1.

## Modeling
Model yang digunakan pada projek ini ada 3 yaitu K-Nearest Neighbor, Random Forest, dan Boosting Algorithm. Pada K-Nearest Neighbor menggunakan parameter n_neighbors=10, pada Random Forest menggunakan parameter n_estimators=50, max_depth=16, random_state=55, n_jobs=-1, dan pada Boosting Algorithm menggunakan parameter learning_rate=0.05, random_state=55. 

- Kelebihan dari K-Nearest Neighbor ialah mudah digunakan, namun KNN hanya cocok untuk dataset dengan fitur yang sedikit karena bisa terjadi curse of dimensionality (kutukan dimensi)
- Kelebihan dari Random Forest ialah sederhana tetapi memiliki stabilitas yang mumpuni
- Kelebihan dari Boosting Algorithm ialah sangat powerful dalam meningkatkan akurasi prediksi.

## Evaluation
Metriks evaluasi yang digunakan untuk ketiga model tersebut adalah MSE(Mean Squared Error). MSE menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi.

<img width="317" alt="image" src="https://user-images.githubusercontent.com/102134676/191325191-a014fde1-87dd-47d2-8cc8-bb5566a7b641.png">


Berikut hasil visualisasi dari metriks MSE:

<img width="300" alt="image" src="https://user-images.githubusercontent.com/102134676/191325558-ee0f90ca-037f-4bf3-a54c-dba202a9e3b9.png">

dapat dilihat bahwa model Random Forest menghasilkan error yang paling sedikit.

<img width="354" alt="image" src="https://user-images.githubusercontent.com/102134676/191326611-d0631a5a-88d7-4097-9d34-e105b4d36c79.png">

Hasil prediksi random forest merupakan hasil yang paling mendekati.

---Ini adalah bagian akhir laporan---
