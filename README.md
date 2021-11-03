# Laporan Proyek Machine Learning - Anak Agung Sinta Trisnajayanti

## Project Overview
Seiring berkembangnya teknologi  seperti sekarang ini banyak kegiatan manusia dapat dilakukan secara online salah satunya yaitu jika kita ingin menonton film. Dimana sebelumnya jika kita ingin menonton film maka harus datang langsung ke bioskop.  Sedangkan sekarang sudah ada teknologi dalam bentuk website yang digunakan untuk kita menonton film dari rumah. [MUBI](https://mubi.com/) adalah bioskop online yang tersedia di lebih dari 200 wilayah yang menawarkan film kultus, klasik, dan pemenang penghargaan. Menurut jurnal [“SISTEM REKOMENDASI FILM MENGGUNAKAN ALGORITMA ITEM-BASED COLLABORATIVE FILTERING DAN BASIS DATA GRAPH”](http://eprints.undip.ac.id/60611/) disebutkan bahwa film box office yang diproduksi terus meningkat setiap tahunnya. Contohnya pada tahun 2009 terdapat 503 film yang rilis dan sebanyak 759 film diproduksi pada tahun 2015. Tidak jarang seseorang yang ingin menonton film menjadi kebingungan karena terlalu banyak film yang tersedia di internet. 

Oleh karena itu, dibutuhkan sebuah sistem yang dapat membantu memberikan informasi yang sesuai dengan keinginan pengguna. Sistem tersebut sering disebut dengan sistem rekomendasi. Pada proyek ini, saya akan membuat sistem rekomendasi film yang berguna untuk bisa merekomendasikan film yang bisa ditonton pengguna. Dataset  yang digunakan dalam proyek ini adalah data film yang sudah terisi rating oleh beberapa user sehingga jumlah rating yang diberikan pada setiap film tidak merata. Untuk menyelesaikan masalah tersebut diharapkan solusi Collaborative Filtering dapat memberikan solusi yang tepat dalam merekomendasikan sebuah film.
## Business Understanding
Menonton film sekarang sudah bisa dilakukan melalui online salah satunya pada platform MUBI. Pada proyek ini, saya akan membuat sistem rekomendasi film yang berguna untuk bisa merekomendasikan film yang bisa ditonton pengguna. Pada proyek ini, saya akan membuat sistem rekomendasi film yang berguna untuk bisa merekomendasikan film yang bisa ditonton pengguna. Dataset  yang digunakan dalam proyek ini adalah data film yang sudah terisi rating oleh beberapa pengguna sehingga jumlah rating yang diberikan pada setiap film tidak merata. Untuk menyelesaikan masalah tersebut diharapkan solusi Collaborative Filtering dapat memberikan solusi yang tepat dalam merekomendasikan sebuah film. 
### Problem Statement
Berikut adalah problem statement dari proyek ini:
* Bagaimana sistem rekomendasi yang dibuat ini dapat memberikan referensi film yang mungkin disukai oleh pengguna?
### Goals
Berikut adalah goals yang ingin dicapai dalam proyek ini: 
*	Menghasilkan rekomendasi sejumlah film yang sesuai dengan preferensi pengguna berdasarkan rating yang telah diberikan sebelumnya.
### Solution Approach
Untuk mencapai tujuan membuat sistem rekomendasi film disini saya menggunakan pendekatan Collaborative Filtering.
*	Collaborative Filtering merupakan cara untuk memberi rekomendasi bedasarkan penilaian komunitas pengguna atau biasa disebut dengan rating. Metode yang saya akan gunakan untuk mendukung collaborative filtering yaitu dengan deep learning. Penggunaan metode deep learning pada sistem rekomendasi lebih efisien dan tepat sasaran. Keberhasilan deep learning untuk mendapatkan rekomendasi baik di dunia akademis maupun di industri membutuhkan pemahaman yang komprehensif review dan ringkasan untuk peneliti dan praktisi berturut-turut untuk lebih memahami kekuatan dan kelemahan, dan skenario aplikasi model ini. 

## Data Understanding
Dataset yang saya ambil berasal dari [kaggle](https://www.kaggle.com/) . yang merupakan salah satu platform di bidang Data Science. Pada proyek ini saya menggunakan dataset [berikut](https://www.kaggle.com/clementmsika/mubi-sqlite-database-for-movie-lovers) dimana sesuai dengan topik yang saya ambil yaitu mengenai data film pada platform [MUBI](https://mubi.com/) . Berikut adalah penjelasan mengenai kolom pada dataset:

**mubi_movie_data.csv**
*	movie_id: ID yang terkait dengan film di Mubi
*	movie_title: Nama film atau judul film
*	movie_release_year: Tahun rilis film
*	movie_url: URL ke halaman film di Mubi
*	movie_title_language: Secara default, judulnya dalam bahasa Inggris.
*	movie_popularity: Jumlah pengguna Mubi yang menyukai film ini
*	movie_image_url: URL gambar ke film di Mubi
*	director_id: ID yang terkait dengan sutradara film di Mubi
*	director_name: Nama lengkap sutradara Film
*	director_url: URL ke halaman sutradara film di Mubi

**mubi_ratings_data.csv**
*	movie_id: ID film terkait dengan peringkat
*	rating_id: Peringkat ID di Mubi
*	rating_url: URL ke peringkat di Mubi
*	rating_score: Skor penilaian mulai dari 1 (terendah) hingga 5 (tertinggi)
*	rating_timestamp_utc: Stempel waktu untuk peringkat film yang dibuat oleh pengguna di Mubi
*	critic: Kritik yang dibuat oleh pengguna menilai film.
*	critic_likes: Jumlah suka terkait dengan kritik yang dibuat oleh pengguna menilai film
*	critic_comments: Jumlah komentar yang terkait dengan kritik yang dibuat oleh pengguna menilai film
*	user_id: ID yang terkait dengan peringkat pengguna film
*	user_trialist
	* 1 = pengguna adalah seorang trialist ketika dia menilai film
	* 0 = pengguna bukan seorang trialist ketika dia menilai film

Pada proyek kali ini saya hanya menggunakan beberapa kolom saja dan mengganti nama kolom tersebut menjadi seperti berikut ini: 

**mubi_movie_data.csv**

Jumlah data yang saya gunakan disini 20.000

![messageImage_1635930938500](https://user-images.githubusercontent.com/89082302/140034744-ed13921c-6256-43ee-b4d5-357a3006b19b.jpg)

**mubi_ratings_data.csv**

Jumlah data yang saya gunakan disini 25.000

![messageImage_1635930948774](https://user-images.githubusercontent.com/89082302/140034751-d1bbaae9-229c-46aa-8606-9ed3d00855c5.jpg)

Dalam proses data understanding, yang pertama saya menggunakan visualisasi data untuk melihat berapa banyak film yang rilis di tahun tertentu. Visualisasi ini menggunakan histplot dimana data diambil dari data_movie.

![messageImage_1635931024269](https://user-images.githubusercontent.com/89082302/140034886-2c774dde-fc0d-4564-9ccc-8f0a3df427ea.jpg)

Dapat dilihat pada gambar di atas bahwa terjadi peningkatan yang pesat untuk film yang rilis mulai dari tahun 1990 sampai tahun 2000an dibandingkan tahun-tahun sebelumnya. 
Kemudian saya juga menggabungkan data_ratings dan data_movie untuk melihat visualisasi data dari 10 besar film yang sudah dirilis menggunakan barplot. Visualisasi data  ini mengambil data pengguna yang memberikan penilaian pada suatu film. 

![messageImage_1635933024129](https://user-images.githubusercontent.com/89082302/140039432-4fc5261f-353f-4bbb-856d-17600763bfbe.jpg)

Pada gambar di atas menunjukkan bahwa pada film “The Exterminating Angel” memiliki data penilaian dari pengguna paling terbanyak. 
Lalu saya juga ingin menampilkan visualisasi data dari kolom Director menggunakan barplot. Dimana disini 10 director terpopuler akan ditampilkan sebagai berikut:

![messageImage_1635933005037](https://user-images.githubusercontent.com/89082302/140039443-a38011a5-6000-4eed-99a8-f3097146979d.jpg)

 Dapat dilihat pada gambar di atas bahwa “Francois Truffaut” memiliki jumlah film yang rilis paling banyak yang menjadikannya masuk ke 10 director terpopuler. 

## Data Preparation
Dalam data preparation ini saya menggunakan beberapa teknik untuk memeriksa ketiga data yang saya gunakan. Data yang dimaksud yaitu pada data_movie, data_ratings, dan df (gabungan kedua data). 
1.   Teknik pertama yaitu mengecek data null karena jika ada data yang kosong atau nol akan membuat prediksi menjadi kurang akurat. Jika terdapat data yang mengandung null maka dihapus menggunakan dataframe.dropna(). Hasil dari cek data null pada 3 data yang saya gunakan sebagai berikut: 

![messageImage_1635931544037](https://user-images.githubusercontent.com/89082302/140036190-0dd806bf-9e0d-4517-a98c-bf8ed968de12.jpg)

2.   Teknik yang kedua yaitu encoding data dimana pada teknik ini digunakan untuk menyandikan nilai unik ke dalam indeks integer pada kolom User_ID dan Movie_ID. Kemudian hasil encoding tersebut saya masukkan ke dalam dataframe df. Hasil dari proses encoding data adalah sebagai berikut: 
  
 **Encoding data pada User_ID**
	
![messageImage_1635931551044](https://user-images.githubusercontent.com/89082302/140037528-bcd514f1-1dd9-44f4-bd39-7ffe75d3675e.jpg)

**Encoding data pada Movie_ID**
	
![messageImage_1635931563219](https://user-images.githubusercontent.com/89082302/140037630-20dfb07e-6700-4439-9eef-421746044f5f.jpg)

Lalu untuk teknik cek data duplicated tidak saya gunakan karena pada dataset kolom Movie_ID memiliki pengaruh yang signifikan ke jumlah data yang saya gunakan jika dilakukan drop. 
Kemudian setelah menerapkan kedua teknik di atas sekarang kita bisa cek kembali data kita mulai dari jumlah pengguna, jumlah film dan rating minimum dan maksimum yang ada sekarang. Berikut adalah hasil mengenai data yang kita punya: 

![messageImage_1635931570419](https://user-images.githubusercontent.com/89082302/140036557-06d76a1e-4284-4e9a-bc5c-f33fc4f64038.jpg)

3.   Selanjutnya membagi data menjadi data train dan data validasi. Dimana persentase pembagian data nya yaitu 80% data train dan 20% data validasi. Dimana perlu dipetakkan (mapping) terlebih dahulu pada data User dan Mook menjadi satu value. Proses ini dilakukan untuk menguji model terhadap data baru.

![messageImage_1635931578158](https://user-images.githubusercontent.com/89082302/140036598-7c07a7ab-33d3-4b89-8c76-d8801b2a3c55.jpg)

## Modeling and Result
Pada proyek ini saya menggunakan pendekatan Collaborative Filtering dengan metode Deep Learning. Pada modeling ini proses pertama yang dilakukan yaitu proses embedding pada data user dan movie. Kemudian dilakukan compile model menggunakan optimizer SGD, metriks MAE dan RMSE. Lalu yang terakhir menampilkan rekomendasi film. Hasil dari rekomendasi film adalah sebagai berikut: 

![messageImage_1635932356155](https://user-images.githubusercontent.com/89082302/140037873-dc1d4172-bf47-45c9-8ae1-87c7b39d863c.jpg)

Dapat dilihat pada gambar di atas bahwa ID pengguna '”78562146” menyukai film “Confidentially Yours” dengan memberikan rating tinggi. Maka dari itu sistem ini akan memberikan 10 rekomendasi film yang mirip dengan yang disukai pengguna. 3 rekomendasi film teratas adalah “The Exterminating Angel”, “Simon of the Desert”, “Hobson's Choice”. 
Metode collaborative filtering memiliki beberapa kelebihan yaitu rekomendasi tetap akan berkerja dalam keadaan dimana konten sulit dianalisi sekalipun, namun metode ini juga memiliki kekurangan yaitu membutuhkan parameter rating, sehingga jika ada item baru sistem tidak akan merekomendasikan item tersebut. 

## Evaluation
Pada evaluation ini saya menggunakan metriks  Mean Absolute Error (MAE) , Root Mean Squared Error (RMSE). MAE dan RMSE menyatakan kesalahan prediksi model rata-rata dalam unit variabel yang diminati. Kedua metrik dapat berkisar dari 0 hingga ∞ dan tidak berbeda dengan arah kesalahan. Mereka adalah skor berorientasi negatif, yang berarti nilai yang lebih rendah lebih baik. Kedua metriks ini memiliki hubungan dengan rating dari pengguna. Berikut adalah penjelasan mengenai metriks yang saya gunakan:

*	Mean Absolute Error (MAE)
MAE mengukur besarnya rata-rata kesalahan dalam serangkaian prediksi, tanpa mempertimbangkan arahnya. Semakin kecil nilai MAE, semakin baik model tersebut dalam melakukan prediksi. Berikut adalah rumus untuk menghitung MAE: 

![messageImage_1635932818334](https://user-images.githubusercontent.com/89082302/140039025-27d77b35-f0df-4b6c-9941-ae4dca073a6f.jpg)

*	Root Mean Squared Error (RMSE) untuk menghitung seberapa berbedanya seperangkat nilai. Semakin kecil nilai RMSE, semakin dekat nilai yang diprediksi dan diamati. Untuk menghitung nilai dari RMSE menggunakan rumus berikut: 

![messageImage_1635932832261](https://user-images.githubusercontent.com/89082302/140039000-e7324e91-82e7-4606-a581-04e042b8e011.jpg)


Di dalam evaluation ini saya juga akan menampilkan visualisasi dari metriks yang saya gunakan dimana menunjukkan penurunan yang artinya nilai MAE dan RMSE semakin kecil setiap epoch dijalankan. 

![messageImage_1635933173677](https://user-images.githubusercontent.com/89082302/140039847-22f4a9f6-a7ac-41fc-acb3-26e1f0f13879.jpg)

## Kesimpulan
Pada proyek ini berhasil membuat sistem rekomendasi film. Dimana sistem dapat merekomendasikan 10 film menggunakan penilaian rating dari pengguna. Kemudian proyek ini juga menggunakan pendekatan Collaborative Filtering dengan metode Deep Learning. Metriks yang digunakan MAE dan RMSE dapat memberikan prediksi yang akurat karena semakin data dilatih nilai error juga semakin kecil.
