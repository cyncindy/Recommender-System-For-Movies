# Laporan Proyek Machine Learning - Sistem Rekomendasi Film (Movie)

## Domain Proyek

Salah satu jenis hiburan bersifat visual yang sangat disukai masyarakat adalah film. Dengan munculnya berbagai judul film yang tak terbatas, perkembangannya terutama di era modern ini mulai berkembang pesat. Hal ini menyebabkan kesulitan bagi segelintir masyarakat untuk mencari judul film. Oleh karena itu, telah dikembangkan berbagai macam sistem, dimana salah satunya adalah sistem rekomendasi yang digunakan untuk membantu masyarakat mencari judul film dengan mudah dan cepat [[1](https://lintar.untar.ac.id/repository/penelitian/buktipenelitian_10390001_7A281222103549.pdf)].

Sistem rekomendasi merupakan salah satu fitur perangkat lunak yang sangat bermanfaat dalam memudahkan pengguna. Karena banyaknya jenis dan jumlah data yang ada, sistem rekomendasi sendiri sangat penting [[2](https://core.ac.uk/download/pdf/299917962.pdf)]. Dalam rangka mengambil keputusan untuk memilih rekomendasi film yang paling sesuai untuk ditonton, maka pengembangan sistem rekomendasi film akan sangat membantu pengguna untuk menentukan film yang ditonton. Salah satu contoh penerapannya adalah kemampuan untuk membantu pengguna menemukan film berdasarkan pada genre film yang telah ditonton sebelumnya. 

Pada pengembangan model sistem rekomendasi, faktor yang ditentukan dapat mencakup genre film yang telah ditonton pengguna sebelumnya, dan lebih jauh lagi dapat didasarkan pula pada rating yang telah diberikan oleh pengguna pada film yang telah ditonton. Pada proyek ini, faktor-faktor tersebut akan digunakan sebagai acuan pembuatan model berbasis Content-Based Filtering dan juga Collaborative Filtering. Algoritma yang digunakan pada perancangan model Content-Based Filtering adalah Cosine Similarity dan K-Nearest Neighbor, sedangkan untuk algoritma pada perancangan Collaborative Filtering adalah Matrix Factorization dengan pendekatan Singular Value Decomposition (SVD).

## Business Understanding

Berdasarkan proyek yang dikerjakan, tujuan utamanya adalah untuk memberikan rekomendasi film yang sesuai dengan preferensi pengguna. Ini merupakan hal yang penting bagi perusahaan dalam rangka meningkatkan penjualan dan memperbaiki pelayanan kepada pengguna, sedangkan untuk pengguna, sistem rekomendasi dapat membantu menemukan produk atau layanan yang relevan dan tepat untuk kebutuhan mereka.

### Problem Statements

- Bagaimana cara membuat sistem rekomendasi film yang mengikuti perilaku, minat, dan preferensi pengguna?

- Bagaimana hasil dan evaluasi model saat membuat sistem rekomendasi film yang sesuai dengan preferensi, minat, atau perilaku pengguna?

### Goals

- Mengetahui cara mengembangkan sistem rekomendasi film yang sesuai dengan preferensi, minat dan perilaku pengguna.

- Mengetahui hasil dan evaluasi model yang didasarkan pada pembuatan sistem rekomendasi film yang berdasar pada preferensi, minat, dan perilaku pengguna.

### Solution Statements

- Dilakukan preprocessing data dan juga Exploratory Data Analysis (EDA) pada dataset yang digunakan untuk melihat keterkaitan antar fitur pada dataset dalam rangka memperoleh wawasan dan pengetahuan dari dataset.

- Dilakukan pengembangan model machine learning yang sesuai untuk perancangan sistem rekomendasi yang nantinya akan dievaluasi menggunakan evaluation matrix. Model yang dibuat berbasis Content-Based Filtering akan digunakan untuk merekomendasikan beberapa item berdasarkan kemiripan antar item yang direkomendasikan terhadap item yang dipilih, dan Collaborative Filtering akan digunakan untuk memberikan rekomendasi item berdasarkan preferensi pengguna berdasarkan rating yang telah diberikan sebelumnya. Hasil rekomendasi kemudian akan ditampilkan dan dilakukan evaluasi yang berdasarkan pada hasil metrik evaluasi yang digunakan.

## Data Understanding

Pada proyek ini, dataset yang digunakan adalah data sekunder yang diperoleh dari Kaggle dengan nama Movie Recommender System Dataset.

Link Dataset: https://www.kaggle.com/datasets/gargmanas/movierecommenderdataset

Dataset ini berformat zip yang memiliki 2 file terpisah diantaranya `movies.csv` dan `ratings.csv`. Dataset ini merupakan dataset yang berisi data movies dan rating yang telah diberikan oleh pengguna.

### Variabel-variabel pada dataset adalah sebagai berikut:

Terdapat tiga fitur yang dapat dilihat pada file `movies.csv` yaitu:

- *movieId*: ID unik untuk setiap movie
- *title*: judul movie
- *genres*: genre movie

Terdapat empat fitur yang dapat dilihat pada file `ratings.csv` yaitu:

- *userId*: ID pengguna yang memberikan rating
- *movieId*: ID film yang diberikan rating
- *rating*: rating yang diberikan oleh pengguna
- *timestamp*: waktu dimana peringkat telah diberikan

Dilakukan juga Analisis Univariat untuk memahami data lebih lanjut, serta dilakukan pula Visualisasi Data agar informasi pada data dapat dengan mudah dipahami.

Berikut adalah hasil dari Exploratory Data Analysis (EDA) yang telah dilakukan.

## Exploratory Data Analysis (EDA)

Proses ini dilakukan guna menganalisis dataset dalam rangka memperoleh pemahaman yang utuh terhadap dataset agar mendapatkan wawasan dan pengetahuan dari dataset.

### Univariate Analysis

Sebelumnya telah diketahui bahwa pada dataset terdapat dua berkas file berformat csv. Dua berkas file csv tersebut akan dibagi menjadi tiga data secara umum berdasarkan pada info yang diperoleh dari movie. Setelah itu akan diperoleh hasil berupa jumlah data dari kategori yang telah dianalisis.

- Diperoleh jumlah data movie sebesar 9.742
- Pengguna yang memberikan peringkat terhadap film berjumlah 610
- Data keseluruhan movie yang telah diberikan peringkat sebesar 9.724

Berdasarkan informasi yang diperoleh tersebut, terdapat 9.742 data unik movie, 610 data pengguna yang memberikan rating, dan 9.724 data unik movie yang telah diberikan peringkat. Setelah diperoleh informasi tersebut, maka selanjutnya akan dilakukan pemrosesan data.

## Data Preparation

Tahap ini sangat penting dalam proses pengembangan model machine learning karena disini proses transformasi data akan dilakukan sehingga bentuknya sesuai untuk proses pemodelan. Pada tahapan ini dilakukan beberapa proses seperti Data Gathering, Data Assessing, dan juga Data Cleaning.

Proses Data Gathering yang dilakukan adalah pada saat dimana data diimpor menggunakan library dataframe pandas agar dapat dibaca dengan baik.

Data Gathering telah dilakukan sebelumnya pada tahap awal, dan selanjutnya dilakukan pula proses Data Assessing, yaitu:

1. Melakukan pengecekan missing value yang digunakan untuk melihat apakah ada data atau informasi yang hilang atau tidak tersedia.

2. Melakukan pengecekan data duplikat (duplicate values).

Selanjutnya dilakukan tahap pembersihan data (Data Cleaning). Berikut adalah langkah-langkah yang dilakukan:

1. Menghapus atau menghilangkan data null menggunakan metode dropping.

2. Melakukan penggabungan data movies dan ratings, dimana penggabungan dilakukan dengan melakukan merge pada kedua dataframe movies dan ratings menjadi satu dataframe yang lengkap pada variabel all_movies.

## Modeling

Dalam mengerjakan proyek ini, pendekatan yang digunakan dalam pengembangan model sistem rekomendasi adalah Content-Based Filtering dan Collaborative Filtering. 

### Content-Based Filtering (Cosine Similarity)

Content based filtering bekerja dengan melibatkan analisis isi suatu item dan mencari persamaan antara konten tersebut dengan konten item lainnya. Contohnya, Budi menyukai film Spiderman maka sistem akan merekomendasikan film dengan genre action lainnya seperti Batman. Perlu diketahui juga bahwa semakin banyak informasi yang didapatkan melalui aktivitas pengguna maka semakin baik pula akurasi sistem rekomendasi yang dibangun.

Berdasarkan pendekatan Content-Based Filtering dalam membangun model sistem rekomendasi yang telah dijalankan, dilakukan beberapa tahapan sebagai berikut:

1. Prepare Data

Proses ini melibatkan persiapan dataframe yang telah dilakukan cleaning pada tahap data preparation sebelumnya.

2. TF-IDF Vectorizer

Teknik ini digunakan pada sistem rekomendasi untuk menemukan representasi fitur penting dari setiap kategori genre. Digunakan fungsi tfidfvectorizer() yang telah tersedia pada library scikit-learn. Hasil TF-IDF dalam bentuk matrix menunjukkan korelasi antara movie dengan genre movie tersebut.

3. Menghitung Cosine Similarity

Cosine Similarity menghitung kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Cosine Similarity menghitung sudut cosinus antara dua vektor, dimana semakin kecil sudut cosinus maka semakin besar nilai Cosine Similarity. Pada proyek ini, perhitungan similarity dilakukan dengan menerapkan function cosine_similarity() yang diperoleh dari library sklearn. Dalam pendekatan Content-Based Filtering, perhitungan kesamaan merupakan tahapan paling penting karena metode tersebut menggunakan prinsip kesamaan antar item dalam rangka menghasilkan rekomendasi yang tepat.

4. Mendapatkan Rekomendasi

Pada tahap ini, rekomendasi akan diperoleh dengan membangun custom function untuk mendapatkan rekomendasi terhadap data input yang diinginkan. Pertama-tama, similarity dari data film yang akan dicari diambil lalu data yang mirip akan dimasukkan ke dalam variabel closest. Top-N recommendation yang dihasilkan oleh sistem akan didefinisikan dalam parameter k dimana hasil akhirnya berupa sejumlah movie yang direkomendasikan berdasarkan tingkat similarity tertinggi. Movie yang dicari akan dihapus agar tidak muncul dalam daftar rekomendasi. Langkah terakhir yaitu return value digunakan untuk mengembalikan nilai dalam bentuk dataframe dimana values yang dikembalikan berupa rekomendasi judul film berdasarkan tingkat kesamaan (similarity).

Berikut adalah hasil output yang diperoleh:

|     |movie_name|genre|
|---|---|---|
|0|Furious 7 (2015)|Action, Crime, Thriller|
|1|Crimson Rivers 2: Angels of The Apocalypse|Action, Crime, Thriller|
|2|Dirty Harry (1971)|Action, Crime, Thriller|
|3|Takers (2010)|Action, Crime, Thriller|
|4|Natural Born Killers (1994)|Action, Crime, Thriller|

Setelah semua langkah-langkah tersebut dilakukan, maka diperoleh Top 5 Movies Recommendations berdasarkan genre movie 'John Wick: Chapter Two (2017)'. Dengan demikian, sistem telah sukses memberikan rekomendasi film yang sesuai, dan dapat dilihat pada hasil yang diperoleh yaitu bahwa sistem memberikan rekomendasi movie yang mirip dengan genre Action|Crime|Thriller.

### Content-Based Filtering (K-Nearest Neighbor)

1. Impor KNeighborsClassifier

Dilakukan impor library KNeighborsClassifier dari sklearn.neighbors, dimana KNeighborsClassifier adalah kelas yang digunakan untuk melakukan klasifikasi berdasarkan K-Nearest Neighbors.

2. Pembuatan Matriks Fitur dan Label

- X dibuat dari matriks TF-IDF yang diubah formatnya menjadi array numpy. Matriks TF-IDF tersebut menggambarkan kemiripan antara setiap movie pada dataset.
- y merupakan label yang berisi nama film.

3. Inisialisasi KNN

- Membuat instance dari KNeighborsClassifier dengan nilai n_neighbors=5, yang berarti model akan mencari 5 movie terdekat untuk setiap dari nilai movie yang diberikan.

4. Pelatihan Model

Dilakukan pelatihan model KNN dengan X sebagai fitur dan y sebagai label.

5. Mendapatkan rekomendasi

Fungsi knn_movie_recommendations dibuat untuk mendapatkan rekomendasi film berdasarkan film yang diberikan. Fungsi ini menerima dua parameter yaitu nama_movie yang merupakan nama film yang ingin diberikan rekomendasi, dan k yang merupakan jumlah tetangga terdekat dari film yang dicari, dimana pada umumnya nilai k adalah 5. Fungsi tersebut juga digunakan untuk mengambil nama film yang paling mirip dari hasil prediksi, kecuali film itu sendiri, dimana dataframe movie_new juga akan digunakan untuk mendapatkan genre dari film yang paling mirip lalu fungsi akan mengembalikan dataframe yang berisi nama film yang paling mirip dan genre film tersebut.

Berikut adalah hasil output yang diperoleh:

|     |movie_name|genre|
|---|---|---|
|33|Batman (1989)|Action, Crime, Thriller|
|227|Shaft (2000)|Action, Crime, Thriller|
|234|Kill Bill: Vol. 1 (2003)|Action, Crime, Thriller|
|531|Die Hard: With a Vengeance (1995)|Action, Crime, Thriller|
|539|Net, The (1995)|Action, Crime, Thriller|

Setelah semua langkah-langkah tersebut dilakukan, maka diperoleh Top 5 Movies Recommendations berdasarkan genre movie 'John Wick: Chapter Two (2017)'. Dengan demikian, sistem telah sukses memberikan rekomendasi film yang sesuai, dan dapat dilihat pada hasil yang diperoleh yaitu bahwa sistem memberikan rekomendasi movie yang mirip dengan genre Action|Crime|Thriller.

Kelebihan Algoritma Content-Based Filtering, yaitu:

- Menganalisis konten item yang disarankan untuk melihat apakah ada hubungannya dengan konten item yang telah dikunjungi atau disukai oleh pengguna. Hal ini memungkinkan sistem untuk memberikan rekomendasi yang lebih personal dengan preferensi pengguna dan lebih relevan [[3](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163)].

- Tidak memerlukan data tentang interaksi pengguna dengan item lain, sehingga membuat algoritma ini lebih privat dan tidak memerlukan pengguna untuk memberikan feedback atau menilai item [[4](https://dspace.uii.ac.id/bitstream/handle/123456789/35942/17523144%20Muhammad%20Rizqi%20Az%20Zayyad.pdf?sequence=1&isAllowed=y)].

Kekurangan Algoritma Content-Based Filtering, yaitu:

- Kurang fleksibel dalam menangani variasi konten yang luas. Misalnya, jika konten item berubah secara signifikan seiring waktu, algoritma ini mungkin tidak dapat menangkap perubahan tersebut dengan efektif [[3](https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/view/9163)].

- Jika konten baru diperkenalkan, maka algoritma ini mungkin tidak dapat memberikan rekomendasi yang relevan karena belum ada data yang cukup untuk menganalisis konten baru tersebut [[4](https://dspace.uii.ac.id/bitstream/handle/123456789/35942/17523144%20Muhammad%20Rizqi%20Az%20Zayyad.pdf?sequence=1&isAllowed=y)].

- Sangat bergantung pada kualitas dan kejelasan konten. Jika konten tidak jelas atau kurang informatif, maka algoritma ini mungkin tidak dapat memberikan rekomendasi yang akurat [[5](https://repository.uinjkt.ac.id/dspace/bitstream/123456789/55992/1/ADDINI%20YUSMAR-FST.pdf)].

### Collaborative Filtering

Collaborative Filtering adalah teknik yang digunakan dalam sistem rekomendasi untuk membuat prediksi otomatis terhadap minat pengguna dan mengumpulkan preferensi atau rasa dari banyak pengguna. Hal ini didasarkan pada asumsi bahwa jika seseorang A memiliki pendapat yang sama dengan seseorang B terhadap suatu isu, maka A lebih mungkin memiliki pendapat B tentang isu yang berbeda daripada pendapat seseorang yang dipilih secara acak. Pendekatan ini berpusat pada hubungan antara pengguna dan item, dengan menentukan kesamaan item berdasarkan kesamaan penilaian item oleh pengguna yang telah menilai kedua item tersebut. Sistem rekomendasi berbasis Collaborative Filtering yang dibangun menggunakan teknik Singular Value Decomposition (SVD) untuk mencari hubungan antara item (film) berdasarkan preferensi pengguna yang telah menilai kedua item tersebut.

Berdasarkan pendekatan Collaborative Filtering dalam membangun model sistem rekomendasi yang telah dijalankan, dilakukan beberapa tahapan sebagai berikut:

1. Impor library

Mengimpor library yang diperlukan untuk analisis data dan operasi matematika.

2. Membaca Dataset

Membaca dataset ratings yang berisi informasi tentang rating yang diberikan pengguna untuk film.

3. Encoding userId dan movieId

Mengubah userId dan movieId menjadi list unik dan melakukan encoding untuk mengubahnya menjadi indeks numerik dalam rangka mempermudah operasi matematika dan pemrosesan data.

4. Membuat Matriks Rating

Mengisi matriks rating dengan rating yang ada dalam dataset, dimana nantinya rating tersebut akan digunakan sebagai input untuk algoritma SVD.

5. Melakukan SVD

Menggunakan fungsi svds dari scipy.sparse.linalg untuk melakukan Singular Value Decomposition pada matriks rating yang membagi matriks rating menjadi tiga komponen yaitu matriks U, vektor sigma, dan matriks Vt.

6. Mencari Nilai k Terbaik

Melakukan iterasi untuk mencari nilai k (jumlah komponen utama) yang memberikan Mean Squared Error (MSE) terkecil. Hal ini dilakukan karena dapat membantu dalam menentukan jumlah komponen utama yang optimal untuk model.

7. Melakukan SVD dengan Nilai k Terbaik

Menggunakan nilai k terbaik untuk melakukan kembali SVD dan mendapatkan prediksi rating.

8. Mendapatkan Rekomendasi

Fungsi recommend_movies mengambil nilai userId dan menghasilkan rekomendasi film dari rating yang diprediksi. Fungsi tersebut mengurutkan rating yang diprediksi untuk setiap pengguna, memilih film dengan rating tertinggi, dan mengembalikan judul film tersebut. Kemudian, sampel userId akan diambil dari dataset dan fungsi rekomendasi akan digunakan untuk menghasilkan rekomendasi film untuk pengguna tersebut.

Berikut adalah hasil output yang diperoleh:


Recommended movies for user 151:
|     |Movie Title|
|---|---|
|0|Restoration (1995)|
|1|Toy Story (1995)|
|2|Dead Presidents (1995)|
|3|It Takes Two (1995)|
|4|Eye for an Eye (1996)|
|5|Richard III (1995)|
|6|Léon: The Professional (a.k.a. The Professiona...)|
|7|Renaissance Man (1994)|

Kelebihan Algoritma Collaborative Filtering, yaitu:

- Hasil rekomendasi yang beragam dan bersifat serendipitous (relevan dan baru) [[6](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/18066)].

Kekurangan Algoritma Collaborative Filtering, yaitu:

- Cold-start problem (tidak dapat menghasilkan rekomendasi karena tidak adanya informasi preferensi) untuk pengguna baru dan item baru [[6](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/18066)].

- Sparse problem (matriks rating pengguna-item yang jarang atau banyak yang kosong dapat mempengaruhi keakuratan algoritma) [[6](https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/18066)].

## Evaluation

Dilakukan evaluasi yang berbeda untuk teknik Content-Based Filtering dan juga Collaborative Filtering, yang mana hasil evaluasi Content-Based Filtering baik dengan pendekatan Cosine Similarity dan K-Nearest Neighbor yaitu menggunakan metrik evaluasi Precision.

- Evaluasi Content-Based Filtering

Berdasarkan teknik evaluasi yang dilakukan menggunakan metrik evaluasi precision, dapat dilihat bahwa rumus dari precision itu sendiri adalah sebagai berikut:

![Image 1](yourlinkhere.png?raw=true)

Rumus tersebut adalah rumus precision yang umumnya digunakan pada sistem rekomendasi. Rumus precision membantu pengguna dalam memilih item yang mirip di antara set item yang tersedia. Berikut adalah hasil output berupa movie yang dihasilkan dari sistem rekomendasi berbasis Content-Based Filtering dengan pendekatan Cosine Similarity:

|     |movie_name|genre|
|---|---|---|
|0|Furious 7 (2015)|Action, Crime, Thriller|
|1|Crimson Rivers 2: Angels of The Apocalypse|Action, Crime, Thriller|
|2|Dirty Harry (1971)|Action, Crime, Thriller|
|3|Takers (2010)|Action, Crime, Thriller|
|4|Natural Born Killers (1994)|Action, Crime, Thriller|

Berdasarkan pada hasil output tersebut, dapat diketahui bahwa hasil dari Top 5 Movie Recommendation yang diberikan menunjukkan bahwa dari 5 item yang direkomendasikan, 5 diantaranya sama-sama memiliki genre yang sama (similar) yang berarti bahwa nilai precision sebesar 5/5 atau 100%.

Setelah itu dilakukan pula evaluasi precision pada hasil output berupa movie yang dihasilkan dari sistem rekomendasi berbasis Content-Based Filtering dengan pendekatan K-Nearest Neighbor:

|     |movie_name|genre|
|---|---|---|
|33|Batman (1989)|Action, Crime, Thriller|
|227|Shaft (2000)|Action, Crime, Thriller|
|234|Kill Bill: Vol. 1 (2003)|Action, Crime, Thriller|
|531|Die Hard: With a Vengeance (1995)|Action, Crime, Thriller|
|539|Net, The (1995)|Action, Crime, Thriller|

Berdasarkan pada hasil output tersebut, dapat diketahui bahwa hasil dari Top 5 Movie Recommendation yang diberikan menunjukkan bahwa dari 5 item yang direkomendasikan, 5 diantaranya sama-sama memiliki genre yang sama (similar) yang berarti bahwa nilai precision sebesar 5/5 atau 100%.

- Evaluasi Collaborative Filtering

Performa model yang menggunakan pendekatan Collaborative Filtering diukur dengan metrik evaluasi Mean Squared Error (MSE). MSE pada sistem rekomendasi digunakan dalam rangka mengukur kesalahan prediksi antara nilai yang diprediksi oleh sistem rekomendasi dan nilai sebenarnya. MSE memungkinkan evaluasi kualitas prediksi sistem terhadap preferensi pengguna. Semakin rendah nilai MSE maka sistem rekomendasi lebih akurat dalam memprediksi preferensi pengguna.

MSE dapat didefinisikan dalam persamaan berikut:

![Image 2](yourlinkhere.png?raw=true)

Pada Collaborative Filtering, nilai MSE dihitung sembari menentukan nilai k yang sesuai untuk dimasukkan ke model SVD. Setelah itu, nilai k terbaik yang diperoleh adalah nilai k yang memberikan nilai MSE terkecil. Tahap akhirnya kemudian adalah melakukan SVD dengan nilai k terbaik yang telah diperoleh setelah dilakukan pengecekan satu per satu terhadap nilai k yang memberikan MSE terkecil.

Berikut adalah hasil nilai k terbaik beserta MSE yang diperoleh:

> Best k: 50, MSE: 0.09369500374812553

Oleh karena itu, nilai k = 50 yang akan digunakan untuk dimasukkan ke model Collaborative Filtering dengan metode SVD.

## Referensi

[1] E. Salim, J. Pragantha, M. D. Lauro, "Perancangan Sistem Rekomendasi Film menggunakan metode Contentbased Filtering", Jurnal Teknik Informatika, Fakultas Teknologi Informasi, Universitas Tarumanagara

[2] M. I. Fathurrahman, D. Nurjanah, R. Rismala, "Sistem Rekomendasi pada Buku dengan Menggunakan Metode Trust-Aware Recommendation", e-Proceeding of Engineering, vol. 4, no. 3, pp. 4966-4977, Desember 2017

[3] M. Fajriansyah, P. P. Adikara, dan A. W. Widodo, "Sistem Rekomendasi Film Menggunakan Content Based Filtering", J-PTIIK, vol. 5, no. 6, pp. 2188–2199, Mei 2021

[4] M. R. A. Zayyad, "SISTEM REKOMENDASI BUKU MENGGUNAKAN METODE CONTENT BASED FILTERING", Skripsi Universitas Islam Indonesia, Juli 2021

[5] A. Yusmar, "SISTEM REKOMENDASI BUKU MENGGUNAKAN METODE CONTENT BASED FILTERING", Skripsi Universitas Islam Negeri Syarif Hidayatullah Jakarta, 2020

[6] H. H. Arfisko, A. T. Wibowo, "Sistem Rekomendasi Film Menggunakan Metode Hybrid Collaborative Filtering Dan Content-Based Filtering", e-Proceeding of Engineering, vol. 9, no. 3, pp. 2149-2159, Juni 2022

