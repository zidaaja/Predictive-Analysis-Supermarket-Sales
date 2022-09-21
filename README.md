# Laporan Proyek Machine Learning - Amazida

## Latar Belakang

Pendapatan kotor merupakan pendapatan dari seluruh total pendapatan yang dikurangi dengan harga pokok penjualan. Pendapatan kotor menjadi tolak ukur paling sederhana untuk menghasilkan keuntungan atau laba untuk sebuah perusahaan atau instansi. Mengetahui laba kotor dapat membantu suatu instansi atau perusahaan dalam hal memahami perkembangan, dapat menentukan kestabilitasan keuangan, dan dapat menjadi bahan evaluasi model serta strategi bisnis.

Supermarket merupakan tempat perbelanjaan modern yang didalamnya terdapat berbagai lini produk yang biasa dibeli untuk kebutuhan sehari-hari. Saat ini pertumbuhan dan persaingan pasar supermarket semakin meningkat. Oleh sebab itu, melihat pendapatan kotor dapat menjadi acuan mengapa persaingan dan pertumbuhannya semakin meningkat.

Melihat pentingnya pendapatan kotor dalam hal perkembangan supermarket, diperlukan adanya suatu model yang dapat memprediksi pendapatan kotor pada umumnya.


## Business Understanding


### Problem Statements

Berdasarkan kondisi yang telah diuraikan sebelumnya, supermarket akan mengembangkan sebuah sistem prediksi pendapatan kotor untuk menjawab permasalahan berikut:
- Fitur apa yang paling berpengaruh pada pendapatan kotor supermarket?
- Bagaimana membuat model yang cocok untuk prediksi pendapatan kotor supermarket?

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang berkolerasi dengan pendapatan supermarket
- Mengetahui model yang tepat berdasarkan error yang paling sedikit

    ### Solution statements
    - Dalam menyelesaikan masalah ini, kita dapat mencoba menggunakan model _development K-Nearest Neighbor, Random Forest, dan Boosting Algorithm_
    - Dari ketiga model tersebut, akan di evaluasi menggunakan _Mean Squared Error_ untuk memilih model terbaik dalam memprediksi pendapatan kotor/_gross income_

