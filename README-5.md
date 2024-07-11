
# Teori Deteksi Tepi Pola Objek

Deteksi tepi adalah salah satu teknik dasar dalam pengolahan citra yang digunakan untuk mengidentifikasi titik-titik di mana intensitas cahaya dalam citra berubah secara signifikan. Deteksi tepi digunakan untuk mengekstrak informasi struktural penting dari citra dan mengurangi jumlah data yang harus diproses, sambil tetap mempertahankan fitur-fitur penting citra.

**Tujuan Deteksi Tepi:**
1. **Identifikasi Batas Objek:** Mendeteksi tepi membantu mengidentifikasi batas-batas objek dalam citra, memisahkan objek dari latar belakangnya.
2. **Ekstraksi Fitur:** Mengidentifikasi fitur penting dalam citra, seperti kontur dan garis, yang dapat digunakan untuk analisis lebih lanjut.
3. **Penyederhanaan Citra:** Mengurangi kompleksitas citra dengan mengabaikan informasi yang tidak penting, fokus pada fitur utama saja.

**Metode Deteksi Tepi:**
1. **Operator Gradien:**
   - **Sobel:** Menggunakan kernel 3x3 untuk mengkalkulasi gradien intensitas pada setiap piksel dalam arah horizontal dan vertikal. Hasilnya digunakan untuk menghitung besar gradien dan arah tepi.
   - **Prewitt:** Mirip dengan Sobel, tetapi menggunakan kernel yang berbeda.
   - **Roberts Cross:** Menggunakan kernel 2x2 untuk menghitung gradien dalam arah diagonal.
2. **Operator Laplacian:**
   - **Laplacian of Gaussian (LoG):** Menggabungkan Gaussian smoothing dengan Laplacian untuk mendeteksi tepi. Mengurangi noise sebelum menghitung laplacian.
3. **Canny Edge Detector:**
   - **Proses Multi-tahap:** Melibatkan Gaussian smoothing, kalkulasi gradien, non-maximum suppression, dan hysteresis thresholding. Merupakan metode yang sangat efektif dan banyak digunakan karena memberikan deteksi tepi yang akurat dan minim noise.

Deteksi tepi adalah teknik penting dalam pengolahan citra yang membantu dalam mengekstraksi informasi penting dan mendukung berbagai aplikasi analisis citra.

# Langkah - langkah 

import cv2
import numpy as np
import matplotlib.pyplot as plt

penjelasan:
cv2: Pustaka OpenCV untuk pemrosesan gambar.
numpy: Pustaka untuk operasi array dan matriks.
matplotlib.pyplot: Pustaka untuk visualisasi data.


image = cv2.imread('widy.jpeg', cv2.IMREAD_COLOR)
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

penjelasan:
cv2.imread('widy.jpeg', cv2.IMREAD_COLOR): Membaca gambar dari file 'widy.jpeg' dalam mode berwarna.
cv2.cvtColor(image, cv2.COLOR_BGR2GRAY): Mengonversi gambar berwarna menjadi gambar skala abu-abu.

_, thresh = cv2.threshold(gray, 100, 255, cv2.THRESH_BINARY)

penjelasan:
cv2.threshold: Menerapkan thresholding pada gambar skala abu-abu.
gray: Gambar input.
100: Nilai ambang batas. Piksel dengan intensitas di atas nilai ini akan diubah menjadi putih (255).
255: Nilai maksimum yang akan diberikan kepada piksel yang melebihi ambang batas.
cv2.THRESH_BINARY: Tipe thresholding yang digunakan (biner).

contours, hierarchy = cv2.findContours(thresh, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

contour_image = image.copy()
cv2.drawContours(contour_image, contours, -1, (0, 255, 0), 3)

penjelasan:
cv2.findContours: Menemukan kontur dalam gambar biner.
thresh: Gambar input.
cv2.RETR_EXTERNAL: Mengambil hanya kontur eksternal.
cv2.CHAIN_APPROX_SIMPLE: Menyederhanakan kontur dengan menghapus titik yang berlebihan.
image.copy(): Membuat salinan dari gambar asli.
cv2.drawContours: Menggambar kontur pada salinan gambar.
contour_image: Gambar tempat kontur akan digambar.
contours: Daftar kontur yang ditemukan.
-1: Menggambar semua kontur.
(0, 255, 0): Warna kontur (hijau dalam format BGR).
3: Ketebalan garis kontur.

edges = cv2.Canny(gray, 100, 200)
cv2.Canny: Mendeteksi tepi dalam gambar menggunakan algoritma Canny.
gray: Gambar input.
100 dan 200: Nilai ambang bawah dan atas untuk deteksi tepi.

plt.figure(figsize=(18, 6))

penjelasan:
plt.figure(figsize=(18, 6)): Membuat figure baru dengan ukuran 18x6 inci untuk menampung subplot.

plt.subplot(1, 4, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

penjelasan:
plt.subplot(1, 4, 1): Membuat subplot pertama dari total 4 subplot dalam satu baris.
cv2.cvtColor(image, cv2.COLOR_BGR2RGB): Mengonversi gambar dari BGR ke RGB agar warna ditampilkan dengan benar di matplotlib.
plt.imshow: Menampilkan gambar.
plt.title('Original Image'): Menambahkan judul pada subplot.
plt.axis('off'): Menghapus sumbu pada subplot.

plt.subplot(1, 4, 2)
plt.imshow(thresh, cmap='gray')
plt.title('Threshold Image')
plt.axis('off')

penjelasan:
plt.subplot(1, 4, 2): Membuat subplot kedua.
plt.imshow(thresh, cmap='gray'): Menampilkan gambar threshold dalam skala abu-abu.
plt.title('Threshold Image'): Menambahkan judul pada subplot.
plt.axis('off'): Menghapus sumbu pada subplot.

plt.subplot(1, 4, 3)
plt.imshow(edges, cmap='gray')
plt.title('Canny Edge Detection')
plt.axis('off')

penjelasan:
plt.subplot(1, 4, 3): Membuat subplot ketiga.
plt.imshow(edges, cmap='gray'): Menampilkan hasil deteksi tepi dalam skala abu-abu.
plt.title('Canny Edge Detection'): Menambahkan judul pada subplot.
plt.axis('off'): Menghapus sumbu pada subplot.

plt.subplot(1, 4, 4)
plt.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB))
plt.title('Contours Detection')
plt.axis('off')

penjelasan:
plt.subplot(1, 4, 4): Membuat subplot keempat.
cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB): Mengonversi gambar dari BGR ke RGB.
plt.imshow: Menampilkan gambar dengan kontur.
plt.title('Contours Detection'): Menambahkan judul pada subplot.
plt.axis('off'): Menghapus sumbu pada subplot.

plt.show()

penjelasan:
plt.show(): Menampilkan semua subplot yang telah dibuat dalam satu figure.