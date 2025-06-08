# ProyekUAS_2306267044_Nabiel
# Implementasi Regresi Linier Kuadrat Terkecil (Least Squares Linear Regression)

## Nama Program
Regresi Linier Metode Kuadrat Terkecil untuk Analisis Data Eksperimental

## Nama & NPM
**Nama:** Muhammad Pavel  
**NPM:** 2306242363

## Deskripsi Program
Program ini mengimplementasikan metode regresi linier menggunakan teknik kuadrat terkecil (least squares) untuk mencari hubungan linier antara dua variabel berdasarkan data eksperimen yang diberikan. Pengguna dapat memasukkan data pasangan (x, y) dan program akan menghitung persamaan regresi linier terbaik dalam bentuk `y = a0 + a1*x`. Selain itu, program juga menampilkan koefisien determinasi (r^2) sebagai ukuran kualitas model regresi.

Program ini sangat berguna untuk analisis data di bidang teknik, sains, dan ekonomi yang sering membutuhkan pemodelan hubungan antar variabel secara matematis.

---

### Cara Menggunakan
1. Kompilasi program menggunakan compiler C (misal: `gcc`).
2. Jalankan program dan masukkan data yang ingin dianalisis.
3. Program akan menampilkan persamaan regresi, koefisien determinasi, serta hasil prediksi.

---

### Catatan
- Program sudah dilengkapi dengan komentar untuk memudahkan pemahaman setiap langkah proses.
- Source code dapat dikembangkan lebih lanjut untuk aplikasi yang lebih kompleks atau dataset yang lebih besar.

```c
#include <stdio.h>
#include <math.h>

/*
    Fungsi: linear_regression
    Deskripsi: Menghitung parameter regresi linier a0 (intersep) dan a1 (kemiringan)
    Input:
        - n   : jumlah data
        - x[] : array data variabel bebas
        - y[] : array data variabel terikat
    Output:
        - a0  : pointer untuk menyimpan hasil intersep
        - a1  : pointer untuk menyimpan hasil kemiringan (slope)
*/
void linear_regression(int n, double x[], double y[], double *a0, double *a1) {
    double sum_x = 0, sum_y = 0, sum_x2 = 0, sum_xy = 0;
    for (int i = 0; i < n; i++) {
        sum_x += x[i];
        sum_y += y[i];
        sum_x2 += x[i] * x[i];
        sum_xy += x[i] * y[i];
    }
    // Rumus regresi linier (least squares)
    *a1 = (n * sum_xy - sum_x * sum_y) / (n * sum_x2 - sum_x * sum_x);
    *a0 = (sum_y - *a1 * sum_x) / n;
}

/*
    Fungsi: calculate_r_squared
    Deskripsi: Menghitung koefisien determinasi (r^2) sebagai indikator kecocokan model
    Input:
        - n   : jumlah data
        - x[] : array data variabel bebas
        - y[] : array data variabel terikat
        - a0, a1: koefisien hasil regresi linier
    Output:
        - r^2 : nilai koefisien determinasi
*/
double calculate_r_squared(int n, double x[], double y[], double a0, double a1) {
    double sum_y = 0;
    for (int i = 0; i < n; i++) {
        sum_y += y[i];
    }
    double y_mean = sum_y / n;
    double sst = 0, sse = 0;
    for (int i = 0; i < n; i++) {
        double y_pred = a0 + a1 * x[i];
        sst += pow(y[i] - y_mean, 2);  // Total sum of squares
        sse += pow(y[i] - y_pred, 2);  // Residual sum of squares
    }
    return 1 - (sse / sst);
}

/*
    Fungsi: predict
    Deskripsi: Menampilkan hasil prediksi y untuk setiap x berdasarkan model regresi linier
    Input:
        - n   : jumlah data
        - x[] : array data variabel bebas
        - a0, a1: koefisien hasil regresi linier
*/
void predict(int n, double x[], double a0, double a1) {
    printf("\nPrediksi berdasarkan model regresi linier:\n");
    printf("x\tPrediksi y\n");
    for (int i = 0; i < n; i++) {
        double y_pred = a0 + a1 * x[i];
        printf("%.2f\t%.2f\n", x[i], y_pred);
    }
}

int main() {
    // Contoh data eksperimen (bisa diganti)
    int n = 5;
    double x[] = {1, 2, 3, 4, 5};
    double y[] = {2, 4, 5, 4, 5};
    double a0, a1;

    // Hitung regresi linier
    linear_regression(n, x, y, &a0, &a1);

    // Tampilkan persamaan regresi
    printf("Persamaan regresi: y = %.2f + %.2fx\n", a0, a1);

    // Hitung koefisien determinasi (r^2)
    double r_squared = calculate_r_squared(n, x, y, a0, a1);
    printf("Koefisien determinasi (r^2): %.4f\n", r_squared);

    // Prediksi nilai y untuk setiap x
    predict(n, x, a0, a1);

    return 0;
}

```
