# TB1-JSTKelompok
**Analisis dan Implementasi Klasifikasi Kualitas Kentang Menggunakan Perceptron dan ADALINE**  
Mata kuliah Jaringan Syaraf Tiruan (IT6053), FTI UKDW.

## Anggota dan kontribusi
| Nama | NIM | Kontribusi |
|---|---|---|
| Hansel Ivano Supratman | 71231039 | Implementasi Perceptron, eksperimen pelatihan, penyusunan laporan bagian 1-4 & slide |
| Nicolas Krisna Prawirajati | 71231019 | Implementasi ADALINE, visualisasi evaluasi, penyusunan laporan bagian 5-8 & pengujian |

## Struktur dan tautan berkas
| Berkas | Isi |
|---|---|
| [TB1_KelompokHN.ipynb](TB1_KelompokHN.ipynb) | Notebook lengkap (kode, penjelasan, keluaran); dapat dijalankan dari awal sampai akhir |
| [TB1_KelompokHN.pdf](TB1_KelompokHN.pdf) | Laporan lengkap dalam format PDF |
| [Presentasi_TB1.pdf](Presentasi_TB1.pdf) | Slide presentasi |
| [dataset.csv](dataset.csv) | Data yang dipakai eksperimen (300 baris) |
| [requirements.txt](requirements.txt) | Dependensi dan versi |
| [hasil_eksperimen.csv](hasil_eksperimen.csv), [hasil_tambahan.json](hasil_tambahan.json) | Keluaran notebook (tabel 8 konfigurasi dan angka pendukung laporan) |
| [figures/](figures/) | Gambar visualisasi yang dipakai laporan dan presentasi |

## Kasus dan data
Melanjutkan Tugas 1 (deteksi kualitas kentang). Perceptron/ADALINE memerlukan masukan numerik, sehingga setiap citra diringkas menjadi rata-rata intensitas kanal merah dan hijau.

| Kolom | Makna |
|---|---|
| `mean_red` | rata-rata intensitas kanal merah citra (numerik) |
| `mean_green` | rata-rata intensitas kanal hijau citra (numerik) |
| `label` | **+1 = Good (kelas positif)**, **−1 = Rotten** |

- 300 observasi, 150 per kelas, tanpa missing value dan tanpa duplikat. Kelas *Defective* pada Tugas 1 tidak dipakai (tugas dua kelas).
- **Transformasi:** citra → rata-rata R dan G; standardisasi Z-score dipelajari hanya dari data latih.
- Data tidak memuat data pribadi.

## Cara menjalankan
```bash
pip install -r requirements.txt
jupyter notebook TB1_KelompokHN.ipynb      # Kernel -> Restart & Run All
# atau tanpa antarmuka:
jupyter nbconvert --to notebook --execute --inplace TB1_KelompokHN.ipynb
```
Versi yang dipakai: Python 3.12.3, numpy 2.4.4, pandas 3.0.2, matplotlib 3.10.8, scikit-learn 1.8.0. **Seed = 42** (split 80:20 stratifikasi).

## Ringkasan hasil (data uji 60 sampel, label [-1, +1], kelas positif = Good)
- Enam konfigurasi terstandardisasi (η = 0,001; 0,01; 0,1; kedua model; 50 epoch): akurasi uji 96,67% (29 TN, 1 FP, 1 FN, 29 TP); Precision = Recall = F1 = 0,967.
- Perceptron tidak pernah mencapai nol kesalahan latih (minimum 7/240 pada diagnostik 2000 epoch) → data hampir, tetapi tidak sepenuhnya, terpisah linear. η hanya menskalakan bobot Perceptron (hasil identik).
- ADALINE: J epoch ke-50 = 0,4417 / 0,1835 / 0,1024 untuk η = 0,001 / 0,01 / 0,1; optimum kuadrat-terkecil J = 0,1024.
- Tanpa standardisasi (η = 0,01): Perceptron 45,00%, ADALINE 50,00% dengan J meledak (>1e6 pada epoch 3; tak hingga pada epoch 66 pada diagnostik 200 epoch).
- Keterbatasan: satu split, 60 data uji, dua fitur warna.

## Referensi
- Rosenblatt, F. (1958). The perceptron. Psychological Review, 65(6), 386–408. https://doi.org/10.1037/h0042519
- Widrow, B., & Hoff, M. E. (1960). Adaptive switching circuits. IRE WESCON Convention Record, Part 4, 96–104. https://isl.stanford.edu/~widrow/papers/c1960adaptiveswitching.pdf
- Raschka, S. (tanpa tahun). Adaline: Adaptive Linear Neuron Classifier. mlxtend. https://rasbt.github.io/mlxtend/user_guide/classifier/Adaline/ (diakses 6 Oktober 2026)
- Raschka, S., & Mirjalili, V. (2019). Python Machine Learning: Machine Learning and Deep Learning with Python, scikit-learn, and TensorFlow 2 (3rd ed.). Packt Publishing.
- Wang, C., & Xiao, Z. (2021). Potato surface defect detection based on deep transfer learning. Agriculture, 11(9), 863. https://doi.org/10.3390/agriculture11090863
- Su, Q., Kondo, N., Al Riza, D. F., & Habaragamuwa, H. (2020). Potato quality grading based on depth imaging and convolutional neural network. Journal of Food Quality, 2020, 8815896. https://doi.org/10.1155/2020/8815896
- Moallem, P., Razmjooy, N., & Ashourian, M. (2013). Computer vision-based potato defect detection using neural networks and support vector machine. International Journal of Robotics and Automation, 28(2), 137–145.

Kode diadaptasi dari struktur `fit/net_input/predict` pada dokumentasi mlxtend; perubahan dijelaskan di notebook dan laporan bagian 3.

## Bantuan AI dan verifikasi
Perbaikan notebook, laporan, dan README dibantu Claude (Anthropic). Verifikasi: seluruh notebook dijalankan ulang dari awal, perhitungan manual dicocokkan otomatis dengan kode (`assert`), dan semua angka laporan diambil dari keluaran notebook.

**URL repository / commit hash versi dinilai:**
