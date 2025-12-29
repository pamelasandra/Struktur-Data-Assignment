# <h1 align="center">Laporan Praktikum Modul 7 - Stack</h1>
<p align="center">Pamela Sandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori
Stack adalah sebuah struktur data linier yang bekerja dengan aturan operasional yang spesifik, di mana proses penambahan maupun penghapusan elemen hanya dapat dilakukan pada satu titik akses saja, yaitu di bagian ujung atau puncak tumpukan. Struktur ini menerapkan prinsip LIFO (Last In, First Out), yang berarti elemen atau objek yang terakhir kali dimasukkan ke dalam tumpukan akan menjadi elemen pertama yang dikeluarkan. Secara sederhana, mekanisme ini menyerupai tumpukan fisik di dunia nyata, di mana akses data terfokus pada elemen paling atas sehingga item yang berada di bawah hanya bisa diambil setelah item di atasnya disingkirkan.

#### A. Materi Minggu pertemuan 7
Pada pertemuan ke-7, mahasiswa diminta untuk mengembangkan sebuah struktur data Stack yang dilengkapi dengan beberapa operasi dasar, yaitu fungsi *push* untuk menambah data dan *pop* untuk menghapus data dari stack.

#### 1. Push
Fungsi ini digunakan untuk memasukkan elemen baru ke dalam stack dengan menempatkannya pada posisi paling atas. Namun, operasi ini tidak dapat dilakukan apabila stack sudah mencapai kapasitas maksimum.

#### 2. Pop
Operasi ini berfungsi untuk menghapus sekaligus mengambil elemen pada posisi teratas stack. Namun, proses tersebut hanya bisa dilakukan jika stack memiliki isi. Apabila stack dalam keadaan kosong, maka akan terjadi kondisi yang disebut underflow.

## Guided 1

### . [stack menggunakan linked list] 

