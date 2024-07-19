# CNN-DQN-KAN for Atari Games

Deep Q-Networks (DQN) adalah salah satu algoritma reinforcement learning yang menggabungkan Q-Learning dengan jaringan saraf tiruan, menawarkan cara yang efektif untuk menangani lingkungan yang kompleks seperti game Atari. DQN menjadi alternatif yang kuat untuk Q-Learning konvensional, dengan kemampuan untuk belajar dari representasi visual yang tinggi menggunakan jaringan saraf dalam.

Dalam proyek ini, saya mencoba untuk mengevaluasi performa yang dihasilkan oleh Kolmogorov Arnold Networks (KAN) ketika digabungkan dengan CNN-DQN pada kasus game Atari. KAN adalah alternatif dari Multi-Layer Perceptron (MLP) yang dapat diterapkan pada berbagai arsitektur jaringan saraf sebagai pengganti MLP. Dalam kode ini, saya membuat empat kombinasi sebagai berikut:

1. **CNN-DQN-MLP (ReLU)**: Fully Connected Layer menggunakan MLP dengan fungsi aktivasi ReLU.
2. **CNN-DQN-KAN (ReLU)**: Fully Connected Layer menggunakan KAN dengan fungsi aktivasi ReLU.
3. **CNN-DQN-MLP (SELU)**: Fully Connected Layer menggunakan MLP dengan fungsi aktivasi SELU.
4. **CNN-DQN-KAN (SELU)**: Fully Connected Layer menggunakan KAN dengan fungsi aktivasi SELU (Hasil Terbaik).

Kode ini dirancang untuk dijalankan di Kaggle, dengan sumber asli kode dari [link Kaggle berikut](https://www.kaggle.com/code/kingjuno/dqn-atari-pytorch). Pengembangan kode CNN-DQN-KAN berasal dari [repository berikut](https://github.com/jakariaemon/CNN-KAN).

Hasil plotting training:

![Deskripsi gambar](images/1.png)

![Deskripsi gambar](images/2.png)

![Deskripsi gambar](images/3.png)

![Deskripsi gambar](images/4.png)

Hasil GIF:
1. **gym_animation-mlp**

   ![gif](video/gym_animation-mlp.gif)

2. **gym_animation-kan-relu**

   ![gif](video/gym_animation_kan_relu.gif)

3. **gym_animation-kan-selu**

   ![gif](video/gym_animation_kan_selu.gif)

## Analisis Perbandingan

**Note:** Semua model hanya dilatih sekali, kecuali model CNN DQN - MLP (SELU) yang dilatih dua kali untuk memastikan apakah ada perubahan performa. Fungsi aktivasi SELU digunakan tanpa inisialisasi LeCun. Hasil ini hanya untuk eksperimen iseng, bukan eksperimen serius. :D

1. **Performa Reward:**
   - **DQN-MLP (ReLU):** Menunjukkan reward yang baik dan stabil di sekitar nilai 18.
   - **DQN-KAN (SELU) dan DQN-KAN (ReLU):** Menunjukkan reward yang baik tetapi memerlukan waktu pelatihan lebih lama dibandingkan DQN-MLP.
   - **DQN-MLP (SELU):** Menunjukkan reward yang kurang stabil dengan fluktuasi signifikan.

2. **Waktu Pelatihan:**
   - **DQN-MLP (ReLU) dan DQN-MLP (SELU):** Memerlukan waktu pelatihan lebih singkat dibandingkan dengan DQN-KAN.
   - **DQN-KAN (ReLU dan SELU):** Memerlukan waktu pelatihan lebih lama tetapi menunjukkan hasil yang lebih stabil.

3. **Ukuran Model:**
   - **DQN-KAN:** Ukuran model jauh lebih besar (~61.8 MB) dibandingkan dengan DQN-MLP (~6 MB).

   Ukuran model yang lebih besar pada DQN-KAN memberikan kemampuan pemodelan yang lebih kompleks tetapi membutuhkan sumber daya komputasi yang lebih besar.

4. **Stabilitas Loss:**
   - Semua model menunjukkan penurunan nilai loss yang cepat pada tahap awal pelatihan dan stabil pada nilai rendah setelah frame 200.000.
   - **DQN-MLP (SELU):** Menunjukkan peningkatan loss signifikan pada beberapa titik, menunjukkan adanya instabilitas.

5. **Kesimpulan:**
   - **DQN-MLP (ReLU):** Pilihan yang efisien dengan waktu pelatihan lebih singkat dan ukuran model lebih kecil, menunjukkan performa reward yang baik dan stabil.
   - **DQN-KAN (ReLU dan SELU):** Meski memerlukan waktu pelatihan lebih lama dan ukuran model lebih besar, memberikan hasil reward yang baik dan stabil dengan biaya komputasi lebih tinggi.
   - **DQN-MLP (SELU):** Menunjukkan reward yang kurang stabil dan fluktuatif, mungkin kurang cocok untuk tugas ini dibandingkan dengan konfigurasi lainnya.

Perbandingan ini menunjukkan adanya trade-off antara kompleksitas model, waktu pelatihan, dan performa yang dihasilkan. Pemilihan model yang tepat bergantung pada kebutuhan spesifik aplikasi dan sumber daya yang tersedia.

**Buat Pengetahuan Bersama:**
Mengapa waktu training dan size model kombinasi KAN lebih besar? Karena arsitektur KAN menggunakan fungsi aktivasi tepi yang dapat dipelajari dan disesuaikan selama pelatihan, berbeda dengan MLP yang memiliki fungsi aktivasi tetap dan tidak dapat dipelajari.
