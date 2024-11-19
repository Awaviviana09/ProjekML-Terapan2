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

## _Content-Based Filtering_

Dalam proyek ini, digunakan pendekatan content-based filtering untuk merekomendasikan anime berdasarkan kemiripan atribut konten seperti genre. Pendekatan ini bergantung pada pengolahan teks menjadi representasi numerik menggunakan metode TF-IDF (Term Frequency-Inverse Document Frequency) dan penghitungan kemiripan menggunakan Cosine Similarity. Berikut adalah penjelasan teori yang mendasari metode ini, kelebihan, kekurangan, serta implementasi dan pengujian modelnya.

- Kelebihan:
  - Memberikan rekomendasi yang relevan sesuai preferensi pengguna.
  - Tidak bergantung pada data pengguna lain, hanya pada interaksi pengguna tersebut.
  - Dapat digunakan untuk pengguna baru yang sudah memiliki sedikit data interaksi.
  - Mudah dijelaskan karena rekomendasi didasarkan pada kesamaan atribut.
  - Skalabel selama data atribut tersedia.

- Kekurangan:
  - Sulit merekomendasikan item baru yang belum memiliki data (cold start).
  - Hanya merekomendasikan item yang mirip, sehingga kurang memberikan variasi.
  - Bergantung pada kualitas data atribut konten.
  - Terbatas pada item yang serupa, sehingga eksplorasi pengguna berkurang.
  - Membutuhkan waktu untuk mengolah data atribut agar akurat.

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



### 2. Implementasi Model

#### 2.1 Proses Pembuatan Model

- Fungsi Rekomendasi, Fungsi berikut mengambil anime tertentu dan mengembalikan daftar rekomendasi berdasarkan kemiripan tertinggi:


      import pandas as pd
      from IPython.display import display, HTML
      
      def anime_recommendations(anime_name, similarity_data, items, k=5):
          """Dapatkan rekomendasi anime berdasarkan data kemiripan."""
          index = similarity_data.loc[:, anime_name].to_numpy().argpartition(range(-1, -k, -1))
          closest = similarity_data.columns[index[-1:-(k+1):-1]].drop(anime_name, errors='ignore')
          return items[items['Name'].isin(closest)].head(k)
      
      def main():
          anime_name = input("Masukkan nama anime: ").strip().lower()
          df_lower = df.assign(Name=df['Name'].str.lower())
      
          if anime_name in df_lower['Name'].values:
              recommendations = anime_recommendations(
                  anime_name.capitalize(),
                  cosine_sim_df,
                  df[['Name', 'Score', 'Genres', 'sypnopsis', 'Type', 'Episodes', 'Studios', 'Rating']]
              )
              display(HTML(recommendations.to_html(index=False, justify='center')))
          else:
              print(f"Anime '{anime_name.capitalize()}' tidak ditemukan.")
      
      if __name__ == "__main__":
          main()

- Uji Coba Model Sebagai contoh, diberikan input anime "Naruto", berikut hasil rekomendasinya:


| **Name**                      | **Score** | **Genres**                                           | **Synopsis**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | **Type**   | **Episodes** | **Studios**      | **Rating**               |
|-------------------------------|-----------|-----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|--------------|------------------|--------------------------|
| Rekka no Honoo                | 7.36      | Action, Adventure, Martial Arts, Shounen, Super Power | Most people think that ninjas are a thing of the past, but Rekka Hanabishi wishes otherwise. Although he comes from a family that makes fireworks, he likes to think of himself as a self-styled, modern-day ninja. Sounds like fun, right? Maybe not. Rekka ends up in lots of fights because he once made the bold announcement that if someone can defeat him, he will become their servant. Then one day, Rekka meets Yanagi Sakoshita, a gentle girl with the ability to heal any wound or injury. Their meeting sets off a chain of events, which culminate into a shocking discovery. Rekka is the last surviving member of a legendary ninja clan that was wiped out centuries ago. Even more astonishing than being an actual ninja, he also wields the power to control fire. What does this mean for Rekka? Who are these strange people after him and Yanagi? Find out in Rekka no Honoo! | TV         | 42           | Studio Pierrot   | PG-13 - Teens 13 or older |
| Naruto: Shippuuden            | 8.16      | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen | It has been two and a half years since Naruto Uzumaki left Konohagakure, the Hidden Leaf Village, for intense training following events which fueled his desire to be stronger. Now Akatsuki, the mysterious organization of elite rogue ninja, is closing in on their grand plan which may threaten the safety of the entire shinobi world. Although Naruto is older and sinister events loom on the horizon, he has changed little in personality—still rambunctious and childish—though he is now far more confident and possesses an even greater determination to protect his friends and home. Come whatever may, Naruto will carry on with the fight for what is important to him, even at the expense of his own body, in the continuation of the saga about the boy who wishes to become Hokage.                                                                                      | TV         | 500          | Studio Pierrot   | PG-13 - Teens 13 or older |
| Boruto: Naruto Next Generations | 5.81     | Action, Adventure, Super Power, Martial Arts, Shounen | Following the successful end of the Fourth Shinobi World War, Konohagakure has been enjoying a period of peace, prosperity, and extraordinary technological advancement. This is all due to the efforts of the Allied Shinobi Forces and the village's Seventh Hokage, Naruto Uzumaki. Now resembling a modern metropolis, Konohagakure has changed, particularly the life of a shinobi. Under the watchful eye of Naruto and his old comrades, a new generation of shinobi has stepped up to learn the ways of the ninja. Boruto Uzumaki is often the center of attention as the son of the Seventh Hokage. Despite having inherited Naruto's boisterous and stubborn demeanor, Boruto is considered a prodigy and is able to unleash his potential with the help of supportive friends and family. Unfortunately, this has only worsened his arrogance and his desire to surpass Naruto which, along with his father's busy lifestyle, has strained their relationship. However, a sinister force brewing within the village may threaten Boruto's carefree life. New friends and familiar faces join Boruto as a new story begins in Boruto: Naruto Next Generations.                    | TV         | Unknown      | Studio Pierrot   | PG-13 - Teens 13 or older |
| Boruto: Jump Festa 2016 Special | 6.22     | Action, Adventure, Comedy, Super Power, Martial Arts, Shounen | The special anime adaptation of Boruto will be screening at Shueisha’s by-invitation anime event Jump Special Anime Festa 2016!                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Special    | 1            | Studio Pierrot   | PG-13 - Teens 13 or older |


