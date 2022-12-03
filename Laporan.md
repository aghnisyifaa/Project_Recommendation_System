# Laporan Proyek Machine Learning Terapan (Predictive_Analytics)- Aghni Syifa Ahmari

## Domain Proyek

Film merupakan media hiburan favorit bagi semua kalangan. Menonton film menjadi aktivitas untuk melepas penat dan dapat dilakukan bersama orang-orang terkasih. Namun tidak sedikit masyarakat yang merasa kewalahan saat menentukan film mana yang akan ditonton karena banyaknya film yang tersedia sampai saat ini.  Untuk mengatasi masalah tersebut, perlu adanya informasi mengenai film yang akan memudahkan masyarakat untuk menemukan film yang cocok dengan preferensinya sebagai user. Oleh sebab itu, user perlu sebuah sistem rekomendasi. Sistem rekomendasi adalah suatu cara yang dapat memberikan informasi atau rekomendasi yang sesuai dengan kesukaan pengguna berdasarkan informasi yang didapat dari pengguna tersebut.

## Business Understanding

### Problem Statements

Berdasarkan latar belakang yang telah dijelaskan diatas, terdapat beberapa masalah yaitu:
- Bagaimana membuat sistem rekomendasi film yang dipersonalisasi dengan teknik *content-based filtering* berdasarkan data pengguna?
- Bagaimana merekomendasikan film lain yang mungkin disukai dan belum pernah ditonton oleh pengguna berdasarkan rating? 

### Goals

Untuk menjawab masalah yang ada, akan dibuat model prediksi dengan tujuan sebagai berikut:
- Menampilkan rekomendasi film yang dipersonalisasi untuk pengguna dengan teknik *content-based filtering*.
- Menampilkan rekomendasi film yang sesuai dengan preferensi pengguna dan belum pernah ditonton sebelumnya dengan teknik *collaborative filtering*.

### Solution statements
Solusi yang dapat dilakukan untuk sistem rekomendasi film dengan menggunakan 2 algoritma *machine learning* yaitu:
- ***Content-based filtering*** : merekomendasikan item yang mirip dengan item yang disukai pengguna di masa lalu. Algoritma ini bekerja dengan menyarankan item serupa yang pernah disukai di masa lalu atau sedang dilihat di masa kini kepada pengguna. Semakin banyak informasi yang diberikan pengguna, semakin baik akurasi sistem rekomendasi.
- ***Collaborative filtering*** : merekomendasikan item dengan bergantung pada pendapat komunitas pengguna.

Algoritma *content based filtering* digunakan untuk merekomendasikan film berdasarkan aktivitas pengguna pada masa lalu, sedangkan algoritma *collaborative filtering* digunakan untuk merekomendasikan film berdasarkan *rating* yang paling tinggi.

