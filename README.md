# Laporan Proyek Machine Learning - Zahwa Genoveva
---
## Domain Proyek 
---
Proyek ini berfokus pada penerapan machine learning di bidang hiburan, khususnya pada rekomendasi anime. Ini adalah proyek akhir sistem rekomendasi untuk memenuhi submission dicoding. Proyek ini membangun model berbasis content based filtering yang dapat menentukan top-N rekomendasi anime.



* #####  Latar Belakang

  ![](https://cloudfront-us-east-1.images.arcpublishing.com/infobae/AK5OFYSU3RDA5KJOIQDN4MXQRQ.jpg)
  
Dalam dunia hiburan digital, platform streaming anime memiliki jumlah judul yang sangat banyak, membuat pengguna sering kesulitan memilih anime yang sesuai dengan preferensi mereka. Sistem rekomendasi dapat menjadi solusi untuk masalah ini, dengan memberikan saran anime yang relevan berdasarkan minat pengguna. Dengan memanfaatkan teknologi Content-Based Filtering, kita dapat membangun sistem rekomendasi yang mempertimbangkan kesamaan konten, seperti genre atau sinopsis, untuk memberikan rekomendasi anime yang sesuai dengan preferensi pengguna.
## Business Understanding
---
#### Problem Statements
Pengguna sering merasa kesulitan memilih anime yang sesuai dengan preferensi mereka karena banyaknya pilihan yang tersedia. Tanpa sistem rekomendasi, pengguna memerlukan waktu lebih lama untuk menemukan anime yang sesuai dengan minat mereka, yang dapat mengurangi pengalaman menonton.


#### Goals
Tujuan dari proyek ini adalah untuk menyediakan rekomendasi anime yang lebih relevan dan personal bagi pengguna. Dengan menggunakan sistem rekomendasi berbasis konten, pengguna dapat dengan cepat menemukan anime yang sesuai dengan selera mereka, berdasarkan anime yang sudah mereka tonton atau pilih sebelumnya. Sistem ini bertujuan untuk meningkatkan pengalaman menonton pengguna dengan memberikan pilihan anime yang tepat.

#### Solution Statements
Solusi yang dapat diimplementasikan untuk mencapai tujuan ini adalah dengan membangun model sistem rekomendasi menggunakan Content-Based Filtering. Dengan pendekatan ini, sistem akan memberikan rekomendasi anime yang relevan berdasarkan konten yang dimiliki, seperti genre dan sinopsis. Metode Cosine Similarity akan digunakan untuk mengukur kesamaan antara anime, memungkinkan sistem memberikan daftar anime yang paling mirip dengan anime yang sudah dipilih oleh pengguna.


## Data Understanding
---
![Image of Dataset](https://github.com/user-attachments/assets/7b575bbb-4e3f-412b-8620-8f1a087903c9)
Informasi dataset dapat dilihat pada **Tabel 1. Informasi dataset** dibawah ini :
Jenis | Keterangan
--- | ---
Sumber | [Kaggle Dataset : Anime Dataset 2023](https://www.kaggle.com/datasets/dbdmobile/myanimelist-dataset/data?select=anime-filtered.csv)
Lisensi | Data files © Original Authors
Kategori | Arts and Entertainment, Movies and TV Shows, Anime and Manga, Popular Culture, Japan
Usability |	10.00
Jenis dan Ukuran Berkas | CSV (9.72 mB)

---

Pada tahap ini, kita akan menganalisis struktur dan karakteristik dataset yang digunakan. Dataset terdiri dari 9 kolom dan 4001 baris, dengan rincian sebagai berikut:

### __1. Deskripsi Data__

Dataset ini terdiri dari 14,952 entri yang masing-masing mewakili satu judul anime. Ada 25 kolom yang menyimpan berbagai informasi tentang anime, seperti nama, genre, skor, dan deskripsi singkat. Beberapa kolom penting yang kita gunakan dalam sistem rekomendasi adalah:
- **Name**: Nama anime.
- **Score**: Skor rata-rata yang diberikan oleh pengguna.
- **Genres**: Genre atau kategori anime (misalnya, Action, Drama, Sci-Fi).
- **Synopsis**: Deskripsi singkat tentang anime.
- **Type**: Jenis anime (misalnya, TV Series, Movie).
- **Studios**: Studio yang memproduksi anime.
- **Rating**: Rating konten anime (misalnya, PG, R).

### __2. Statistik Dasar__

- **Jumlah Entri**: 14,952 anime.
- **Kolom yang Tersedia**: Ada 25 kolom dengan data yang beragam seperti angka (numeric) dan kategori (kategori teks).
- **Data Missing**: Beberapa kolom seperti *Synopsis* dan *Ranked* memiliki nilai yang hilang pada beberapa entri.

### __3. Visualisasi__

Dalam bagian ini, kita akan membahas beberapa visualisasi yang memberikan gambaran lebih jelas mengenai dataset anime yang digunakan. Berikut adalah tiga visualisasi utama yang dapat membantu memahami distribusi dan pola dalam data.

#### - Distribusi Jumlah Anime Berdasarkan Tipe
Visualisasi ini menunjukkan distribusi jumlah anime berdasarkan tipe (misalnya, TV Series, Movie, OVAs, dll). Dari visualisasi ini, kita dapat melihat tipe anime yang paling banyak ditemukan dalam dataset. Ini akan memberikan informasi tentang seberapa populer atau dominannya setiap tipe anime di dalam koleksi dataset kita.

![Distribusi Jumlah Anime](https://github.com/user-attachments/assets/aa264b76-2028-4389-8929-f802f8318dee)

- Bar chart yang menunjukkan jumlah anime untuk masing-masing tipe seperti TV Series, Movie, OVA, dll.

#### - Top 20 Anime dengan Rating Tertinggi
Dalam visualisasi ini, kita menampilkan 20 anime dengan rating tertinggi berdasarkan skor yang diberikan oleh pengguna. Ini memberikan gambaran mengenai anime yang paling disukai dan mendapat penilaian terbaik. Visualisasi ini membantu kita untuk melihat anime mana saja yang paling dihargai oleh komunitas.

![top](https://github.com/user-attachments/assets/cd13053f-940b-4fc8-bbf3-84a47fb930c9)

- Bar chart atau horizontal bar chart berikut menampilkan nama anime dan skor tertinggi mereka.

#### - 10 Genre Anime Terbanyak
Visualisasi ini memperlihatkan genre-genre anime yang paling banyak muncul dalam dataset. Setiap anime dapat memiliki lebih dari satu genre, sehingga genre yang muncul lebih dari sekali akan lebih sering tampil dalam daftar ini. Dengan visualisasi ini, kita bisa memahami genre anime yang paling populer dan sering dicari oleh pengguna.

![genre](https://github.com/user-attachments/assets/bc09aa50-ac69-49ee-bc07-8d30c9548ea8)

- Bar chart yang menampilkan genre dengan jumlah anime terbanyak. Ini memungkinkan kita untuk mengetahui genre yang paling banyak ditemukan dalam koleksi dataset.

Dengan visualisasi ini, kita bisa mendapatkan wawasan yang lebih mendalam tentang bagaimana distribusi anime dalam berbagai kategori (tipe dan genre), serta mengidentifikasi anime-anime yang paling populer berdasarkan rating.

## Data Preparation
---
Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:
