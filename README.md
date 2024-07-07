# PENGOLAHAN CITRA TUGAS UAS
## Segementasi Gambar Citra Digital Dengan Algoritma K-means Clustering
Dibuat Oleh:
* SATRIA WIGUNA  **312210530**
* LATIF NUR ANHARI  **312210xxx**
* M. ZAINAL MUTAQIM  **312210xxx**

---
#### A. K-means Clustering
---
K-means Clustering adalah metode segmentasi gambar yang digunakan untuk mengelompokkan data (piksel-piksel) ke dalam sejumlah bagian (cluster) di mana setiap cluster memiliki pusat (centroid) yang mewakili karakteristik kelompok tersebut berdasarkan kesamaan warna, tekstur atau intensitasnya. Tujuannya adalah untuk menyederhanakan representasi gambar dan mempermudah analisis dengan mengelompokkan piksel yang memiliki karakteristik serupa ke dalam cluster yang sama. 

![ilustrasi](https://github.com/kelaskodingpelitabangsa/UAS4-Pengolahan-Citra/blob/main/ilustrasi.png)

#### B. Penjelasan Program
---
Berikut adalah program Python yang telah dirapikan dan dijelaskan setiap langkahnya. Program ini menggunakan OpenCV untuk memproses gambar, melakukan clustering dengan algoritma k-means, dan menampilkan hasilnya menggunakan matplotlib.

#### 1. Import Library
```
import numpy as np
import matplotlib.pyplot as plt
import cv2
```

* ```NumPy```: Digunakan untuk operasi array, yang sangat penting untuk manipulasi gambar.
* ```Matplotlib```: Digunakan untuk menampilkan gambar dan hasil segmentasi.
* ```cv2```: Digunakan untuk membaca dan memproses gambar.

#### 2. Membaca dan Mengkonversi Gambar
```
image = cv2.imread('images/satria.jpg')
image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
```

* ```cv2.imread('images/relax.jpg')```: Membaca gambar dari file dengan nama ```satria.jpg``` di folder ```images```. OpenCV membaca gambar dalam format BGR (Blue, Green, Red).
* ```cv2.cvtColor(image, cv2.COLOR_BGR2RGB)```: Mengkonversi gambar dari format BGR ke RGB karena matplotlib menggunakan format RGB untuk menampilkan gambar.
Menampilkan Gambar Asli
```
plt.figure(figsize=(12, 6))
plt.subplot(1, 2, 1)
plt.imshow(image)
plt.title('Gambar Asli')
plt.axis('off')
```
* ```plt.figure(figsize=(12, 6))```: Membuat figur baru dengan ukuran 12x6 inci.
* ```plt.subplot(1, 2, 1)```: Membuat subplot pertama dari dua subplot yang ada di baris pertama.
* ```plt.imshow(image)```: Menampilkan gambar asli.
* ```plt.title('Gambar Asli')```: Memberi judul pada subplot.
* ```plt.axis('off')```: Menghilangkan sumbu pada tampilan gambar.
#### 4. Persiapan Data Untuk K-means
```bash
pixel_vals = image.reshape((-1, 3))
pixel_vals = np.float32(pixel_vals)
```
* ```image.reshape((-1, 3))```: Mengubah dimensi gambar menjadi array 2D di mana setiap baris berisi tiga nilai warna (RGB). Bentuk awal gambar adalah ```(tinggi, lebar, 3)```, yang diubah menjadi ```(tinggi * lebar, 3)```.
* ```np.float32(pixel_vals)```: Mengkonversi tipe data dari integer 8-bit ke float 32-bit yang dibutuhkan oleh algoritma k-means.
#### 5. Kriteria Untuk Algoritma K-means

```bash
criteria = (cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER, 100, 0.85)
k = 3
```

* ```criteria```: Kriteria untuk menghentikan algoritma k-means. Terdiri dari dua kondisi:
  - ```cv2.TERM_CRITERIA_EPS```: Menghentikan jika perubahan pusat cluster kurang dari nilai epsilon tertentu.
  - ```cv2.TERM_CRITERIA_MAX_ITER```: Menghentikan setelah jumlah iterasi tertentu (100 iterasi).
  - ```0.85```: Nilai epsilon yang menentukan akurasi yang diinginkan.
* ```k```: Jumlah cluster yang diinginkan (3 cluster).
#### 6. Melakukan K-means Clustering

```bash
retval, labels, centers = cv2.kmeans(pixel_vals, k, None, criteria, 10, cv2.KMEANS_RANDOM_CENTERS)
centers = np.uint8(centers)
segmented_data = centers[labels.flatten()]
segmented_image = segmented_data.reshape((image.shape))
```
* ```cv2.kmeans()```: Fungsi OpenCV untuk melakukan k-means clustering.

  * ```pixel_vals```: Data piksel yang akan dikelompokkan.
  * ```k```: Jumlah cluster.
  * ```None```: Label awal (tidak ada dalam kasus ini).
  * ```criteria```: Kriteria untuk menghentikan algoritma.
  * ```10```: Jumlah percobaan untuk menemukan clustering terbaik.
* ```cv2.KMEANS_RANDOM_CENTERS```: Metode untuk menginisialisasi pusat cluster secara acak.
* ```retval```: Jumlah kuadrat jarak dari semua piksel ke pusat cluster terdekat.
* ```labels```: Label dari setiap piksel menunjukkan ke cluster mana mereka termasuk.
* ```centers```: Pusat cluster dalam bentuk nilai RGB.
* ```centers = np.uint8(centers)```: Mengkonversi pusat cluster ke tipe data 8-bit.
* ```segmented_data = centers[labels.flatten()]}```: Mengganti setiap piksel dengan pusat cluster terdekatnya.
* ```segmented_image = segmented_data.reshape((image.shape))```: Mengubah data tersegmentasi kembali ke bentuk gambar asli.

#### 7. Menampilkan Gambar Trsegmentasi
```
plt.subplot(1, 2, 2)
plt.imshow(segmented_image)
plt.title('Gambar Tersegmentasi (K=3)')
plt.axis('off')
plt.tight_layout()
plt.show()
```
* ```plt.subplot(1, 2, 2)```: Membuat subplot kedua dari dua subplot yang ada di baris pertama.
* ```plt.imshow(segmented_image)```: Menampilkan gambar tersegmentasi.
* ```plt.title('Gambar Tersegmentasi (K=3)')```: Memberi judul pada subplot.
* ```plt.axis('off')```: Menghilangkan sumbu pada tampilan gambar.
* ```plt.tight_layout()```: Mengatur tata letak subplot agar tidak saling tumpang tindih.
* ```plt.show()```: Menampilkan seluruh figur dengan subplot.
### C. Hasil Output
---
![hasil](https://github.com/kelaskodingpelitabangsa/UAS4-Pengolahan-Citra/blob/main/hasil.JPG)

### D. Cara Menjalankan Program
---
1. Pastikan Anda telah menginstal library yang diperlukan: numpy, matplotlib, dan opencv-python.
2. Tempatkan gambar (relax.jpg) di direktori images.
3. Salin dan tempel kode lengkap ke dalam sel Visual Studio Code.
4. Jalankan sel untuk melihat gambar asli dan gambar tersegmentasi berdampingan.
   
Dengan kode ini, Anda dapat melakukan segmentasi gambar menggunakan K-means clustering dan melihat hasilnya secara visual.


