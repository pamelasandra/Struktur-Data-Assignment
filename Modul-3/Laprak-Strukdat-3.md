# <h1 align="center">Laporan Praktikum Modul 3 - Abstract Data Type (ADT)</h1>
<p align="center">Pamelasandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori
Tipe Data Abstrak (ADT) merupakan suatu model konseptual yang menetapkan sebuah tipe data beserta serangkaian operasi dasar (primitif) yang dapat dilaksanakan pada tipe data tersebut. Anggap ADT sebagai "rencana" yang tidak hanya menggambarkan struktur data (contohnya, sebuah struct di C++), tetapi juga menetapkan semua fungsi yang dapat berinteraksi dengannya. Fungsi-fungsi dasar ini dibagi menjadi beberapa kategori, seperti Konstruktor untuk menciptakan objek baru, Selector untuk mengakses atau mengambil data di dalamnya (sering diawali dengan Get), dan operator lain untuk validasi, input/output, sampai perbandingan.

Dalam praktiknya, konsep ADT diimplementasikan dengan membagi kode menjadi dua file utama untuk mencapai modularitas: satu file header (.h) dan satu file body (.cpp). File header (.h) berperan sebagai spesifikasi atau "wajah publik" dari ADT, mencakup deklarasi tipe data (seperti struct mahasiswa) dan prototipe untuk semua fungsi primitifnya. Sementara itu, berkas body (.cpp) memuat implementasi atau kode program rinci dari setiap fungsi yang telah dideklarasikan di header. Program utama (driver) dapat menggunakan ADT ini dengan mengimpor file header (.h), yang memungkinkan adanya pemisahan jelas antara antarmuka (cara penggunaan) dan implementasi (cara kerja).

### 1. ...

```C++
#include <iostream>
using namespace std;

struct Mahasiswa {
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;
};

float hitungNilaiAkhir(float uts, float uas, float tugas) {
    return 0.3 * uts + 0.4 * uas + 0.3 * tugas;
}

int main() {
    Mahasiswa mhs[10];
    int n;

    cout << "Masukkan jumlah mahasiswa (max 10): ";
    cin >> n;

    if (n > 10) n = 10;

    for (int i = 0; i < n; i++) {
        cout << "\nData mahasiswa ke-" << i + 1 << endl;
        cout << "Nama   : ";
        cin.ignore();
        getline(cin, mhs[i].nama);
        cout << "NIM    : ";
        getline(cin, mhs[i].nim);
        cout << "UTS    : ";
        cin >> mhs[i].uts;
        cout << "UAS    : ";
        cin >> mhs[i].uas;
        cout << "Tugas  : ";
        cin >> mhs[i].tugas;

        mhs[i].nilaiAkhir = hitungNilaiAkhir(mhs[i].uts, mhs[i].uas, mhs[i].tugas);
    }

    cout << "\n=========================================\n";
    cout << "Daftar Nilai Mahasiswa\n";
    cout << "=========================================\n";
    cout << "Nama\t\tNIM\t\tNilai Akhir\n";
    cout << "-----------------------------------------\n";

    for (int i = 0; i < n; i++) {
        cout << mhs[i].nama << "\t\t"
             << mhs[i].nim << "\t\t"
             << mhs[i].nilaiAkhir << endl;
    }

    cout << "=========================================\n";

    return 0;
}

```
Penjelasan singkat 1
Program pertama dirancang untuk menyimpan informasi maksimum 10 mahasiswa dengan memanfaatkan array struktur. Struktur yang diterapkan mencakup beberapa field, yaitu nama, nim, uts, uas, tugas, serta nilaiAkhir. Nilai akhir mahasiswa dihitung secara otomatis menggunakan fungsi dengan rumus 0.3 × uts + 0.4 × uas + 0.3 × tugas. Program meminta masukan dari pengguna untuk setiap mahasiswa, lalu menampilkan informasi dalam format tabel yang berisi nama, NIM, dan nilai akhir. Tujuan utama dari program ini adalah untuk melatih penggunaan array of struct, implementasi fungsi, dan perhitungan nilai yang berbasis pada struktur data di C++


### 2. ...

```h

#ifndef PELAJARAN_H
#define PELAJARAN_H

#include <string>
using namespace std;

struct pelajaran {
    string namaMapel;
    string kodeMapel;
};

pelajaran create_pelajaran(string namaPel, string kodePel);
void tampil_pelajaran(pelajaran pel);

#endif

```

