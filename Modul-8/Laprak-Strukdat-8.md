# <h1 align="center">Laporan Praktikum Modul 8 - Queue</h1>
<p align="center">Pamela Sandra Amelia Br Ginting - 103112430228</p>

## Dasar Teori
Queue (antrean) adalah struktur data linear yang cara kerjanya menyerupai antrean di dunia nyata, seperti antrean pada loket tiket kereta api. Dalam mekanisme ini, individu yang pertama kali datang akan menjadi orang pertama yang dilayani, sedangkan mereka yang bergabung belakangan harus menunggu hingga giliran terakhir. Oleh karena itu, prinsip utama yang mendasari Queue adalah FIFO (First In, First Out), yang berarti data yang pertama kali dimasukkan ke dalam sistem akan menjadi data yang pertama kali diproses atau dikeluarkan. Dalam bahasa pemrograman C, struktur data ini umumnya diimplementasikan dengan memanfaatkan tipe data array statis maupun struktur linked list yang lebih dinamis.

#### A. Materi queue
Praktikum ini memfokuskan pada implementasi struktur data Queue dengan memanfaatkan linked list, yang secara teknis jauh lebih sederhana dibandingkan operasi list pada umumnya. Hal ini dikarenakan Queue mengikuti prinsip FIFO (First In, First Out), di mana aktivitas penghapusan elemen (dequeue) hanya terfokus pada bagian Head (depan), sementara penyisipan elemen baru (enqueue) selalu dilakukan di bagian Tail (belakang), atau sebaliknya sesuai dengan logika yang diterapkan. Dalam praktiknya, struktur antrean ini sangat fleksibel karena dapat dibangun baik menggunakan Singly Linked List maupun Doubly Linked List untuk mengelola aliran datanya.

#### 1. Enqueue
EnQueue merupakan proses memasukkan data ke akhir antrian dalam bentuk array, sehingga simbol atau elemen yang ditambahkan akan berada di urutan paling belakang.

#### 2. Dequeue
ueue merupakan proses penghapusan elemen yang dilakukan dari bagian terdepan antrian.

## Guided 
### . [guided 1]
### . Penggunaan Queue 

```C++
//queue.h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
#include<string>

using namespace std;

struct Node {
    string nama;
    Node* next;
};

struct queue {
    Node* head;
    Node* tail;
};

void createQueue(queue &Q);
bool isEmpty(queue Q);
bool isFull(queue Q);
void enQueue(queue &Q, const string &nama);
void deQueue(queue &Q);
void viewQueue(queue Q);
void clearQueue(queue &Q);

#endif

//queue.cpp
#include "queue.h"
using namespace std;

void createQueue(queue &Q) {
    Q.head = nullptr;
    Q.tail = nullptr;
}

bool isEmpty(queue Q) {
    return Q.head == nullptr;
}

bool isFull(queue) {
    return false;
}

void enQueue(queue &Q, const string &nama) {
    Node* baru = new Node{nama, nullptr};
    if (isEmpty(Q)) {
        Q.head = Q.tail = baru;
    } else {
        Q.tail->next = baru;
        Q.tail = baru;
    }
    cout << "nama " << nama << " berhasil ditambahkan kedalam queue!" << endl;
}

void deQueue(queue &Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
        return;
    }
    Node* hapus = Q.head;
    cout << "Menghapus data " << hapus->nama << "..." << endl;
    Q.head = Q.head->next;
    if (Q.head == nullptr) {
        Q.tail = nullptr;
    }
    delete hapus;
}

void viewQueue(queue Q) {
    if (isEmpty(Q)) {
        cout << "Queue kosong!" << endl;
        return;
    }
    int i = 1;
    for (Node* p = Q.head; p != nullptr; p = p->next) {
        cout << i++ << ". " << p->nama << endl;
    }
}

void clearQueue(queue &Q) {
    while (!isEmpty(Q)) {
        deQueue(Q);
    }
}

//main.cpp
#include "queue.h"
#include "queue.cpp"
#include <iostream>
using namespace std;

int main() {
    queue Q;
    createQueue(Q);

    enQueue(Q, "dhimas");
    enQueue(Q, "Arvin");
    enQueue(Q, "Rizal");
    enQueue(Q, "Hafizh");
    enQueue(Q, "Fathur");
    enQueue(Q, "Atha");
    cout << endl;

    cout << "--- Isi Queue Setelah enQueue ---" << endl;
    viewQueue(Q);

    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    cout << endl;

    cout << "--- Isi Queue Setelah deQueue ---" << endl;
    viewQueue(Q);

    clearQueue(Q);
    return 0;
}
   
```
Program ini dirancang untuk membangun dan mengelola sistem antrean (Queue) berbasis linked list yang beroperasi sesuai dengan prinsip FIFO (First In, First Out), di mana data yang pertama kali dimasukkan akan menjadi data yang pertama kali diproses atau dikeluarkan. Secara fungsional, program ini memberikan fleksibilitas kepada pengguna untuk menambahkan elemen baru ke dalam antrean, menghapus data yang berada di posisi paling depan, hingga membersihkan seluruh isi antrean secara sekaligus. Selain itu, tersedia pula prosedur viewQueue yang berfungsi untuk memindai dan menampilkan seluruh urutan data yang sedang tersimpan di dalam antrean secara sistematis.


