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

- Melakukan cek data yang kosong
- Melakukan cek jumlah film
- Melakukan cek jumlah kategori film
- Melakukan cek kategori film berdasarkan sampel
- Membuang data duplikat
- Membuat dictionary berdasarkan id, judul film, dan kategori film

## Modeling
Untuk menemukan kemiripan film berdasarkan kategorinya maka dilakukan beberapa tahapan yaitu:
- tf-idf vectorizer: teknik ini digunakan untuk menemukan representasi fitur penting dari setiap kategori film.
- Cosine Similarity: mengidentifikasi kesamaan antara satu film dengan film lainnya
- Membuat Fungsi Rekomendasi Film

## Referensi
Reddy, S., Nalluri, S., Kunisetti, S., Ashok, S., Venkatesh, B.
        &emsp; &emsp;Content-Based Movie Recommendation System Using Genre Correlation
         &emsp; &emsp;Smart Intelligent Computing and Applications . Smart Innovation, Systems and Technologies, vol 105. Springer, Singapore (2019)
