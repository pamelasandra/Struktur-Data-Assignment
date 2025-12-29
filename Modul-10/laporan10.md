# <h1 align="center">Laporan Praktikum Modul 10 - tree(bagian pertama)</h1>
<p align="center">Pamela Sandra Amelia Br Ginting - 103112430152</p>

## Dasar Teori
Tree secara matematis didefinisikan sebagai tipe khusus dari graph tak berarah yang saling terhubung, namun tidak memiliki sirkuit (lintasan tertutup). Berbeda dengan struktur data linear yang elemennya berurutan secara sekuensial, Tree mengorganisir data secara hierarkis.

Karakteristik Utama Tree (T)
Suatu struktur data dapat dikategorikan sebagai Tree jika memenuhi kriteria berikut:
1. Empty Tree: T bisa berada dalam keadaan kosong (tidak memiliki node sama sekali).
2. Akar (Root): Hanya terdapat tepat satu node yang tidak memiliki pendahulu (predecessor). Node ini berada di puncak hierarki dan menjadi titik awal akses seluruh data.
3. Satu Pendahulu: Setiap node lainnya (selain root) hanya diizinkan memiliki tepat satu node pendahulu. Ini menjamin bahwa struktur data  tetap bercabang secara hierarkis dan tidak membentuk siklus atau hubungan yang membingungkan.

#### A. Materi modul 10
Pada pertemuan ini, kita akan membahas fungsi fungsi pada struktur tree pada BST (Binary Search Tree).

#### 1. Insert
Jika node yang akan di-insert lebih kecil, maka di-insert pada Left Subtree
Jika lebih besar, maka di-insert pada Right Subtree.

#### 2. Search
Proses pencarian elemen pada binary tree dapat menggunakan algoritma rekursif binary search.
Berikut adalah algoritma binary search :
1. Pencarian pada binary search tree dilakukan dengan menaruh pointer dan membandingkan nilai
yang dicari dengan node awal ( root )
2. Jika nilai yang dicari tidak sama dengan node, maka pointer akan diganti ke child dari node yang
ditunjuk:
a. Pointer akan pindah ke child kiri bila, nilai dicari lebih kecil dari nilai node yang ditunjuk saat
itu
b. Pointer akan pindah ke child kanan bila, nilai dicari lebih besar dari nilai node yang ditunjuk
saat itu
3. Nilai node saat itu akan dibandingkan lagi dengan nilai yang dicari dan apabila belum ditemukan,
maka perulangan akan kembali ke tahap 2
4. Pencarian akan berhenti saat nilai yang dicari ketemu, atau pointer menunjukan nilai NULL

#### 3. Delete
LEAF, tidak perlu dilakukan modifikasi.
2. Node dengan 1 Child, maka child langsung menggantikan posisi Parent.
3. Node dengan 2 Child:
- Left Subtree, yang diambil adalah node yang paling kiri (nilai terbesar).
- Right Subtree, yang diambil adalah node yang paling kanan (nilai terkecil).

#### 4. Most Left
Most-left node adalah node yang berada paling kiri dalam tree. Dalam konteks binary search tree
(BST), most-left node adalah node dengan nilai terkecil, yang dapat ditemukan dengan mengikuti
anak kiri (left child) dari root hingga mencapai node yang tidak memiliki anak kiri lagi.

#### 5. Most right
Most-right node adalah node yang berada paling kanan dalam tree. Dalam konteks binary search
tree (BST), most-right node adalah node dengan nilai terbesar, yang dapat ditemukan dengan
mengikuti anak kanan (right child) dari root hingga mencapai node yang tidak memiliki anak kanan
lagi.

#### 6. Pre-Order
Proses Traverse yang melakukan tahapan cetak node yang dikunjungi, kunjungi left node , kunjungi right node.

#### 7. In-Order
Proses Traverse yang melakukan tahapan kunjungi left node, cetak node yang dikunjungi, kunjungi right node.

#### 8. Post-Order
Proses Traverse yang melakukan tahapan kunjungi left node, kunjungi right node, cetak node yang dikunjungi


## Guided 1

### . [Binary Searh Tree] 