## Data Understanding
Data atau dataset yang digunakan pada proyek *machine learning* ini adalah data *Movie Recommendation* dataset yang didapat dari situs Kaggle. Dataset ini berisikan informasi mengenai film dari tahun 1996 sampai 2016. 
Terdapat 4 file data dalam dataset. 
Sumber dataset : [*Movie Recommendation* Dataset](https://www.kaggle.com/datasets/bandikarthik/movie-recommendation-system).

### Dataset ini terdiri dari beberapa dataset berikut:

* links : daftar link film.
* movies : daftar film.
* ratings : daftar penilaian yang diberikan pengguna terhadap film.
* tags : daftar kata kunci dari film tersebut

Untuk memahami *Movie Recommendation* dataset akan menggunakan beberapa teknik *Univariate Explanatory Data Analysis (EDA)* pada variabel-variabel berikut:
1.   Dataset *links*

Dataset links memiliki jumlah data sebanyak 34208 data dan jumlah data link film yang unik berdasarkan movieId sebanyak 34208 data. Info Dataset links dapat dilihat pada tabel 1 berikut :

Tabel 1. Info dataset links

| # | Column  | Non-Null Count | Dtype   |
|---|---------|----------------|---------|
| 0 | movieId | 34208 non-null | int64   |
| 1 | imdbId  | 34208 non-null | int64   |
| 2 | tmdbId  | 33912 non-null | float64 |

Pada Tabel 1, dapat dilihat bahwa:

* Terdapat 2 buah kolom bertipe int64 yaitu movieId dan imdbId
* Terdapat 1 buah kolom bertipe float64 yaitu tmdbId

2.   Dataset *movies*

Dataset movies memiliki total jumlah data sebanyak 34208 dan jumlah data movies unik berdasarkan movieId sebanyak 34208. Terdapat judul film sebanyak 34185 judul dan 1446 genre yang berbeda. Info Dataset movies dapat dilihat pada tabel 2 berikut :

Tabel 2. Info Dataset movies

| # | Column  | Non-Null Count | Dtype  |
|---|---------|----------------|--------|
| 0 | movieId | 34208 non-null | int64  |
| 1 | title   | 34208 non-null | object |
| 2 | genres  | 34208 non-null | object |


Pada Tabel 2, dapat dilihat bahwa:

* Terdapat 1 buah kolom bertipe int64 yaitu movieId
* Terdapat 2 buah kolom bertipe object yaitu title dan genres

3.   Dataset *ratings*

Dataset ratings memiliki jumlah data sebanyak 22884377 data. Karena data terlalu banyak, maka data yang akan digunakan hanya 10000 data saja. Jumlah data unik ratings dari user sebanyak 106 data, dan dari film sebanyak  3466 data. Info Dataset ratings dapat dilihat pada tabel 3 berikut:

Tabel 3. Info Dataset ratings

| # | Column    | Dtype   |
|---|-----------|---------|
| 0 | userId    | int64   |
| 1 | movieId   | int64   |
| 2 | rating    | float64 |
| 3 | timestamp | int64   |

Pada Tabel 3, dapat dilihat bahwa:

* Terdapat 3 buah kolom bertipe int64 yaitu userId, movieId dan timestamp
* Terdapat 1 buah kolom bertipe float64 yaitu rating

Deskripsi dari variabel ratings dapat dilihat pada tabel 4 berikut:

Tabel 4. Deskripsi Dataset ratings

|       |       userId |     movieId |       rating |    timestamp |
|------:|-------------:|------------:|-------------:|-------------:|
| count | 10000.000000 |  10000.0000 | 10000.000000 | 1.000000e+04 |
|  mean |    49.805200 |  10429.1596 |     3.460650 | 1.130739e+09 |
|  std  |    30.826058 |  21014.5552 |     1.170348 | 1.623057e+08 |
|  min  |     1.000000 |      1.0000 |     0.500000 | 8.345235e+08 |
|  25%  |    20.000000 |   1089.0000 |     3.000000 | 9.746870e+08 |
|  50%  |    45.000000 |   2398.0000 |     3.500000 | 1.137894e+09 |
|  75%  |    74.000000 |   5460.2500 |     4.000000 | 1.284972e+09 |
|  max  |   106.000000 | 141956.0000 |     5.000000 | 1.452383e+09 |

Pada tabel 4, dapat dilihat dari nilai max dan min bahwa nilai nilai rating terkecil yaitu 0.5 dan nilai rating terbesar yaitu 5

4.   Dataset tags

Variabel tags memiliki jumlah data sebanyak 586994 data. Karena data terlalu banyak, maka data yang akan digunakan hanya 10000 data saja. Info Dataset tags dapat dilihat pada tabel 4 berikut:

Tabel 5. Info Dataset tags

| # |    Column |  Non-Null Count |  Dtype |
|--:|----------:|----------------:|-------:|
| 0 |    userId | 586994 non-null |  int64 |
| 1 |   movieId | 586994 non-null |  int64 |
| 2 |       tag | 586978 non-null | object |
| 3 | timestamp | 586994 non-null |  int64 |

## Data Preparation
Dalam proses persiapan data dibagi menjadi 2 berdasarkan algoritma yang digunakan yaitu pada *content-based filtering* dan *collaborative filtering* . Berikut tahapan-tahapan persiapan data:
***Content-based filtering***

- **Menangani *missing value*** : mengecek data yang kosong. Untuk menghindari bias, missing value tidak diisi dengan modus. Maka missing value akan di hapus menggunakan fungsi dropna
- **Mengurutkan data** : mengurutkan data secara *ascending*.
- **Menangani duplikat data** : Menghapus data yang duplikat dengan fungsi drop_duplicates(). 
- **Konversi data menjadi list** : Melakukan konversi data *series* menjadi *list* menggunakan fungsi tolist() dari *library numpy*. Hal ini dilakukan untuk menyederhanakan data menjadi bentuk *list*.
- **Membuat Dictionary** : Membuat *dictionary* untuk menentukan pasangan *key-value* pada data movie_id, movie_name, dan movie_genre yang telah disiapkan sebelumnya. Hal ini dilakukan untuk persiapan data sebelum model dilatih.


***Collaborative filtering***

- ***Encode*** **fitur userId dan movieId** : Melakukan persiapan data untuk menjadikan (*encode*) fitur ‘userId’ dan ‘movieID’ ke dalam indeks integer. H
- **Memetakan userId dan movieId** : Memetakan userId dan movieId ke dataframe yang berkaitan. Hal ini diperlukan agar data yang sudah di *encode* dipetakan kemudian dimasukan kedalam dataframe yang berkaitan.
- **Cek data dan ubah nilai rating**: cek beberapa hal dalam data seperti jumlah *user*, jumlah *movie*, dan mengubah nilai *rating* menjadi *float*, cek nilai *minimum* dan *maximum*. Hal ini dilakukan untuk mengecek data yang sudah siap digunakan untuk pemodelan.
- **Membagi data untuk latih dan validasi** : Membagi dataset menjadi data latih dan data validasi dengan perbandingan 80:20 yaitu 80 persen data akan menjadi data latih dan 20 persen data akan menjadi data validasi . Hal ini dilakukan supaya kita dapat melakukan validasi dengan benar tanpa bias dari model.

## Modeling

Pada tahap ini, model *machine learning* yang akan dipakai ada 2 algoritma. Berikut algoritma yang akan digunakan:

1.   *Content-based filtering* : algoritma *content-based filtering* dibuat dengan apa yang disukai pengguna pada masa lalu.
		- **kelebihan** : Model tidak memerlukan data tentang pengguna lain, karena rekomendasi bersifat khusus untuk pengguna ini. Hal ini mempermudah penskalaan ke sejumlah besar pengguna.
		- **kekurangan** : Model hanya dapat membuat rekomendasi berdasarkan minat pengguna yang ada. Dengan kata lain, model memiliki kemampuan terbatas untuk memperluas minat pengguna yang ada.
2.   *Collaborative filtering* : algoritma *collaborative filtering* dibuat dengan memanfaatkan tingkat *rating* dari film tersebut. 
		- **kelebihan** : Tidak memerlukan pengetahuan domain dan model dapat membantu pengguna menemukan minat baru..
		- **kekurangan** :Tidak dapat menangani item baru dan sulit menyertakan fitur samping untuk kueri/item.

Hasil dari masing-masing model:

1. ***Content-based filtering***

Berikut adalah film yang disukai pengguna di masa lalu:

Tabel 6. Film yang disukai pengguna di masa lalu.

|   | id |     movie_name |                        genre |
|--:|---:|---------------:|-----------------------------:|
| 1 |  2 | Jumanji (1995) | Adventure|Children|Fantasy |

Pada tabel 6, dapat dilihat bahwa pengguna menyukai film yang berjudul *Jumanji (1995)* yang bergenre *Adventure, Children, dan Fantasy*. Maka hasil 5 rekomendasi terbaik berdasarkan algoritma *content-based filtering* adalah sebagai berikut :

Tabel 7. Hasil rekomendasi algoritma *content-based filtering*

|   |                                       movie_name |                        genre |
|--:|-------------------------------------------------:|-----------------------------:|
| 0 |                              Return to Oz (1985) | Adventure\|Children\|Fantasy |
| 1 | Chronicles of Narnia: Prince Caspian, The (2008) | Adventure\|Children\|Fantasy |
| 2 |                       Golden Compass, The (2007) | Adventure\|Children\|Fantasy |
| 3 |                    NeverEnding Story, The (1984) | Adventure\|Children\|Fantasy |
| 4 |        Darby O'Gill and the Little People (1959) | Adventure\|Children\|Fantasy |

Dapat dilihat pada tabel 7, ada 5 film yang direkomendasikan bergenre yang sama yaitu *Adventure, Children, Fantasy*. Hal ini didasarkan pada kesukaan penonton atau pengguna pada masa lalu.

2. ***Collaborative filtering***

Berikut merupakan film berdasarkan *rating* yang ada :

![Capture](https://user-images.githubusercontent.com/89571899/205448050-b5772d04-0c25-4e00-ab86-cbfc223cd528.PNG)


Gambar 1. Hasil rekomendasi algoritma *collaborative filtering*

Pada Gambar 1, film yang memiliki *rating* tinggi dari pengguna paling banyak bergenre *Crime, Mystery, Thriller*. Dan hasil rekomendasi juga menunjukan 10 film dengan genre *Crime, Mystery, Thriller*.

## Evaluation
Hasil evaluasi dari masing-masing model:

1. ***Content-based filtering***

Film yang direkomendasikan di masa lalu yaitu film Jumanji (1995) dengan genre Adventure, Children, dan Fantasy. Top 5 item hasil rekomendasi film semua memilki genre yang sama atau *relevant* yaitu Adventure, Children, dan Fantasy. Maka hasil rekomendasi dapat dievaluasi menggunakan rumus presisi berikut :

*recommender system precision*: P = $\frac{n of our recommendations that are relevant}{n of items we recommended}$

Dengan begitu hasil presisi yang didapat adalah 100 persen .

2.  ***Collaborative filtering***

Evaluasi metrik yang digunakan untuk mengukur kinerja model adalah metrik RMSE (Root Mean Squared Error). RMSE adalah metode pengukuran dengan mengukur perbedaan nilai dari prediksi sebuah model sebagai estimasi atas nilai yang diobservasi. Root Mean Square Error adalah hasil dari akar kuadrat Mean Square Error. Keakuratan metode estimasi kesalahan pengukuran ditandai dengan adanya nilai RMSE yang kecil. Metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih kecil dikatakan lebih akurat daripada metode estimasi yang mempunyai Root Mean Square Error (RMSE) lebih besa


Rumus dari matriks RMSE adalah sebagai berikut:

MSE = $\sqrt{\frac{1}{n} \Sigma_{i=1}^n({y}-\hat{y})^2}$

Dimana :

y = Nilai Aktual permintaan

$\hat{y}$ = Nilai hasil peramalan

n = banyaknya data

Berikut visualisasi RMSE menggunakan *collaborative filtering*:

![Capture](https://user-images.githubusercontent.com/89571899/205448366-1477f18b-1ceb-4175-95c8-7e436cb2c45b.PNG)

Gambar 2. Visualisasi RMSE 

Bisa dilihat pada Gambar 2. hasilnya nilai error akhir sebesar sekitar 0.15 dan error pada data validasi sebesar 0.24.


**Kesimpulan** :  Model yang dibangun menghasilkan 5 rekomendasi film terbaik menggunakan teknik *content-based filtering* dengan presisi 100 persen dan berhasil menghasilkan 10 rekomendasi terbaik menggunakan teknik *collaborative filtering* dengan RMSE sebesar 0.15 .

**Referensi** :

[1]	Ichwanto Hadi, dkk (2020).“Sistem Rekomendasi Film menggunakan User-based Collaborative Filtering dan K-modes Clustering”. Jurnal Infra, Vol 8, No 1 (2020).

		
**---Ini adalah bagian akhir laporan---**


