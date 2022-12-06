# Laporan Proyek Machine Learning - Yunus Ahmad Hasan Baktir

## Project Overview

Netflix merupakan salah satu platform streaming media dan video paling populer. Mereka memiliki lebih dari 8000 film atau acara tv dengan berbagai kategori yang tersedia di platform mereka. Pelanggan menggunakan platform ini untuk mendapatkan hiburan dari film atau acara tv. Dengan banyaknya kategori film atau acara tv dengan berbagai kategori, maka diperlukan rekomendasi film berdasarkan kategori yang disukai oleh pelanggan. 
Proyek ini bertujuan membuat sistem rekomendasi film berdasarkan kedekatan dengan kategori film dari judul film yang terakhir ditonton oleh pelanggan. Tujuannya agar pelanggan mendapatkan rekomendasi film setelah film selesai ditonton, dan menggunakan platform ini lebih lama lagi. 

## Business Understanding
Setelah menonton satu film, pelanggan akan direkomendasikan film berdasarkan kategori film yang mirip dengan film yang ditonton nya terakhir. Agar pelanggan menonton kembali film di platform tersebut. Semakin lama pelanggan menonton film yang sesuai dengan kategori film yang pelanggan suka semakin lama pelanggan platform tersebut dan menguntungkan bagi perusahaan.

### Problem Statements

Menjelaskan pernyataan masalah latar belakang:
- Fitur apa yang digunakan untuk menemukan film dengan berdasarkan kemiripan kategori film ?
- Sistem rekomendasi apa yang cocok untuk menemukan film memiliki kemiripan dengan kategori film yang ditonton terakhir ?
- Sistem rekomendasi yang cocok untuk menemukan film yang memiliki kemiripan dan rating im

### Goals

Menjelaskan tujuan dari pernyataan masalah:
- Mengetahui fitur yang digunakan sebagai kategori film
- Membuat sistem rekomendasi yang cocok untuk menemukan film yang memiliki kemiripan kategori film yang ditonton terakhir.


## Solution Statements
Untuk mencapai goals diatas, maka perlu dibuat sistem rekomendasi dengan alur sebagai berikut: 
- Data Understanding: Memahami data yang digunakan.
- Univariate Exploratory Data Analysis: Pada tahap ini, Anda melakukan analisis dan eksplorasi setiap variabel pada data. Jika dibutuhkan, Anda dapat melakukan eksplorasi lebih lanjut mengenai keterkaitan antara satu variabel dengan variabel lainnya.
- Data Preparation: Pada tahap ini memastikan data yang digunakan memiliki kategori film masing-masing
- Model Development dengan Content Based Filtering: Model ini akan merekomendasikan film yang mirip dengan film yang ditonton terakhir. Tahap ini akan ditemukan fitur penting dari setiap kategori film dengan tfidf vectorizer dan menghitung tingkat kesamaan dengan cosine similarity. Setelah itu, kita akan membuat sejumlah rekomendasi film untuk pelanggan berdasarkan kesamaan yang telah dihitung sebelumnya.

## Data Understanding
Data yang digunakan adalah dataset Netflix Movies and TV Shows. 
### Tentang Dataset
Netflix adalah salah satu platform streaming media dan video paling populer. Mereka memiliki lebih dari 8000 film atau acara TV yang tersedia di platform mereka, pada pertengahan 2021, mereka memiliki lebih dari 200 juta Pelanggan secara global. Kumpulan data tabular ini terdiri dari daftar semua film dan acara TV yang tersedia di Netflix, bersama dengan detail seperti - pemeran, sutradara, peringkat, tahun rilis, durasi, dll.

Link Dataset: *[Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)*.
### Metadata
Jumlah baris data: 8807 baris
License: CC0: Public Domain

### Variabel-variabel pada Netflix Movies and TV Shows dataset adalah sebagai berikut:
- show_id : Id unik setiap film atau acara tv
- type : Pengenal film atau acara tv
- title : Judul film atau acara tv
- director : Sutradara film
- cast : Aktor yang main di film atau acara tv
- country : Negara dimana film atau acara tv di produksi
- date_added : Tanggal dimasukkan ke netflix
- release_year : Aktual rilis dari film atau acara tv
- rating : TV Rating dari film atau acara tv
- duration : Total durasi film atau acara tv
- listed_in : Kategori film atau acara tv
- description : Cerita singkat film atau acara tv

### Univariate Exploratory Data Analysis
Melakukan pengecekan data unik masing-masing fitur.

## Data Preparation
Tahapan data preparation yang dilakukan:

### Cek Missing Value
Pada tahap ini dilakukan pengecekan pada data apakah ada data yang missing value atau tidak. Hasilnya sebagai berikut:
| Fitur | Total |
|---|---|
|  show_id | 0 | 
|  type |  0 | 
|  title |  0 | 
|  director |  2634 | 
|  cast |  825 | 
|  country |  831 | 
|  date_added |  10 | 
|  release_year |  0 | 
|  rating |  4 | 
|  duration |  3 | 
|  listed_in |  0 | 
|  description |  0 | 

Karena fitur utama kita yang akan gunakan yaitu show_id, title dan listed_in tidak ada yang kosong, jadi tidak perlu tindakan khusus untuk ini.

### Cek jumlah film
Kemudian cek jumlah film berdasarkan fitur show_id yang unik. Hasilnya ada 8807 film.

