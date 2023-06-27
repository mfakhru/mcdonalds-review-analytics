# Laporan Proyek Machine Learning - Muhammad Fakhrurrozi Sutisna

## Domain Proyek

McDonald's merupakan salah satu restoran _fast food_ terbesar di dunia. Restoran ini merupakan hasil penemuan seorang pria bernama Ray Kroc pada tahun 1954 di California. Sampai saat ini, McDonald's memiliki lebih dari 36.000 restoran yang tersebar di lebih dari 100 negara [[1]](https://www.mcdonalds.com/us/en-us/about-us/about-us.html). Sehingga restoran ini sangat terkemuka dan tentu banyak orang yang tahu. 

![mcdonald](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/e4293feb-be54-470e-8421-319f3d928544)

Gambar 1. Logo McDonald's

Pada pada riset [[2]](https://ejournal.aibpmjournals.com/index.php/APJME/article/view/1070), membahas mengenai kebiasaan konsumen McDonald's selama masa pandemi. Secara singkat riset tersebut membahas tentang perubahan perilaku konsumen McDonald's selama pandemi COVID-19, termasuk perubahan dalam frekuensi kunjungan, mode pelayanan yang disukai, dan metode pembayaran yang disukai. Kemudian terdapat sebuah artikel [[3]](https://www.start.io/blog/who-is-mcdonalds-target-market-mcdonalds-brand-analysis-audience-marketing-strategy-competitors/), membahas mengenai analisis merek. Bahwa McDonald's secara garis besar selalu konsisten dan tetap kuat dengan pelayanannya. Kemudian operasional yang dilakukan selalu disesuaikan dengan lingkungan lokal. 

Berdasarkan hal tersebut menarik untuk dibahas, dengan menggunakan data yang ada pada Kaggle merupakan hasil _review_ restoran McDonald's di United States. Proyek ini akan melakukan _predictive analytics_ terhadap data McDonald's _Review Store_, juga melakukan _sentiment analysis_ serta pembuatan model dengan menggunakan metode Linear Regresi dan metode Naive Bayes. Harapannya adalah dengan adanya analisis ini akan lebih mengetahui umpan balik atau ulasan yang diberikan oleh konsumen kepada McDonald's. Sehingga McDonald's dapat selalu menjaga nilai-nilai operasional dan memperbaiki kekurangan pada restoran McDonald's yang tersebar di berbagai kota bahkan negara.


## Business Understanding

### Problem Statements
- Bagaimana _review_ konsumen terhadap McDonald's di United States?
- Berapa banyak persentase _review_ berdasarkan _rating_ bintang 1 sampai 5?
- Bagaimana presentase sentimen _review_ McDonald's di United States?

### Goals
- _Review_ konsumen terhadap McDonald's beravariasi dari rentang bintang 1 sampai 5, hal ini dapat menunjukan sebuah parameter operasional yang dijalankan oleh resotran tersebut. Sehingga dengan adanya anlisis ini akan memudahkan McDonald's untuk melihat kesuksesan penerapan operasional.
- _Review_ terbanyak berada di bintang 5, dan kemudian disusul dengan bintang 1. 
- Tingkat sentimen bervariasi berdasarkan kata-kata yang dituliskan pada _review_. Tingkat sentimen ini akan menjadi lebih mudah untuk dikategorikan daripada hanya membaca sebuah ulasan yang diberikan oleh konsumen. Maka dari itu, jika dilakukan analisis terkait tingkat sentimen, maka seharusnya akan memudahkan McDonald's melakukan evaluasi.

### Solution Statment
- Melakukan analisa dengan _exploratory data analysis_ (EDA) sehingga dapat melihat variasi _review_ dan _rating_ yang diberikan oleh konsumen terhadap McDonald's, kemudian melakukan _ploting_ data tersebut sehingga dapat terlihat visualisasi dari hasil analisis.
- Melakukan _cleansing_ data dengan tokenisasi dan normalisasi data, sehingga data yang digunakan lebih bersih dan jelas.
- Melakukan analisis dengan TextBlob untuk memeriksa tingkat sentimen dari setiap _review_ yang diberikan oleh konsumen.
- Melakukan _modeling machine learning_ dengan menggunakan metode Linear Regresi dan Naive Bayes dengan ekstraksi fitur menggunakan TF-IDF.
- Dengan beberapa _solution statment_ di atas, ini akan memberikan kemudahan bagi McDonald's untuk melakukan evaluasi mengenai operasional yang sudah diterapkan. Tingkat sentimen yang telah diolah akan dapat mengkategorikan ulasan-ulasan yang diberikan oleh konsumen.

## Data Understanding
Dataset yang digunakan merupakan _review_ konsumen terhadap restoran _fast food_ yaitu McDonald's. Sumber dataset berasal dari Kaggle dengan judul [McDonald's Store Reviews](https://www.kaggle.com/datasets/nelgiriyewithana/mcdonalds-store-_review_s). Data diunduh dengan bantuan API Kaggle. 

Berikut informasi pada dataset:
- Format CSV (Comma-Seperated Values)
- Ukuran file 8.71 MB
- Memiliki 33396 sample data dengan 10 fitur
- Memiliki 1 fitur bertipe int64, 2 fitur bertipe float64, dan 7 fitur bertipe object

Informasi selengkapnya dapat diperhatikan pada Gambar 2.

![data-info](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/aaab4454-07a8-40c9-9ee4-c934cdb7a6bf)  
Gambar 2. Informasi Data


### Variabel-variabel pada dataset McDonald's Store Reviews adalah sebagai berikut:
- reviewer_id: Kode unik untuk setiap _review_
- store_name: Berisi nama _store_ yaitu McDonald's
- category: Kategori  _store_ McDonald's
- store_address: Berisi alamat _store_
- latitude: Koordinat latitude lokasi _store_
- longitude: Koordinat longitude lokasi _store_
- rating_count: Jumlah _rating_ pada _store_
- review_time: Waktu _review_
- review: Tulisan _review_ dari konsumen
- rating: _Rating review_ terdiri dari bintang 1 sampai 5

Untuk memahami variabel-variabel tersebut dilakukan beberapa tahapan _exploratory data analysis_, yaitu dengan melihat informasi dari data yang digunakan, type data apa data tersebut seperti yang ditampilkan pada Gambar 2.

Setelah itu dilakukan analisa terhadap _rating_ yang diberikan oleh customer, berapa rata-rata, total rating, dan sebagainya. Berikut merupakan hasil analisa, yang dapat ditampilkan pada Gambar 3.

![rating-sclae-desc](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/f8ba6388-5af5-4831-87d9-a8678d9a151d)    
Gambar 3. Skala _Rating_

Berdasarkan gambar tersebut, _rating_ yang diberikan oleh konsumen terendah yaitu 1 dan tertinggi adalah 5. Kemudian untuk rata-rata _rating_ yang diberikan yaitu 3.13. Data yang digunakan yaitu untuk restoran McDonald's yang ada di United States. Pada tahap ini, yang dilakukan analisa hanya berfokus terhadap fitur _rating_. Karena fitur ini sangat cocok untuk dijadikan parameter utama.

Setelah menganalisa _rating_, selanjutnya adalah melakukan _drop_ atau membuang fitur atau kolom yang tidak digunakan seperti reviewr_id, store_name, category, karena fitur tersebut cenderung tidak memiliki banyak variasi data. Seperti yang ditampilkan pada Gambar 4 berikut.

![data-unique](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/4ae0487f-2e87-4f4f-8b94-542dbcddcaf2)  
Gambar 4. Data Unik

Terlihat bahwa pada store_name, hanya ada McDonald's dan ýýýMcDonald's yang dipastikan bahwa kedua kata tersebut adalah maksud yang sama. Kemudian pada category hanya ada _Fast food restaurant_. Sedangkan pada review_id, merupakan kode unik berupa id para konsumen yang beberikan ulasan.

Selanjutnya mengubah store_address dengan hanya mengambil alamat jalan dan nama kota. Karena berdasarkan informasi pada Gambar 5.

![store-address](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/5183f552-7f28-4ef8-a2c3-f27634439b9f)       
Gambar 5. Alamat Restoran

Berdasarkan Gambar 5 tersebut, bahwa terdapat informasi jalan, nama kota, singkatan negara bagian dan kode pos, serta negara.

Selain melihat informasi pada data yang digunakan, hal penting lainnya yang dilakukan yaitu dengan melakukan visualisasi data. Pada Gambar 6 berikut, akan ditampilkan distribusi _rating_ berdasarkan bintang. 

![hist-rating](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/c0852650-af37-49fa-af33-1f64328ec757)   
Gambar 6. Distribusi _Rating_

Berdasarkan Gambar 6 tersebut, terlihat bahwa tertinggi ada pada _rating_ bintang 5 dan selanjutkan ada pada _rating_ bintang 1. Jumlah pada setiap _rating_ akan ditampilkan pada Gambar 7.

![count-rating](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/96d4c2fc-d45c-4685-b555-0026de41df04)   
Gambar 7. Total _Rating_

Ternyata, data tersebut tidak sepenuhnya merata pada setiap retoran. Berdasarkan perhitungan, data ulasan terbanyak ada di 9814 International Dr, Orlando sebanyak 1890 ulasan dengan presentase dari total keseluruhan yaitu 5.8%. Secara lengkap akan ditampilkan pada Gambar 8 berikut ini.

![presentase-store-review](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/2ac8c700-70a1-43a3-95ac-b1ce40bc157f)   
Gambar 8. Presentase Ulasan per-Restoran

Jika dilihat dengan visualisasi, maka akan seperti pada Gambar 9 berikut.

![hist-store](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/0228a0a1-b79c-4f09-b73a-2a0025d71a48)    
Gambar 9. Distribusi Ulasan setiap Restoran

## Data Preparation
Berikut tahapan yang dilakukan untuk data _preparation_:
- Melakukan _cleansing_ data menggunakan tokenisasi, dengan melakukan tokenisasi dapat membantu mengubah ulasan konsumen menjadi kata-kata individual, frasa, atau entitas yang lebih terdefinisi. Sehingga untuk melakukan analisis lebih lanjut akan lebih baik karena kata atau frasa sudah dalam entitas yang terpisah. 
- Proses _stopwords_ menggunakan bahasa inggris, proses ini akan berguna untuk selanjutnya mengambil kata-kata penting pada setiap ulasan. Ini akan membantu menghilangkan kata-kata seperti _"a", "an", "the", "in", "is", "and"_, dan lainnya.
- Melakukan normalisasi, pada proses ini menggunakan SnowballStemmer yaitu salah satu algoritma _stemming_ yang digunakan untuk pemrosesan teks. Dengan melakukan normalisasi akan mendapatkan kata-kata yang sudah dalam bentuk standar dan seragam. Contohnya mengubah huruf besar menjadi kecil, mengganti sinonim menjadi kata standar.
- Melakukan ekstraksi fitur dengan TF-IDF, metode ini digunakan menghitung bobot kata dalam dokumen berdasarkan frekuensi kemunculan kata tersebut. Sehingga dapat membantu dalam mengidentifikasi kata-kata yang memiliki pengaruh tinggi dalam ulasan konsumen terhadap sentimen atau aspek tertentu. Kata-kata kunci yang berhubungan dengan pengalaman konsumen atau aspek tertentu akan lebih mudah didapatkan.
- Memeriksa tingkat sentimen dari data yang sudah dibersihkan, sehingga menambahkan fitur sentimen untuk nantinya akan dilakukan _modeling_. Hal tersebut dilakukan dengan bantuan _library_ TextBlob. Sehingga didapatkan tingkat sentimen pada setiap _rating_. Jika tingkat sentimen negatif maka itu merupakan hal buruk, begitu sebaliknya.
- Melakukan _split_ data latih dan data uji, dengan proporsi 85:15 agar data seimbang.

## Modeling
Setelah melakukan tahap sebelumnya sehingga data yang digunakan siap untuk membuat model, selanjutkan digunakan dua metode pembuatan model sebagai perbandingan.

- Model dengan menggunakan algoritma Linear Regression, hal tersebut karena algoritma ini mudah untuk dipahami dan data yang digunakan yaitu _true or false_ pada tingkat sentimen. Jadi cocok untuk menyelesaikan permasalahan regresi.
    
    Secara rinci fitur _review_ digunakan untuk melakukan prediksi sentimen, kemudian fitur _sentiment_ merupakan target atau label yang ingin diprediksi. Selanjutnya akan membuat model LinearRegression dengan fitur latih data yang telah dilakukan preproses dan label latih. Sehingga ini akan membangun model yang dapat mempelajari pola hubungan linier antara fitur _review_ dan label sentimen. Evaluasi model menggunakan MSE dan R2 Score membantu dalam mengukur tingkat kesalahan dan kemampuan model dalam menjelaskan variasi dalam data pengujian.
- Model dengan menggunakan algoritma Naive Bayes, hal tersebut digunakan algoritma klasifikasi ini sering digunakan dalam analisis sentimen. Selain itu, Naive Bayes adalah algoritma yang relatif sederhana dan mudah diimplementasikan.

    Secara rinci fitur yang digunakan yaitu _review_ dan _rating_. Sehingga model Naive Bayes ini sangat cocok dengan variabel diskrit seperti teks, yang sering kali mewakili frekuensi atau jumlah kemunculan suatu kata dalam teks. Selain itu Naive Bayes ini dirancang khusus untuk melakukan klasifikasi dengan lebih dari dua kelas (multikelas). Oleh karena itu, pada model Naive Bayes dalam proses melatih dan menguji model agar dapat melakukan klasifikasi _rating_ pada data _review_, perlu dilakukan evaluasi berupa akurasi dan _classification report_ memberikan informasi tentang kinerja model dalam melakukan klasifikasi.

Untuk data yang digunakan pada masing-masing model menggunakan data preparation yang sama. Hanya saja untuk data dengan algoritma Linear Regression, variable y itu menggunakan sentimen.Sedangkan untuk algoritma Naive Bayes, menggunakan _rating_.

## Evaluation
Pada bagian evaluasi, berdasarkan dua pemodelan yang dilakukan:
### 01 Metode Algoritma Linear Regression
Evaluasi dilakukan dengan melihat nilai _Mean Squared Error_ (MSE), yaitu metrik evaluasi yang digunakan untuk mengukur sejauh mana perbedaan antara nilai prediksi dan nilai sebenarnya dalam suatu model regresi. Nilai MSE yang didapatkan pada evaluasi model proyek ini yaitu 0.158485132777049. Nilai tersebut cukup bagus karena semakin rendah nilai MSE, semakin baik model regresi tersebut, karena artinya prediksi model lebih dekat dengan nilai sebenarnya.

Selain itu terdapat juga nilai R2 (R-squared), nilai ini seharusnya berkisar antara 0 hingga 1. Dan jika nilai R2 negatif menunjukkan bahwa model Anda tidak cocok dengan data dengan baik. Sayangnya pada nilai R2 ini, yaitu -0.2122069608431636.

Lebih jelas dapat dilihat pada Gambar 10.

![linear-reg](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/2e7de69e-5fc2-424f-831d-0001bf143c42)       
Gambar 10. Evaluasi Linear Regresi

### 02 Metode Algoritma Naive Bayes
Pertama yaitu nilai akurasi, dimana nilai akurasi proyek ini adalah 0.628588882101405 atau sekitar 62,86%. Ini berarti model Naive Bayes Anda berhasil memprediksi dengan benar sekitar 62,86% dari total sampel dalam dataset pengujian.

Kemudian untuk _precission_, _recall_, _f1-score_ dapat dilihat pada Gambar 11. 

![naive-bay](https://github.com/mfakhru/mcdonalds-review-analytics/assets/68620507/1ccde765-1d32-45e9-ab86-b213d17bc6ca)   
Gambar 11. Evaluasi Naive Bayes

Berdasarkan Gambar 11, dapat sedikit disimpulkan bahwa model Naive Bayes memiliki performa yang lebih baik dalam memprediksi kelas 1 _star_ dan 5 _stars_, dengan _recall_ yang tinggi. Namun, performa model tersebut kurang baik dalam memprediksi kelas 2 _stars_, 3 _stars_, dan 4 _stars_, dengan _recall_ yang rendah. Ini dikarenakan dengan adanya ketidakseimbangan dalam kualitas prediksi antara kelas-kelas tersebut. Sehingga perlu diperhatikan performa pada masing-masing kelas yaitu kelas bintang 1-5.

Maka berdasarkan dua metode tersebut yaitu Linear Regresi dan Naive Bayes, bahwa proyek _predictive analytics_ yang dilakukan terhadap data McDonald's _Review Store_ dapat dilakukan analisa _modeling_ dengan dua metode tersebut. Tergantung dengan variabel y atau label yang digunakan.

## Referensi
[1] https://www.mcdonalds.com/  
[2] L. Sudershan Reddy, Ranjith P. V., Khor Sheue Shan, Lee Xue Qi, Koh Pay San, Lim Yi Ying, Aprajita Dubey, Tharuneswar J., and Kajal Rani, "_A Study of Changes in McDonald's Consumer Behaviour during Pandemic_," Asia Pasific Journal of Management and Education (APJME), vol. 5, no. 3, pp. 103-117, Nov. 2022. [Online]. _Available_: https://ejournal.aibpmjournals.com/index.php/APJME/article/view/1070.   
[3] Admin, "_Who is McDonald’s Target Market? McDonald’s Brand Analysis – Audience, Marketing Strategy & Competitors_," start.io, September 5, 2022. [Online]. _Available_: https://www.start.io/blog/who-is-mcdonalds-target-market-mcdonalds-brand-analysis-audience-marketing-strategy-competitors/.