```C++
//stack.h
#ifndef STACK
#define STACK
#define Nil NULL

#include<iostream>
using namespace std;

typedef struct node *address;

struct node{
    int dataAngka;
    address next;
};

struct stack{
    address top;
};

bool isEmpty(stack listStack);
void createStack(stack &listStack);
address alokasi(int angka);
void dealokasi(address &node);

void push(stack &listStack, address nodeBaru);
void pop(stack &listStack);
void update(stack &listStack, int posisi);
void view(stack listStack);
void searchData(stack listStack, int data);

#endif


//stack.cpp
#include "stack.h"
#include <iostream>

//ubah kapasitas sesuai kebutuhan
using namespace std;

bool isEmpty(stack listStack){
    if(listStack.top == Nil){
        return true;
    } else {
        return false;
    }
}

void createStack(stack &listStack){
    listStack.top = Nil;
}

address alokasi(int angka){
    address nodeBaru = new node;
    nodeBaru->dataAngka = angka;
    nodeBaru->next = Nil;
    return nodeBaru;
}

void dealokasi(address &node){
    node->next = Nil;
    delete node;
}

void push(stack &listStack, address nodeBaru){
    nodeBaru->next = listStack.top;
    listStack.top = nodeBaru;
    cout << "Node " << nodeBaru->dataAngka << " berhasil ditambahkan kedalam stack!" << endl;
}

void pop(stack &listStack){
    address nodeHapus;
    if(isEmpty(listStack) == true){
        cout << "Stack kosong!" << endl;
    } else {
        nodeHapus = listStack.top;
        listStack.top = listStack.top->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
        cout << "node " <<  nodeHapus->dataAngka << " berhasil dihapus dari stack!" << endl;
    }
}

void update(stack &listStack, int posisi){
    if(isEmpty(listStack) == true){
        cout << "Stack kosong!" << endl;
    } else {
        if(posisi == 0){
            cout << "Posisi tidak valid!" << endl;
        } else {
            address nodeBantu = listStack.top;
            int count = 1;
            bool found = false;
            while(nodeBantu != Nil){
                if(count < posisi){
                    nodeBantu = nodeBantu->next;
                    count++;
                } else if(count == posisi){
                    cout << "Update node poisisi ke-" << posisi << endl;
                    cout << "Masukkan angka : ";
                    cin >> nodeBantu->dataAngka;
                    cout << "Data berhasil diupdate!" << endl;
                    cout << endl;
                    found = true;
                    break;
                }
            }
            if(found == false){
                cout << "Posisi " << posisi << " tidak valid!" << endl;
            }
        }
    }
}

void view(stack listStack){
    if(isEmpty(listStack) == true){
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = listStack.top;
        while(nodeBantu != Nil){
            cout << nodeBantu->dataAngka << " ";
            nodeBantu = nodeBantu->next;
        }
    }
    cout << endl;
}

void searchData(stack listStack, int data){
    if(isEmpty(listStack) == true){
        cout << "List kosong!" << endl;
    } else {
        address nodeBantu = listStack.top;
        int posisi = 1;
        bool found = false;
        cout << "Mencari data " << data << "..." << endl;
        while(nodeBantu != Nil){
            if(nodeBantu->dataAngka == data){
                cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << endl;
                found = true;
                cout << endl;
                break;
            } else {
                posisi++;
                nodeBantu = nodeBantu->next;
            }
        }
        if(found == false){
            cout << "Data " << data << " tidak ditemukan didalam stack!" << endl;
            cout << endl;
        }
    }
}


//main.cpp
#include "stack.h"
#include <iostream>

using namespace std;

int main(){
    stack listStack;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createStack(listStack);

    nodeA = alokasi(1);
    nodeB = alokasi(2);
    nodeC = alokasi(3);
    nodeD = alokasi(4);
    nodeE = alokasi(5);

    push(listStack, nodeA);
    push(listStack, nodeB);
    push(listStack, nodeC);
    push(listStack, nodeD);
    push(listStack, nodeE);
    cout << endl;

    cout << "--- Stack setelah push ---" << endl;
    view(listStack);
    cout << endl;

    pop(listStack);
    pop(listStack);
    cout << endl;

    cout << "--- Stack setelah pop 2 kali ---" << endl;
    view(listStack);
    cout << endl;

    update(listStack, 2);
    update(listStack, 1);
    update(listStack, 4);
    cout << endl;

    cout << "--- Stack setelah update ---" << endl;
    view(listStack);
    cout << endl;

    searchData(listStack, 4);
    searchData(listStack, 9);

    return 0;
}
   
```
Program ini mengimplementasikan struktur data Stack berbasis Singly Linked List, yang memungkinkan pengelolaan memori dilakukan secara dinamis sesuai dengan jumlah data yang masuk. Dalam operasinya, program menyediakan fungsi push untuk menyisipkan elemen baru di posisi puncak serta fungsi pop untuk mengambil atau menghapus elemen teratas sesuai prinsip LIFO. Selain operasi dasar tersebut, program ini juga memiliki fitur tambahan yang cukup fleksibel, seperti kemampuan untuk mengubah nilai pada posisi tertentu, menampilkan seluruh urutan data dari atas ke bawah, hingga melakukan pencarian data spesifik untuk memverifikasi keberadaan elemen di dalam tumpukan.


## Guided 1

### . [Stack menggunakan fungsi array] 