### . [guided 2]
### . Penggunaan Queue dengan beberapa implementasi

```C++
//queue.h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

const int MAKSIMAL = 5;

struct queue {
    string nama[MAKSIMAL];
    int head;
    int tail;
};

bool isFull(queue Q);
bool isEmpty(queue Q);
void createQueue(queue &Q); //terbentuk queue dengan head = -1 dan tail = -1
void enQueue(queue &Q, string nama); 
void deQueue(queue &Q);
void viewQueue(queue Q);

#endif

//queue.cpp
#include "queue.h"
#include <iostream>

using namespace std;

// NOTE : 
// Implementasi 1 = head diam, tail bergerak (Queue Linear Statis, kerana head nya tetap diam)
// Implementasi 2 = head bergerak, tail bergerak (Queue Linear Dinamis, karena head & tail nya sama-sama bergerak)
// Implementasi 3 = head dan tail berputar (Queue Circular, karena jika udh mentok tapi masih ada space, diputar sehingga tail bisa ada didepan head)

bool isEmpty(queue Q){
    if(Q.head == -1 && Q.tail == -1){
        return true;
    } else {
        return false;
    }
}

//isFull implmenetasi 1 & 2
bool isFull(queue Q){
    if(Q.tail == MAKSIMAL - 1){
        return true;
    } else {
        return false;
    }
}

// //isFull implementasi 3
// bool isFull(queue Q){
//     if((Q.tail + 1) % MAKSIMAL == Q.head){
//         return true;
//     } else {
//         return false;
//     }
// }

void createQueue(queue &Q){ //terbentuk queue dengan head = -1 dan tail = -1 
    Q.head = -1;
    Q.tail = -1;
}
 

//enqueue implementasi 1 & 2
void enQueue(queue &Q, string nama){
    if(isFull(Q) == true){
        cout << "Queue sudah penuh!" << endl;
    } else {
        if(isEmpty(Q) == true){
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.nama[Q.tail] = nama;
        cout << "nama " << nama << " berhasil ditambahkan kedalam queue!" << endl;
    }
}

// //enQueue implementasi 3
// void enQueue(queue &Q, string nama){
//     if(isFull(Q) == true){
//         cout << "Queue sudah penuh!" << endl;
//     } else {
//         if(isEmpty(Q) == true){
//             Q.head = Q.tail = 0;
//         } else {
//             Q.tail = (Q.tail + 1) % MAKSIMAL; // bergerak melingkar
//         }
//         Q.nama[Q.tail] = nama;
//         cout << "nama " << nama << " berhasil ditambahkan kedalam queue!" << endl;
//     }
// }

//dequeue implementasi 1
void deQueue(queue &Q){
    if(isEmpty(Q) == true){
        cout << "Queue kosong!" << endl;
    } else {
        cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
        for(int i = 0; i < Q.tail; i++){
            Q.nama[i] =  Q.nama[i+1];
        }
        Q.tail--;
        if(Q.tail < 0){ //kalo semua isi queue nya udh dikelaurin, set head & tail ke -1
            Q.head = -1;
            Q.tail = -1;
        }
    }
}

// //dequeue implementasi 2
// void deQueue(queue &Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
//         Q.head++;
//         if(Q.head > Q.tail){ //kalo elemennya udh abis (head akan lebih 1 dari tail), maka reset ulang head & tail ke -1
//             Q.head = -1;
//             Q.tail = -1;
//         }
//     }
// }

// //deQueue implementasi 3
// void deQueue(queue &Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         cout << "Mengahapus data " << Q.nama[Q.head] << "..." << endl;
//         if(Q.head == Q.tail){ //kalo elemennya tinggal 1, langsungkan saja head & tail nya reset ke -1
//             Q.head = -1;
//             Q.tail = -1;
//         } else {
//             Q.head = (Q.head + 1) % MAKSIMAL; // bergerak melingkar
//         }
//     }
// }

//viewQueue implementasi 1 & 2
void viewQueue(queue Q){
    if(isEmpty(Q) == true){
        cout << "Queue kosong!" << endl;
    } else {
        for(int i = Q.head; i <= Q.tail; i++){
            cout << i -  Q.head + 1 << ". " << Q.nama[i] << endl;
        }
    }
    cout << endl;
}

// //viewQueue implementasi 3
// void viewQueue(queue Q){
//     if(isEmpty(Q) == true){
//         cout << "Queue kosong!" << endl;
//     } else {
//         int i = Q.head;
//         int count = 1;
//         while(true){
//             cout << count << ". " << Q.nama[i] << endl;
//             if(i == Q.tail){
//                 break;
//             }
//             i = (i + 1) % MAKSIMAL;
//             count++;
//         }   
//     }
// }

//main.cpp
#include "queue.h"
#include "queue.cpp"
#include <iostream>

using namespace std;

int main(){
    queue Q;

    createQueue(Q);
    enQueue(Q, "dhimas");
    enQueue(Q, "Arvin");
    enQueue(Q, "Rizal");
    enQueue(Q, "Hafizh");
    enQueue(Q, "Fathur");
    enQueue(Q, "Daffa");
    cout << endl;

    cout << "--- Isi Queue Setelah enQueue ---" << endl;
    viewQueue(Q);
    cout << endl;

    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    deQueue(Q);
    // deQueue(Q);
    // deQueue(Q);
    cout << endl;

    cout << "--- Isi Queue Setelah deQueue ---" << endl;
    viewQueue(Q);

    return 0;
}
```
Program ini dirancang untuk mengelola sistem antrean dengan prinsip FIFO menggunakan media array, yang dijabarkan ke dalam tiga model implementasi berbeda. Model pertama menggunakan Head tetap dan Tail bergerak, di mana data selalu dihapus dari posisi nol dan elemen lainnya akan bergeser maju. Model kedua adalah Head dan Tail yang berpindah, di mana kedua penanda tersebut terus bergeser ke arah kanan setiap kali terjadi penambahan atau penghapusan tanpa menggeser elemen fisik. Terakhir, terdapat model Head dan Tail yang berputar (Circular Queue), sebuah metode efisien yang memungkinkan penanda kembali ke posisi awal array saat mencapai batas akhir, sehingga ruang memori yang telah kosong dapat digunakan kembali secara optimal.