```C++

#include <iostream>
#include "pelajaran.h"
using namespace std;

pelajaran create_pelajaran(string namaPel, string kodePel) {
    pelajaran p;
    p.namaMapel = namaPel;
    p.kodeMapel = kodePel;
    return p;
}

void tampil_pelajaran(pelajaran pel) {
    cout << "nama pelajaran : " << pel.namaMapel << endl;
    cout << "nilai : " << pel.kodeMapel << endl;
}

```

```C++

#include <iostream>
#include "pelajaran.h"
using namespace std;

int main() {
    string namaPel = "Struktur Data";
    string kodePel = "STD";

    pelajaran pel = create_pelajaran(namaPel, kodePel);
    tampil_pelajaran(pel);

    return 0;
}


```
penjelasan singkat 2
Program kedua menerapkan prinsip Tipe Data Abstrak (ADT) dengan memisahkan kode ke dalam tiga berkas, yaitu pelajaran.h, pelajaran.cpp, dan main.cpp. Berkas pelajaran.h mencakup deklarasi struktur pelajaran yang memiliki atribut namaMapel dan kodeMapel, serta prototipe fungsi create_pelajaran() dan tampil_pelajaran(). File pelajaran.cpp mengandung implementasi kedua fungsi tersebut, di mana create_pelajaran() berfungsi untuk membuat objek pelajaran berdasarkan parameter nama dan kode, sedangkan tampil_pelajaran() digunakan untuk menampilkan hasilnya. Dalam fail main.cpp, program utama menciptakan satu objek pelajaran bernama “Struktur Data” dengan kode “STD”, lalu menampilkan hasilnya pada layar. Program ini memperlihatkan penerapan pemrograman modular dan pemisahan logika di antara berkas dalam konsep ADT

### 3. ...

```C++

#include <iostream>
using namespace std;

void tampilArray(int arr[3][3]) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            cout << arr[i][j] << "\t";
        }
        cout << endl;
    }
}

void tukarElemen(int arr1[3][3], int arr2[3][3], int baris, int kolom) {
    int temp = arr1[baris][kolom];
    arr1[baris][kolom] = arr2[baris][kolom];
    arr2[baris][kolom] = temp;
}

void tukarPointer(int *p1, int *p2) {
    int temp = *p1;
    *p1 = *p2;
    *p2 = temp;
}

int main() {
    int A[3][3] = {
        {1, 2, 3},
        {4, 5, 6},
        {7, 8, 9}
    };

    int B[3][3] = {
        {10, 11, 12},
        {13, 14, 15},
        {16, 17, 18}
    };

    int *ptr1, *ptr2;
    ptr1 = &A[1][1];  
    ptr2 = &B[2][2];  
    cout << "Array A sebelum ditukar:\n";
    tampilArray(A);
    cout << "\nArray B sebelum ditukar:\n";
    tampilArray(B);

    tukarElemen(A, B, 0, 0);

    cout << "\nSetelah menukar elemen A[0][0] dengan B[0][0]:\n";
    cout << "Array A:\n";
    tampilArray(A);
    cout << "\nArray B:\n";
    tampilArray(B);

    tukarPointer(ptr1, ptr2);

    cout << "\nSetelah menukar nilai yang ditunjuk pointer:\n";
    cout << "Array A:\n";
    tampilArray(A);
    cout << "\nArray B:\n";
    tampilArray(B);

    return 0;
}




```
penjelasan singkat  3
Program ketiga dirancang untuk mengelola dua array dua dimensi berukuran 3x3 serta dua pointer integer. Program ini memiliki beberapa fungsi utama, yaitu tampilArray() untuk menampilkan konten array 2D dengan rapi, tukarElemen() untuk menukar nilai pada lokasi tertentu antara dua array 2D, dan tukarPointer() untuk menukar isi dua variabel yang diarahkan oleh pointer. Di dalam fungsi utama (main()), dua array diinisialisasi dan ditampilkan terlebih dahulu, setelah itu dilakukan proses pertukaran nilai baik lewat fungsi tukarElemen() maupun dengan tukarPointer(). Hasil akhirnya menunjukkan modifikasi konten array setelah pertukaran. Program ini menunjukkan bagaimana pointer dan array dua dimensi dapat digunakan bersamaan untuk mengolah data secara langsung di dalam memori.

##### Output 1
![Screenshot Output 1](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-3/Output-3-1.png)

##### Output 2
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-3/Output-3-2.png)

##### Output 3
![Screenshot Output 3](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-3/Output-3-3.png)


## Kesimpulan
...

## Referensi
[1]
<br>Chaniago, M. B., & Sastradipraja, C. K. (2022). Buku Ajar
Algoritma dan Struktur Data. Kaizen Media Publishing.
<br>