## Data Understanding
Dataset yang digunakan pada proyek ini adalah dataset Penjualan di supermarket yang dapat diunduh pada link berikut ini: [Supermarket Sales](https://www.kaggle.com/datasets/aungpyaeap/supermarket-sales).

### Variabel-variabel pada Supermarket sales dataset adalah sebagai berikut:
- Invoice id: Nomor identifikasi faktur penjualan yang dihasilkan komputer
- Branch: Cabang supercenter (3 cabang tersedia diidentifikasi oleh A, B dan C).
- City: Lokasi _supercenter_
- Customer type: Jenis pelanggan, dicatat oleh Anggota untuk pelanggan yang menggunakan kartu anggota dan Normal untuk tanpa kartu anggota.
- Gender: Jenis kelamin pelanggan
- Product line: Grup kategorisasi barang umum - Aksesori elektronik, Aksesori mode, Makanan dan minuman, Kesehatan dan kecantikan, Rumah dan gaya hidup, Olahraga dan perjalanan
- Unit price: Harga setiap produk dalam $
- Quantity: Jumlah produk yang dibeli oleh pelanggan
- Tax 5%: biaya pajak 5% untuk pembelian pelanggan
- Total: Total harga termasuk pajak
- Date: Tanggal pembelian (Catatan tersedia dari Januari 2019 hingga Maret 2019)
- Time: Waktu pembelian (10 pagi hingga 9 malam)
- Payment: Pembayaran yang digunakan pelanggan untuk pembelian (tersedia 3 metode – Tunai, Kartu kredit, dan _Ewallet_)
- COGS: Harga pokok penjualan
- Gross margin percentage: Persentase margin kotor
- Gross income: Pendapatan kotor
- Rating: Peringkat stratifikasi pelanggan pada pengalaman berbelanja mereka secara keseluruhan (Pada skala 1 hingga 10)

Terdapat 1000 data dan 17 kolom pada dataset tersebut.

Saya menggunakan variabel "gross income" sebagai target variabel. Selain itu, untuk memahami seluruh variabel saya melakukan _Exploratory Data Analysis_.

Saya menggunakan 2 Teknik yaitu teknik Univariate dan Multivariate EDA. 
Pada fitur numerik univariate saya mendapatkan informasi mengenai peningkatan pendapatan kotor sebanding dengan penurunan jumlah sampel.

<img width="212" alt="image" src="https://user-images.githubusercontent.com/102134676/191318514-0c99ebff-0625-4c17-820b-1800cb7738bd.png">
Gambar 1. Histogram gross income


Pada analisis multivariate ketika mengecek rata-rata Pendapatan kotor terhadap masing-masing fitur, saya mendapatkan informasi bahwa rata-rata seluruh fitur tidak memiliki dampak yang besar terhadap _gross income_ atau pendapatan kotor. Kemudian, saya melihat relasi antara semua fitur numerik dengan fitur target ‘gross income’.

<img width="427" alt="image" src="https://user-images.githubusercontent.com/102134676/191319419-190b4676-0760-47aa-a647-edc1c51c1b48.png">
Gambar 2. pairplot gross income



## Data Preparation
Untuk tahapan data preparation yang saya lakukan yaitu:
### One-Hot-Encoding
Melakukan Encoding fitur dengan menggunakan _One-hot-encoding_ untuk mengubah seluruh variabel kategori menjadi numerik, yaitu variabel "Branch, City, Customer type, Gender, Product line, Time, Payment, dan day".
### Reduksi dimensi
Reduksi dimensi dengan _Principal Component Analysis_ (PCA) untuk mengurangi fitur yang sama atau yang memiliki korelasi tinggi, yaitu pada variabel "Tax 5%, Total, dan cogs".
### Splitting dataset
Membagi dataset dengan fungsi train_test_split dari library sklearn.
### Standarisasi dataset
Melakukan standarisasi dengan _standard scaler_ untuk mengubah nilai mean menjadi 0 dan standar deviasi 1.

## Modeling
Model yang digunakan pada projek ini ada 3 yaitu _K-Nearest Neighbor, Random Forest, dan Boosting Algorithm_. Pada _K-Nearest Neighbor_ menggunakan parameter n_neighbors=10, pada _Random Forest_ menggunakan parameter n_estimators=50, max_depth=16, random_state=55, n_jobs=-1, dan pada _Boosting Algorithm_ menggunakan parameter learning_rate=0.05, random_state=55. 

- Kelebihan dari _K-Nearest Neighbor_ ialah mudah digunakan, namun KNN hanya cocok untuk dataset dengan fitur yang sedikit karena bisa terjadi curse of dimensionality (kutukan dimensi)
- Kelebihan dari _Random Forest_ ialah sederhana tetapi memiliki stabilitas yang mumpuni
- Kelebihan dari _Boosting Algorithm_ ialah sangat powerful dalam meningkatkan akurasi prediksi.

## Evaluation
Metriks evaluasi yang digunakan untuk ketiga model tersebut adalah MSE(_Mean Squared Error_). MSE menghitung jumlah selisih kuadrat rata-rata nilai sebenarnya dengan nilai prediksi. Nilai MSE yang paling rendah menunjukan bahwa hasil prediksi sesuai dengan hasil yang sebenarnya. Hasil metriks dapat dilihat sebagai berikut:

<img width="179" alt="image" src="https://user-images.githubusercontent.com/102134676/191391055-e76b4121-707a-4116-9db3-43bb8aa3d6e4.png">
Gambar 3. MSE

Pada baris KNN menunjukan error _train_ 0.003591 dan _test_ 0.004173, pada baris RF menunjukan _train_ 0.000001	_test_ 0.000004, dan pada baris Boosting menunjukan _train_ 0.00142 _test_ 0.001371. Untuk memudahkan membandingkan ketiga model tersebut dapat divisualisasikan sebagai berikut:

<img width="300" alt="image" src="https://user-images.githubusercontent.com/102134676/191325558-ee0f90ca-037f-4bf3-a54c-dba202a9e3b9.png">

Gambar 4. Plot nilai MSE
Dapat dilihat bahwa model dengan _Random Forest_ menghasilkan error yang paling sedikit, yaitu 0.000001 pada data _train_, dan	0.000004 pada data _test_. Sedangkan pada model K-Nearest Neighbor menghasilkan error yang paling tinggi , yaitu 0.003591 pada data _train_, dan	0.004173 pada data _test_.

<img width="354" alt="image" src="https://user-images.githubusercontent.com/102134676/191326611-d0631a5a-88d7-4097-9d34-e105b4d36c79.png">
Gambar 5. Pengujian prediksi dengan Random Forest

Berdasarkan gambar tersebut terlihat bahwa prediksi _random forest_ merupakan hasil yang paling mendekati, maka untuk prediksi pendapatan kotor pada supermarket dapat menggunakan Model _Random Forest_.

## Kesimpulan
Model Machine learning yang paling tepat untuk memprediksi pendapatan kotor supermarket dapat dikembangkan dengan model _Random Forest_, karena error yang didapatkan paling sedikit diantara ketiga model yang dicoba yaitu 0.000001 pada data _train_, dan 0.000004 pada data _test_ sehingga ini sudah cukup untuk memenuhi tujuan dari yang diharapkan. Namun, untuk meningkatkan performa dalam pengujian bisa saja untuk melakukan pengaturan parameter.

## Referensi
[1] Internal Revenue Service. “Publication 525, Taxable and Nontaxable Income.”

[2] Harahap, M., Rozi, F., Yennimar, Y., & Siregar, S. D. (2021). Analisis Wawasan Penjualan Supermarket dengan Data Science. Data Sciences Indonesia (DSI), 1(1), 1-7.

[3] Riza, F. (2021). Analisis dan Prediksi Data Penjualan Menggunakan Machine Learning dengan Pendekatan Ilmu Data. Data Sciences Indonesia (DSI), 1(2), 62-68.
---Ini adalah bagian akhir laporan---