```C++
//bst.h
#ifndef BST_H
#define BST_H
#define Nil NULL

using namespace std;

typedef struct BST *node; //alias pointer = node

struct BST{ //nama struct BST
    int angka;
    node left;
    node right;
};

typedef node BinTree; //alias tree = BinTree (merujuk ke node root dari BST)

bool isEmpty(BinTree tree);
void createTree(BinTree &tree);
node alokasi(int angka);
void dealokasi(node nodeHapus);

void insertNode(BinTree &tree, node nodeBaru);
void searchByData(BinTree tree, int angka);
void preOrder(BinTree tree);
void inOrder(BinTree tree);
void postOrder(BinTree tree);

bool deleteNode(BinTree &tree, int angka);
node mostRight(BinTree tree);
node mostLeft(BinTree tree);
void deleteTree(BinTree &tree);
int size(BinTree tree);
int height(BinTree tree);

#endif

//bst.cpp
#include "bst.h"
#include <iostream>

using namespace std;

//NOTE : parameter tree disini maksudnya merujuk ke node; baik itu node root atau node lain dari tree

bool isEmpty(BinTree tree){
    if(tree == Nil){
        return true;
    } else {
        return false;
    }
}

void createTree(BinTree &tree){
    tree = Nil;
}

node alokasi(int angkaInput){
    node nodeBaru = new BST;
    nodeBaru->angka = angkaInput;
    nodeBaru->left = Nil;
    nodeBaru->right = Nil;
    return nodeBaru;
}

void dealokasi(node nodeHapus){
    delete nodeHapus;
}

void insertNode(BinTree &tree, node nodeBaru){
    if(tree == Nil){
        tree = nodeBaru;
        cout << "Node " << nodeBaru->angka << " berhasil ditambahkan ke dalam tree!" << endl;
        return;
    } else if(nodeBaru->angka < tree->angka){
        insertNode(tree->left, nodeBaru);
    } else if(nodeBaru->angka > tree->angka){
        insertNode(tree->right, nodeBaru);
    }
}

void searchByData(BinTree tree, int angkaCari){
    if(isEmpty(tree) == true){
        cout << "Tree kosong!" << endl;
    } else {
        node nodeBantu = tree;
        node parent = Nil;
        bool ketemu = false;
        while(nodeBantu != Nil){
            if(angkaCari < nodeBantu->angka){
                parent = nodeBantu;
                nodeBantu = nodeBantu->left;
            } else if(angkaCari > nodeBantu->angka){
                parent = nodeBantu;
                nodeBantu = nodeBantu->right;
            } else if(angkaCari == nodeBantu->angka){
                ketemu = true;
                break;
            }
        }
        if(ketemu == false){
            cout << "Data tidak ditemukan" << endl;
        } else if(ketemu == true){
            cout << "Data ditemukan didalam tree!" << endl;
            cout << "Data Angka : " << nodeBantu->angka << endl;

            //menampilkan parentnya & pengecekan sibling
            node sibling = Nil;
            if(parent != Nil){
                cout << "Parent : " << parent->angka << endl;
                if(parent->left == nodeBantu){
                    sibling = parent->right;
                } else if(parent->right == nodeBantu){
                    sibling = parent->left;
                }
            } else {
                cout << "Parent : - (node root)"<< endl;
            }

            //menampilkan siblingnya
            if(sibling != Nil){
                cout << "Sibling : " << sibling->angka << endl;
            } else {
                cout << "Sibling : - " << endl;
            }

            //menampilkan childnya
            if(nodeBantu->left != Nil){
                cout << "Child kiri : " << nodeBantu->left->angka << endl;
            } else if(nodeBantu->left == Nil){
                cout << "Child kiri : -" << endl;
            }
            if(nodeBantu->right != Nil){
                cout << "Child kanan : " << nodeBantu->right->angka << endl;
            } else if(nodeBantu->right == Nil){
                cout << "Child kanan : -" << endl;
            }
        }
    }
}

void preOrder(BinTree tree){ //tengah - kiri - kanan atau root - child kiri - child kanan
    if(tree == Nil){
        return;
    }
    cout << tree->angka << " - ";
    preOrder(tree->left);
    preOrder(tree->right);
}

void inOrder(BinTree tree){ //kiri - tengah - kanan atau child kiri - root - child kanan
    if(tree == Nil){
        return;
    }
    inOrder(tree->left);
    cout << tree->angka << " - ";
    inOrder(tree->right);
}

void postOrder(BinTree tree){ //kiri - kanan - tengah atau child kiri - child kanan - root
    if(tree == Nil){
        return;
    }
    postOrder(tree->left);
    postOrder(tree->right);
    cout << tree->angka << " - ";
}



bool deleteNode(BinTree &tree, int angka) {
    if (tree == Nil) {
        return false; //data tidak ditemukan di subtree ini
    } else {
        if (angka < tree->angka) {
            return deleteNode(tree->left, angka);
        } else if (angka > tree->angka) {
            return deleteNode(tree->right, angka);
        } else {
            //jika node yang mau dihapus ditemukan
            //Case 1 : node yang mau dihapus adalah leaf
            if (tree->left == Nil && tree->right == Nil) {
                node tmp = tree;
                tree = Nil;
                dealokasi(tmp);
            }
            //Case 2 : node yang mau dihapus hanya punya right child
            else if (tree->left == Nil) {
                node tmp = tree;
                tree = tree->right;
                dealokasi(tmp);
            }
            //Case 3 : node yang mau dihapus hanya punya left child
            else if (tree->right == Nil) {
                node tmp = tree;
                tree = tree->left;
                dealokasi(tmp);
            }
            // Case 4 : jika node yang mau dihapus punya dua child, maka ambil mostleft dari subtree kanan untuk menggantikan node yang mau dihapus
            else {
                //mostleft dari subtree kanan = node successor (node penerus)
                node successor = mostLeft(tree->right);
                //salin data successor ke node saat ini
                tree->angka = successor->angka;
                //hapus successor pada subtree kanan
                return deleteNode(tree->right, successor->angka);
            }
            return true; //berhasil dihapus
        }
    }
}

node mostRight(BinTree tree){
    while (tree->right != Nil){
        tree = tree->right;
    }
    return tree;    
}

node mostLeft(BinTree tree){
    while (tree->left != Nil){
        tree = tree->left;
    }
    return tree;
}

void deleteTree(BinTree &tree){
    if(tree == Nil){
        return;
    } else {
        deleteTree(tree->left);
        deleteTree(tree->right);
        dealokasi(tree);
        tree = Nil;
    }
}

int size(BinTree tree){ //mengembalikan jumlah semua node
    if(isEmpty(tree) == true){
        return 0;
    } else {
        return 1 + size(tree->left) + size(tree->right);
    }
    cout << endl;
}

int height(BinTree tree){ //mengembalikan jumlah level tree
    if(isEmpty(tree) == true){
        return -1; //tree kosong jika height = -1
    } else {
        int hl = height(tree->left);
        int hr = height(tree->right);
        int maxHeight;
        if (hl > hr){
            maxHeight = hl;
        } else {
            maxHeight = hr;
        }
        return 1 + maxHeight;
    }
    cout << endl;
}
//main.cpp
#include <iostream>
#include "bst.h"
#include "bst.cpp"

using namespace std;

int main() {
    BinTree tree;
    createTree(tree);

    int pilih, angka;

    do {
        cout << "========= MENU BST =========" << endl;
        cout << "1. Insert Node" << endl;
        cout << "2. Delete Node" << endl;
        cout << "3. Search Data" << endl;
        cout << "4. Tampilkan PreOrder" << endl;
        cout << "5. Tampilkan InOrder" << endl;
        cout << "6. Tampilkan PostOrder" << endl;
        cout << "7. Size Tree (jumlah node)" << endl;
        cout << "8. Height Tree (tinggi level)" << endl;
        cout << "9. Tampilkan mostright" << endl;
        cout << "10. Tampilkan mostleft" << endl;
        cout << "11. Delete Seluruh Tree" << endl;
        cout << "0. Keluar" << endl;
        cout << "pilihan anda : ";
        cin >> pilih;
        cout << endl;

        switch (pilih){
        case 1:
            cout << "Masukkan angka: ";
            cin >> angka;
            insertNode(tree, alokasi(angka));
            cout << endl;
            break;

        case 2:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "Masukkan angka yang ingin dihapus: ";
                cin >> angka;
                if(deleteNode(tree, angka)){
                    cout << "Data " << angka << " berhasil dihapus!" << endl;
                } else {
                    cout << "Data " << angka << " tidak ditemukan!" << endl;
                }
            }
            cout << endl;
            break;

        case 3:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "Masukkan angka yang ingin dicari: ";
                cin >> angka;
                searchByData(tree, angka);
            }
            cout << endl;
            break;

        case 4:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "PreOrder : ";
                preOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 5:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "InOrder : ";
                inOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 6:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                cout << "PostOrder : ";
                postOrder(tree);
                cout << endl;
            }
            cout << endl;
            break;

        case 7:
            cout << "Size Tree = " << size(tree) << endl;
            cout << endl;
            break;

        case 8:
            cout << "Height Tree = " << height(tree) << endl;
            cout << endl;
            break;

        case 9: 
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
                cout << endl;
            } else {
                cout << "Mostright : " << mostRight(tree)->angka << endl;
                cout << endl;
            }
            break;
        
        case 10:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
                cout << endl;
            } else {
                cout << "Mostleft : " << mostLeft(tree)->angka << endl;
                cout << endl;
            }
            break;

        case 11:
            if(isEmpty(tree) == true){
                cout << "Tree kosong!" << endl;
            } else {
                deleteTree(tree);
                cout << "Seluruh tree berhasil dihapus!" << endl;
            }
            cout << endl;
            break;

        case 0:
            cout << "Keluar dari program..." << endl;
            break;

        default:
            cout << "Pilihan tidak valid!" << endl;
            break;
        }

    } while (pilih != 0);

    return 0;
}
   
```
Melalui antarmuka menu pada file main.cpp, program ini menyediakan kontrol penuh untuk mengelola struktur data Binary Search Tree (BST) secara interaktif. Pengguna dapat menyusun pohon dengan menambahkan data baru melalui fitur Insert, serta mengelola isinya dengan fitur Delete untuk menghapus node tertentu. Program ini juga dilengkapi dengan fungsi Search guna memverifikasi keberadaan data di dalam hierarki. Untuk keperluan visualisasi, tersedia tiga jenis penelusuran (traversal), yaitu Preorder, Inorder, dan Postorder, ditambah dengan kemampuan menampilkan node paling kiri (Most Left) dan paling kanan (Most Right). Selain itu, sistem dapat menghitung total populasi node secara otomatis dan menyediakan opsi untuk melakukan Reset atau menghapus seluruh struktur pohon secara permanen.

