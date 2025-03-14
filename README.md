# 124240052.tugaskuis
tugas 2 praktikum algoritma
// Rahmat Agung Aryanto (124240052)
#include <iostream>
#include <cstring>
using namespace std;

struct dataPenduduk {
    char nk[20];
    char nama[50];
    char alamat[70];
    char jenisKelamin;
}; 
void input(){
    FILE *file = fopen("kependudukan.dat", "ab");
    if (!file) {
        cout << "Gagal membuka file!" << endl;
        return;
    }
    dataPenduduk p;
    cout << "Masukkan nomer kependudukan :";
    cin >> p.nk;
    cout << "Masukkan nama : ";
    cin >> p.nama;
    cout << "Masukkan alamat : ";
    cin >> p.alamat ;
    cout << "Masukkan jenis kelamin :";
    cin >> p.jenisKelamin;
    fwrite(&p, sizeof(dataPenduduk), 1, file);
    fclose(file);
    cout << "Data berhasil ditambahkan!" << endl;
}

    void output(){
        int n=0;
        FILE *file = fopen("kependudukan.dat", "rb");
    if (!file) {
        cout << "Belum ada data tersimpan." << endl;
        return;
    }
    dataPenduduk p[30];
    while (fread(&p[n], sizeof(dataPenduduk), 1, file)) {
         n++;
    }fclose(file);
     
    for(int i = 0; i < n -1; i++){
        for(int j = 0; j <n -1 -i;j++){
            if(strcmp(p[j].nk, p[j + 1].nk) > 0)
         {
            swap(p[j], p[j + 1]);
             
            }
        }
     }
     cout << "\nData Kependudukan:\n";
    cout << "Nomer kependudukan\tNama\tAlamat\tJenis kelamin" << endl;
     for (int i = 0; i < n; i++) {
        cout << p[i].nk << "\t"
        << p[i].nama << "\t"
        << p[i].alamat << "\t"
        << p[i].jenisKelamin << endl;}
    }
    void search(){
        int i = 0;
        string cari;
        bool found = false; 
        int n=0;
        FILE *file = fopen("kependudukan.dat", "rb");
        if (!file) {
        cout << "Belum ada data tersimpan." << endl;
        return;
        }
        dataPenduduk p[30];
        while (fread(&p[n], sizeof(dataPenduduk), 1, file)) {
            n++;
       }fclose(file);
       cout << "Selamat datang di menu Searching Data" << endl;
       cout << "Masukkan Nomer kependudukan yang dicari : ";
       cin >> cari;
        while (i < n && !found) {
            if (p[i].nk == cari) {
                found = true;
            } else {
                i++;
            }
        }
        if (found) {
            cout << "Data ditemukan sebagai berikut : " << endl;
            cout << "Nomer kependudukan : " << p[i].nk << endl;
            cout << "Nama : " << p[i].nama << endl;
            cout << "Alamat: " << p[i].alamat << endl;
            cout << "Jenis kelamin: " << p[i].jenisKelamin << endl;
        } else {
            cout << "Data tidak ditemukan" << endl;
        }
    }
    void edit(){
        int i = 0;
        string cari;
        bool found = false; 
        int n=0;
        FILE *file = fopen("kependudukan.dat", "rb+");
        
        if (!file) {
            cout << "Belum ada data tersimpan." << endl;
            return;
        }
        dataPenduduk p[30];
        while (fread(&p[n], sizeof(dataPenduduk), 1, file)) {
            n++;
       }
        cout << "Masukkan Nomer kependudukan yang data alamat akan diperbarui : ";
        cin >> cari;
        while (i < n && !found) {
            if (p[i].nk == cari) {
                found = true;
            } else {
                i++;
            }
        }
        if (found) {
            cout << "Data ditemukan sebagai berikut : " << endl;
            cout << "Nomer kependudukan : " << p[i].nk << endl;
            cout << "Nama : " << p[i].nama << endl;
            cout << "Alamat: " << p[i].alamat << endl;
            cout << "Jenis kelamin: " << p[i].jenisKelamin << endl;
            cout << "Masukkan alamat baru : ";
            cin >> p[i].alamat ;
            fseek(file, i * sizeof(dataPenduduk), SEEK_SET);
            fwrite(&p[i], sizeof(dataPenduduk), 1, file);
            
             cout << "Data berhasil dperbarui!" << endl;
        } else {
            cout << "Data tidak ditemukan\nTidak bisa memperbarui data " << endl;
        }
        fclose(file);
    }

    void hapus(){
    string cari;
    bool found = false;
    int n = 0;

    FILE *file = fopen("kependudukan.dat", "rb");
    if (!file) {
        cout << "Belum ada data tersimpan." << endl;
        return;
    }

    dataPenduduk p[30];
    while (fread(&p[n], sizeof(dataPenduduk), 1, file)) {
        n++;
    }
    fclose(file);

    cout << "Masukkan Nomer Kependudukan yang ingin dihapus: ";
    cin >> cari;

    int dataApus = -1;
    for (int i = 0; i < n; i++) {
        if (p[i].nk == cari) {
            found = true;
            dataApus = i;
            break;
        }
    }

    if (found) {
        file = fopen("kependudukan.dat", "wb");
        for (int i = 0; i < n; i++) {
            if (i != dataApus) {
                fwrite(&p[i], sizeof(dataPenduduk), 1, file);
            }
        }
        fclose(file);
        cout << "Data berhasil dihapus!" << endl;
    } else {
        cout << "Data tidak ditemukan!" << endl;
    }
}
    


int main(){
    char lanjut;
    int pilihan;
    do {cout << "\nSistem data kependudukan" << endl;
        cout << "1. Input data" << endl;
        cout << "2. Output data" << endl;
        cout << "3. Search data" << endl;
        cout << "4. Edit data" << endl;
        cout << "5. Hapus data" << endl;
        cout << "6. keluar" << endl;
        cout << "Pilih menu: ";
        cin >> pilihan; 

    switch (pilihan)
    {
    case 1:
        input();
        break;
    
    case 2:
        output();
        break;
    case 3:
        search();
        break;
    case 4:
        edit();
       break;
    case 5:
       hapus();
      break;
    case 6:
    cout<<"keluar"<< endl;
    cout << "terima kasih telah menggunakan program ini"<<endl;
        break;
    }cout << "apakah anda ingin melanjutkan program? (y/t) :";
        cin >> lanjut ;
      }while (lanjut== 'y'|| lanjut == 'Y');

    return 0;
}
