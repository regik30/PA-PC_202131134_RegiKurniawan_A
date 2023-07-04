
## Authors

- Regi Kurniawan
- 202131134
- Pengolahan Citra A


# teori terkait

Deteksi objek dalam pengolahan citra adalah proses mengidentifikasi dan membedakan objek tertentu dari latar belakang atau lingkungan sekitarnya. Terdapat beberapa teori dan teknik yang digunakan dalam deteksi objek, di antaranya:

1. Segmentasi Citra: Segmentasi citra adalah proses pemisahan objek dari latar belakangnya. Teknik segmentasi seperti thresholding, pemrosesan morfologi, pemisahan berdasarkan warna, dan metode pemisahan berbasis tepi (edge-based) seperti deteksi tepi Canny dapat digunakan untuk memisahkan objek dari latar belakang.

2. Ekstraksi Fitur: Ekstraksi fitur melibatkan pengambilan fitur-fitur penting dari objek yang dapat membedakannya dari objek lain. Fitur-fitur ini dapat berupa tekstur, warna, bentuk, atau pola pada objek. Metode seperti Transformasi Fourier, Analisis Tekstur, dan Ekstraksi Fitur berbasis statistik seperti Histogram of Oriented Gradients (HOG) dan Local Binary Patterns (LBP) dapat digunakan untuk mengekstraksi fitur-fitur ini.

3. Klasifikasi: Setelah fitur-fitur diekstraksi, langkah selanjutnya adalah melakukan klasifikasi objek berdasarkan fitur-fitur tersebut. Berbagai metode klasifikasi dapat digunakan, termasuk Jaringan Saraf Tiruan (Artificial Neural Networks), Pohon Keputusan (Decision Trees), dan Metode Jarak Terdekat (K-Nearest Neighbors). Dalam pendekatan ini, model klasifikasi dilatih menggunakan data yang telah diklasifikasikan sebelumnya, sehingga dapat mengklasifikasikan objek baru berdasarkan fitur-fitur yang diekstraksi.

4. Deteksi Berbasis Tepi: Deteksi berbasis tepi melibatkan deteksi tepi atau batas objek dalam citra. Metode deteksi tepi seperti Operator Sobel, Operator Canny, atau Transformasi Hough dapat digunakan untuk menemukan tepi objek yang dapat digunakan untuk mengidentifikasi dan memisahkan objek dari latar belakangnya.

5. Pengenalan Pola: Teori pengenalan pola berkaitan erat dengan deteksi objek, di mana pola-pola tertentu diidentifikasi dan dibandingkan dengan pola-pola yang diketahui sebelumnya. Metode seperti jaringan saraf konvolusional (Convolutional Neural Networks) atau metode pengenalan pola statistik seperti Support Vector Machines (SVM) dapat digunakan untuk mengenali objek berdasarkan pola-pola yang kompleks pada citra.

6. Metode Pengacakan: Metode pengacakan atau pemindaian citra adalah pendekatan yang melibatkan pemindaian citra dengan menggunakan jendela geser dan mengidentifikasi objek berdasarkan perbedaan fitur antara objek dan latar belakang. Metode seperti HOG dan Metode Viola-Jones sering digunakan dalam pendekatan ini.

Perlu dicatat bahwa deteksi objek dalam pengolahan citra adalah bidang yang luas dan terus berkembang. Terdapat berbagai pendekatan dan teknik yang dapat digunakan tergantung pada jenis objek yang ingin dideteksi, kompleksitasnya, dan karakteristik citra yang ada.


## Screenshots

