# Analisis Sentimen Ulasan Berbahasa Indonesia (NusaX-Senti) - UTS Milestone 1

Proyek kelompok mata kuliah Machine Learning. Topik: text mining, klasifikasi sentimen tiga kelas (negative, neutral, positive) pada teks ulasan berbahasa Indonesia, memakai classical machine learning.

- Kelompok: Sinergi
- Anggota: Melva Romaulina Br Sitorus (231110028)
            Hotnida Junita PAsaribu (221111292)
            Karin Kenisa Br Sitepu (231111550)
- Project ID: A14

## Isi repository

| Berkas | Keterangan |
|---|---|
| `UTS_ML_Milestone1_NusaX_Sentiment_v2.ipynb` | Notebook eksperimen lengkap (EDA, preprocessing, fitur, baseline, kandidat, validasi, error analysis awal) |
| `Laporan_UTS_Milestone1_NusaX_Sentiment.pdf` | Laporan Milestone 1 |
| `requirements.txt` | Versi library, dibuat otomatis oleh notebook pada sel terakhir |
| `experiment_log.csv` | Log semua run eksperimen (model, fitur, seed, metrik) |
| `error_analysis_sample_kategori.csv` | 50 sampel error beserta kategori penyebab (draft yang diperiksa kelompok) |

Berkas `requirements.txt`, `experiment_log.csv`, dan `error_analysis_sample_kategori.csv` dihasilkan saat notebook dijalankan; unggah hasil dari run kelompok.

## Dataset

- Nama: NusaX-Senti, subset bahasa Indonesia (train 500, valid 100, test 400)
- Sumber: https://github.com/IndoNLP/nusax/tree/main/datasets/sentiment (folder `indonesian`)
- Referensi: Winata dkk. (2023), NusaX: Multilingual Parallel Sentiment Dataset for 10 Indonesian Local Languages, EACL 2023. https://arxiv.org/abs/2205.15960
- Lisensi: CC BY-SA 4.0 ([ISI: konfirmasi pada repository sumber])
- Data tidak disalin ke repository ini. Notebook mengunduh langsung dari URL mentah GitHub sehingga tidak perlu unggah data manual.

## Cara menjalankan ulang

1. Buka notebook di Google Colab (Upload, atau buka dari GitHub).
2. Pilih menu Runtime, lalu Restart and run all.
3. Tunggu seluruh sel selesai (data kecil, hanya beberapa menit).
4. Untuk menjalankan lokal: `pip install -r requirements.txt`, lalu jalankan notebook dengan Jupyter. Butuh koneksi internet untuk mengunduh dataset.

Seed acak ditetapkan `SEED = 42` pada seluruh pembagian data dan model, sehingga hasil dapat diulang pada versi library yang sama.

## Desain evaluasi singkat

- Train dan valid digabung menjadi dev set 600 teks; dipakai untuk memilih fitur dan model dengan Stratified 5-Fold.
- Test set 400 teks tidak dipakai saat memilih model; dipakai satu kali untuk baseline dan model terpilih.
- TF-IDF dipelajari di dalam scikit-learn Pipeline sehingga tidak terjadi data leakage.
- Metrik utama: macro-F1. Metrik pendukung: accuracy, macro-precision, macro-recall, confusion matrix.

## Ringkasan hasil awal

Angka berikut berasal dari run notebook dengan seed 42 (macro-F1 rata-rata ± simpangan baku, Stratified 5-Fold pada dev 600).

| Model | Fitur | Macro-F1 CV |
|---|---|---|
| Logistic Regression (baseline) | word_1gram | 0.7459 ± 0.0384 |
| Logistic Regression | char_2-5gram | 0.7741 ± 0.0337 |
| Linear SVM | char_2-5gram | 0.7679 ± 0.0399 |
| Random Forest | word_1gram | 0.7522 ± 0.0333 |

Pada test set: baseline macro-F1 0.7353, Logistic Regression + char_2-5gram 0.7424. Selisih antar model masih lebih kecil daripada variasi antar-fold, sehingga belum ada model final. Tabel lengkap ada di laporan (Tabel 14 dan Tabel 25).

## Keterbatasan

Dataset kecil; kelas neutral paling sulit dikenali; preprocessing belum menangani slang dan negasi; tuning dan model final menjadi bagian tahap selanjutnya.

## Penggunaan AI

AI digunakan sebagai alat bantu menyusun kerangka notebook, laporan, dan draft kategori error. Kelompok bertanggung jawab atas kebenaran data, kode, hasil, dan isi laporan.
