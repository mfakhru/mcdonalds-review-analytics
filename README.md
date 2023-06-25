# Laporan Proyek Machine Learning - Muhammad Fakhrurrozi Sutisna

## Domain Proyek

McDonald's merupakan salah satu restoran _fast food_ terbesar di dunia. Restoran ini merupakan hasil penemuan seorang pria bernama Ray Kroc pada tahun 1954 di California. Sampai saat ini, McDonald's memiliki lebih dari 36.000 restoran yang tersebar di lebih dari 100 negara [[1]](https://www.mcdonalds.com/us/en-us/about-us/about-us.html). Sehingga restoran ini sangat terkemuka dan tentu banyak orang yang tahu. 

![mcdonald](https://github.com/mfakhru/mcdonalds-review-analytics/blob/main/pict/mcdonald.jpg)

Gambar 1. Logo McDonald's

Pada pada riset [[2]](https://ejournal.aibpmjournals.com/index.php/APJME/article/view/1070), membahas mengenai kebiasaan konsumen McDonald's selama masa pandemi. Secara singkat riset tersebut membahas tentang perubahan perilaku konsumen McDonald's selama pandemi COVID-19, termasuk perubahan dalam frekuensi kunjungan, mode pelayanan yang disukai, dan metode pembayaran yang disukai. Kemudian terdapat sebuah artikel [[3]](https://www.start.io/blog/who-is-mcdonalds-target-market-mcdonalds-brand-analysis-audience-marketing-strategy-competitors/), membahas mengenai analisis merek. Bahwa McDonald's secara garis besar selalu konsisten dan tetap kuat dengan pelayanannya. Kemudian operasional yang dilakukan selalu disesuaikan dengan lingkungan lokal. 

Berdasarkan hal tersebut menarik untuk dibahas, dengan menggunakan data yang ada pada Kaggle merupakan hasil _review_ restoran McDonald's di United States. Proyek ini akan melakukan _predictive analytics_ terhadap data McDonald's _Review Store_, juga melakukan _sentiment analysis_ serta pembuatan model dengan menggunakan metode Linear Regresi dan metode Naive Bayes. 


## Business Understanding

### Problem Statements
- Bagaimana _review_ konsumen terhadap McDonald's di United States?
- Berapa banyak persentase _review_ berdasarkan _rating_ bintang 1 sampai 5?
- Bagaimana presentase sentimen _review_ McDonald's di United States?

### Goals
- _Review_ konsumen terhadap McDonald's beravariasi dari rentang bintang 1 sampai 5.
- _Review_ terbanyak berada di bintang 5, dan kemudian disusul dengan bintang 1.
- Tingkat sentimen bervariasi berdasarkan kata-kata yang dituliskan pada _review_.

### Solution Statment
- Melakukan analisa dengan _exploratory data analysis_ (EDA) sehingga dapat melihat variasi _review_ dan _rating_ yang diberikan oleh konsumen terhadap McDonald's, kemudian melakukan _ploting_ data tersebut sehingga dapat terlihat visualisasi daripada hasil analisis.
- Melakukan _cleansing_ data dengan tokenisasi dan normalisasi data, sehingga data yang digunakan lebih bersih dan jelas.
- Melakukan analisis dengan TextBlob untuk memeriksa tingkat sentimen dari setiap _review_ yang diberikan oleh konsumen.
- Melakukan _modeling machine learning_ dengan menggunakan metode Linear Regresi dan Naive Bayes dengan ekstraksi fitur menggunakan TF-IDF.

## Data Understanding
Dataset yang digunakan merupakan _review_ konsumen terhadap restoran _fast food_ yaitu McDonald's. Data tersebut didapatkan dari Kaggle dengan judul [McDonald's Store _Review_s](https://www.kaggle.com/datasets/nelgiriyewithana/mcdonalds-store-_review_s). Data tersebut digunakan dengan cara unduh melalui API Kaggle.


### Variabel-variabel pada McDonald's Store _Review_s dataset adalah sebagai berikut:
- _review_er_id: Kode unik untuk setiap _review_
- store_name: Berisi nama _store_ yaitu McDonald's
- category: Kategori daripada store McDonald's
- store_address: Berisi alamat setiap _store_
- latitude: Koordinat latitude lokasi _store_
- longitude: Koordinat longitude lokasi _store_
- rating_count: Jumlah _rating_ pada _store_
- review_time: Waktu _review_
- review: Tulisan _review_ dari customer
- rating: _Rating review_ terdiri dari bintang 1 sampai 5

Untuk memahami variabel-variabel tersebut dilakukan beberapa tahapan _exploratory data analysis_, yaitu dengan melihat informasi dari data yang digunakan, type data apa data tersebut, setelah itu dilakukan analisa terhadap _rating_ yang diberikan oleh customer, berapa rata-rata, total rating, dan sebagainya. Kemudian melakukan drop terhadap kolom yang tidak digunakan seperti _review_r_id, store_name, category, karena dirasa kolom tersebut tidak diperlukan. Selanjutnya mengubah store_address dengan hanya mengambil alamat jalan dan nama kota. Karena berdasarkan info yang dicari dengan mencari data unik pada kolom-kolom tersebut sudah dipastikan bahwa kolom tersebut tidak begitu diperlukan. Untuk visualisasi daripada histogram dapat diperiksa pada file .ipynb.

## Data Preparation
Berikut tahapan yang dilakukan untuk data preparation:
- Melakukan cleansing data menggunakan tokenization kemudian dilanjutkan dengan stopwords bahasa inggris, dan melakukan normalisasi data. Sehingga data yang dimiliki akan lebih bersih.
- Memeriksa tingkat sentiment dari data yang sudah dibersihkan, sehingga menambahkan kolom sentiment untuk nantinya akan dilakukan modeling. Hal tersebut dilakukan dengan bantuan library TextBlob. Sehingga kita mendapatkan tingkat sentiment pada setiap rating. Jika tingkat sentiment negatif maka itu merupakan hal buruk, begitu sebaliknya.
- Melakukan split data train dan data test, dengan proporsi 85:15 agar data seimbang.
- Melakukan ekstraksi fitur dengan TF-IDF.

## Modeling
Setelah melakukan tahap sebelumnya sehingga data yang digunakan siap untuk membuat model, selanjutkan digunakan dua metode pembuatan model sebagai perbandingan.

- Model dengan menggunakan algoritma Linear Regression, hal tersebut karena algoritma ini mudah untuk dipahami dan data yang digunakan yaitu true or false pada tingkat sentiment. Jadi cocok untuk menyelesaikan permasalahan regresi.
- Model dengan menggunakan algoritma Naive Bayes, hal tersebut digunakan algoritma klasifikasi ini sering digunakan dalam analisis sentiment. Selain itu, Naive Bayes adalah algoritma yang relatif sederhana dan mudah diimplementasikan.

Untuk data yang digunakan pada masing-masing model menggunakan data preparation yang sama. Hanya saja untuk data dengan algoritma Linear Regression, variable y itu menggunakan sentiment.Sedangkan untuk algoritma Naive Bayes, menggunakan rating.

## Evaluation
Pada bagian evaluasi, berdasarkan dua pemodelan yang dilakukan:
### 01 Metode Algoritma Linear Regression
Evaluasi dilakukan dengan melihat nilai Mean Squared Error (MSE), yaitu metrik evaluasi yang digunakan untuk mengukur sejauh mana perbedaan antara nilai prediksi dan nilai sebenarnya dalam suatu model regresi. Nilai MSE yang didapatkan pada evaluasi model proyek ini yaitu 0.158485132777049. Nilai tersebut cukup bagus karena semakin rendah nilai MSE, semakin baik model regresi tersebut, karena artinya prediksi model lebih dekat dengan nilai sebenarnya.

Selain itu terdapat juga nilai R2 (R-squared), nilai ini seharusnya berkisar antara 0 hingga 1. Dan jika nilai R2 negatif menunjukkan bahwa model Anda tidak cocok dengan data dengan baik. Sayangnya pada nilai R2 ini, yaitu -0.2122069608431636.

### 02 Metode Algoritma Naive Bayes
Pertama yaitu nilai akurasi, dimana nilai akurasi proyek ini adalah 0.628588882101405 atau sekitar 62,86%. Ini berarti model Naive Bayes Anda berhasil memprediksi dengan benar sekitar 62,86% dari total sampel dalam dataset pengujian.

Kemudian untuk precission, recall, f1-score dapat dilihat pada file .ipynb. Namun dapat sedikit disimpulkan bahwa model Naive Bayes memiliki performa yang lebih baik dalam memprediksi kelas 1 star dan 5 stars, dengan recall yang tinggi. Namun, performa model tersebut kurang baik dalam memprediksi kelas 2 stars, 3 stars, dan 4 stars, dengan recall yang rendah. Ini dikarenakan dengan adanya ketidakseimbangan dalam kualitas prediksi antara kelas-kelas tersebut. Sehingga perlu diperhatikan performa pada masing-masing kelas yaitu kelas bintang 1-5.

## Referensi
[1] https://www.mcdonalds.com/  
[2] https://ejournal.aibpmjournals.com/index.php/APJME/article/view/1070   
[3] https://www.start.io/blog/who-is-mcdonalds-target-market-mcdonalds-brand-analysis-audience-marketing-strategy-competitors/