### Cek kategori film
Melihat seluruh kategori film yang ada pada fitur listed_in. Hasilnya sebagai berikut:
array(['Documentaries', 'International TV Shows, TV Dramas, TV Mysteries',
       'Crime TV Shows, International TV Shows, TV Action & Adventure',
       'Docuseries, Reality TV',
       'International TV Shows, Romantic TV Shows, TV Comedies',
       'TV Dramas, TV Horror, TV Mysteries', 'Children & Family Movies',
       'Dramas, Independent Movies, International Movies',
       'British TV Shows, Reality TV', 'Comedies, Dramas',
       'Crime TV Shows, Docuseries, International TV Shows',
       'Dramas, International Movies',
       'Children & Family Movies, Comedies',
       'British TV Shows, Crime TV Shows, Docuseries',
       'TV Comedies, TV Dramas', 'Documentaries, International Movies',
       'Crime TV Shows, Spanish-Language TV Shows, TV Dramas',
       'Thrillers',
       'International TV Shows, Spanish-Language TV Shows, TV Action & Adventure',
       'International TV Shows, TV Action & Adventure, TV Dramas',
       'Comedies, International Movies',
       'Comedies, International Movies, Romantic Movies',
       'Docuseries, International TV Shows, Reality TV',
       'Comedies, International Movies, Music & Musicals', 'Comedies',
       'Horror Movies, Sci-Fi & Fantasy', 'TV Comedies',
       'British TV Shows, International TV Shows, TV Comedies',
       'International TV Shows, TV Dramas, TV Thrillers', "Kids' TV",
       'Dramas, International Movies, Thrillers',
       'Action & Adventure, Dramas, International Movies',
       "Kids' TV, TV Comedies", 'Action & Adventure, Dramas',
       "Kids' TV, TV Sci-Fi & Fantasy",
       'Action & Adventure, Classic Movies, Dramas',
       'Dramas, Horror Movies, Thrillers',
       'Action & Adventure, Horror Movies, Thrillers',
       'Action & Adventure', 'Dramas, Thrillers',
       'International TV Shows, TV Dramas',
       'International TV Shows, TV Dramas, TV Sci-Fi & Fantasy',
       'Action & Adventure, Anime Features, International Movies',
       'Reality TV', 'Docuseries, International TV Shows',
       'Documentaries, International Movies, Sports Movies',
       'International TV Shows, Reality TV, Romantic TV Shows',
       'British TV Shows, Docuseries, International TV Shows',
       'Anime Series, International TV Shows',
       'Comedies, Dramas, International Movies',
       'Crime TV Shows, TV Comedies, TV Dramas',
       'Action & Adventure, Comedies, Dramas', "Anime Series, Kids' TV",
       'International Movies, Thrillers', "Kids' TV, Korean TV Shows",
       'Documentaries, Sports Movies', 'Sci-Fi & Fantasy, Thrillers',
       'Dramas, International Movies, Romantic Movies',
       'Documentaries, Music & Musicals',
       "Kids' TV, TV Comedies, TV Sci-Fi & Fantasy",
       "British TV Shows, Kids' TV", 'Docuseries, Science & Nature TV',
       'Children & Family Movies, Dramas',
       "Kids' TV, TV Dramas, Teen TV Shows",
       'Crime TV Shows, International TV Shows, Spanish-Language TV Shows',
       'Docuseries, International TV Shows, Spanish-Language TV Shows',
       'Dramas', 'Comedies, Romantic Movies', 'Dramas, Romantic Movies',
       'Comedies, Dramas, Independent Movies',
       'Crime TV Shows, TV Action & Adventure, TV Comedies',
       'Children & Family Movies, Music & Musicals',
       'Action & Adventure, Classic Movies, Cult Movies',
       'International TV Shows, TV Action & Adventure, TV Comedies',
       'Action & Adventure, Sci-Fi & Fantasy',
       'Action & Adventure, Comedies', 'Classic Movies, Comedies, Dramas',
       'Comedies, Cult Movies', 'Comedies, Cult Movies, Music & Musicals',
       'Comedies, Music & Musicals', 'TV Shows',
       'Action & Adventure, International Movies',
       'Anime Series, International TV Shows, Teen TV Shows',
       'Action & Adventure, Children & Family Movies, Cult Movies',
       'Comedies, Dramas, Romantic Movies',
       'Comedies, Cult Movies, Sci-Fi & Fantasy',
       'Classic Movies, Dramas',
       'Action & Adventure, Children & Family Movies, Comedies',
       'Dramas, Faith & Spirituality', 'Documentaries, LGBTQ Movies',
       'Action & Adventure, Classic Movies', 'Docuseries',
       'International TV Shows, TV Comedies',
       'Dramas, Independent Movies',
       'Action & Adventure, Comedies, International Movies',
       'International TV Shows, Spanish-Language TV Shows, TV Dramas',
       'Crime TV Shows, International TV Shows, TV Dramas',
       'Action & Adventure, Horror Movies, International Movies',
       'Comedies, International Movies, Sci-Fi & Fantasy',
       'Action & Adventure, International Movies, Music & Musicals',
       'Dramas, International Movies, Music & Musicals',
       'Horror Movies, International Movies', 'Reality TV, Teen TV Shows',
       'Crime TV Shows, TV Dramas, TV Mysteries',
       'International TV Shows, Reality TV',
       'International TV Shows, TV Comedies, TV Dramas',
       'Dramas, Independent Movies, Romantic Movies', 'Horror Movies',
       'Documentaries, LGBTQ Movies, Sports Movies',
       'Horror Movies, International Movies, Thrillers',
       'Action & Adventure, Anime Features',
       'TV Dramas, TV Mysteries, TV Sci-Fi & Fantasy',
       'International TV Shows, Spanish-Language TV Shows, TV Comedies',
       'Children & Family Movies, Comedies, Music & Musicals',
       'Comedies, Independent Movies',
       'Anime Series, International TV Shows, Romantic TV Shows',
       'Classic Movies, Dramas, Independent Movies',
       'International TV Shows, Romantic TV Shows, Spanish-Language TV Shows',
       'International TV Shows, TV Dramas, Teen TV Shows',
       'Stand-Up Comedy',
       'Action & Adventure, Anime Features, Children & Family Movies',
       'International TV Shows, Romantic TV Shows, TV Dramas',
       'International Movies, Music & Musicals',
       'TV Action & Adventure, TV Dramas, TV Mysteries',
       'Horror Movies, Independent Movies, International Movies',
       'Comedies, Cult Movies, International Movies',
       'Classic Movies, Dramas, International Movies', 'Movies',
       'Crime TV Shows, Docuseries',
       'Children & Family Movies, Comedies, Sci-Fi & Fantasy',
       'Anime Series, International TV Shows, TV Thrillers',
       'Action & Adventure, Horror Movies, Sci-Fi & Fantasy',
       'Classic Movies, Comedies, Cult Movies',
       'TV Dramas, Teen TV Shows',
       'Action & Adventure, Sci-Fi & Fantasy, Thrillers',
       'Children & Family Movies, Comedies, Dramas',
       'Dramas, Sports Movies',
       'Action & Adventure, Dramas, Sci-Fi & Fantasy',
       'Action & Adventure, Comedies, Cult Movies',
       'Dramas, Independent Movies, Thrillers',
       'TV Dramas, TV Sci-Fi & Fantasy',
       'Action & Adventure, International Movies, Thrillers',
       'British TV Shows, International TV Shows, Reality TV',
       'TV Action & Adventure, TV Dramas, Teen TV Shows', 'Anime Series',
       'Crime TV Shows, TV Action & Adventure, TV Sci-Fi & Fantasy',
       'Crime TV Shows, International TV Shows, TV Comedies',
       'Stand-Up Comedy & Talk Shows, TV Comedies',
       'Classic & Cult TV, TV Action & Adventure, TV Dramas',
       'Children & Family Movies, Sports Movies',
       'TV Action & Adventure, TV Sci-Fi & Fantasy',
       'Anime Series, Stand-Up Comedy & Talk Shows', 'TV Dramas',
       'Anime Features, Children & Family Movies, International Movies',
       'Classic & Cult TV, Crime TV Shows, International TV Shows',
       'Crime TV Shows, International TV Shows, Romantic TV Shows',
       'Horror Movies, LGBTQ Movies',
       'Action & Adventure, Dramas, Romantic Movies',
       'Documentaries, International Movies, Music & Musicals',
       'TV Comedies, TV Dramas, Teen TV Shows',
       'Children & Family Movies, Comedies, Sports Movies',
       'Children & Family Movies, Dramas, International Movies',
       'Comedies, Documentaries, International Movies',
       'Romantic TV Shows, TV Dramas',
       'Anime Series, TV Horror, TV Thrillers',
       'International Movies, Romantic Movies',
       'TV Action & Adventure, TV Dramas, TV Sci-Fi & Fantasy',
       "Kids' TV, Korean TV Shows, TV Comedies",
       'British TV Shows, Crime TV Shows, International TV Shows',
       'Crime TV Shows, TV Horror, TV Mysteries',
       'Docuseries, International TV Shows, Science & Nature TV',
       'British TV Shows, International TV Shows, TV Dramas',
       "Kids' TV, TV Action & Adventure, TV Sci-Fi & Fantasy",
       'International Movies, Romantic Movies, Thrillers',
       'Action & Adventure, Cult Movies, International Movies',
       'Action & Adventure, Comedies, Sci-Fi & Fantasy',
       "International TV Shows, Kids' TV, TV Mysteries",
       'Action & Adventure, Thrillers',
       'Dramas, Faith & Spirituality, International Movies',
       'Action & Adventure, Classic Movies, Comedies',
       'Action & Adventure, Comedies, Sports Movies',
       'Action & Adventure, Children & Family Movies, Classic Movies',
       'Action & Adventure, Children & Family Movies, Dramas',
       'Horror Movies, Thrillers', 'Action & Adventure, Romantic Movies',
       'Dramas, Romantic Movies, Sci-Fi & Fantasy',
       'Dramas, Music & Musicals, Romantic Movies',
       'Anime Series, Crime TV Shows, International TV Shows',
       'Reality TV, Romantic TV Shows',
       'International Movies, Music & Musicals, Romantic Movies',
       'Reality TV, TV Action & Adventure, TV Mysteries',
       'Crime TV Shows, TV Dramas',
       'International TV Shows, Reality TV, Spanish-Language TV Shows',
       'Crime TV Shows, TV Dramas, TV Thrillers',
       'British TV Shows, Docuseries',
       'International TV Shows, Korean TV Shows, TV Comedies',
       'Action & Adventure, Anime Features, Classic Movies',
       'TV Action & Adventure, TV Dramas, TV Horror',
       'Crime TV Shows, International TV Shows, TV Thrillers',
       'Anime Series, Crime TV Shows, TV Horror',
       'Anime Features, Documentaries', 'Comedies, Horror Movies',
       'International TV Shows, Spanish-Language TV Shows, Stand-Up Comedy & Talk Shows',
       'Children & Family Movies, Documentaries, International Movies',
       'Romantic TV Shows, TV Comedies, TV Dramas',
       'Dramas, Faith & Spirituality, Romantic Movies',
       'Dramas, Independent Movies, LGBTQ Movies',
       'Comedies, Independent Movies, LGBTQ Movies',
       'Action & Adventure, Cult Movies, Sci-Fi & Fantasy',
       'Cult Movies, Horror Movies',
       'Action & Adventure, Dramas, Sports Movies',
       'Anime Series, Romantic TV Shows, Teen TV Shows',
       'Dramas, International Movies, LGBTQ Movies',
       'Dramas, Romantic Movies, Thrillers',
       'Children & Family Movies, Dramas, Faith & Spirituality',
       'Dramas, International Movies, Sports Movies',
       'Action & Adventure, Horror Movies',
       'Documentaries, International Movies, LGBTQ Movies',
       'Dramas, Independent Movies, Sci-Fi & Fantasy',
       'Comedies, Independent Movies, International Movies',
       'Reality TV, TV Horror, TV Thrillers',
       'TV Action & Adventure, TV Horror, TV Sci-Fi & Fantasy',
       'International TV Shows, TV Horror, TV Sci-Fi & Fantasy',
       'Independent Movies, International Movies, Thrillers',
       'Independent Movies, Thrillers', 'Documentaries, Dramas',
       'Action & Adventure, Sports Movies',
       'Dramas, International Movies, Sci-Fi & Fantasy',
       'Comedies, Independent Movies, Romantic Movies',
       'Horror Movies, Romantic Movies, Sci-Fi & Fantasy',
       'International TV Shows, Stand-Up Comedy & Talk Shows',
       'Action & Adventure, Anime Features, Horror Movies',
       'Cult Movies, Dramas, Music & Musicals', 'TV Dramas, TV Thrillers',
       'Crime TV Shows, International TV Shows, Korean TV Shows',
       'TV Horror, TV Mysteries, TV Thrillers',
       'Comedies, Horror Movies, International Movies',
       'Crime TV Shows, Docuseries, TV Mysteries',
       'Comedies, International Movies, Sports Movies',
       'Classic Movies, Music & Musicals',
       'Reality TV, TV Comedies, TV Horror',
       'Children & Family Movies, Faith & Spirituality, Music & Musicals',
       'International TV Shows, Korean TV Shows, Stand-Up Comedy & Talk Shows',
       'Dramas, Music & Musicals',
       'Docuseries, Science & Nature TV, TV Action & Adventure',
       "British TV Shows, Kids' TV, TV Dramas",
       'International TV Shows, Korean TV Shows, Romantic TV Shows',
       'Horror Movies, Independent Movies',
       "Anime Series, Kids' TV, TV Action & Adventure",
       'Comedies, Dramas, Music & Musicals', 'TV Horror, Teen TV Shows',
       'Comedies, LGBTQ Movies, Thrillers',
       'Docuseries, Reality TV, Science & Nature TV',
       'Crime TV Shows, Spanish-Language TV Shows, TV Action & Adventure',
       'Romantic TV Shows, Teen TV Shows', 'TV Comedies, Teen TV Shows',
       'Romantic TV Shows, TV Dramas, Teen TV Shows',
       'Children & Family Movies, Sci-Fi & Fantasy',
       'Romantic TV Shows, TV Action & Adventure, TV Dramas',
       'Comedies, International Movies, LGBTQ Movies',
       'Dramas, Sci-Fi & Fantasy', "Kids' TV, TV Thrillers",
       'TV Action & Adventure, TV Comedies, TV Sci-Fi & Fantasy',
       'British TV Shows, Romantic TV Shows, TV Dramas',
       'Anime Series, International TV Shows, Spanish-Language TV Shows',
       'Docuseries, TV Comedies',
       'Comedies, Romantic Movies, Sports Movies',
       'TV Action & Adventure, TV Comedies, TV Dramas',
       'Children & Family Movies, Dramas, Sports Movies',
       'Action & Adventure, Dramas, Independent Movies',
       'Spanish-Language TV Shows, TV Dramas', 'Dramas, LGBTQ Movies',
       'TV Horror, TV Mysteries, TV Sci-Fi & Fantasy',
       'Action & Adventure, Dramas, Faith & Spirituality',
       'International TV Shows, TV Mysteries, TV Thrillers',
       'British TV Shows, Classic & Cult TV, International TV Shows',
       'Action & Adventure, Comedies, Independent Movies',
       'Music & Musicals', "British TV Shows, Kids' TV, TV Comedies",
       'Docuseries, Spanish-Language TV Shows',
       'Dramas, Independent Movies, Sports Movies',
       'TV Dramas, TV Mysteries, TV Thrillers',
       'Comedies, LGBTQ Movies, Music & Musicals',
       'International TV Shows, TV Action & Adventure, TV Mysteries',
       "Kids' TV, TV Comedies, Teen TV Shows",
       'International TV Shows, TV Dramas, TV Horror',
       'Comedies, International Movies, Thrillers',
       'Classic & Cult TV, TV Action & Adventure, TV Sci-Fi & Fantasy',
       'International TV Shows, TV Horror, TV Mysteries',
       'Children & Family Movies, Documentaries',
       'Music & Musicals, Romantic Movies', 'Romantic Movies',
       'Children & Family Movies, Classic Movies, Comedies',
       'TV Action & Adventure, TV Dramas',
       'Dramas, LGBTQ Movies, Romantic Movies',
       'Children & Family Movies, Comedies, Romantic Movies',
       'Comedies, Sports Movies', 'International Movies',
       'International TV Shows, Romantic TV Shows, TV Mysteries',
       'Stand-Up Comedy & Talk Shows',
       'Action & Adventure, International Movies, Romantic Movies',
       'Reality TV, TV Comedies',
       'Cult Movies, Dramas, International Movies', "Kids' TV, TV Dramas",
       'Crime TV Shows, International TV Shows, TV Mysteries',
       'Action & Adventure, Sci-Fi & Fantasy, Sports Movies',
       'TV Dramas, TV Sci-Fi & Fantasy, TV Thrillers',
       'Romantic TV Shows, TV Dramas, TV Sci-Fi & Fantasy',
       'Docuseries, TV Sci-Fi & Fantasy',
       'Anime Features, International Movies',
       "British TV Shows, Classic & Cult TV, Kids' TV",
       'British TV Shows, Reality TV, Romantic TV Shows',
       'Documentaries, Faith & Spirituality, International Movies',
       "Kids' TV, Reality TV, TV Dramas", 'LGBTQ Movies, Thrillers',
       'TV Action & Adventure, TV Mysteries, TV Sci-Fi & Fantasy',
       'Reality TV, Science & Nature TV',
       "Kids' TV, TV Action & Adventure, TV Comedies",
       'International TV Shows, Romantic TV Shows, TV Action & Adventure',
       'Children & Family Movies, Dramas, Independent Movies',
       'Comedies, Music & Musicals, Romantic Movies',
       'International TV Shows, Korean TV Shows, Reality TV',
       'Classic & Cult TV, TV Dramas, TV Sci-Fi & Fantasy',
       'Anime Features, Children & Family Movies',
       'Action & Adventure, International Movies, Sci-Fi & Fantasy',
       'Crime TV Shows, TV Action & Adventure, TV Dramas',
       'Classic & Cult TV, TV Action & Adventure, TV Horror',
       'International TV Shows, Korean TV Shows, TV Dramas',
       'International TV Shows, TV Action & Adventure, TV Horror',
       'Action & Adventure, Comedies, Romantic Movies',
       'International TV Shows, Korean TV Shows, TV Action & Adventure',
       "Classic & Cult TV, Kids' TV, TV Action & Adventure",
       'Anime Series, International TV Shows, TV Horror',
       'International TV Shows, Korean TV Shows, TV Horror',
       'Children & Family Movies, Comedies, International Movies',
       'International Movies, Sci-Fi & Fantasy',
       'International Movies, Sci-Fi & Fantasy, Thrillers',
       'Children & Family Movies, Dramas, Romantic Movies',
       'Anime Series, Romantic TV Shows',
       'Comedies, Dramas, LGBTQ Movies',
       'British TV Shows, International TV Shows, TV Action & Adventure',
       'Docuseries, Science & Nature TV, TV Comedies',
       'International TV Shows, Stand-Up Comedy & Talk Shows, TV Comedies',
       'Children & Family Movies, Dramas, Music & Musicals',
       'Action & Adventure, Independent Movies, International Movies',
       'Action & Adventure, Children & Family Movies, Sci-Fi & Fantasy',
       'Horror Movies, Independent Movies, Sci-Fi & Fantasy',
       'TV Dramas, TV Sci-Fi & Fantasy, Teen TV Shows',
       'Anime Features, International Movies, Sci-Fi & Fantasy',
       'Dramas, Independent Movies, Music & Musicals',
       "Kids' TV, TV Comedies, TV Dramas",
       'Children & Family Movies, Documentaries, Sports Movies',
       'Independent Movies, Sci-Fi & Fantasy, Thrillers',
       'Anime Features, Music & Musicals, Sci-Fi & Fantasy',
       'TV Comedies, TV Dramas, TV Sci-Fi & Fantasy',
       'Crime TV Shows, TV Action & Adventure',
       'Comedies, Faith & Spirituality, Romantic Movies',
       "Kids' TV, TV Action & Adventure",
       'Action & Adventure, Independent Movies',
       'International TV Shows, Reality TV, TV Comedies',
       'Docuseries, Reality TV, Teen TV Shows',
       'Crime TV Shows, International TV Shows, Reality TV',
       'Anime Series, Teen TV Shows',
       'Crime TV Shows, Romantic TV Shows, TV Dramas',
       'Anime Features, Romantic Movies',
       'Horror Movies, Sci-Fi & Fantasy, Thrillers',
       'International TV Shows, TV Comedies, TV Sci-Fi & Fantasy',
       'International TV Shows, Romantic TV Shows',
       'Anime Features, Music & Musicals',
       'Anime Features, International Movies, Romantic Movies',
       'International TV Shows, Romantic TV Shows, Teen TV Shows',
       'Docuseries, Stand-Up Comedy & Talk Shows',
       'Horror Movies, Independent Movies, Thrillers',
       'TV Action & Adventure, TV Comedies, TV Horror',
       'Documentaries, Stand-Up Comedy',
       "Kids' TV, Spanish-Language TV Shows",
       "British TV Shows, Kids' TV, TV Thrillers",
       "Kids' TV, TV Action & Adventure, TV Dramas",
       'Anime Series, Crime TV Shows',
       'Dramas, Sci-Fi & Fantasy, Thrillers',
       'TV Comedies, TV Dramas, TV Horror',
       'Children & Family Movies, Comedies, LGBTQ Movies',
       'International TV Shows, TV Action & Adventure, TV Sci-Fi & Fantasy',
       'Docuseries, TV Dramas',
       'Horror Movies, International Movies, Romantic Movies',
       'Crime TV Shows, Docuseries, Science & Nature TV',
       'International Movies, Music & Musicals, Thrillers',
       "Kids' TV, Spanish-Language TV Shows, Teen TV Shows",
       'Comedies, Horror Movies, Independent Movies',
       'Action & Adventure, International Movies, Sports Movies',
       'Action & Adventure, Independent Movies, Sci-Fi & Fantasy',
       'Horror Movies, LGBTQ Movies, Music & Musicals',
       'Comedies, Music & Musicals, Sports Movies',
       'TV Horror, TV Mysteries, Teen TV Shows',
       'Romantic TV Shows, TV Comedies',
       "Kids' TV, Reality TV, Science & Nature TV",
       'International Movies, Romantic Movies, Sci-Fi & Fantasy',
       'TV Comedies, TV Horror, TV Thrillers', 'TV Action & Adventure',
       'International TV Shows, Spanish-Language TV Shows, TV Horror',
       'Crime TV Shows, TV Action & Adventure, TV Thrillers',
       'Music & Musicals, Stand-Up Comedy',
       'British TV Shows, TV Comedies',
       'TV Comedies, TV Sci-Fi & Fantasy, Teen TV Shows',
       'TV Comedies, TV Sci-Fi & Fantasy',
       'Romantic TV Shows, Spanish-Language TV Shows, TV Comedies',
       'Crime TV Shows, International TV Shows, TV Sci-Fi & Fantasy',
       'British TV Shows, International TV Shows, Romantic TV Shows',
       "Crime TV Shows, Kids' TV",
       'Horror Movies, International Movies, Sci-Fi & Fantasy',
       'TV Comedies, TV Mysteries',
       'Cult Movies, Horror Movies, Independent Movies',
       'British TV Shows, Docuseries, TV Comedies',
       'Comedies, Documentaries',
       'Reality TV, Science & Nature TV, TV Action & Adventure',
       'TV Comedies, TV Dramas, TV Mysteries',
       'Crime TV Shows, TV Comedies, Teen TV Shows',
       "Docuseries, Kids' TV, Science & Nature TV",
       'Reality TV, Spanish-Language TV Shows',
       'Action & Adventure, Anime Features, Sci-Fi & Fantasy',
       "Crime TV Shows, Kids' TV, TV Comedies",
       'Dramas, Faith & Spirituality, Independent Movies',
       'Documentaries, Faith & Spirituality',
       'British TV Shows, International TV Shows, Stand-Up Comedy & Talk Shows',
       'Comedies, Dramas, Faith & Spirituality',
       'Classic & Cult TV, TV Comedies',
       'Dramas, Romantic Movies, Sports Movies',
       'Stand-Up Comedy & Talk Shows, TV Mysteries, TV Sci-Fi & Fantasy',
       'TV Sci-Fi & Fantasy, TV Thrillers',
       'Comedies, Independent Movies, Music & Musicals',
       'Comedies, Cult Movies, Independent Movies',
       'Documentaries, Dramas, International Movies',
       'British TV Shows, TV Horror, TV Thrillers',
       'British TV Shows, Docuseries, Science & Nature TV',
       'Children & Family Movies, Comedies, Cult Movies', 'Sports Movies',
       'Sci-Fi & Fantasy', 'Comedies, LGBTQ Movies',
       'Comedies, Independent Movies, Thrillers',
       'Classic Movies, Cult Movies, Dramas',
       'British TV Shows, TV Comedies, TV Dramas',
       'Action & Adventure, Children & Family Movies, Independent Movies',
       'Action & Adventure, Documentaries, International Movies',
       'Children & Family Movies, Independent Movies',
       'Comedies, Cult Movies, Dramas',
       'International TV Shows, TV Horror, TV Thrillers',
       'Classic Movies, Thrillers',
       'Crime TV Shows, TV Dramas, TV Horror',
       'British TV Shows, Docuseries, Reality TV',
       'Documentaries, LGBTQ Movies, Music & Musicals',
       'Classic Movies, Dramas, Romantic Movies',
       'Crime TV Shows, Romantic TV Shows, Spanish-Language TV Shows',
       'Classic Movies, Cult Movies, Horror Movies',
       'Anime Series, Crime TV Shows, TV Thrillers',
       'Children & Family Movies, Classic Movies',
       'Classic Movies, Comedies, International Movies',
       'Comedies, Sci-Fi & Fantasy',
       'Action & Adventure, Cult Movies, Dramas',
       'Documentaries, Faith & Spirituality, Music & Musicals',
       'British TV Shows, Classic & Cult TV, TV Comedies',
       'International Movies, Sports Movies', 'International TV Shows',
       "Classic & Cult TV, Kids' TV, Spanish-Language TV Shows",
       'Romantic TV Shows, Spanish-Language TV Shows, TV Dramas',
       'Children & Family Movies, Comedies, Faith & Spirituality',
       'British TV Shows, Crime TV Shows, TV Dramas',
       'Classic Movies, Dramas, Music & Musicals',
       'Cult Movies, Horror Movies, Thrillers',
       'Action & Adventure, Classic Movies, Sci-Fi & Fantasy',
       'TV Action & Adventure, TV Comedies',
       'Classic Movies, Comedies, Music & Musicals', 'Independent Movies',
       'Documentaries, Horror Movies',
       'Classic & Cult TV, TV Horror, TV Mysteries',
       'Comedies, Faith & Spirituality, International Movies',
       'Dramas, Horror Movies, Sci-Fi & Fantasy',
       'British TV Shows, TV Dramas, TV Sci-Fi & Fantasy',
       'Comedies, Cult Movies, Horror Movies',
       'Comedies, Cult Movies, Sports Movies',
       'Classic Movies, Documentaries',
       'Action & Adventure, Faith & Spirituality, Sci-Fi & Fantasy',
       'Action & Adventure, Children & Family Movies',
       'International TV Shows, Reality TV, TV Action & Adventure',
       'Docuseries, Science & Nature TV, TV Dramas', 'Anime Features',
       'Action & Adventure, Horror Movies, Independent Movies',
       'Action & Adventure, Classic Movies, International Movies',
       'Cult Movies, Independent Movies, Thrillers',
       'Crime TV Shows, TV Comedies',
       'Classic Movies, Cult Movies, Documentaries',
       "Classic & Cult TV, Kids' TV, TV Comedies",
       'Classic Movies, Dramas, LGBTQ Movies',
       'Classic Movies, Dramas, Sports Movies',
       'Action & Adventure, Cult Movies',
       'Action & Adventure, Comedies, Music & Musicals',
       'Classic Movies, Horror Movies, Thrillers',
       'Classic Movies, Comedies, Independent Movies',
       'Children & Family Movies, Classic Movies, Dramas',
       'Dramas, Faith & Spirituality, Sports Movies',
       'Classic Movies, Comedies, Romantic Movies',
       'Dramas, Horror Movies, Music & Musicals',
       'Classic Movies, Independent Movies, Thrillers',
       'Children & Family Movies, Faith & Spirituality',
       'Classic Movies, Comedies, Sports Movies',
       'Comedies, Dramas, Sports Movies',
       'Action & Adventure, Romantic Movies, Sci-Fi & Fantasy',
       'Classic & Cult TV, TV Sci-Fi & Fantasy',
       'Comedies, Cult Movies, LGBTQ Movies',
       'Comedies, Horror Movies, Sci-Fi & Fantasy',
       'Action & Adventure, Comedies, Horror Movies',
       'Classic & Cult TV, Crime TV Shows, TV Dramas',
       'Action & Adventure, Documentaries, Sports Movies',
       'International Movies, LGBTQ Movies, Romantic Movies',
       'Cult Movies, Dramas, Thrillers'], dtype=object)
