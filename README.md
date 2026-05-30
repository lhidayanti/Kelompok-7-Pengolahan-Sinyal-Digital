# Implementasi Voice Activity Detection pada Noisy Speech Menggunakan Zero Crossing Rate (ZCR) dan Short-Time Fourier Transform (STFT)

Proyek ini merupakan Laporan Akhir Proyek Mata Kuliah **Pengolahan Sinyal Digital** yang disusun oleh **Kelompok 7**, Program Studi S1 Sains Data, Universitas Negeri Surabaya.

## Anggota Kelompok 7
1. **Lailil Hidayanti** - (24031554036)
2. **Nurlaila Lutfi Azizah** - (24031554205)

**Dosen Pengampu:** Dr. Atik Wintarti, M.Kom.

---

## 1. Latar Belakang & Deskripsi Proyek
*Voice Activity Detection* (VAD) adalah teknik untuk mendeteksi dan mengklasifikasikan segmen sinyal ucapan manusia, khususnya membedakan antara bagian bersuara (*voiced*) dan bagian tidak bersuara atau hening (*unvoiced/silence*). Teknologi ini sangat penting untuk sistem komunikasi, pengenalan suara (*speech recognition*), dan peredaman bising (*noise reduction*).

Namun, rekaman suara di dunia nyata jarang sekali benar-benar bersih. Ketika suara tercampur dengan kebisingan lingkungan (*noisy speech*), deteksi menjadi lebih kompleks karena derau dapat mengaburkan karakteristik sinyal asli. Proyek ini mengimplementasikan dua pendekatan untuk mengatasi masalah tersebut:
1. **Zero Crossing Rate (ZCR):** Analisis domain waktu untuk menghitung berapa kali sinyal berubah tanda (melewati nilai nol), yang efektif membedakan derau frekuensi tinggi atau komponen *unvoiced*.
2. **Short-Time Fourier Transform (STFT):** Analisis domain frekuensi-waktu untuk melihat magnitudo energi sinyal pada tiap frame waktu tertentu guna mendeteksi aktivitas vokal yang memiliki energi lebih terpusat.

---

## 2. Arsitektur Pemrosesan Sinyal (Metodologi)
Alur kodingan dan analisis sinyal pada proyek ini dibagi menjadi beberapa tahap utama:

1. **Signal Preprocessing & Resampling:** Mengubah seluruh sampling rate file audio uji menjadi standar **8000 Hz** agar beban komputasi lebih efisien.
2. **Amplitudo Normalization:** Menormalisasi nilai amplitudo sinyal berdasarkan nilai absolut maksimumnya agar memiliki rentang skala yang seragam.
3. **Noise Injection (Simulasi):** Menambahkan *White Gaussian Noise* (WGN) buatan dengan target **Signal-to-Noise Ratio (SNR) 10 dB** pada dataset bersih untuk menguji ketangguhan algoritma VAD.
4. **Framing:** Memotong sinyal audio yang panjang menjadi frame pendek berdurasi **15 ms** dengan teknik *overlap* sebesar **50%** (analisis sinyal waktu pendek).
5. **Hamming Windowing:** Menerapkan fungsi Hamming Window pada setiap frame untuk memperhalus potongan dan mengurangi kebisingan spektral (*spectral leakage*).
6. **Feature Extraction & Thresholding:** Menghitung nilai ZCR dan magnitudo STFT dari tiap frame untuk menentukan batasan (*threshold*) kapan sebuah suara manusia terdeteksi aktif.

---

## 3. Struktur Repositori
Berikut adalah penjelasan mengenai file-file yang ada di dalam repositori ini:
* `PROJEK_PSD_FINAL_KELOMPOK_7.ipynb` : File Jupyter Notebook utama yang berisi seluruh kodingan Python (preprocessing, pengolahan, visualisasi sinyal, dan algoritma VAD).
* `1089-134686-0001.wav` & `*.wav` : File audio sampel/dataset bawaan yang digunakan untuk eksperimen pengujian dengan derau (WGN).
* `rekaman.wav` : File audio rekaman asli kelompok yang digunakan sebagai data uji dunia nyata tanpa penambahan derau simulasi.
* `rekaman.mp4` : Video demonstrasi jalannya program aplikasi dan visualisasi grafik sinyal hasil deteksi VAD.

---

## 4. Kebutuhan Library (Prerequisites)
Sebelum menjalankan file notebook (`.ipynb`), pastikan Anda sudah menginstal beberapa library Python di bawah ini:

```bash
pip install numpy librosa soundfile scipy matplotlib
