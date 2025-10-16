# <h1 align="center">Laporan Praktikum Modul 1 - Codeblocks IDE & Pengenalan Bahas C++ (1)</h1>
<p align="center">Pamela Sandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori
Materi ini memperkenalkan Code::Blocks, sebuah lingkungan pengembangan (IDE) gratis yang digunakan untuk menulis program dalam bahasa C++. Anda akan belajar cara menginstal , membuat proyek baru , menulis kode, dan menjalankan program. Selain itu, modul ini juga menjelaskan cara mengatasi masalah umum, seperti ketika program tidak bisa berjalan, dengan fitur seperti Clean project , serta cara memahami pesan kesalahan (error messages) yang muncul saat ada kesalahan penulisan kode.


Pada bagian dasar pemrograman, dijelaskan konsep-konsep inti C++. Ini mencakup struktur dasar program , penggunaan tipe data (seperti int untuk angka bulat dan float untuk desimal) , dan variabel untuk menyimpan nilai. Anda juga akan mempelajari operator untuk operasi matematika dan logika , serta struktur kontrol alur program seperti pernyataan kondisional (if-else, switch) untuk membuat keputusan dan perulangan (for, while, do-while) untuk menjalankan tugas berulang kali.


### 1. ...

```C++
#include <iostream>
using namespace std;

int main() {
    float a, b;

    cout << "Masukkan bilangan pertama: ";
    cin >> a;
    cout << "Masukkan bilangan kedua: ";
    cin >> b;

    cout << "\nPenjumlahan : " << a + b << endl;
    cout << "Pengurangan : " << a - b << endl;
    cout << "Perkalian   : " << a * b << endl;
    cout << "Pembagian   : " << a / b << endl;

    return 0;
}

```
Penjelasan singkat 1
Di program ini, kami mengaturnya agar bisa meminta pengguna memasukkan dua buah angka, dan kami pastikan programnya bisa menerima angka desimal (tipe float). Setelah kedua angka tersebut diinput, program yang kami buat akan langsung memprosesnya untuk melakukan empat operasi aritmatika dasar. Terakhir, hasilnya—baik itu penjumlahan, pengurangan, perkalian, maupun pembagian—akan langsung kami tampilkan di layar pengguna.


### 2. ...

```C++

#include <iostream>
using namespace std;

int main() {
    int angka;

    cout << "Masukkan angka (0-100): ";
    cin >> angka;

    if (angka < 0 || angka > 100 ) {
        cout << "Angka di luar jangkauan" << endl;

        return 0;
    }

    string satuan[] = {"", "satu", "dua", "tiga", "empat", "lima", "enam",  "tujuh", "delapan", "sembilan"};
    string belasan[] = {"Sepuluh", "Sebelas", "Dua Belas", "Tiga Belas", "Empat Belas", "Lima Belas", "Enam Belas", "Tujuh Belas", "Delapan Belas", "Sembilan Belas"};
    string puluhan[] = {"", "", "Dua Puluh", "Tiga Puluh", "Empat Puluh", "Lima Puluh", "Enam Puluh", "Tujuh Puluh", "Delapan Puluh", "Sembilan Puluh"};

    if (angka == 0) {
        cout << "Nol" << endl;
    } else if (angka == 100) {
        cout << "Seratus" << endl;
    } else if (angka >= 10 && angka < 20) {
        cout << belasan[angka - 10] << endl;
    } else {
        int puluh = angka / 10;
        int satu = angka % 10;

        if (puluh > 0) cout << puluhan[puluh];
        if (puluh > 0 && satu > 0) cout << " ";
        if (satu >  0) cout << satuan[satu];
        cout << endl;
    }
    return 0;
}

```
penjelasan singkat 2
Program C++ ini adalah sebuah alat konversi yang menerjemahkan bilangan bulat dari 0 hingga 100 ke dalam bentuk teks Bahasa Indonesia.Cara kerjanya dimulai dengan meminta input angka dari pengguna, lalu program akan memeriksa apakah angka tersebut berada dalam rentang yang diizinkan. Jika inputnya valid, program akan menggunakan logika khusus: angka-angka seperti 0, 100, dan kelompok belasan (10-19) akan langsung diubah ke bentuk katanya. Untuk angka lainnya, program akan memecahnya menjadi digit puluhan dan satuan, kemudian menggabungkan kedua tulisan tersebut untuk menghasilkan representasi teks yang lengkap.


### 3. ...

```C++

#include <iostream>
using namespace std;

int main() {
    int n;
    cout << "Input: ";
    cin >> n;

    cout << "Output:" << endl;

    for (int i = n; i >= 1; i--) {
        for (int s = n; s > i; s--) {
            cout << "  ";
        }

        for (int j = i; j >= 1; j--) {
            cout << j << " ";
        }

        cout << "* ";

        for (int j = 1; j <= i; j++) {
            cout << j;
            if (j < i) cout << " ";
        }

        cout << endl;
    }

    for (int s = 0; s < n; s++) {
        cout << "  ";
    }
    cout << "*" << endl;

    return 0;
}



```
penjelasan singkat  3
Program C++ ini dirancang untuk mencetak sebuah pola angka yang simetris dan reflektif, seperti cermin. Berikan sebuah angka sebagai input, dan program akan menggunakan angka itu untuk memulai polanya. Di setiap baris, program akan menampilkan dua urutan angka yang dipisahkan oleh tanda bintang (*) di tengah. Urutan di sebelah kiri akan menghitung mundur ke angka 1, sementara urutan di sebelah kanan akan menghitung maju dari 1. Pola ini akan semakin mengecil di setiap barisnya, hingga akhirnya hanya tersisa satu tanda bintang di bagian paling bawah.

##### Output 1
![Screenshot Output 1](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul 1/Output-1-1.png)

##### Output 2
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul 1/Output-1-2.png)

##### Output 3
![Screenshot Output 3](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul 1/Output-1-3.png)


## Kesimpulan
...

## Referensi
[1]
<br>Asyiknya Belajar Struktur Data di Planet C++. (n.d.). (n.p.):
Elex Media Komputindo.
<br>