```C++
//stack.h
#ifndef STACK_TABLE
#define STACK_TABLE

#include <iostream>
using namespace std;

const int MAX = 10;

struct stackTable{
    int data[MAX];
    int top; // -1 = kosong

};

bool isEmpty(stackTable s);
bool isFull(stackTable s);
void createStack(stackTable &s);

void push(stackTable &s, int angka);
void pop(stackTable &s);
void update(stackTable &s, int posisi);
void view(stackTable s);
void searchData(stackTable s, int data);

#endif

//stack.cpp
#include "stack.h"
#include <iostream>

using namespace std;

bool isEmpty(stackTable s) {
    return s.top == -1;
}

bool isFull(stackTable s){
    return s.top == MAX -1;
}

void createStack(stackTable &s) {
    s.top = -1;
}

void push(stackTable &s, int angka){
    if(isFull(s)){
        cout << "Stack Penuh!" << endl;
    } else {
        s.top++;
        s.data[s.top] = angka;
        cout << "Data " << angka << " berhasil ditambahkan kedalam stack!" << endl;
    }
}

void pop(stackTable &s){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
    } else {
        int val = s.data[s.top];
        s.top--;
        cout << "Data " << val << " Berhasil dihapus dari stack!" << endl;
    }
}

void update(stackTable &s, int posisi){
    if(isEmpty(s)){
        cout << "Stack kosong!" << endl;
        return;
    }
    if(posisi <= 0){
        cout << "Posisi tidak valid!" << endl;
        return;
    }

    //index = top - (posisi -1)
    int idx = s.top - (posisi -1);
    if(idx < 0 || idx > s.top){
        cout << "Posisi " << posisi << " Tidak valid!" << endl;
        return;
    }

    cout << "Update data posisi ke-" << posisi << endl;
    cout << "Masukkan angka: ";
    cin >> s.data[idx];
    cout << "Data berhasil diupdate!" << endl;
    cout << endl;
}

void view(stackTable s){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
    } else {
        for(int i = s.top; i >= 0; --i){
            cout << s.data[i] << " ";
        }
    }
    cout << endl;
}

void searchData(stackTable s, int data){
    if(isEmpty(s)){
        cout << "Stack Kosong!" << endl;
        return;
    }
    cout << "Mencari data" << data << "..." << endl;
    int posisi = 1;
    bool found = false;

    for(int i = s.top; i >= 0; --i){
        if(s.data[i] == data){
            cout << "Data " << data << " ditemukan pada posisi ke-" << posisi << endl;
            cout << endl;
            found = true;
            break;
        }
        posisi++;
    }

    if(!found){
        cout << "Data " << data << " tidak ditemukan didalam stack!" << endl;
        cout << endl;
    }
}

//main.cpp
#include "stack.h"
#include <iostream>

using namespace std;

int main(){
    stackTable s;
    createStack(s);

    push(s, 1);
    push(s, 2);
    push(s, 3);
    push(s, 4);
    push(s, 5);
    cout << endl;

    cout << "--- Stack setelah push ---" << endl;
    view(s);
    cout << endl;

    pop(s);
    pop(s);
    cout << endl;

    cout << "--- Stack setelah pop 2 kali ---" << endl;
    view(s);
    cout << endl;

    //Posisi dihitung dari TOP(1-based)
    update(s, 2);
    update(s, 1);
    update(s, 4);
    cout << endl;

    cout << "--- Stack setelah update ---" << endl;
    view(s);
    cout << endl;

    searchData(s, 4);
    searchData(s, 9);

    return 0;
}

```
Program ini mengelola tumpukan data dengan Stack berbasis Array yang memiliki batas kapasitas hingga 10 entri. Sistem kontrol tumpukan ini mengandalkan variabel top sebagai penanda indeks terakhir; posisi -1 digunakan untuk mengidentifikasi bahwa tumpukan sedang dalam keadaan kosong. Untuk menjaga validitas operasi, program menyertakan fungsi isEmpty dan isFull guna memantau ketersediaan ruang sebelum data ditambah via push atau diambil via pop. Di samping fungsi standar tersebut, aplikasi ini menawarkan fleksibilitas lebih melalui fitur pengeditan data, pencarian elemen spesifik, serta fungsi pemindaian untuk menampilkan seluruh isi tumpukan mulai dari elemen paling atas hingga dasar.

## Unguided

## Soal 1

```C++
//stack.h
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 20;

struct Stack{
    int data[MAX];
    int top;

};

void createStack(Stack &S);
void push(Stack &S, infotype x);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);

#endif


//stack.cpp
#include "stack.h"
#include <iostream>

using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype X) {
    if(S.top == MAX - 1){
        cout << "Stack Penuh!" << endl;
    } else {
        S.top++;
        S.data[S.top] = X;
    }
}

infotype pop(Stack &S) {
    if(S.top == - 1){
        cout << "Stack kosong!" << endl;
        return -1;
    } else {
        int val = S.data[S.top];
        S.top--;
        return val;
    }
}

void printInfo(Stack S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        cout << "[TOP] " ;
        for(int i = S.top; i >= 0; --i){
            cout << S.data[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        if (S.top <= 0) return;
    }

    int i = 0;
    int j = S.top;

    while (i < j) {
        int temp = S.data[i];
        S.data[i] = S.data[j];
        S.data[j] = temp;
        i++;
        j--; 
    }
}


//main.cpp
#include "stack.h"
#include <iostream>
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);

    push(S, 3);
    push(S, 4);
    push(S, 8);
    pop(S);
    push(S, 2);
    push(S, 3);
    pop(S);
    push(S, 9);

    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);

    return 0;
}

```
### Output soal 1 :
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-7/Output-7-1.png)