## Unguided

## soal 1. 

```C++
//bstree.h
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

// alokasi node
address alokasi(infotype x);

// insert node ke BST
void insertNode(address &root, infotype x);

// mencari node
address findNode(infotype x, address root);

// traversal inorder
void InOrder(address root);

#endif


//bstree.cpp
#include <iostream>
#include "bstree.h"
using namespace std;

// fungsi alokasi
address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

// fungsi insert BST
void insertNode(address &root, infotype x) {
    if (root == Nil) {
        root = alokasi(x);
    } else if (x < root->info) {
        insertNode(root->left, x);
    } else if (x > root->info) {
        insertNode(root->right, x);
    }
    // jika sama → tidak dimasukkan
}

// fungsi cari node
address findNode(infotype x, address root) {
    if (root == Nil || root->info == x)
        return root;
    if (x < root->info)
        return findNode(x, root->left);
    return findNode(x, root->right);
}

// traversal InOrder
void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " ";
        InOrder(root->right);
    }
}

//main.cpp
#include <iostream>
#include "bstree.h"

using namespace std;

int main() {
    cout << "Hello World" << endl;

    address root = Nil;
    insertNode(root,1);
    insertNode(root,2);
    insertNode(root,6);
    insertNode(root,4);
    insertNode(root,5);
    insertNode(root,3);
    insertNode(root,6);
    insertNode(root,7);

    InOrder(root);
    return 0;
}

```