### Cek Film Berdasarkan Sampel Kategori Film
Melakukan cek film berdasarkan salah satu kategori film yaitu kategori 'TV Action & Adventure, TV Dramas'. Hasilnya sebagai berikut:
|index|show\_id|type|title|director|cast|country|date\_added|release\_year|rating|duration|listed\_in|description|
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|1717|s1718|TV Show|The Liberator|NaN|Bradley James, Martin Sensmeier, Jose Miguel Vasquez, Forrest Goodluck, Bryan Hibbard, Matt Mercurio, Harrison Stone, Billy Breed, Tatanka Means, Kiowa Gordon|United States|November 11, 2020|2020|TV-MA|1 Season|TV Action & Adventure, TV Dramas|A diverse, deeply brave crew of ragtag soldiers become some of the most heroic fighters of the European invasion in World War II\. Based on true events\.|
|5046|s5047|TV Show|Valor|NaN|Christina Ochoa, Matt Barr, Corbin Reid, Charlie Barnett, W\. Tré Davis|United States|February 6, 2018|2017|TV-14|1 Season|TV Action & Adventure, TV Dramas|Following an unsuccessful mission in Somalia, the two surviving members of a U\.S\. Army helicopter crew are embroiled in an unseemly conspiracy\.|
|5836|s5837|TV Show|Marco Polo|NaN|Lorenzo Richelmy, Benedict Wong, Chin Han, Joan Chen, Michelle Yeoh, Rick Yune, Claudia Kim, Remy Hii, Zhu Zhu, Tom Wu, Mahesh Jadu, Olivia Cheng, Uli Latukefu, Pierfrancesco Favino, Jacqueline Chan, Leonard Wu, Gabriel Byrne|United States|July 1, 2016|2016|TV-MA|2 Seasons|TV Action & Adventure, TV Dramas|Set in a world of greed, betrayal, sexual intrigue and rivalry, “Marco Polo” is based on the famed explorer’s adventures in Kublai Khan’s court\.|
|8064|s8065|TV Show|Spartacus|NaN|Andy Whitfield, Liam McIntyre, Dustin Clare, John Hannah, Manu Bennett, Lucy Lawless, Peter Mensah, Nick E\. Tarabay, Viva Bianca, Lesley-Ann Brandt, Jai Courtney, Daniel Feuerriegel|United States| February 1, 2015|2013|TV-MA|4 Seasons|TV Action & Adventure, TV Dramas|A Thracian man is condemned to a brutal death in the arena, only to outlast his executioners and be reborn as the enslaved gladiator Spartacus\.|