Program ini mengimplementasikan konsep Stack dengan menggunakan Array sebagai media penyimpanannya. Melalui mekanisme tumpukan, data ditambahkan ke posisi teratas menggunakan fungsi push dan dikeluarkan melalui fungsi pop. Dalam skenario yang dijelaskan, operasi pop dijalankan dua kali untuk membuang nilai terakhir yang dimasukkan (angka 3 dan 8), sehingga dari total enam data yang masuk, kini hanya tersisa empat elemen. Terakhir, program menggunakan fungsi balikstack untuk memproses urutan data dan menampilkannya ke layar melalui prosedur printInfo.

### soal 2. 


```C++
//stack.h
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 20;

struct Stack{
    int data[MAX];
    int top;

};

void createStack(Stack &S);
void push(Stack &S, infotype X);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, int X);

#endif


//stack.cpp
#include "stack.h"
#include <iostream>

using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype X) {
    if(S.top == MAX - 1){
        cout << "Stack Penuh!" << endl;
    } else {
        S.top++;
        S.data[S.top] = X;
    }
}

infotype pop(Stack &S) {
    if(S.top == - 1){
        cout << "Stack kosong!" << endl;
        return -1;
    } else {
        int val = S.data[S.top];
        S.top--;
        return val;
    }
}

void printInfo(Stack S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        cout << "[TOP] " ;
        for(int i = S.top; i >= 0; --i){
            cout << S.data[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        if (S.top <= 0) return;
    }

    int i = 0;
    int j = S.top;

    while (i < j) {
        int temp = S.data[i];
        S.data[i] = S.data[j];
        S.data[j] = temp;
        i++;
        j--; 
    }
}
void pushAscending(Stack &S, int X) {
    Stack temp;
    createStack(temp);

    while (S.top != -1 && S.data[S.top] > X) {
        int val = pop(S);
        push(temp, val);
    }

    push(S, X);

    while (temp.top != -1) {
        push(S, pop(temp));
    }
}


//main.cpp
#include <iostream>
#include "stack.h"
using namespace std;

int main() {
    cout << "Hello world!" << endl;

    Stack S;
    createStack(S);
    pushAscending(S,3);
    pushAscending(S,4);
    pushAscending(S,8);
    pushAscending(S,2);
    pushAscending(S,3);
    pushAscending(S,9);
    printInfo(S);

    cout << "balik stack" << endl;
    balikStack(S);
    
    printInfo(S);
    return 0;
}

```
### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-7/Output-7-2.png)

Program ini mengimplementasikan struktur data Stack berbasis array dengan modifikasi khusus pada proses penyisipan datanya. Alih-alih memasukkan data secara biasa, program menggunakan fungsi pushAscending yang secara otomatis mengurutkan elemen dari nilai terkecil hingga terbesar pada saat ditambahkan ke dalam tumpukan. Setelah urutan tersebut ditampilkan melalui printInfo, program memanfaatkan fungsi balikStack untuk memutar balik seluruh urutan data yang ada. Hasil akhir dari proses pembalikan ini kemudian dicetak kembali menggunakan printInfo, sehingga pengguna dapat melihat data baik dalam kondisi terurut menaik maupun urutan sebaliknya.

### soal 3.