Berdasarkan Tabel 1. Hasil Pengujian Model Content-Based Filtering (dengan Filter Genres), sistem telah berhasil merekomendasikan anime yang paling mirip dengan Naruto. Rekomendasi ini mencakup beberapa seri dan film dari waralaba Naruto itu sendiri, seperti Naruto: Shippuuden dan Boruto: Naruto Next Generations. Hal ini menunjukkan bahwa jika seorang pengguna menyukai Naruto, sistem dapat memberikan rekomendasi untuk seri atau film lain dalam waralaba yang sama. Dengan pendekatan ini, sistem mengidentifikasi anime-anime yang memiliki kemiripan dalam genre dengan Naruto, sehingga pengguna dapat menemukan konten yang relevan dengan preferensi mereka berdasarkan kesukaan terhadap anime tersebut.


## Evaluation
---

Untuk menentukan kinerja model, perlu untuk mengevaluasi model yang sudah dibangun. Evaluasi sistem rekomendasi dilakukan menggunakan metrik precision. Precision digunakan untuk mengukur sejauh mana sistem memberikan rekomendasi yang relevan terhadap kebutuhan pengguna. Dalam kasus ini, rekomendasi dianggap relevan jika skor anime (Score) lebih tinggi dari ambang batas tertentu, yaitu 5. Metrik ini bertujuan mengukur seberapa relevan rekomendasi yang dihasilkan oleh sistem terhadap kebutuhan pengguna. Berikut adalah penjelasan detail proses evaluasi.

---
__Proses Evaluasi__

__1. Input Evaluasi:__

Anime yang diinputkan oleh pengguna adalah "Doraemon".
Sistem menghasilkan 10 rekomendasi teratas (top-10 recommendations) yang paling mirip dengan Doraemon, berdasarkan kesamaan atribut seperti genre, studio, dan skor (Score).

__2. Definisi Relevansi:__

Untuk menentukan relevansi, kami menetapkan ambang batas (threshold) skor sebesar 5.
Anime dengan skor (Score) lebih besar dari 5 dianggap relevan, sedangkan yang lainnya tidak relevan.


__3. Perhitungan Precision:__

Precision dihitung dengan rumus berikut:

<p align="center">
  <img src="https://github.com/user-attachments/assets/20de3ebe-f245-4aa6-98e2-a3d7e35974ec" alt="tf-idf">
</p>

Di mana:
Jumlah Rekomendasi Relevan: Jumlah anime dalam daftar rekomendasi yang skornya melebihi ambang batas (Score > 5).

Jumlah Total Rekomendasi (k): Total jumlah rekomendasi yang diberikan oleh sistem (dalam hal ini, 
𝑘 = 10).

__4. Hasil Evaluasi:__

Dari hasil rekomendasi:
9 dari 10 anime yang direkomendasikan memiliki skor lebih besar dari 5.
Dengan demikian, precision dihitung sebagai berikut:

<p align="center">
  <img src="https://github.com/user-attachments/assets/e17abe3e-9195-4d67-a3ca-244b6fec2a20" alt="tf-idf">
</p>

kode program:

<p align="center">
  <img src="https://github.com/user-attachments/assets/8f6f87e4-24d6-4c8c-829b-d1ec78e3060b">
</p>

Berdasarkan evaluasi di atas, precision sistem adalah 90%. Ini berarti, dari setiap 10 rekomendasi yang diberikan oleh sistem, 9 di antaranya relevan dengan kebutuhan pengguna. Hasil ini menunjukkan bahwa sistem mampu secara efektif merekomendasikan anime dengan kualitas yang sesuai berdasarkan preferensi input awal.


### Kesimpulan
---

Sistem rekomendasi berbasis Content-Based Filtering yang diuji dengan input "Naruto" berhasil memberikan rekomendasi dengan tingkat relevansi yang baik, mencapai precision sebesar 90%. Hal ini menunjukkan bahwa sistem mampu mengenali dan merekomendasikan anime yang sesuai dengan preferensi pengguna berdasarkan kemiripan atribut. Meskipun demikian, terdapat peluang untuk meningkatkan akurasi dengan mempertimbangkan atribut tambahan seperti ulasan pengguna atau tingkat popularitas. Secara keseluruhan, sistem ini efektif untuk membantu pengguna menemukan konten yang relevan dan sesuai dengan kesukaannya.

## Referensi
--- 
 
[1] Sellitasari, Shelvi., Ainurrasyid., & Suryanto, Agus. (2013). _PERBEDAAN PRODUKSI TANAMAN APEL (Malus sylvestris mill.) PADA AGROKLIMAT YANG BERBEDA (Studi Kasus Pada Sentra Produksi Tanaman Apel di Kota Batu dan Kabupaten Malang)_. Tersedia: [tautan](https://protan.studentjournal.ub.ac.id/index.php/protan/article/view/1). Diakses pada 24 Oktober 2024.
