# Model Klasifikasi Kategori Produk Amazon

Model ini memprediksi kategori produk Amazon berdasarkan nama dan deskripsi produk.  Model dilatih menggunakan dataset Amazon Sales Dataset dari Kaggle.

## Deskripsi Model

Model ini adalah model neural network sederhana yang menggunakan arsitektur *feedforward* dengan dua lapisan *dense* dan *dropout* untuk mencegah *overfitting*.  Proses pelatihan menggunakan fungsi kerugian `sparse_categorical_crossentropy` dan pengoptimal `adam`.  Model dikonversi ke format TensorFlow Lite untuk deployment pada perangkat mobile.

**Arsitektur Model:**

* Lapisan Input:  Jumlah fitur TF-IDF (5000 dalam kasus ini).
* Lapisan Tersembunyi 1:  128 neuron, fungsi aktivasi ReLU, dropout 0.3.
* Lapisan Tersembunyi 2:  64 neuron, fungsi aktivasi ReLU, dropout 0.3.
* Lapisan Output:  Jumlah kelas kategori, fungsi aktivasi softmax.

## Data

Dataset yang digunakan adalah Amazon Sales Dataset dari Kaggle ([https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset](https://www.kaggle.com/datasets/karkavelrajaj/amazon-sales-dataset)).  Dataset ini telah diproses untuk:

* Memilih kolom `product_name`, `category`, dan `about_product`.
* Menggabungkan kolom `product_name` dan `about_product` menjadi satu fitur teks.
* Menghapus baris dengan nilai yang hilang.
* Mengambil kategori terakhir jika terdapat beberapa kategori yang dipisahkan oleh "|".
* Merepresentasikan fitur teks menggunakan TF-IDF dengan `max_features=5000`.
* Meng-encode label kategori menggunakan LabelEncoder.
* Membagi data menjadi set pelatihan, validasi, dan pengujian (70%, 15%, 15%).

## Preprocessing

Preprocessing data meliputi:

* **TF-IDF Vectorization:**  Mengubah teks menjadi representasi numerik menggunakan TF-IDF.
* **Label Encoding:** Mengubah label kategori menjadi representasi numerik.

## Pelatihan

Model dilatih dengan parameter berikut:

* Epochs: 50
* Batch size: 32
* Optimizer: Adam
* Fungsi kerugian: Sparse Categorical Crossentropy
* Metrik: Accuracy
* Early Stopping: Digunakan untuk mencegah overfitting.

## Evaluasi

Model dievaluasi pada set pengujian dan menghasilkan:

* **Test Loss:** [Masukkan nilai Test Loss di sini]
* **Test Accuracy:** [Masukkan nilai Test Accuracy di sini]

## Deployment

Model telah dikonversi ke format TensorFlow Lite (`model_user_category.tflite`) untuk deployment yang efisien pada perangkat mobile.

## Penggunaan

Untuk memprediksi kategori produk, berikan teks nama dan deskripsi produk sebagai input.  Model akan memberikan prediksi kategori.  Contoh penggunaan:

```python
sample_text = ["Logitech K380 Wireless Multi-Device Keyboard"]
# ... (kode untuk memproses input dan melakukan prediksi) ...
print(f"Predicted category: {predicted_category[0]}")