### Output soal 1 :
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-10/Output-10-1.png)


Program ini mengandalkan kombinasi fungsi alokasi memori dan metode insert untuk menyusun struktur data Binary Search Tree (BST). Setiap kali node baru ditambahkan, sistem secara otomatis menempatkannya sesuai aturan hierarki BST (nilai lebih kecil ke kiri, nilai lebih besar ke kanan). Untuk memverifikasi hasilnya, program menggunakan teknik penelusuran In-Order, sebuah metode traversal yang secara sistematis mengunjungi sub-pohon kiri terlebih dahulu, memproses atau mencetak nilai pada node induk, lalu diakhiri dengan mengunjungi sub-pohon kanan. Dengan urutan kerja tersebut, output yang dihasilkan akan selalu menampilkan data dalam urutan yang teratur dari nilai terkecil hingga terbesar.

### soal 2. 

```C++
//bstree.h
#ifndef BSTREE_H
#define BSTREE_H

#define Nil NULL

typedef int infotype;
typedef struct Node* address;

struct Node {
    infotype info;
    address left;
    address right;
};

address alokasi(infotype x);
void insertNode(address &root, infotype x);
void InOrder(address root);

int hitungNode(address root);
int hitungTotal(address root);
int hitungKedalaman(address root, int start);

#endif

//bstree.cpp
#include <iostream>
#include "bstree.h"
using namespace std;

address alokasi(infotype x) {
    address P = new Node;
    if (P != Nil) {
        P->info = x;
        P->left = Nil;
        P->right = Nil;
    }
    return P;
}

void insertNode(address &root, infotype x) {
    if (root == Nil)
        root = alokasi(x);
    else if (x < root->info)
        insertNode(root->left, x);
    else if (x > root->info)
        insertNode(root->right, x);
}

void InOrder(address root) {
    if (root != Nil) {
        InOrder(root->left);
        cout << root->info << " ";
        InOrder(root->right);
    }
}

int hitungNode(address root) {
    if (root == Nil)
        return 0;
    return 1 + hitungNode(root->left) + hitungNode(root->right);
}

int hitungTotal(address root) {
    if (root == Nil)
        return 0;
    return root->info + hitungTotal(root->left) + hitungTotal(root->right);
}

int hitungKedalaman(address root, int start) {
    if (root == Nil)
        return start;
    int kiri = hitungKedalaman(root->left, start + 1);
    int kanan = hitungKedalaman(root->right, start + 1);
    return (kiri > kanan) ? kiri : kanan;
}

//main.cpp
#include <iostream>
#include "bstree.h"
using namespace std;

int main() {
    address root = Nil;

    insertNode(root,1);
    insertNode(root,2);
    insertNode(root,6);
    insertNode(root,4);
    insertNode(root,5);
    insertNode(root,3);
    insertNode(root,7);

    InOrder(root);
    cout << "\n";

    cout << "kedalaman : " << hitungKedalaman(root,0) << endl;
    cout << "jumlah Node : " << hitungNode(root) << endl;
    cout << "total : " << hitungTotal(root) << endl;

    return 0;
}

```

### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-10/Output-10-2.png)


Program ini mengelola basis data tanaman dengan mengimplementasikan struktur Binary Search Tree (BST) melalui fungsi alokasi memori dan insertNode. Selain membangun hierarki data, program ini dilengkapi dengan fitur analisis kuantitatif seperti hitungJumlahNode untuk mengetahui populasi elemen dan hitungTotalInfo untuk mengakumulasi nilai informasi di dalamnya. Salah satu aspek teknis yang ditekankan adalah pengukuran struktur pohon melalui penghitungan kedalaman (depth). Program ini membedakan secara jelas bahwa kedalaman dihitung berdasarkan jarak suatu node dari akar (root), sementara ketinggian (height) dihitung dari jarak node tersebut ke daun (leaf) paling ujung di bawahnya.

### soal 3.

```C++
//bstree.h
#ifndef BSTREE_H
#define BSTREE_H
#define Nil NULL

using namespace std;

typedef int infotype;

struct Node {
    infotype info;
    Node* left;
    Node* right;
};

typedef Node* address;

address alokasi(infotype X);
void insertNode(address &root, infotype X);
address findNode(infotype X, address &root);
void printInorder(address root);
void preOrder(address root);
void postOrder(address root);

#endif

//bstree.cpp
#include "bstree.h"
#include <iostream>
using namespace std;

address alokasi(infotype X){
    address nodeBaru = new Node;
    nodeBaru->info = X;
    nodeBaru->left = Nil;
    nodeBaru->right = Nil;
    return nodeBaru;
}

void insertNode(address &root, infotype X){
    if(root == Nil){
        root = alokasi(X);
    } else if (X < root->info){
        insertNode(root->left, X);
    } else if (X > root->info){
        insertNode(root->right, X);
    }
}

address findNode(infotype X, address &root){
    if(root == Nil){
        cout << "Tree kosong!" << endl;
    } else {
        address nodeBantu = root;
        address parent = Nil;
        bool ketemu = false;
        while(nodeBantu != Nil){
            if(X < nodeBantu->info){
                parent = nodeBantu;
                nodeBantu = nodeBantu->left;
            } else if (X > nodeBantu->info){
                parent = nodeBantu;
                nodeBantu = nodeBantu->right;
            } else if (X == nodeBantu->info){
                ketemu = true;
                break;
            }
        }
        if(ketemu == false){
            cout << "Data tidak ditemukan" << endl;
        } else if(ketemu = true){
            cout << "Data ditemukan didalam tree!" << endl;
            cout << "Data: " << nodeBantu->info << endl;
        }
    }
    return Nil;
}

void printInorder(address root){
    if(root != Nil){
        printInorder(root->left);
        cout << root->info << " - ";
        printInorder(root->right);
    }
}

void preOrder(address root){
    if(root == Nil){
        return;
    }
    cout << root->info << " - ";
    preOrder(root->left);
    preOrder(root->right);
}

void postOrder(address root){
    if(root == Nil){
        return;
    }
    postOrder(root->left);
    postOrder(root->right);
    cout << root->info << " - ";
}

//main.cpp
#include <iostream>
#include "bstree.h"
using namespace std;
int main()
{
    cout << "Hello World" << endl;
    address root = Nil;
    insertNode(root, 6);
    insertNode(root, 7);
    insertNode(root, 4);
    insertNode(root, 5);
    insertNode(root, 2);
    insertNode(root, 3);
    insertNode(root, 1);
    cout << "Tampilkan preOrder : " ;
             preOrder(root); 
             cout << endl;
    cout << "Tampilkan postOrder : "; 
             postOrder(root);
             cout << endl;
    return 0;
}

```