### Membuat dictionary berdasarkan id, judul film, dan kategori film
Membuat dictionary berdasarkan id, judul film dan kategori film. Hasilnya sebagai berikut:
|index|id|title|listed\_in|
|---|---|---|---|
|0|s1|Dick Johnson Is Dead|Documentaries|
|1|s2|Blood & Water|International TV Shows, TV Dramas, TV Mysteries|
|2|s3|Ganglands|Crime TV Shows, International TV Shows, TV Action & Adventure|
|3|s4|Jailbirds New Orleans|Docuseries, Reality TV|
|4|s5|Kota Factory|International TV Shows, Romantic TV Shows, TV Comedies|
|5|s6|Midnight Mass|TV Dramas, TV Horror, TV Mysteries|
|6|s7|My Little Pony: A New Generation|Children & Family Movies|
|7|s8|Sankofa|Dramas, Independent Movies, International Movies|
|8|s9|The Great British Baking Show|British TV Shows, Reality TV|
|9|s10|The Starling|Comedies, Dramas|
|10|s11|Vendetta: Truth, Lies and The Mafia|Crime TV Shows, Docuseries, International TV Shows|
|11|s12|Bangkok Breaking|Crime TV Shows, International TV Shows, TV Action & Adventure|
|12|s13|Je Suis Karl|Dramas, International Movies|
|13|s14|Confessions of an Invisible Girl|Children & Family Movies, Comedies|
|14|s15|Crime Stories: India Detectives|British TV Shows, Crime TV Shows, Docuseries|
|15|s16|Dear White People|TV Comedies, TV Dramas|
|16|s17|Europe's Most Dangerous Man: Otto Skorzeny in Spain|Documentaries, International Movies|
|17|s18|Falsa identidad|Crime TV Shows, Spanish-Language TV Shows, TV Dramas|
|18|s19|Intrusion|Thrillers|
|...|...|...|...|