```C++
//stack.h
#ifndef STACK_H
#define STACK_H

#include <iostream>
using namespace std;

typedef int infotype;

const int MAX = 20;

struct Stack{
    int data[MAX];
    int top;

};

void createStack(Stack &S);
void push(Stack &S, infotype X);
infotype pop(Stack &S);
void printInfo(Stack S);
void balikStack(Stack &S);
void pushAscending(Stack &S, int X);
void getInputStream(Stack &S);

#endif


//stack.cpp
#include "stack.h"
#include <iostream>

using namespace std;

void createStack(Stack &S) {
    S.top = -1;
}

void push(Stack &S, infotype X) {
    if(S.top == MAX - 1){
        cout << "Stack Penuh!" << endl;
    } else {
        S.top++;
        S.data[S.top] = X;
    }
}

infotype pop(Stack &S) {
    if(S.top == - 1){
        cout << "Stack kosong!" << endl;
        return -1;
    } else {
        int val = S.data[S.top];
        S.top--;
        return val;
    }
}

void printInfo(Stack S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        cout << "[TOP] " ;
        for(int i = S.top; i >= 0; --i){
            cout << S.data[i] << " ";
        }
    }
    cout << endl;
}

void balikStack(Stack &S) {
    if(S.top == - 1){
        cout << "Stack Kosong!" << endl;
    } else {
        if (S.top <= 0) return;
    }

    int i = 0;
    int j = S.top;

    while (i < j) {
        int temp = S.data[i];
        S.data[i] = S.data[j];
        S.data[j] = temp;
        i++;
        j--; 
    }
}
void pushAscending(Stack &S, int X) {
    Stack temp;
    createStack(temp);

    while (S.top != -1 && S.data[S.top] > X) {
        int val = pop(S);
        push(temp, val);
    }

    push(S, X);

    while (temp.top != -1) {
        push(S, pop(temp));
    }
}

void getInputStream(Stack &S) {
    createStack(S);

    char n;
    while(true){
        n = cin.get();
        if(n == '\n') {
            break;
        }
        if(n >= '0' && n <= '9' ) {
            int val = n - '0';
            push(S, val);
        }
    }
}


//main.cpp
#include "stack.h"
#include <iostream>
using namespace std;

int main() {
    cout << "Hello world!" << endl;
    Stack S;
    createStack(S);
    getInputStream(S);
    printInfo(S);
    cout << "balik stack" << endl;
    balikStack(S);
    printInfo(S);
    return 0;
}

```
### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-7/Output-7-3.png)


Program ini mengimplementasikan struktur data Stack berbasis array dengan mekanisme input yang lebih interaktif, di mana pengguna dapat memasukkan sejumlah data secara berurutan hingga prosesnya dihentikan dengan menekan tombol Enter. Perbedaan utama pada versi ini adalah tidak digunakannya fungsi push konvensional; sebagai gantinya, program memanfaatkan fungsi getInputStream untuk menangkap aliran data secara terus-menerus hingga kapasitas array mencapai batas maksimal. Setelah seluruh data tersimpan, program menjalankan fungsi balikStack untuk memutar balik urutan elemen di dalam tumpukan, lalu menggunakan prosedur printInfo untuk menampilkan hasil akhir tersebut ke layar.

### Kesimpulan
Pembelajaran ini memberikan pemahaman mendalam mengenai struktur data Stack yang telah dimodifikasi dengan berbagai fitur fungsional. Mahasiswa mempelajari penggunaan fungsi pushAscending, sebuah metode penyisipan data yang secara otomatis mengurutkan elemen sehingga nilai terbesar berada di posisi puncak (top) dan nilai terkecil berada di dasar tumpukan. Selain itu, program ini menawarkan fleksibilitas input bagi pengguna melalui fungsi getStreamInput, yang memungkinkan pengisian data secara manual hingga mencapai kapasitas maksimal sebanyak 20 elemen. Untuk melengkapi fungsionalitasnya, tersedia pula fitur balikStack yang bertugas memutar balik urutan data di dalam tumpukan, di mana seluruh hasil pemrosesan akhirnya ditampilkan secara sistematis melalui prosedur printInfo.


## Referensi
[1] Stack in C++ STL. https://www.geeksforgeeks.org/cpp/stack-in-cpp-stl/
[2] stack::push() and stack::pop() in C++ STL. https://www.geeksforgeeks.org/cpp/stack-push-and-pop-in-c-stl/