## Unguided

## soal 1. {alternatif 1}

```C++
//queue.h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 5;

struct queue {
    int info[MAX];
    int head;
    int tail;
};

void createQueue(queue &Q);
bool isEmpty(queue Q);
bool isFull(queue Q);
int enqueue(queue &Q, infotype X); 
void dequeue(queue &Q);
void printInfo(queue Q);

#endif

//queue.cpp
#include "queue.h"
#include <iostream>

using namespace std;

bool isEmpty(queue Q){
    if(Q.head == -1 && Q.tail == -1){
        return true;
    } else {
        return false;
    }
}

bool isFull(queue Q){
    if(Q.tail == MAX - 1 ){
        return true;
    } else {
        return false;
    }
}


void createQueue(queue &Q){ 
    Q.head = -1;
    Q.tail = -1;
}
 


int enqueue(queue &Q, infotype X){
    if(isFull(Q) == true){
        cout << "Queue sudah penuh!" << endl;
    } else {
        if(isEmpty(Q) == true){
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = X;
    }
    return 0;
}

void dequeue(queue &Q){
    if(isEmpty(Q)){
        cout << "Queue kosong!" << endl;
    } else {
        for(int i = Q.head; i < Q.tail; i++){
            Q.info[i] = Q.info[i+1];
        }
        Q.tail--;
        if(Q.tail < Q.head){ 
            Q.head = -1;
            Q.tail = -1;
        }
    }
}

void printInfo(queue Q){
      cout << Q.head << " - " << Q.tail << " | ";
    if(isEmpty(Q) == true){
        cout << "Empty Queue";
    } else {
        for(int i = Q.head; i <= Q.tail; i++){
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}

//main.cpp
#include "queue.h"
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello World" << endl;
    queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "----------------------" << endl;
    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
### Output soal 1 :
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-8/Output-8-1.png)

Program ini mengimplementasikan sistem antrean (Queue) menggunakan array dengan kapasitas statis yang dibatasi maksimal sebanyak 5 elemen. Metode yang digunakan dalam pengelolaan antrean ini adalah pendekatan Head Tetap, di mana posisi elemen terdepan selalu terkunci pada indeks nol array. Sebagai konsekuensinya, setiap kali ada data baru yang masuk, variabel Tail akan bergerak maju untuk menunjuk posisi terakhir, dan setiap kali terjadi penghapusan data, seluruh elemen yang tersisa di dalam antrean harus digeser secara manual satu langkah ke depan agar posisi terdepan kembali mengisi indeks nol.

### soal 2. {alternatif 2}

```C++
//queue.h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 5;