![alt text](https://github.com/regik30/PA-PC_202131134_RegiKurniawan_A/blob/main/Original%20Image.jpg?raw=true)

![alt text](https://github.com/regik30/PA-PC_202131134_RegiKurniawan_A/blob/main/Rincian%20Gambar.jpg?raw=true)
## Deployment

To deploy this project run

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load the input image
image = cv2.imread("buah.jpg")

# Convert the image to grayscale
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Apply Gaussian blur to reduce noise
blurred = cv2.GaussianBlur(gray, (5, 5), 0)

# Perform edge detection using Canny
edges = cv2.Canny(blurred, 50, 150)

# Find contours in the edge image
contours, _ = cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)

# Create a figure and axes
fig, ax = plt.subplots()

# Plot the original image
ax.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

# List to store the detected contours
detected_contours = []

# Loop over the contours and draw them on the image
for contour in contours:
    # Draw the contour on the image
    cv2.drawContours(image, [contour], -1, (0, 255, 0), 2)
    
    # Add the contour to the detected_contours list
    detected_contours.append(contour)

# Plot the image with detected contours
ax.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

# Show the plot
plt.show()




# Create a blank black image of the same size as the input image
black_image = np.zeros_like(image)

# Create a figure and axes using plt.subplot
fig, axs = plt.subplots(1, 4, figsize=(12, 8))

# Loop over the contours and draw them on the image
for contour in contours:
    # Draw the contour on the image
    cv2.drawContours(image, [contour], -1, (0, 0, 255), 2)
    
    # Add the contour to the detected_contours list
    detected_contours.append(contour)

# Plot the image with detected contours
axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))

# Plot the original image with contours
#axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
cv2.drawContours(image, contours, -1, (0, 0, 255), 2)
axs[0].set_title("Asli")

# Plot the object 1
object_image = np.zeros_like(image)
cv2.fillPoly(object_image, [contours[2]], (255, 255, 255))
object_result = cv2.bitwise_and(image, object_image)
axs[1].imshow(cv2.cvtColor(object_result, cv2.COLOR_BGR2RGB))
axs[1].set_title("Jeruk")

# Plot the object 2
object_image = np.zeros_like(image)
cv2.fillPoly(object_image, [contours[3]], (255, 255, 255))
object_result = cv2.bitwise_and(image, object_image)
axs[2].imshow(cv2.cvtColor(object_result, cv2.COLOR_BGR2RGB))
axs[2].set_title("Pir")

# Plot the object 3
object_image = np.zeros_like(image)
cv2.fillPoly(object_image, [contours[1]], (255, 255, 255))
object_result = cv2.bitwise_and(image, object_image)
axs[3].imshow(cv2.cvtColor(object_result, cv2.COLOR_BGR2RGB))
axs[3].set_title("Salak")

# Adjust the spacing between subplots
plt.tight_layout()

