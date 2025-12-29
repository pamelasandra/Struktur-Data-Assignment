# <h1 align="center">Laporan Praktikum Modul 4 Singly Linked List(1)</h1>
<p align="center">Pamela Sandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori

SLL merupakan alternatif dari array yang lebih dinamis dalam mengelola memori. Jika array menggunakan blok memori yang berurutan, SLL menghubungkan node-node yang tersebar melalui sistem rantai pointer searah. Setiap node membawa data sekaligus "alamat" untuk menuju elemen berikutnya, yang berakhir ketika pointer menunjuk ke nilai kosong (NULL).

Kemudahan SLL terletak pada manipulasinya; kita bisa dengan mudah menambah atau menghapus node di posisi mana pun (awal, tengah, atau akhir) hanya dengan mengubah arah pointer. Selain itu, SLL lebih efisien dalam penggunaan ruang karena kapasitasnya menyesuaikan jumlah data yang ada secara real-time.

### Guided 

### 1. Linked List 1
#### mainguided1.cpp
```C++
#include "list.h"

#include<iostream>
using namespace std;

int main(){
    linkedlist List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "2211110014", 21);
    nodeC = alokasi("Rizal", "2311110029", 20);
    nodeD = alokasi("Satrio", "2211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);

    return 0;
}
```
#### listguided1.cpp
```C++
#include "list1.h"
#include <iostream>
using namespace std;


bool isEmpty(linkedlist List) {
    if(List.first == Nil){
        return true; 
    } else {
        return false;
    }
}

void createList(linkedlist &List) {
    
    List.first = Nil;
}

address alokasi(string nama, string nim, int umur) { 
    
    address nodeBaru = new node; 
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim; 
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

void dealokasi(address &node) {
    
    node->next = Nil;
    delete node;
}

void insertFirst(linkedlist &List, address nodeBaru) {
    
    nodeBaru->next = List.first; 
    List.first = nodeBaru;
}

void insertAfter(linkedlist &List, address nodeBaru, address Prev) {
    
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(linkedlist &List, address nodeBaru) {
    
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

void printList(linkedlist List) {
    
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) { 
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim 
            << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}
```
#### list1.h
```C++

#ifndef LIST_H
#define LIST_H
#define Nil NULL

#include <iostream>
using namespace std;

struct mahasiswa{
    string nama;
    string nim;
    int umur;
};

typedef mahasiswa dataMahasiswa; 

typedef struct node *address; 

struct node{
    dataMahasiswa isidata;
    address next;
};

struct linkedlist{ 
    address first;
};

bool isEmpty(linkedlist List);
void createList(linkedlist &List);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedlist List);
void insertFirst(linkedlist &List, address nodeBaru);
void insertAfter(linkedlist &List, address nodeBaru, address Prev);
void insertLast(linkedlist &List, address nodeBaru);

#endif
```
Implementasi Singly Linked List untuk data mahasiswa ini terorganisir dalam tiga file yang saling terintegrasi. list1.h berperan sebagai cetak biru yang menetapkan struktur data serta prototipe fungsi. Logika operasional dari fungsi-fungsi tersebut, seperti manajemen memori dan manipulasi node, dijabarkan secara detail di dalam listguided1.cpp. Terakhir, mainguided1.cpp berfungsi sebagai pusat kendali yang menjalankan seluruh fungsi tersebut untuk menginisialisasi, mengisi, dan memverifikasi data pada linked list melalui tampilan program.
    
