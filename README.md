# PinaringanASD20MARET
Pinaringan Iman Santoso
1203230037 (IF-03-03)

Latihan Praktikum Algoritma Struktur Data - Array, Pointer, dan Fungsi

KOMPONEN PENILAIAN	YA	TIDAK
Soal 1 sesuai dengan output yang diinginkan	✔	

Soal 2 sesuai dengan output yang diinginkan	✔	

BONUS SOAL 1 dikerjakan	✔	

SOAL NO.1
Source code :

    #include <stdio.h>
    #include <stdbool.h>
    int value(char card) {
        if (card >= '2' && card <= '9')
            return card - '0';
        else if (card == 'J')
            return 14; // J memiliki nilai 14 agar berada di belakang K
        else if (card == 'Q')
            return 15; // Q memiliki nilai 15 agar berada di belakang J
        else if (card == 'K')
            return 16; // K memiliki nilai 16 agar berada di belakang Q
        else // Assuming 'A' represents 1
            return 1;
    }
    
    void bubble_sort(char cards[], int n) {
        int i, j, steps = 0;
        bool swapped;
        char temp;
    
        printf("Initial order: %s\n", cards);
    
        for (i = 0; i < n; i++) {
            swapped = false;
            for (j = 0; j < n - i - 1; j++) {
                if (value(cards[j]) > value(cards[j+1])) {
                    // Swap cards
                    temp = cards[j];
                    cards[j] = cards[j+1];
                    cards[j+1] = temp;
                    swapped = true;
                    steps++;
                    printf("Pertukaran %d: %s\n", steps, cards);
                }
            }
            if (!swapped)
                break;
        }
        printf("Jumlah minimal langkah pertukaran: %d\n", steps);
    }
    
    int main() {
        int n, i;
        printf("Masukkan jumlah kartu: ");
        scanf("%d", &n);
    
        char cards[n+1]; // +1 for '\0'
        printf("Masukkan nilai kartu: ");
        for (i = 0; i < n; i++) {
            scanf(" %c", &cards[i]); // Read cards one by one
        }
        cards[n] = '\0'; // Null-terminate the string
    
        bubble_sort(cards, n);
    
        return 0;
    }
    

Hasil run / output :

