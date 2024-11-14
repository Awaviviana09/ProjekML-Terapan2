# Laporan Proyek Machine Learning - Zahwa Genoveva
---
## Domain Proyek 
---
Proyek ini berfokus pada penerapan machine learning di bidang hiburan, khususnya pada rekomendasi anime, dengan judul proyek "Sistem Rekomendasi Anime Menggunakan Algoritma Cosine Similarity dan Collaborative Filtering".



* #####  Latar Belakang
Rekomendasi anime menjadi salah satu solusi penting dalam industri hiburan, mengingat jumlah judul anime yang terus berkembang. 
Dengan banyaknya pilihan anime yang tersedia, banyak pengguna yang kesulitan menemukan anime yang sesuai dengan preferensi mereka. 
Oleh karena itu, pengembangan sistem rekomendasi yang efektif dan efisien menjadi sangat penting. Berbagai metode telah diterapkan untuk meningkatkan kualitas rekomendasi, baik itu melalui pendekatan berbasis konten, collaborative filtering, atau teknik hybrid yang menggabungkan keduanya.
  
  ![](https://cloudfront-us-east-1.images.arcpublishing.com/infobae/AK5OFYSU3RDA5KJOIQDN4MXQRQ.jpg)
  
Salah satu teknik yang populer adalah penggunaan cosine similarity untuk menghitung kemiripan antar item (anime) berdasarkan fitur yang ada, seperti genre, rating, atau atribut lainnya. 
Metode ini memungkinkan sistem rekomendasi memberikan rekomendasi yang lebih relevan dan sesuai dengan preferensi pengguna, tanpa memerlukan data eksplisit tentang preferensi pengguna sebelumnya. 
Penggunaan machine learning dalam sistem rekomendasi ini dapat mengungkap pola yang lebih kompleks yang sulit ditemukan dengan metode konvensional.
## Business Understanding
---
#### Problem Statements
Berdasarkan latar belakang di atas, beberapa masalah yang dapat diidentifikasi dalam proyek ini adalah:

* Bagaimana cara merancang sistem rekomendasi anime yang mampu memberikan rekomendasi yang relevan kepada pengguna?
* Apa faktor-faktor yang harus dipertimbangkan untuk meningkatkan akurasi rekomendasi dalam sistem?
* Bagaimana cara mengatasi masalah sparsity dalam data pengguna dan item yang terbatas?
* Algoritma apa yang paling efektif dalam memberikan rekomendasi anime yang tepat berdasarkan preferensi pengguna?


#### Goals
* Mengembangkan sistem rekomendasi anime menggunakan cosine similarity dan algoritma collaborative filtering.
* Mengoptimalkan akurasi sistem rekomendasi sehingga mampu memberikan rekomendasi dengan relevansi tinggi sesuai dengan rating atau preferensi pengguna.
* Membangun model yang dapat memberikan rekomendasi untuk pengguna berdasarkan input berupa anime favorit atau preferensi genre.

#### Solution Statements
Untuk mencapai tujuan proyek ini, beberapa solusi yang dapat diterapkan adalah:

* Data Preprocessing:

  * Membersihkan dan menyiapkan data anime, termasuk penghapusan data yang tidak relevan dan pengisian nilai yang hilang.
  * Melakukan konversi data ke format yang sesuai untuk model, termasuk encoding kategori seperti genre dan studio.
  * Melakukan pembagian data menjadi data latih dan uji untuk menguji performa model.

* Algoritma Rekomendasi:

  * Cosine Similarity: Digunakan untuk menghitung kemiripan antar anime berdasarkan atribut yang ada, seperti genre, rating, dan studi yang terlibat. Teknik ini berguna untuk menemukan anime yang mirip dengan anime yang disukai pengguna.
  * Collaborative Filtering: Menggunakan data interaksi pengguna (misalnya rating) untuk memberikan rekomendasi berdasarkan preferensi pengguna yang serupa. Metode ini dapat meningkatkan relevansi rekomendasi dengan memanfaatkan data interaksi antar pengguna.
  * Matrix Factorization: Sebagai metode alternatif yang dapat digunakan untuk menangani masalah sparsity dalam data rekomendasi, dengan memecah matriks interaksi pengguna-item menjadi dua matriks yang lebih kecil dan memprediksi rating yang hilang.

* Evaluasi Model:

  * Mengukur performa sistem rekomendasi dengan menggunakan metrik seperti akurasi dan presisi. Akurasi dapat dihitung berdasarkan seberapa sering rekomendasi anime yang relevan ditemukan dalam daftar top-N rekomendasi.
  * Precision dihitung dengan membandingkan anime yang direkomendasikan dengan anime yang disukai pengguna, serta mengukur persentase rekomendasi yang memiliki rating tinggi (di atas threshold yang ditentukan).


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

###  1. Deskripsi Data