## Unguided 

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h”
```C++
Type infotype : int
Type address : pointer to ElmList
Type ElmList <
    info : infotype
    next : address
>
Type List : < First : address >
procedure CreateList( input/output L : List )
function alokasi( x : infotype ) -> address
procedure dealokasi( input/output P : address )
procedure printInfo( input L : List )
procedure insertFirst( input/output L : List, input P : address )
```
### Kemudian buatlah implementasi dari procedure-procedure yang digunakan didalam file “Singlylist.cpp”. Kemudian buat program utama didalam file “main.cpp” dengan implementasi sebagai berikut :
```C++
int main() {
    List L;
    address P1, P2, P3, P4, P5 = Nil;

    createList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);
    
    return 0;
}
```
### KODE PROGRAM
#### main.cpp
```C++
// File: main.cpp

#include "ungu1singlist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5 = NULL;

    createList(&L);

    P1 = alokasi(2);
    insertFirst(&L, P1);

    P2 = alokasi(0);
    insertFirst(&L, P2);

    P3 = alokasi(8);
    insertFirst(&L, P3);

    P4 = alokasi(12);
    insertFirst(&L, P4);

    P5 = alokasi(9);
    insertFirst(&L, P5);

    printInfo(L);

    // Bagian tambahan untuk membersihkan memori (dealokasi semua elemen)
    address current = L.First;
    address temp;
    while (current != NULL) {
        temp = current;
        current = current->next;
        dealokasi(temp);
    }
    L.First = NULL;

    return 0;
}
```
#### list.cpp
```C++
// File: Singlylist.h

#ifndef SINGLYLIST_H
#define SINGLYLIST_H

typedef int infotype;
typedef struct ElmList *address;

typedef struct ElmList {
    infotype info;
    address next;
} ElmList;

typedef struct {
    address First;
} List;

void createList(List *L);
address alokasi(infotype X);
void dealokasi(address P);

void insertFirst(List *L, address P);
void printInfo(List L);

#endif // SINGLYLIST_H
```
#### singlylist.h
```C++
// File: Singlylist.h

#ifndef SINGLYLIST_H
#define SINGLYLIST_H

typedef int infotype;
typedef struct ElmList *address;

typedef struct ElmList {
    infotype info;
    address next;
} ElmList;

typedef struct {
    address First;
} List;

void createList(List *L);
address alokasi(infotype X);
void dealokasi(address P);

void insertFirst(List *L, address P);
void printInfo(List L);

#endif // SINGLYLIST_H
```
#### Output 1
![Screenshot Output 1](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-4/Output-4-1.png)


Program ini membagi tugas ke dalam tiga bagian utama untuk membangun sebuah linked list. Bagian pertama adalah unguided1list.h yang berfungsi sebagai cetak biru atau kerangka dasar. Bagian kedua, unguided1list.cpp, adalah tempat di mana semua instruksi teknis dan manipulasi data benar-benar dituliskan. Terakhir, program utama di unguided1main.cpp bertugas mencoba hasil pengkodean tersebut; ia memasukkan lima data angka secara berurutan dan menampilkannya ke layar guna memastikan logika penyisipan data sudah tepat.

### 2. Dari soal Latihan pertama, lakukan penghapusan node 9 menggunakan deleteFirst(), node 2 menggunakan deleteLast(), dan node 8 menggunakan deleteAfter(). Kemudian tampilkan jumlah node yang tersimpan menggunakan nbList() dan lakukan penghapusan seluruh node menggunakan deleteList().