![image](https://github.com/Santosyouknow/PinaringanASD20MARET/assets/161540041/48481908-a6c0-4500-a25c-54fe64103fa3)



Penjelasan code / program :
```c
#include <stdio.h>
#include <stdbool.h>
```
Baris-baris ini merupakan direktif preprosesor yang memberitahu kompiler untuk menyertakan file header standar input-output dan boolean. Ini diperlukan karena program menggunakan fungsi seperti printf dan scanf, serta tipe boolean `bool`.

```c
int value(char card) {
    if (card >= '2' && card <= '9')
        return card - '0';
    else if (card == 'J')
        return 14; // J memiliki nilai 14 agar berada di belakang K
    else if (card == 'Q')
        return 15; // Q memiliki nilai 15 agar berada di belakang J
    else if (card == 'K')
        return 16; // K memiliki nilai 16 agar berada di belakang Q
    else // Mengasumsikan 'A' memiliki nilai 1
        return 1;
}
```
Fungsi `value` ini mengambil karakter yang mewakili sebuah kartu dan mengembalikan nilai numeriknya. Ini memeriksa apakah kartu berada di antara '2' dan '9', dalam hal ini mengonversi karakter ke nilai integer. Jika kartu adalah 'J', 'Q', atau 'K', itu memberikan nilai-nilai tertentu (14, 15, 16 secara berturut-turut). Jika tidak, diasumsikan 'A' mewakili nilai 1.

```c
void bubble_sort(char cards[], int n) {
    int i, j, steps = 0;
    bool swapped;
    char temp;

    printf("Urutan awal: %s\n", cards);

    for (i = 0; i < n; i++) {
        swapped = false;
        for (j = 0; j < n - i - 1; j++) {
            if (value(cards[j]) > value(cards[j+1])) {
                // Tukar kartu
                temp = cards[j];
                cards[j] = cards[j+1];
                cards[j+1] = temp;
                swapped = true;
                steps++;
                printf("Pertukaran %d: %s\n", steps, cards);
            }
        }
        if (!swapped)
            break;
    }
    printf("Jumlah minimal langkah pertukaran: %d\n", steps);
}
```
Fungsi ini `bubble_sort` mengurutkan sebuah array kartu dalam urutan naik menggunakan algoritma bubble sort. Ini mengambil array kartu `cards[]` dan panjangnya `n` sebagai argumen. Di dalam fungsi, ada dua loop: loop luar `i` untuk mengulangi semua elemen array, dan loop dalam `j` untuk melakukan perbandingan dan pertukaran. Variabel `steps` menghitung jumlah pertukaran yang dilakukan selama pengurutan. Fungsi ini juga mencetak urutan awal kartu dan langkah-langkah perantara saat pengurutan.

```c
int main() {
    int n, i;
    printf("Masukkan jumlah kartu: ");
    scanf("%d", &n);

    char cards[n+1]; // +1 untuk '\0'
    printf("Masukkan nilai kartu: ");
    for (i = 0; i < n; i++) {
        scanf(" %c", &cards[i]); // Baca kartu satu per satu
    }
    cards[n] = '\0'; // Memberi terminasi nol pada string

    bubble_sort(cards, n);

    return 0;
}
```
Ini adalah fungsi `main` di mana eksekusi program dimulai. Ini meminta pengguna untuk memasukkan jumlah kartu dan kemudian nilai masing-masing kartu. Ini membaca masukan ini dan menyimpannya dalam array `cards[]`. Setelah itu, ia memanggil fungsi `bubble_sort` dengan melewatkan array kartu dan panjangnya. Terakhir, ia mengembalikan 0 untuk menunjukkan penyelesaian program yang sukses.




SOAL NO.2
Source code :
    
    #include <stdio.h>
    #include <stdlib.h>
    
    // Function to mark the positions reachable by the knight
    void koboImaginaryChess(int i, int j, int size, int *chessBoard) {
        // Array to represent possible moves of a knight
        int moves[8][2] = {{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
                           {1, -2}, {1, 2}, {2, -1}, {2, 1}};
    
        // Check and mark reachable positions
        for (int k = 0; k < 8; k++) {
            int ni = i + moves[k][0];
            int nj = j + moves[k][1];
            if (ni >= 0 && ni < size && nj >= 0 && nj < size) {
                chessBoard[ni * size + nj] = 1;
            }
        }
    }
    
    int main() {
        // Allocate memory for chess board
        int *chessBoard = (int *)malloc(8 * 8 * sizeof(int));
        if (chessBoard == NULL) {
            printf("Memory allocation failed\n");
            return 1;
        }
    
        // Initialize chess board with zeros
        for (int i = 0; i < 8 * 8; i++) {
            chessBoard[i] = 0;
        }
    
        // Input the position of the knight
        int i, j;
        printf("Enter the position of the knight (i j): ");
        scanf("%d %d", &i, &j);
    
        // Call function to mark reachable positions
        koboImaginaryChess(i, j, 8, chessBoard);
    
        // Mark the position of the knight
        chessBoard[i * 8 + j] = 0;
    
        // Print the chess board
        printf("Chess board:\n");
        for (int row = 0; row < 8; row++) {
            for (int col = 0; col < 8; col++) {
                printf("%d ", chessBoard[row * 8 + col]);
            }
            printf("\n");
        }
    
        // Free dynamically allocated memory
        free(chessBoard);
    
        return 0;
    }


Hasil Run / Output :
 
![image](https://github.com/Santosyouknow/PinaringanASD20MARET/assets/161540041/3f81bec2-6c35-4dd4-94b6-916eaff58694)

Penjelasan code : 
```c
#include <stdio.h>
#include <stdlib.h>
```
Baris ini mengimpor dua header file standar dalam bahasa C, yaitu `<stdio.h>` untuk fungsi input/output standar dan `<stdlib.h>` untuk alokasi memori dinamis dan fungsi-fungsi lain yang terkait dengan pengelolaan memori.

```c
// Function to mark the positions reachable by the knight
void koboImaginaryChess(int i, int j, int size, int *chessBoard) {
    // Array to represent possible moves of a knight
    int moves[8][2] = {{-2, -1}, {-2, 1}, {-1, -2}, {-1, 2},
                       {1, -2}, {1, 2}, {2, -1}, {2, 1}};
```
Di sini, kita mendefinisikan fungsi `koboImaginaryChess` yang akan menandai posisi yang dapat dicapai oleh kuda. Array `moves` digunakan untuk menyimpan kemungkinan gerakan kuda dalam bentuk perubahan baris (`moves[k][0]`) dan kolom (`moves[k][1]`).

```c
    // Check and mark reachable positions
    for (int k = 0; k < 8; k++) {
        int ni = i + moves[k][0];
        int nj = j + moves[k][1];
        if (ni >= 0 && ni < size && nj >= 0 && nj < size) {
            chessBoard[ni * size + nj] = 1;
        }
    }
```
Dalam loop `for`, setiap kemungkinan gerakan kuda diperiksa untuk memastikan apakah posisinya berada dalam batas papan catur. Jika ya, posisi tersebut ditandai dalam papan catur dengan mengatur nilai elemen array `chessBoard` yang sesuai menjadi 1.

```c
int main() {
    // Allocate memory for chess board
    int *chessBoard = (int *)malloc(8 * 8 * sizeof(int));
    if (chessBoard == NULL) {
        printf("Memory allocation failed\n");
        return 1;
    }
```
Fungsi `main` adalah titik awal dari program. Di sini, kita mengalokasikan memori untuk papan catur menggunakan fungsi `malloc`. Jika alokasi gagal, program akan mencetak pesan kesalahan dan keluar.

```c
    // Initialize chess board with zeros
    for (int i = 0; i < 8 * 8; i++) {
        chessBoard[i] = 0;
    }
```
Setelah memori dialokasikan, kita inisialisasi semua elemen papan catur dengan nilai 0.

```c
    // Input the position of the knight
    int i, j;
    printf("Enter the position of the knight (i j): ");
    scanf("%d %d", &i, &j);
```
Program meminta pengguna untuk memasukkan posisi awal kuda dengan menggunakan fungsi `scanf`.

```c
    // Call function to mark reachable positions
    koboImaginaryChess(i, j, 8, chessBoard);
```
Fungsi `koboImaginaryChess` dipanggil untuk menandai posisi yang dapat dicapai oleh kuda dari posisi awal yang dimasukkan pengguna.

```c
    // Mark the position of the knight
    chessBoard[i * 8 + j] = 0;
```
Nilai 2 yang menunjukkan posisi kuda diganti menjadi 0.

```c
    // Print the chess board
    printf("Chess board:\n");
    for (int row = 0; row < 8; row++) {
        for (int col = 0; col < 8; col++) {
            printf("%d ", chessBoard[row * 8 + col]);
        }
        printf("\n");
    }
```
Akhirnya, program mencetak papan catur yang telah ditandai. Setiap elemen dari array `chessBoard` dicetak, dengan spasi sebagai pemisah antar kolom dan newline sebagai pemisah antar baris.

```c
    // Free dynamically allocated memory
    free(chessBoard);

    return 0;
}
```
Di bagian akhir fungsi `main`, memori yang dialokasikan untuk papan catur dibebaskan menggunakan fungsi `free`, dan nilai 0 dikembalikan sebagai kode keluaran yang menunjukkan bahwa program telah berhasil dijalankan.


