# <h1 align="center">Laporan Praktikum Modul 2 - Pengenalan Bahasa C++ (Bagian Kedua)</h1>
<p align="center">Pamelasandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori
Kebutuhan perangkat lunak adalah fondasi dari setiap sistem, yang mendefinisikan semua fungsi, fitur, dan batasan yang harus dipenuhi oleh perangkat lunak. Kebutuhan ini secara umum dibagi menjadi dua kelompok besar. Pertama adalah Kebutuhan Fungsional, yang secara spesifik menjelaskan APA yang harus dilakukan sistem, seperti kemampuan untuk mencetak laporan, memutar musik, atau menghitung jumlah langkah pengguna. Kedua adalah Kebutuhan Non-Fungsional (sering juga disebut kualitas atau batasan), yang mendefinisikan BAGAIMANA sistem harus bekerja atau seberapa baik performanya. Kebutuhan non-fungsional mencakup aspek seperti kecepatan respons (performa), keamanan, usabilitas, dan batasan teknologi yang harus dipatuhi.

Dalam sistem operasi, Proses adalah program yang sedang dieksekusi, dan ia merupakan unit aktivitas yang dikelola oleh OS. Untuk mengontrol proses ini, OS menggunakan struktur data penting yang disebut Process Control Block (PCB), yang menyimpan seluruh informasi mengenai keadaan (state), register, dan kontrol proses tersebut. Sebuah proses akan melalui siklus hidup dengan berbagai keadaan: dimulai dari New (baru dibuat), kemudian ke Ready (siap dieksekusi, menunggu CPU), beralih ke Running (sedang dieksekusi), bisa juga berpindah ke Blocked (menunggu I/O atau event), dan diakhiri dengan Exit (proses selesai). Untuk memastikan semua proses berjalan bersamaan (multitasking), OS menggunakan mekanisme seperti Context Switching (perpindahan cepat antar proses) dan Swapping (pemindahan proses ke disk jika memori utama penuh).


### 1. ...

```C++
#include <iostream>
using namespace std;

const int SIZE = 3;

// Fungsi untuk input matriks
void inputMatriks(int mat[SIZE][SIZE]) {
    cout << "Masukkan elemen matriks 3x3:\n";
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            cout << "Elemen [" << i << "][" << j << "]: ";
            cin >> mat[i][j];
        }
    }
}

// Fungsi untuk tampilkan matriks
void tampilkanMatriks(int mat[SIZE][SIZE]) {
    cout << "Matriks:\n";
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            cout << mat[i][j] << " ";
        }
        cout << endl;
    }
}

// Fungsi penjumlahan matriks
void penjumlahan(int A[SIZE][SIZE], int B[SIZE][SIZE], int hasil[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            hasil[i][j] = A[i][j] + B[i][j];
        }
    }
}

// Fungsi pengurangan matriks
void pengurangan(int A[SIZE][SIZE], int B[SIZE][SIZE], int hasil[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            hasil[i][j] = A[i][j] - B[i][j];
        }
    }
}

// Fungsi perkalian matriks
void perkalian(int A[SIZE][SIZE], int B[SIZE][SIZE], int hasil[SIZE][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            hasil[i][j] = 0;
            for (int k = 0; k < SIZE; k++) {
                hasil[i][j] += A[i][k] * B[k][j];
            }
        }
    }
}

int main() {
    int matriksA[SIZE][SIZE], matriksB[SIZE][SIZE], hasil[SIZE][SIZE];
    int pilihan;

    cout << "=== Program Operasi Matriks 3x3 ===\n";
    inputMatriks(matriksA);
    cout << "\nMatriks A:\n";
    tampilkanMatriks(matriksA);

    inputMatriks(matriksB);
    cout << "\nMatriks B:\n";
    tampilkanMatriks(matriksB);

    cout << "\nPilih operasi:\n1. Penjumlahan\n2. Pengurangan\n3. Perkalian\n";
    cin >> pilihan;

    switch (pilihan) {
        case 1:
            penjumlahan(matriksA, matriksB, hasil);
            cout << "\nHasil Penjumlahan:\n";
            tampilkanMatriks(hasil);
            break;
        case 2:
            pengurangan(matriksA, matriksB, hasil);
            cout << "\nHasil Pengurangan:\n";
            tampilkanMatriks(hasil);
            break;
        case 3:
            perkalian(matriksA, matriksB, hasil);
            cout << "\nHasil Perkalian:\n";
            tampilkanMatriks(hasil);
            break;
        default:
            cout << "Pilihan tidak valid!\n";
    }

    return 0;
}


```
penjelasan singkat 1
Program C++ ini dirancang untuk menghitung penjumlahan, pengurangan, atau perkalian antara dua matriks 3x3. Alurnya sederhana seperti pengguna memasukkan kedua matriks kemudian memilih operasi yang diinginkan, dan program terakhir menggunakan perulangan untuk memproses dan menampilkan hasil perhitungan elemen matriks tersebut. Program ini secara efektif memudahkan pengguna untuk melakukan perhitungan matriks dasar secara otomatis dengan interaksi input dan output yang responsif.

