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

- **Distribusi Jumlah Anime Berdasarkan Tipe**  
   Visualisasi ini menunjukkan jumlah anime berdasarkan tipe (TV, Movie, OVA, dll). Gambar di atas membantu memahami jenis anime yang mendominasi dataset.

- **Top 20 Anime dengan Rating Tertinggi**  
   Gambar ini menampilkan daftar 20 anime dengan skor tertinggi yang menunjukkan anime paling populer di dataset.

- **10 Genre Anime Terbanyak**  
   Visualisasi ini memperlihatkan genre yang paling sering muncul, memberikan wawasan tentang preferensi genre dalam dataset.


Berikut adalah tabel yang berisi gambar visualisasi untuk setiap analisis:


| **Visualisasi**                         | **Gambar**                                                                                           |
|-----------------------------------------|-----------------------------------------------------------------------------------------------------|
| **Distribusi Jumlah Anime Berdasarkan Tipe** | ![Distribusi Jumlah Anime](https://github.com/user-attachments/assets/aa264b76-2028-4389-8929-f802f8318dee)                               |
| **Top 20 Anime dengan Rating Tertinggi** | ![top](https://github.com/user-attachments/assets/cd13053f-940b-4fc8-bbf3-84a47fb930c9)                                   |
| **10 Genre Anime Terbanyak**            | ![genre](https://github.com/user-attachments/assets/bc09aa50-ac69-49ee-bc07-8d30c9548ea8)                                               |


Dengan visualisasi ini, kita bisa mendapatkan wawasan yang lebih mendalam tentang bagaimana distribusi anime dalam berbagai kategori (tipe dan genre), serta mengidentifikasi anime-anime yang paling populer berdasarkan rating.

## Data Preparation
---
Berikut adalah tahapan-tahapan dalam melakukan pra-pemrosesan data:


### **1. Penanganan Nilai Hilang**
Pada tahap awal, dilakukan identifikasi nilai hilang. Berikut adalah jumlah nilai hilang sebelum dilakukan pembersihan:

| Kolom       | Nilai Hilang |
|-------------|--------------|
| Name        | 0            |
| Score       | 0            |
| Genres      | 0            |
| Type        | 0            |
| sypnopsis   | 1350         |
| Studios     | 0            |
| Episodes    | 0            |
| Rating      | 0            |

Kolom **sypnopsis** ditemukan memiliki 1.350 baris dengan nilai kosong, sedangkan kolom lainnya tidak memiliki nilai hilang. Untuk memastikan integritas data, baris dengan nilai kosong pada kolom ini dihapus.

Setelah pembersihan, jumlah nilai hilang adalah sebagai berikut:

| Kolom       | Nilai Hilang |
|-------------|--------------|
| Name        | 0            |
| Score       | 0            |
| Genres      | 0            |
| Type        | 0            |
| sypnopsis   | 0            |
| Studios     | 0            |
| Episodes    | 0            |
| Rating      | 0            |

Jumlah data setelah pembersihan adalah **13.602 baris**. 

---

### **2. Jumlah Data Sebelum dan Sesudah Pembersihan**

| Kondisi                 | Jumlah Data |
|-------------------------|-------------|
| Sebelum Pembersihan     | 14.952      |
| Setelah Pembersihan     | 13.602      |

Sebanyak **1.350 baris** dihapus karena adanya nilai hilang pada kolom **sypnopsis**.

---

### **3. Penghapusan Kolom yang Tidak Dibutuhkan**
Beberapa kolom yang tidak relevan untuk analisis lebih lanjut dihapus, yaitu:

- **anime_id**
- **English name**
- **Japanese name**
- **Aired**
- **Premiered**
- **Producers**
- **Licensors**
- **Source**
- **Duration**
- **Ranked**
- **Popularity**
- **Members**
- **Favorites**
- **Watching**
- **Completed**
- **On-Hold**
- **Dropped**

Setelah penghapusan kolom, dataset hanya menyisakan kolom berikut untuk dianalisis lebih lanjut:

| **Kolom**    | **Deskripsi**                                                    |
|--------------|------------------------------------------------------------------|
| Name         | Nama anime                                                      |
| Score        | Skor rating dari pengguna                                       |
| Genres       | Genre atau kategori anime                                       |
| sypnopsis    | Sinopsis anime                                                  |
| Type         | Jenis anime (TV, Movie, dll.)                                   |
| Episodes     | Jumlah episode                                                  |
| Studios      | Studio produksi anime                                           |
| Rating       | Rating berdasarkan kategori usia (PG-13, R, dll.)               |

---

### **4. Informasi Dataset Setelah Pembersihan**
Dataset yang telah dibersihkan memiliki struktur sebagai berikut:

- Jumlah baris: **13.602**
- Jumlah kolom: **8**
- Tipe data: Kombinasi integer, float, dan object.






# Modeling
---

Dalam proyek ini, digunakan pendekatan content-based filtering untuk merekomendasikan anime berdasarkan kemiripan atribut konten seperti genre. Pendekatan ini bergantung pada pengolahan teks menjadi representasi numerik menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency) dan penghitungan kemiripan menggunakan Cosine Similarity. Berikut adalah penjelasan teori yang mendasari metode ini, kelebihan, kekurangan, serta implementasi dan pengujian modelnya.

### 1. Algoritma yang Digunakan

#### 1.1 TF-IDF (Term Frequency - Inverse Document Frequency)

**TF-IDF** adalah metode yang digunakan untuk mengubah data teks menjadi vektor numerik. Setiap kata diberikan bobot yang lebih tinggi jika kata tersebut sering muncul dalam dokumen tertentu, namun jarang ditemukan dalam dokumen lainnya. Ini memastikan bahwa kata-kata yang lebih relevan untuk suatu dokumen akan diberi bobot lebih besar.

#### Rumus TF-IDF:

<p align="center">
  <img src="https://github.com/user-attachments/assets/06202bcb-9e97-4269-b7fa-daa9ab60e6f6" alt="tf-idf">
</p>


Di mana:

![pisah rumus](https://github.com/user-attachments/assets/e3ec8588-212e-45a8-bce7-bab771a3a944)


Keterangan:

    - \( t \) adalah term atau kata yang sedang dihitung.
    - \( d \) adalah dokumen tempat kata \( t \) muncul.
    - \( N \) adalah jumlah total dokumen dalam koleksi data.



#### 1.2 Cosine Similarity

Setelah mengubah data teks menjadi vektor menggunakan TF-IDF, kita menghitung kesamaan antara anime menggunakan **Cosine Similarity**. Cosine Similarity mengukur kesamaan antara dua vektor dengan menghitung sudut antara keduanya. Semakin kecil sudutnya, semakin mirip kedua vektor tersebut.

#### Rumus Cosine Similarity:

<p align="center">
  <img src="https://github.com/user-attachments/assets/25b0a410-58a1-4988-a597-699120475bf1" alt="tf-idf">
</p>

Keterangan:

    - (A·B)menyatakan produk titik dari vektor A dan B.
    - ||A|| mewakili norma Euclidean (magnitudo) dari vektor A.
    - ||B|| mewakili norma Euclidean (magnitudo) dari vektor B.

Untuk melakukan pengujian model, digunakan potongan kode berikut.

## 3. Implementasi Model

### 3.1 Proses Pembuatan Model

1. **Menggunakan TfidfVectorizer**: Kami menggunakan `TfidfVectorizer` dari pustaka `sklearn` untuk mengubah data teks (kolom 'Genres') menjadi representasi vektor TF-IDF.
   
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity
import pandas as pd

# Menggunakan TfidfVectorizer untuk menghasilkan matriks TF-IDF
tfidf_vectorizer = TfidfVectorizer()
tfidf_matrix = tfidf_vectorizer.fit_transform(df['Genres'])

# Menghitung Cosine Similarity antara anime
cosine_sim = cosine_similarity(tfidf_matrix)

# Membuat DataFrame dari Cosine Similarity
cosine_sim_df = pd.DataFrame(cosine_sim, index=df['Name'], columns=df['Name'])
print("Shape dari cosine similarity matrix:", cosine_sim_df.shape)