struct queue {
    int info[MAX];
    int head;
    int tail;
};

void createQueue(queue &Q);
bool isEmpty(queue Q);
bool isFull(queue Q);
int enqueue(queue &Q, infotype X); 
void dequeue(queue &Q);
void printInfo(queue Q);

#endif

//queue.cpp
#include "queue.h"
#include <iostream>

using namespace std;

bool isEmpty(queue Q){
    if(Q.head == -1 && Q.tail == -1){
        return true;
    } else {
        return false;
    }
}

bool isFull(queue Q){
    if(Q.tail == MAX - 1 ){
        return true;
    } else {
        return false;
    }
}


void createQueue(queue &Q){ 
    Q.head = -1;
    Q.tail = -1;
}

int enqueue(queue &Q, infotype X){
    if(isFull(Q) == true){
        cout << "Queue sudah penuh!" << endl;
    } else {
        if(isEmpty(Q) == true){
            Q.head = Q.tail = 0;
        } else {
            Q.tail++;
        }
        Q.info[Q.tail] = X;
    }
    return 0;
}


void dequeue(queue &Q){
     if(isEmpty(Q) == true){
         cout << "Queue kosong!" << endl;
     } else {
         Q.head++;
         if(Q.head > Q.tail){
             Q.head = -1;
             Q.tail = -1;
         }
     }
 }

void printInfo(queue Q){
      cout << Q.head << " - " << Q.tail << " | ";
    if(isEmpty(Q) == true){
        cout << "Empty Queue";
    } else {
        for(int i = Q.head; i <= Q.tail; i++){
            cout << Q.info[i] << " ";
        }
    }
    cout << endl;
}

//main.cpp
#include "queue.h"
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello World" << endl;
    queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "----------------------" << endl;
    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-8/Output-8-2.png)


Program ini mengimplementasikan struktur data Queue menggunakan media array dengan kapasitas penyimpanan tetap maksimal 5 elemen. Berbeda dengan model statis, program ini menerapkan metode di mana posisi Head dan Tail bersifat dinamis; kedua penanda tersebut akan terus berpindah atau bergeser maju setiap kali terjadi proses penambahan data (enqueue) maupun penghapusan data (dequeue). Dengan pendekatan ini, program tidak perlu menggeser posisi fisik elemen di dalam array saat data terdepan diambil, melainkan cukup memindahkan indeks head ke posisi berikutnya.

