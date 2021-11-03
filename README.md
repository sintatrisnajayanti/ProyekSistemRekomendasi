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
![messageImage_1635931076378](https://user-images.githubusercontent.com/89082302/140035048-5ddc099c-cb5d-49b0-b108-b2015e0c57c7.jpg)

Pada gambar di atas menunjukkan bahwa pada film “The Exterminating Angel” memiliki data penilaian dari pengguna paling terbanyak. 
Lalu saya juga ingin menampilkan visualisasi data dari kolom Director menggunakan barplot. Dimana disini 10 director terpopuler akan ditampilkan sebagai berikut.
![messageImage_1635931082928](https://user-images.githubusercontent.com/89082302/140035089-cc7592c9-2862-423b-b4ed-12081a5479c8.jpg)

 Dapat dilihat pada gambar di atas bahwa “Francois Truffaut” memiliki jumlah film yang rilis paling banyak yang menjadikannya masuk ke 10 director terpopuler. 
## Data Preparation
## Modeling and Result
## Evaluation