## Modeling
Untuk menemukan kemiripan film berdasarkan kategorinya maka dilakukan beberapa tahapan yaitu:
### Tf-idf Vectorizer
 TFIDF adalah Suatu metode algoritma yang berguna untuk menghitung bobot setiap kata yang umum digunakan. Teknik ini digunakan untuk menemukan representasi fitur penting dari setiap kategori film. 
 Tahapan yang dilakukan yaitu:
 #### Melakukan perhitungan idf pada  fitur listed_in
 Melakukan pembobotan pada fitur listed_in untuk menemukan fitur penting dari setiap kategori film.
 #### Mapping array dari fitur index integer ke fitur nama
 Didapat fitur penting dari setiap kategori film di fitur listed_in. Lalu diubah menjadi array berisi kata dari fitur penting tersebut.
Hasilnya sebagai berikut : ['action', 'adventure', 'anime', 'british', 'children', 'classic', 'comedies', 'comedy', 'crime', 'cult', 'documentaries', 'docuseries', 'dramas', 'faith', 'family', 'fantasy', 'features', 'fi', 'horror', 'independent', 'international', 'kids', 'korean', 'language', 'lgbtq', 'movies', 'music', 'musicals', 'mysteries', 'nature', 'reality', 'romantic', 'sci', 'science', 'series', 'shows', 'spanish', 'spirituality', 'sports', 'stand', 'talk', 'teen', 'thrillers', 'tv', 'up']
Dari output diatas didapat 45 kata penting dalam fitur listed_in
#### Lakukan fit dan transformasi ke dalam bentuk matriks
   Setelah dilakukan transformasi matriks kita akan coba lihat matriks tfidf nya. 
   Didapat shape matriks nya sebagai berikut : (8807, 45)