### soal 3. {alternatif3}

```C++
//queue.h
#ifndef QUEUE_H
#define QUEUE_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 5;

struct queue {
    int info[MAX];
    int head;
    int tail;
};

void createQueue(queue &Q);
bool isEmpty(queue Q);
bool isFull(queue Q);
int enqueue(queue &Q, infotype X); 
void dequeue(queue &Q);
void printInfo(queue Q);

#endif

//queue.cpp
#include "queue.h"
#include <iostream>

using namespace std;

bool isEmpty(queue Q)
{
    if (Q.head == -1 && Q.tail == -1)
    {
        return true;
    }
    else
    {
        return false;
    }
}

bool isFull(queue Q)
{
    if ((Q.tail + 1) % MAX == Q.head)
    {
        return true;
    }
    else
    {
        return false;
    }
}

void createQueue(queue &Q)
{
    Q.head = -1;
    Q.tail = -1;
}

int enqueue(queue &Q, infotype X)
{
    if (isFull(Q) == true)
    {
        cout << "Queue sudah penuh!" << endl;
    }
    else
    {
        if (isEmpty(Q) == true)
        {
            Q.head = Q.tail = 0;
        }
        else
        {
            Q.tail = (Q.tail + 1) % MAX;
        }
        Q.info[Q.tail] = X;
    }
    return 0;
}

void dequeue(queue &Q)
{
    if (isEmpty(Q) == true)
    {
        cout << "Queue kosong!" << endl;
    }
    else
    {
        if (Q.head == Q.tail)
        {
            Q.head = -1;
            Q.tail = -1;
        }
        else
        {
            Q.head = (Q.head + 1) % MAX;
        }
    }
}

void printInfo(queue Q)
{
    if (isEmpty(Q) == true)
    {
    cout << Q.head << " - " << Q.tail << " | Empty Queue" << endl;
    return;
    }
    else
    {
        cout << Q.head << " - " << Q.tail << " | ";
        int i = Q.head;
        int count = 1;
        while (true)
        {
            cout << Q.info[i] << " ";

            if (i == Q.tail)
                break;

            cout << " ";
            i = (i + 1) % MAX;
        }
        cout << endl;
    }
}

//main.cpp
#include "queue.h"
#include <iostream>

using namespace std;

int main()
{
    cout << "Hello World" << endl;
    queue Q;
    createQueue(Q);

    cout << "----------------------" << endl;
    cout << " H - T \t | Queue info" << endl;
    cout << "----------------------" << endl;
    printInfo(Q);
    enqueue(Q, 5); printInfo(Q);
    enqueue(Q, 2); printInfo(Q);
    enqueue(Q, 7); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);
    enqueue(Q, 4); printInfo(Q);
    dequeue(Q);    printInfo(Q);
    dequeue(Q);    printInfo(Q);

    return 0;
}
```
### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-8/Output-8-3.png)


Program ini mengimplementasikan struktur data Queue (antrean) berbasis array dengan kapasitas statis maksimal 5 elemen, menggunakan pendekatan Circular Queue (Antrean Melingkar). Dalam model ini, posisi Head dan Tail tidak hanya bergerak maju secara linear, tetapi dapat kembali ke titik awal (indeks 0) saat telah mencapai batas akhir array. Mekanisme ini memastikan bahwa ruang memori yang telah dikosongkan oleh proses dequeue di bagian depan dapat digunakan kembali oleh data baru, sehingga penggunaan kapasitas array menjadi jauh lebih optimal dan efisien.


### Kesimpulan
Pembelajaran ini memberikan pemahaman fundamental mengenai Queue (antrean) sebagai struktur data linear yang beroperasi berdasarkan prinsip FIFO (First In, First Out). Mekanisme ini memastikan bahwa elemen yang pertama kali dimasukkan ke dalam sistem akan menjadi elemen yang pertama kali diproses atau dikeluarkan. Karakteristik ini kontras dengan Stack (tumpukan) yang menggunakan prinsip LIFO (Last In, First Out), di mana elemen terakhir yang masuk justru menjadi yang pertama keluar.
