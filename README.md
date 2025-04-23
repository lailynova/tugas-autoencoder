# Denoising Autoencoder untuk CIFAR-10

Proyek ini mengimplementasikan autoencoder konvolusional untuk menghapus noise dari gambar CIFAR-10. Model dilatih untuk merekonstruksi gambar bersih dari versi yang telah diberi noise, dengan tujuan meningkatkan kualitas visual gambar yang terdistorsi.

## Dataset

Dataset yang digunakan adalah CIFAR-10, yang terdiri dari 60.000 gambar berwarna berukuran 32x32 piksel dalam 10 kelas berbeda. Untuk keperluan pelatihan, gambar-gambar ini diperbesar menjadi 256x256 piksel dan ditambahkan noise Gaussian untuk mensimulasikan kondisi gambar yang terdistorsi.

- **Gambar Bersih**: Gambar asli dari CIFAR-10.
- **Gambar Noisy**: Gambar yang telah ditambahkan noise Gaussian dengan mean 0 dan standar deviasi 25.

## Arsitektur Autoencoder

Model autoencoder terdiri dari dua bagian utama:

### Encoder

- **Conv2d(3, 32, kernel_size=3, stride=2, padding=1)**
- **BatchNorm2d(32)**
- **ReLU()**
- **Conv2d(32, 64, kernel_size=3, stride=2, padding=1)**
- **BatchNorm2d(64)**
- **ReLU()**
- **Conv2d(64, 128, kernel_size=3, stride=2, padding=1)**
- **BatchNorm2d(128)**
- **ReLU()**

Encoder mengurangi dimensi spasial gambar dan mengekstraksi fitur penting dari gambar yang telah diberi noise.

### Decoder

- **ConvTranspose2d(128, 64, kernel_size=3, stride=2, padding=1, output_padding=1)**
- **BatchNorm2d(64)**
- **ReLU()**
- **ConvTranspose2d(64, 32, kernel_size=3, stride=2, padding=1, output_padding=1)**
- **BatchNorm2d(32)**
- **ReLU()**
- **ConvTranspose2d(32, 3, kernel_size=3, stride=2, padding=1, output_padding=1)**
- **Sigmoid()**

Decoder berfungsi untuk merekonstruksi gambar bersih dari representasi fitur yang dihasilkan oleh encoder.

## Pelatihan

- **Loss Function**: L1 Loss (Mean Absolute Error)
- **Optimizer**: Adam dengan learning rate 0.001
- **Epochs**: 100
- **Batch Size**: 8

Model dilatih untuk meminimalkan perbedaan antara output dan gambar bersih menggunakan L1 Loss, yang dikenal efektif dalam tugas denoising karena lebih toleran terhadap outlier dibandingkan MSE.

## Performa

Selama pelatihan, loss secara bertahap menurun, menunjukkan bahwa model belajar merekonstruksi gambar dengan lebih akurat. Berikut adalah contoh output dari model setelah pelatihan:

![Contoh Hasil](/auto.png)

*Gambar atas: Gambar Noisy | Gambar tengah: Gambar Bersih | Gambar bawah: Output Model*

## Kesimpulan

Autoencoder konvolusional ini berhasil mengurangi noise dari gambar CIFAR-10, menghasilkan gambar yang lebih bersih dan mendekati aslinya. Arsitektur yang digunakan sederhana namun efektif, dan dapat dikembangkan lebih lanjut untuk tugas denoising pada dataset lain atau dengan jenis noise yang berbeda.

---

**Catatan**: Pastikan untuk mengganti `path_to_output_image.png` dengan path yang sesuai ke gambar hasil output model Anda. 
