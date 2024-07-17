# PA-PC_202231093_MUHAMMADFAKHRUNSYAM_B

## UAS Pengolahan Citra

### Mengimport Library
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
OpenCV (Open Source Computer Vision Library) adalah pustaka perangkat lunak yang dikembangkan untuk pengolahan gambar dan visi komputer. Salah satu modul yang sering digunakan adalah cv2, yang memungkinkan pengguna untuk membaca, menulis, dan memanipulasi gambar serta video dalam berbagai format. Bersama dengan OpenCV, numpy digunakan untuk operasi array, yang sangat berguna dalam memanipulasi data gambar. Dengan menggunakan numpy, kita dapat dengan mudah mengubah dan menganalisis matriks gambar. Selain itu, matplotlib adalah pustaka plotting yang digunakan untuk menampilkan data dalam bentuk grafik. Modul ini dapat digunakan untuk menampilkan gambar yang telah dimanipulasi oleh OpenCV. Ketiga pustaka ini sering digunakan bersama untuk berbagai aplikasi dalam visi komputer, seperti pengenalan objek, deteksi tepi, dan pengolahan citra medis. Dengan menggabungkan ketiganya, kita dapat membuat pipeline yang kuat untuk analisis dan visualisasi gambar.
```bash
image = cv2.imread('JERUK.jpg')
```
Perintah image = cv2.imread('JERUK.jpg') digunakan untuk membaca file gambar dengan nama "JERUK.jpg" menggunakan pustaka OpenCV dalam Python. Fungsi cv2.imread() ini mengembalikan array numpy yang merepresentasikan gambar tersebut. Setiap elemen dalam array ini mewakili piksel gambar dalam format BGR (Blue, Green, Red) secara default. Array numpy ini dapat dimanipulasi lebih lanjut untuk melakukan berbagai operasi pengolahan gambar seperti pengubahan ukuran, pemotongan, deteksi tepi, dan lain-lain. Setelah gambar dibaca dan dimuat ke dalam variabel image, kita dapat menggunakan fungsi OpenCV lainnya untuk menampilkan, mengedit, atau menganalisis gambar tersebut sesuai kebutuhan. OpenCV sangat efisien dalam menangani berbagai format gambar dan mendukung banyak operasi pengolahan gambar tingkat lanjut.
```bash
hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
```
Perintah hsv_image = cv2.cvtColor(image, cv2.COLOR_BGR2HSV) digunakan untuk mengkonversi gambar dari format BGR (Blue, Green, Red) ke format HSV (Hue, Saturation, Value) menggunakan pustaka OpenCV. Dalam pengolahan citra, format HSV sering kali lebih berguna dibandingkan format BGR atau RGB karena memisahkan informasi warna (hue) dari intensitas cahaya (value), sehingga lebih mudah untuk melakukan operasi seperti deteksi warna, penyesuaian kecerahan, dan segmentasi warna. Fungsi cv2.cvtColor() mengambil gambar yang telah dibaca sebelumnya dan mengubahnya ke dalam ruang warna yang berbeda. Variabel hsv_image kemudian menyimpan gambar yang telah dikonversi dalam format HSV. Dengan menggunakan gambar dalam format HSV, kita dapat lebih efektif melakukan berbagai operasi pengolahan citra, terutama yang berkaitan dengan analisis warna.
```bash
lower_yellow = np.array([0, 50, 100], dtype="uint8")
upper_yellow = np.array([30, 255, 255], dtype="uint8")
```
Perintah lower_yellow = np.array([0, 50, 100], dtype="uint8") dan upper_yellow = np.array([30, 255, 255], dtype="uint8") digunakan untuk mendefinisikan rentang warna kuning dalam format HSV menggunakan pustaka numpy. Array lower_yellow mewakili batas bawah warna kuning, dengan nilai hue (0), saturation (50), dan value (100). Array upper_yellow mewakili batas atas warna kuning, dengan nilai hue (30), saturation (255), dan value (255). Dengan mendefinisikan rentang ini, kita dapat melakukan operasi segmentasi warna untuk mengekstraksi piksel-piksel dalam gambar yang memiliki warna kuning di antara kedua batas ini. Variabel-variabel ini akan digunakan bersama fungsi OpenCV lainnya, seperti cv2.inRange(), untuk membuat masker yang hanya berisi piksel dalam rentang warna kuning yang telah ditentukan. Hal ini sangat berguna dalam berbagai aplikasi visi komputer, seperti pelacakan objek, deteksi warna, dan analisis citra.
```bash
lower_green = np.array([31, 60, 5], dtype="uint8")
upper_green = np.array([150, 255, 255], dtype="uint8")
```
Perintah lower_green = np.array([31, 60, 5], dtype="uint8") dan upper_green = np.array([150, 255, 255], dtype="uint8") digunakan untuk mendefinisikan rentang warna hijau dalam format HSV menggunakan pustaka numpy. Array lower_green mewakili batas bawah warna hijau, dengan nilai hue (31), saturation (60), dan value (5). Array upper_green mewakili batas atas warna hijau, dengan nilai hue (150), saturation (255), dan value (255). Dengan mendefinisikan rentang ini, kita dapat melakukan segmentasi warna untuk mengekstraksi piksel-piksel dalam gambar yang memiliki warna hijau di antara kedua batas ini. Variabel-variabel ini akan digunakan bersama fungsi OpenCV lainnya, seperti cv2.inRange(), untuk membuat masker yang hanya berisi piksel dalam rentang warna hijau yang telah ditentukan. Segmentasi warna hijau ini sangat berguna dalam berbagai aplikasi.
```bash
mask_orange = cv2.inRange(hsv_image, lower_yellow, upper_yellow)
mask_leaves = cv2.inRange(hsv_image, lower_green, upper_green)
```
Perintah mask_orange = cv2.inRange(hsv_image, lower_yellow, upper_yellow) dan mask_leaves = cv2.inRange(hsv_image, lower_green, upper_green) digunakan untuk membuat masker biner berdasarkan rentang warna tertentu dalam gambar HSV. Fungsi cv2.inRange() mengambil gambar dalam format HSV, bersama dengan dua array yang mendefinisikan batas bawah dan atas warna yang ingin diekstraksi. Dalam hal ini, mask_orange dibuat untuk mengekstraksi piksel yang sesuai dengan rentang warna kuning yang didefinisikan oleh lower_yellow dan upper_yellow. Sedangkan mask_leaves dibuat untuk mengekstraksi piksel yang sesuai dengan rentang warna hijau yang didefinisikan oleh lower_green dan upper_green. Masker yang dihasilkan adalah gambar biner dengan nilai piksel 255 untuk piksel yang berada dalam rentang warna yang ditentukan, dan 0 untuk piksel lainnya. Masker ini sangat berguna untuk operasi pengolahan citra lanjutan, seperti segmentasi objek, analisis warna, dan pelacakan objek, memungkinkan kita untuk fokus pada area spesifik dalam gambar berdasarkan warnanya.
```bash
segmented_orange = cv2.bitwise_and(image, image, mask=mask_orange)
segmented_leaves = cv2.bitwise_and(image, image, mask=mask_leaves)
```
Perintah segmented_orange = cv2.bitwise_and(image, image, mask=mask_orange) dan segmented_leaves = cv2.bitwise_and(image, image, mask=mask_leaves) digunakan untuk melakukan segmentasi gambar berdasarkan masker biner yang telah dibuat. Fungsi cv2.bitwise_and() melakukan operasi AND bitwise antara dua gambar dengan menggunakan masker yang disediakan. Dalam perintah pertama, segmented_orange dibuat dengan mengaplikasikan mask_orange pada gambar asli image, sehingga hanya piksel yang sesuai dengan rentang warna kuning yang didefinisikan oleh masker yang akan dipertahankan dalam gambar hasil. Demikian pula, dalam perintah kedua, segmented_leaves dibuat dengan mengaplikasikan mask_leaves pada gambar asli, sehingga hanya piksel yang sesuai dengan rentang warna hijau yang didefinisikan oleh masker yang akan dipertahankan. Hasil dari operasi ini adalah dua gambar baru di mana hanya area-area dengan warna kuning dan hijau yang tampak, sementara area lain menjadi hitam. Teknik ini sangat berguna dalam pengolahan citra untuk mengekstraksi dan menganalisis objek tertentu berdasarkan warnanya, seperti memisahkan buah jeruk dari daun dalam sebuah gambar.
```bash
mask_orange_no_leaves = cv2.bitwise_not(mask_leaves)
mask_orange_no_leaves = cv2.bitwise_and(mask_orange, mask_orange_no_leaves)
```
Kode yang Anda berikan menggunakan OpenCV untuk manipulasi citra. Pada baris pertama, cv2.bitwise_not(mask_leaves) digunakan untuk membuat kebalikan dari masker mask_leaves, menghasilkan mask_orange_no_leaves yang menunjukkan area di mana tidak ada daun (misalnya, latar belakang atau bagian lain). Kemudian, pada baris kedua, cv2.bitwise_and(mask_orange, mask_orange_no_leaves) menghasilkan masker yang menunjukkan area di mana masker mask_orange dan mask_orange_no_leaves bersama-sama bernilai 1 (true). Hasilnya adalah masker baru yang hanya mempertahankan area di mana ada oranye dan tidak ada daun, sesuai dengan tujuan manipulasi citra yang Anda lakukan.
```bash
fig, axs = plt.subplots(2, 2, figsize=(12, 10))

axs[0, 0].imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
axs[0, 0].set_title('Gamber Jeruk')

axs[0, 1].imshow(mask_pineapple_no_leaves, cmap='gray')
axs[0, 1].set_title('Mask Jeruk (Tanpa Daun)')

axs[1, 0].imshow(cv2.cvtColor(segmented_pineapple, cv2.COLOR_BGR2RGB))
axs[1, 0].set_title('Segmentasi Jeruk')

axs[1, 1].imshow(cv2.cvtColor(segmented_leaves, cv2.COLOR_BGR2RGB))
axs[1, 1].set_title('Segmentasi Jeruk')

plt.show()
```
Kode yang saya berikan menggunakan Matplotlib untuk menampilkan beberapa gambar dalam satu grid. Pertama, gambar pertama (di pojok kiri atas) menampilkan citra asli dari sebuah jeruk, diubah ke ruang warna RGB agar dapat ditampilkan dengan benar menggunakan cv2.cvtColor. Judulnya adalah "Gamber Jeruk".