# Display the plot
plt.show()
```


## Penjelasan

Berikut adalah penjelasan langkah-langkah dalam kode tersebut:

1. Impor library yang diperlukan: Pertama, kita mengimpor library yang dibutuhkan, yaitu cv2, numpy, dan matplotlib.

2. Memuat gambar masukan: Gambar asli dimuat menggunakan fungsi `cv2.imread("buah.jpg")` dan disimpan dalam variabel `image`.

3. Mengubah gambar menjadi skala abu-abu: Gambar asli dikonversi menjadi skala abu-abu menggunakan fungsi `cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)`. Hasilnya disimpan dalam variabel `gray`.

4. Mengurangi noise dengan Gaussian Blur: Gambar skala abu-abu yang telah didapatkan diberikan efek Gaussian blur untuk mengurangi noise menggunakan fungsi `cv2.GaussianBlur(gray, (5, 5), 0)`. Gambar hasil blur disimpan dalam variabel `blurred`.

5. Deteksi tepi menggunakan Canny: Pada gambar hasil blur, kita melakukan deteksi tepi menggunakan metode Canny dengan menggunakan fungsi `cv2.Canny(blurred, 50, 150)`. Hasil deteksi tepi disimpan dalam variabel `edges`.

6. Mencari kontur pada gambar tepi: Dengan menggunakan fungsi `cv2.findContours(edges.copy(), cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)`, kita mencari kontur pada gambar tepi. Kontur-kontur yang terdeteksi disimpan dalam variabel `contours`.

7. Membuat figure dan axes: Pada langkah ini, kita membuat figure dan axes menggunakan `plt.subplots()` untuk keperluan visualisasi.

8. Menampilkan gambar asli: Gambar asli ditampilkan menggunakan `ax.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))` setelah diubah ke format RGB.

9. Menyimpan kontur yang terdeteksi: Kita membuat sebuah list kosong dengan nama `detected_contours` untuk menyimpan kontur-kontur yang terdeteksi nantinya.

10. Melakukan perulangan pada kontur: Kita menggunakan loop `for` untuk mengiterasi setiap kontur yang terdapat pada variabel `contours`.

11. Menggambar kontur pada gambar: Untuk setiap kontur, kita menggunakan `cv2.drawContours(image, [contour], -1, (0, 255, 0), 2)` untuk menggambar kontur pada gambar asli. Kontur digambar dengan warna hijau dan ketebalan garis 2 piksel.

12. Menyimpan kontur yang terdeteksi: Setiap kontur yang terdeteksi ditambahkan ke dalam list `detected_contours` menggunakan perintah `detected_contours.append(contour)`.

13. Menampilkan gambar dengan kontur yang terdeteksi: Gambar asli yang telah digambar konturnya ditampilkan menggunakan `ax.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))`.

14. Menampilkan plot: Terakhir, kita menggunakan `plt.show()` untuk menampilkan plot dengan gambar asli beserta kontur yang terdeteksi.

Berikut adalah penjelasan halaman ke-2:

1. Membuat gambar hitam kosong dengan ukuran yang sama dengan gambar asli: Baris pertama dalam kode membuat gambar hitam kosong dengan menggunakan `np.zeros_like(image)`. Gambar hitam ini akan digunakan nanti untuk menyorot objek yang terdeteksi.

2. Membuat figure dan axes menggunakan `plt.subplots`: Dalam langkah ini, kita membuat sebuah figure dengan 1 baris dan 4 kolom menggunakan `plt.subplots(1, 4, figsize=(12, 8))`. Hal ini memungkinkan kita untuk menampilkan gambar-gambar dalam 4 subplot yang berbeda.

3. Melakukan perulangan pada kontur dan menggambar kontur pada gambar asli: Kita menggunakan loop `for` untuk mengiterasi setiap kontur yang terdapat pada variabel `contours`. Untuk setiap kontur, kita menggunakan `cv2.drawContours(image, [contour], -1, (0, 0, 255), 2)` untuk menggambar kontur pada gambar asli dengan warna merah (0, 0, 255) dan ketebalan garis 2 piksel.

4. Menyimpan kontur yang terdeteksi: Setiap kontur yang terdeteksi ditambahkan ke dalam list `detected_contours` menggunakan perintah `detected_contours.append(contour)`.

5. Menampilkan gambar dengan kontur yang terdeteksi: Gambar asli yang telah digambar konturnya ditampilkan dalam subplot pertama (`axs[0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))`).

6. Menyorot objek yang terdeteksi: Dalam subplot kedua hingga keempat, kita ingin menyorot setiap objek yang terdeteksi secara terpisah. Untuk setiap objek, kita membuat gambar kosong menggunakan `np.zeros_like(image)`. Kemudian, kita menggunakan `cv2.fillPoly(object_image, [contours[i]], (255, 255, 255))` untuk mengisi objek dengan warna putih pada gambar kosong berdasarkan kontur yang sesuai. Terakhir, kita menggunakan `cv2.bitwise_and(image, object_image)` untuk menggabungkan gambar asli dengan gambar objek yang terisi putih. Hasilnya disimpan dalam variabel `object_result`.

7. Menampilkan subplot dengan objek yang terdeteksi: Subplot kedua hingga keempat menampilkan gambar dengan objek yang terdeteksi secara terpisah. Kita menggunakan `axs[i-1].imshow(cv2.cvtColor(object_result, cv2.COLOR_BGR2RGB))` untuk menampilkan gambar objek dalam format RGB.

8. Memberikan judul pada setiap subplot: Kita menggunakan `axs[i].set_title()` untuk memberikan judul pada setiap subplot sesuai dengan objek yang terdeteksi.

9. Menyesuaikan jarak antara subplot: `plt.tight_layout()` digunakan untuk menyesuaikan jarak antara subplot agar tampilan lebih rapi.

10. Menampilkan plot: Terakhir, kita menggunakan `plt.show()` untuk menampilkan plot dengan gambar asli beserta kontur yang terdeteksi dan objek yang disorot secara terpisah dalam subplot-subplot yang sesuai.

## Hasil Output

![alt text](https://github.com/regik30/PA-PC_202131134_RegiKurniawan_A/blob/main/hasil-output.png?raw=true)