# PCD_UAS_202231104_2024_ITPLN
# Teori Pendukung 
Geometrix pada pengolahan citra digital adalah cabang ilmu yang mempelajari sifat dan perubahan geometris gambar. Beberapa konsep teori yang mendasari geometrix dalam pengolahan citra digital meliputi:

1. Transformasi Geometris
Transformasi geometris adalah operasi yang mengubah posisi, orientasi, atau ukuran objek dalam gambar. Jenis-jenis transformasi geometris meliputi:

Translasi: Memindahkan objek sejauh vektor tertentu tanpa mengubah bentuk atau orientasi.<br>
Rotasi: Memutar objek di sekitar titik tertentu.<br>
Skalasi: Mengubah ukuran objek secara proporsional atau tidak proporsional.<br>
Refleksi: Membalik objek terhadap sumbu tertentu.<br>
Shear: Menggeser bagian objek searah sumbu x atau y, yang mengubah bentuk tetapi tidak mengubah luas.<br>

3. Interpolasi
Pada transformasi geometris, sering kali diperlukan interpolasi untuk menentukan nilai piksel baru. Jenis-jenis interpolasi meliputi:

Nearest Neighbor: Menentukan nilai piksel baru dengan nilai piksel terdekat.<br>
Bilinear Interpolation: Menghitung nilai piksel baru berdasarkan rata-rata tertimbang dari piksel-piksel di sekitarnya.<br>
Bicubic Interpolation: Menggunakan lebih banyak tetangga piksel untuk menghitung nilai baru, menghasilkan hasil yang lebih halus.<br>
4. Homografi
Homografi adalah transformasi perspektif yang menggambarkan hubungan antara dua gambar dari bidang yang sama. Homografi digunakan dalam registrasi gambar, mosaicking, dan rekonstruksi 3D.

5. Pendeteksian dan Pencocokan Fitur
Fitur-fitur penting dalam gambar, seperti titik sudut atau tepi, dapat dideteksi dan dicocokkan antara dua gambar untuk memahami transformasi geometris yang terjadi. Algoritma yang sering digunakan meliputi:

Harris Corner Detector
SIFT (Scale-Invariant Feature Transform)
SURF (Speeded-Up Robust Features)
6. Kalibrasi Kamera
Kalibrasi kamera melibatkan penentuan parameter intrinsik dan ekstrinsik kamera untuk mengoreksi distorsi dan memahami hubungan geometris antara dunia 3D dan gambar 2D.

7. Model Geometris 3D
Model geometris 3D digunakan dalam aplikasi seperti rekonstruksi 3D, pengenalan bentuk, dan analisis objek. Teknik seperti triangulasi dan pemetaan stereo digunakan untuk membangun model 3D dari gambar 2D.


# Import Library 
```pyton
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
Codingan diatas befungsi untuk memuat dan menampilkan gambar, serta menggunakan Matplotlib untuk menampilkan hasilnya dalam bentuk grafik <br>
# Pemanggilan gambar/foto kita yang telah di uploud 
```pyton
img = cv2.imread('foto.jpg')
```
Codingan diatas berfungsi untuk memanggil gambar yang telah kita uploud sesuai dengan nama file nya. <br>
# Menampilkan Gambar Asli 
```pyton
plt.subplot(2, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk membuat subplot yang memiliki 2 baris dan 3 kolom, dan memilih subplot pertama.
Pada line kedua berfungsi untuk menampilkan gambar dalam subplot pertama.
Pada line ketiga berfungsi untuk memberikan judul pada subplot dengan nama Original Image.
Pada line keempat berfungsi untuk menyembunyikan sumbu untuk tampilan gambar yang lebih bersih.<br>
# Memutar Gambar Sebesar 45 Derajat
```pyton
(h, w) = img.shape[:2]
center = (w // 2, h // 2)
M = cv2.getRotationMatrix2D(center, 45, 1.0)
img_rotated = cv2.warpAffine(img, M, (w, h))
plt.subplot(2, 3, 2)
plt.imshow(cv2.cvtColor(img_rotated, cv2.COLOR_BGR2RGB))
plt.title('Rotated Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk mendapatkan tinggi dan lebar gambar.
Pada line kedua berfungsi untuk menentukan titik pusat gambar.
Pada line ketiga berfungsi untuk menerapkan matriks rotasi pada gambar.
Pada line keempat samapai ketujuh berfungsi untuk membuat subplot, menampilkan gambar yang sudah diputar,memberikan judul, dan yang terakhir menyembunyikan sumbu supaya tampilan gambar lebih bersih.<br>
# Mengubah Ukuran Gambar Menjadi Setengah Ukuran Aslinya
```pyton
img_resized = cv2.resize(img, (img.shape[1]//3, img.shape[0]//2))
plt.subplot(2, 3, 3)
plt.imshow(cv2.cvtColor(img_resized, cv2.COLOR_BGR2RGB))
plt.title('Resized Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk mengubah ukuran gambar
Pada line kedua berfungsi untuk membuat subplot ketiga pada gambar
Pada line ketiga, keempat, kelima berfungsi untuk menampilkan gambar yang sudah diubah ukurannya, membuat judul dan terakhir menyembunyikan sumbu supaya tampilan gambar bersih.<br>
# Memangkas Gambar Ke Wilayah Tertentu (Misalnya Kuartal Kiri Atas
```pyton
img_cropped = img[0:img.shape[0]//2, 0:img.shape[1]//2]
plt.subplot(2, 3, 4)
plt.imshow(cv2.cvtColor(img_cropped, cv2.COLOR_BGR2RGB))
plt.title('Cropped Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk memotong bagian kiri atas gambar.
Pada line kedua berfungsi untuk membuat sublot keempat pada gambar.
Pada line ketiga, keempat, dan kelima berfungsi untuk menampilkan gambar yang sudah dipotong, memberikan judul, dan yang terakhir menyembunyikan sumbu supaya gambar bersih.<br>
# Membalik Gambar Secara Horizontal
```pyton
img_flipped = cv2.flip(img, 1)
plt.subplot(2, 3, 5)
plt.imshow(cv2.cvtColor(img_flipped, cv2.COLOR_BGR2RGB))
plt.title('Flipped Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk membalik gambar secara horizontal.
Pada line kedua berfungsi untuk membuat sublot kelima pada gambar.
Pada line ketiga, keempat, dan kelima berfungsi untuk menampilkan gambar yang sudah dibalik, memberikan judul, dan yang terakhir menyembunyikan sumbu supaya gambar bersih.<br>
# Menejarmahkan Gambar Dengan 50 Piksel Ke Kanan Dan 20 Piksel Ke Bawah
```pyton
rows, cols = img.shape[:2]
M_translate = np.float32([[1, 0, 250], [0, 1, 180]])
img_translated = cv2.warpAffine(img, M_translate, (cols, rows))
plt.subplot(2, 3, 6)
plt.imshow(cv2.cvtColor(img_translated, cv2.COLOR_BGR2RGB))
plt.title('Translated Image')
plt.axis('off')
```
Pada line pertama berfungsi untuk menemukan garis asli dari citra/gambar.
Pada line kedua dan ketiga berfungsi untuk membuat matriks translasi untuk mentranslasi gambar sebesar 250 piksel ke kanan dan 180 piksel ke bawah.
Pada line keempat berfungsi untuk membuat sublot keenam pada gambar.
Pada line kelima samapai ketujuh berfungsi untuk, menampilkan gambar yang sudah ditranslasi, memberikan judul, dan yang terakhir menyembunyikan sumbu supaya tampilan gambar bersih.<br>