### 2. ...

```C++

#include <iostream>
using namespace std;

// Fungsi swap menggunakan pointer (C-style)
void swapPointer(int *a, int *b, int *c) {
    int temp = *a;
    *a = *b;
    *b = *c;
    *c = temp;
}

// Fungsi swap menggunakan reference (C++)
void swapReference(int &a, int &b, int &c) {
    int temp = a;
    a = b;
    b = c;
    c = temp;
}

int main() {
    int x = 10, y = 20, z = 30;

    cout << "=== Swap Menggunakan Pointer ===\n";
    cout << "Sebelum: x=" << x << ", y=" << y << ", z=" << z << endl;
    swapPointer(&x, &y, &z);
    cout << "Sesudah: x=" << x << ", y=" << y << ", z=" << z << endl;

    // Reset nilai
    x = 10; y = 20; z = 30;

    cout << "\n=== Swap Menggunakan Reference ===\n";
    cout << "Sebelum: x=" << x << ", y=" << y << ", z=" << z << endl;
    swapReference(x, y, z);
    cout << "Sesudah: x=" << x << ", y=" << y << ", z=" << z << endl;

    return 0;
}

```
penjelasan singkat 2
Program C++ ini berfungsi untuk menggeser nilai tiga variabel (cyclic shift) dan secara bersamaan mendemonstrasikan perbedaan antara dua metode passing parameter: pointer dan reference. Fungsi swapPointer mencapai penukaran dengan mengirimkan alamat memori variabel (gaya C) dan mengakses nilainya melalui dereferensi *, sementara fungsi swapReference menggunakan reference (fitur khas C++) yang memungkinkan fungsi langsung bekerja pada variabel asli tanpa perlu menggunakan alamat, di mana kedua metode tersebut berhasil menggeser urutan nilai (a menjadi b, b menjadi c, dan seterusnya).

### 3. ...

```C++

#include <iostream>
using namespace std;

const int UKURAN = 10;
int arrA[UKURAN] = {11, 8, 5, 7, 12, 26, 3, 54, 33, 55};

// Fungsi cari minimum
int cariMinimum() {
    int min = arrA[0];
    for (int i = 1; i < UKURAN; i++) {
        if (arrA[i] < min) {
            min = arrA[i];
        }
    }
    return min;
}

// Fungsi cari maksimum
int cariMaksimum() {
    int max = arrA[0];
    for (int i = 1; i < UKURAN; i++) {
        if (arrA[i] > max) {
            max = arrA[i];
        }
    }
    return max;
}

// Prosedur hitung rata-rata (void, tampilkan hasil)
void hitungRataRata() {
    float sum = 0;
    for (int i = 0; i < UKURAN; i++) {
        sum += arrA[i];
    }
    float rataRata = sum / UKURAN;
    cout << "Rata-rata: " << rataRata << endl;
}

// Fungsi tampilkan isi array
void tampilkanArray() {
    cout << "Isi array: ";
    for (int i = 0; i < UKURAN; i++) {
        cout << arrA[i] << " ";
    }
    cout << endl;
}

int main() {
    int pilihan;

    do {
        cout << "\n--- Menu Program Array ---\n";
        cout << "1. Tampilkan isi array\n";
        cout << "2. Cari nilai maksimum\n";
        cout << "3. Cari nilai minimum\n";
        cout << "4. Hitung nilai rata-rata\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                tampilkanArray();
                break;
            case 2:
                cout << "Nilai maksimum: " << cariMaksimum() << endl;
                break;
            case 3:
                cout << "Nilai minimum: " << cariMinimum() << endl;
                break;
            case 4:
                hitungRataRata();
                break;
            case 0:
                cout << "Keluar program.\n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```
penjelasan singkat  3
Program C++ ini adalah alat bantu sederhana berbasis menu interaktif yang dirancang untuk menganalisis data angka yang tersimpan dalam array berisi 10 elemen. Fungsi utamanya adalah menyediakan empat operasi dasar: menampilkan keseluruhan isi array, mencari nilai maksimum (cariMaksimum), mencari nilai minimum (cariMinimum), dan menghitung rata-rata (hitungRataRata) semua elemen. Pengguna dapat berinteraksi dengan program untuk memilih operasi yang diinginkan, dan program akan terus berjalan hingga pengguna memilih opsi untuk keluar.

##### Output 1
![Screenshot Output 1](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul%202/output-2-1.png)

##### Output 2
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul%202/Output-2-2.png)

##### Output 3
![Screenshot Output 3](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul%202/Output-2-3.png)


## Kesimpulan
...

## Referensi
[1]
<br>Asyiknya Belajar Struktur Data di Planet C++. (n.d.). (n.p.):
Elex Media Komputindo.

<br>