#### main.cpp
```C++
// File: unguided1main.cpp

#include "ungu2singlist.h"
#include <iostream>

using namespace std;

int main() {
    List L;
    address P1, P2, P3, P4, P5;

    createList(&L);

    P1 = alokasi(2); insertFirst(&L, P1);
    P2 = alokasi(0); insertFirst(&L, P2);
    P3 = alokasi(8); insertFirst(&L, P3);
    P4 = alokasi(12); insertFirst(&L, P4);
    P5 = alokasi(9); insertFirst(&L, P5);

    cout << "List Awal (untuk verifikasi): ";
    printInfo(L);
    cout << endl << endl;

    address P_del;
    
    deleteFirst(&L, &P_del);
    dealokasi(P_del);
    
    deleteLast(&L, &P_del); 
    dealokasi(P_del);
    
    address Prec = search(L, 12); 

    if (Prec != NULL && Prec->next != NULL && Prec->next->info == 8) {
        deleteAfter(&L, &P_del, Prec);
        dealokasi(P_del);
    }

    printInfo(L);
    cout << endl; 
    
    cout << "Jumlah node : " << nbList(L) << endl; 

    deleteList(&L);
    cout << endl << "- List Berhasil Terhapus -" << endl;

    cout << "Jumlah node : " << nbList(L) << endl; 

    return 0;
}
```
#### list.cpp
```C++
// File: unguided1list.cpp

#include "ungu2singlist.h"
#include <iostream>

using namespace std;

void createList(List *L) {
    (*L).First = NULL;
}

address alokasi(infotype X) {
    address P = new ElmList;
    if (P != NULL) {
        P->info = X;
        P->next = NULL;
    }
    return P;
}

void dealokasi(address P) {
    delete P;
}

void insertFirst(List *L, address P) {
    if (P != NULL) {
        P->next = (*L).First;
        (*L).First = P;
    }
}

void printInfo(List L) {
    address P = L.First;
    if (P == NULL) return; 

    while (P != NULL) {
        cout << P->info << " ";
        P = P->next;
    }
}

address search(List L, infotype X) {
    address P = L.First;
    while (P != NULL) {
        if (P->info == X) {
            return P;
        }
        P = P->next;
    }
    return NULL;
}

int nbList(List L) {
    int count = 0;
    address P = L.First;
    while (P != NULL) {
        count++;
        P = P->next;
    }
    return count;
}

void deleteFirst(List *L, address *P) {
    *P = (*L).First;
    if (*P != NULL) {
        (*L).First = (*L).First->next;
        (*P)->next = NULL; 
    }
}

void deleteLast(List *L, address *P) {
    address Last = (*L).First;
    address Prec = NULL;
    
    if (Last != NULL && Last->next == NULL) {
        *P = Last;
        (*L).First = NULL;
        return;
    }

    while (Last != NULL && Last->next != NULL) {
        Prec = Last;
        Last = Last->next;
    }

    if (Last != NULL) {
        *P = Last;
        Prec->next = NULL;
    }
}

void deleteAfter(List *L, address *Pdel, address Prec) {
    if (Prec != NULL && Prec->next != NULL) {
        *Pdel = Prec->next;
        Prec->next = (*Pdel)->next;
        (*Pdel)->next = NULL;
    } else {
        *Pdel = NULL;
    }
}

void deleteList(List *L) {
    address P;
    while ((*L).First != NULL) {
        deleteFirst(L, &P);
        dealokasi(P);
    }
}
```
#### singlylist.h
```C++
// File: unguided1list.h

#ifndef UNGUIDED1LIST_H
#define UNGUIDED1LIST_H

typedef int infotype;
typedef struct ElmList *address;

typedef struct ElmList {
    infotype info;
    address next;
} ElmList;

typedef struct {
    address First;
} List;

void createList(List *L);
address alokasi(infotype X);
void dealokasi(address P);

void insertFirst(List *L, address P);
void printInfo(List L);

int nbList(List L);
address search(List L, infotype X); 
void deleteFirst(List *L, address *P);
void deleteLast(List *L, address *P);
void deleteAfter(List *L, address *Pdel, address Prec);
void deleteList(List *L);

#endif // UNGUIDED1LIST_H
```

#### Output 2
![Screenshot Output 2](https://github.com/kyyyyraapamelasandra/Struktur-Data-Assigment/blob/main/Modul-4/Output-4-2.jpg)

Ketiga berkas ini secara kolektif membangun sistem manajemen data linear dalam C++. ungu2singlist.h mendefinisikan struktur ElmList dan prototipe operasinya, sementara ungu2list.cpp menangani detail teknis manipulasi pointer dan memori, termasuk fitur penghapusan elemen yang sangat lengkap. Skenario pengujian dijalankan pada ungu2main.cpp, di mana list L diisi secara terbalik melalui insertFirst, lalu dimodifikasi dengan menghapus elemen di awal, akhir, dan tengah (menghapus angka 8) sebelum akhirnya list dibubarkan sepenuhnya menggunakan deleteList.



## Kesimpulan
Praktikum ini telah berhasil merealisasikan struktur data singly linked list menggunakan bahasa C++ dengan fitur manipulasi yang lengkap. Implementasi mencakup pembuatan struktur node, pengelolaan memori dinamis, hingga berbagai teknik penyisipan dan penghapusan elemen. Melalui skenario pengujian, list awal yang berisi rangkaian angka 9, 12, 8, 0, 2 berhasil dimodifikasi secara sistematis hingga menyisakan elemen 12 dan 0. Hasil ini mempertegas konsep penting mengenai peran pointer dalam menghubungkan data secara non-sekuensial serta perbedaan efisiensi waktu operasi di berbagai posisi list. Selain itu, ditekankan pula pentingnya manajemen memori eksplisit demi menjaga stabilitas program dari risiko memory leak.

