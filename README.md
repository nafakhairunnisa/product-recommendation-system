# Sistem Rekomendasi Produk E-Commerce dengan Collaborative & Content-Based Filtering

![Gambar Belanja Produk](https://github.com/nafakhairunnisa/product-recommendation-system/blob/main/img/shutter-speed-BQ9usyzHx_w-unsplash.jpg?raw=true)
Foto oleh Shutter Speed di [Unsplash](https://unsplash.com/id/foto/keranjang-belanja-mainan-BQ9usyzHx_w?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash).
      

## Overview
Proyek ini membangun sistem rekomendasi produk e-commerce menggunakan pendekatan **collaborative filtering** (SVD++) dan **content-based filtering** (TF-IDF & cosine similarity). Sistem ini bertujuan memberikan saran produk yang relevan bagi pengguna berdasarkan rating, pola pembelian, dan produk yang pernah dibeli sebelumnya.

## Tujuan Proyek
1. Mengembangkan sistem rekomendasi yang dapat mempertimbangkan fitur produk yang lebih komprehensif, termasuk deskripsi produk dan diskon harga, untuk memberikan rekomendasi yang lebih relevan dan kontekstual bagi pengguna.

2. Menerapkan sistem rekomendasi dengan memanfaatkan interaksi historis pengguna (seperti rating dan pola pembelian) untuk menghasilkan rekomendasi yang lebih personal dan meningkatkan relevansi saran produk, sehingga dapat meningkatkan kepuasan dan loyalitas pengguna.

## Metodologi
- **Content-Based Filtering**: TF-IDF + cosine similarity
- **Collaborative Filtering**: SVD++
- Dataset: 1000+ rating dan review produk e-commerce (sumber: [Amazon Sales Dataset dari Kaggle](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset))

## Evaluasi Model

**1. Content-Based Filtering**
  Precision@10 = 1.0

**2. Collaborative Filtering**
  - RMSE = 0.2670
  - MAE = 0.2013
> Nilai error yang rendah menunjukkan prediksi rating sangat dekat dengan nilai aktual.

## Insight Utama
- Model berhasil memahami preferensi pengguna dari rating, pola pembelian, dan produk yang pernah dibeli sebelumnya
- Sistem rekomendasi ini scalable untuk ditambahkan ke aplikasi nyata

## Tools & Teknologi
- Python, Pandas, NumPy, Matplotlib, Seaborn
- Scikit-Learn (data preprocessing & modeling)
- Surprise Library (Collaborative Filtering)
- TF-IDF & Cosine Similarity (Content-Based Filtering)
- NLTK & spaCy (Text Preprocessing)
- Google Colab (Notebook Environment)

## Cara Menjalankan
Clone repo:
```
git clone https://github.com/nafakhairunnisa/product-recommendation-system.git
```
Install requirements:
```
pip install pandas numpy scikit-learn scipy matplotlib seaborn scikit-surprise spacy nltk
python -m spacy download en_core_web_sm  # Model bahasa Inggris untuk spaCy
python -m nltk.download stopwords  # Download stopwords NLTK
```
Jalankan notebook:
```
jupyter notebook Submission_dari_MLT_Recomendation_System.ipynb
```
## Future Work
Deployment sebagai web service