#### Mengubah vektor tfidf dalam bentuk matriks dengan fungsi todense()
    Hasils matriks sebagai berikut:
    ```
    matrix([[0.        , 0.        , 0.        , ..., 0.        , 0.0.        ],
        [0.        , 0.        , 0.        , ..., 0.        , 0.71023461, 0.        ],
        [0.30013058, 0.30013058, 0.        , ..., 0.        , 0.63809531, 0.        ],
        ...,
        [0.        , 0.        , 0.        , ..., 0.        , 0.        , 0.        ],
        [0.        , 0.        , 0.        , ..., 0.        , 0.        , 0.        ],
        [0.        , 0.        , 0.        , ..., 0.        , 0.        ,  0.        ]])
#### Membuat dataframe untuk melihat tf-idf matrix
Dataframe yang akan dibuat sebagai berikut:
- Kolom diisi dengan kategori film
- Baris diisi dengan judul film

Dan berikut 10 sampel hasilnya sebagai berikut:
|title|comedies|children|movies|up|adventure|shows|independent|fantasy|features|sports|music|anime|thrillers|musicals|tv|sci|docuseries|language|reality|teen|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|The Book of Eli|0\.0|0\.0|0\.0|0\.0|0\.3634007263096119|0\.0|0\.0|0\.49527091045719385|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.49527091045719385|0\.0|0\.0|0\.0|0\.0|
|The Debt Collector 2|0\.0|0\.0|0\.0|0\.0|0\.7071067811865476|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|High & Low The Red Rain|0\.0|0\.0|0\.32945355293097434|0\.0|0\.6206980723060077|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Seven Souls in the Skull Castle: Season Bird|0\.0|0\.0|0\.30616781119130454|0\.0|0\.576827199214963|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Blurred Lines: Inside the Art World|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Time: The Kalief Browder Story|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|1\.0|0\.0|0\.0|0\.0|
|LEGO Ninjago|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.4899278147569689|0\.0|0\.0|0\.0|0\.0|0\.0|
|Cabin Fever|0\.0|0\.0|0\.2950615022347444|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.6409724564050553|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Silicon Cowboys|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|
|Stargate SG-1|0\.0|0\.0|0\.0|0\.0|0\.23734158509350728|0\.0|0\.0|0\.32346766098223334|0\.0|0\.0|0\.0|0\.0|0\.0|0\.0|0\.5046022040460812|0\.32346766098223334|0\.0|0\.0|0\.0|0\.0|

### Cosine Similarity
Teknik ini digunakan untuk mengidentifikasi kesamaan antara satu film dengan film lainnya.
#### Menghitung Cosine Similarity
Hitung cosine similarity dari matriks tfidf sebelumnya yang telah dibuat. Hasilnya sebagai berikut:
array([[1., 0., 0., ..., 0., 0.,0.],[0., 1., 0.62052765, ..., 0., 0.,0.11412729], [0., 0.62052765, 1., ..., 0., 0.,0.04447042], ..., [0., 0., 0., ..., 1., 0.28783572,0.08462917], [0., 0., 0., ..., 0.28783572, 1.,0.0712125 ], [0., 0.11412729, 0.04447042, ..., 0.08462917, 0.0712125 ,1.]])
#### Membuat dataframe dari variabel cosine_sim dengan baris dan kolom berupa judul film
Membuat dataframe dari variabel cosine_sim dengan baris dan kolom berupa judul film. Hasilnya sebagai berikut: 
|title|Good Morning Call|Palazuelos mi rey|Ever After High|Tragic Jungle|For the Love of Spock|
|---|---|---|---|---|---|
|Robocar Poli|0\.5519072940018179|0\.4379458415276092|0\.6848584084665825|0\.0|0\.0|
|Aamir|0\.07485691787345836|0\.05939996852469007|0\.0|0\.36180244626912356|0\.0|
|Flipped|0\.3481741568825253|0\.0|0\.0|0\.3687651455822124|0\.0|
|Agatha and the Truth of Murder|0\.0|0\.0|0\.0|0\.3662988369874051|0\.0|
|Vientos de agua|0\.6967498310591975|0\.9106964835185762|0\.2907276189139735|0\.11557895624245162|0\.0|
|Snowden|0\.0|0\.0|0\.0|0\.1778078916916985|0\.0|
|Mighty Little Bheem: Kite Festival|0\.5800716613013976|0\.3878358478154841|0\.8792204228355435|0\.0|0\.0|
|Black Island|0\.07485691787345836|0\.05939996852469007|0\.0|0\.36180244626912356|0\.0|
|Harvey Street Kids|0\.5800716613013976|0\.3878358478154841|0\.8792204228355435|0\.0|0\.0|
|Sexify|0\.877389465592375|0\.6381687759117486|0\.4090476197029853|0\.16261715042876512|0\.0|

#### Membuat Fungsi Rekomendasi Film
Membuat fungsi rekomendasi Film berdasarkan kemiripan dataframe

Parameter:
---
title : tipe data string (str)
            Judul film (index kemiripan dataframe)
similarity_data : tipe data pd.DataFrame (object)
                  Kesamaan dataframe, simetrik, dengan judul film sebagai 
                  indeks dan kolom
items : tipe data pd.DataFrame (object)
        Mengandung kedua nama dan fitur lainnya yang digunakan untuk mendefinisikan kemiripan
k : tipe data integer (int)
    Banyaknya jumlah rekomendasi yang diberikan
---
Pada index ini, kita mengambil k dengan nilai similarity terbesar 
pada index matrix yang diberikan (i).

Sebagai contoh kita akan kita akan cek rekomendasi film memiliki kategori yang mirip dengan film 'Jaguar'
|index|id|title|listed\_in|
|---|---|---|---|
|19|s20|Jaguar|International TV Shows, Spanish-Language TV Shows, TV Action & Adventure|

Hasilnya sebagai berikut:
|index|title|listed\_in|
|---|---|---|
|0|The Ministry of Time|International TV Shows, Spanish-Language TV Shows, TV Action & Adventure|
|1|Sky Rojo|International TV Shows, Spanish-Language TV Shows, TV Action & Adventure|
|2|Diablero|International TV Shows, Spanish-Language TV Shows, TV Action & Adventure|
|3|Victim Number 8|International TV Shows, Spanish-Language TV Shows, TV Action & Adventure|
|4|El Chema|Crime TV Shows, Spanish-Language TV Shows, TV Action & Adventure|



## Referensi
Reddy, S., Nalluri, S., Kunisetti, S., Ashok, S., Venkatesh, B.
        &emsp; &emsp;Content-Based Movie Recommendation System Using Genre Correlation
         &emsp; &emsp;Smart Intelligent Computing and Applications . Smart Innovation, Systems and Technologies, vol 105. Springer, Singapore (2019)