### Output:
![Screenshot Output 2](https://github.com/pamelasandra/Struktur-Data-Assignment/blob/main/Modul-10/Output-10-3.png)


Program ini dirancang untuk membangun struktur data Binary Search Tree (BST) dan menyajikan datanya melalui dua metode penelusuran yang berbeda, yaitu Pre-Order dan Post-Order. Pada metode Pre-Order, program memproses atau mencetak data langsung pada node induk terlebih dahulu sebelum mengeksplorasi cabang kiri dan dilanjutkan ke cabang kanan. Sebaliknya, pada metode Post-Order, program akan menelusuri seluruh sub-pohon kiri dan sub-pohon kanan hingga tuntas, baru kemudian memproses nilai pada node induk atau akar sebagai tahap akhir.

### Kesimpulan
Pada materi tree ini, dibahas beberapa fungsi utama yang digunakan dalam struktur data tree, seperti proses penyisipan data menggunakan fungsi alokasi dan insertNode. Selain itu, juga dibahas perhitungan jumlah node melalui fungsi hitungJumlahNode, perhitungan total nilai informasi dengan fungsi hitungTotalInfo, serta perhitungan kedalaman tree menggunakan fungsi hitungKedalaman. Meskipun secara konsep kedalaman dan ketinggian tree terlihat serupa, keduanya memiliki perbedaan dalam implementasi. Oleh karena itu, perhitungan kedalaman dan ketinggian pada suatu tree merupakan dua fungsi yang berbeda dan tidak dapat disamakan.