Kedua, gambar di sebelah kanan atas menampilkan masker mask_pineapple_no_leaves dalam skala abu-abu (cmap='gray'), yang menunjukkan area di mana tidak ada daun di jeruk. Ini membantu dalam memisahkan bagian jeruk dari daunnya. Judulnya adalah "Mask Jeruk (Tanpa Daun)".

Ketiga, gambar di pojok kiri bawah menampilkan hasil segmentasi dari jeruk, disajikan kembali dalam warna RGB. Ini mungkin merupakan hasil dari proses pengolahan atau segmentasi yang dilakukan pada citra asli untuk menyoroti atau memisahkan jeruk dari latar belakang atau objek lainnya. Judulnya adalah "Segmentasi Jeruk".

Terakhir, gambar di pojok kanan bawah menampilkan segmentasi daun jeruk dalam warna RGB. Ini menunjukkan bagian dari citra yang dianggap sebagai daun dari jeruk, yang juga mungkin hasil dari proses segmentasi yang terpisah. Judulnya adalah "Segmentasi Daun Jeruk".

Penggunaan subplot dengan plt.subplots memungkinkan penempatan gambar-gambar ini dalam satu tata letak grid, memudahkan untuk membandingkan hasil segmentasi dan pemrosesan yang berbeda dari citra jeruk dan daunnya.
