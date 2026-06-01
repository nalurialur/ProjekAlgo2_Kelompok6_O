# ProjekAlgo2_Kelompok3_O
#include <iostream>
#include <fstream>
#include <iomanip>
using namespace std;

#define MAX 100

struct Data {
    string food_name;
    string drink_name;
    int food_price;
    int drink_price;
    int drink_amount;
    int food_amount;
};

Data menuData[MAX];  
int current = 0;

//====================== LOGIN SYSTEM =====================
bool loginSystem(){
    string username;
    string password;
    int attempts = 3;

    while(attempts > 0){
        cout << "===========================================" << endl;
        cout << "     welcome to our sweetmunch bakery!     " << endl;
        cout << "===========================================" << endl;
        cout << "please enter the right username & password" << endl;
        cout << "username masukin dulu mpruy: ";
        cin >> username;
        cout << "password yang bener jangan coba-coba: ";
        cin >> password;

        if(username == "nanana3" && password == "enbesarsemua"){
            cout << "\nLogin success bray!\n" << endl;
            system("pause");
            system("cls");
            return true;
        } else {
            attempts--;
            if(attempts > 0){  
                cout << "\n username sama passwordnya benerin dulu! salah itu mpruy" << endl;
                cout << "(jiakh kesempatan loginnya tinggal:  " << attempts << " kali)" << endl;  
            } else {
                cout << "udah salah username atau password, kesempatan loginnya habis pula. gue tutup ye programnya!" << endl;
            }
            system("pause");
            system("cls");
        }
    }
    return false;
}

//====================== INPUT DATA MENU ============================
void inputMenu() {
    if(current >= MAX){
        cout << "Etalase penuh!" << endl;
        return;
    }
    cout << "----------------------------------------" << endl;
    cout << "                INPUT MENU              " << endl;
    cout << "----------------------------------------" << endl;
    cout << "Food name: ";  cin >> ws; getline(cin, menuData[current].food_name);
    cout << "Food price: "; cin >> menuData[current].food_price;       
    cout << "Food stock: "; cin >> menuData[current].food_amount;
    cout << "Drink name: "; cin >> ws; getline(cin, menuData[current].drink_name);
    cout << "Drink price: "; cin >> menuData[current].drink_price;     
    cout << "Drink stock: "; cin >> menuData[current].drink_amount;
    current++;
    cout << "Data successfully added!" << endl;
}

//================== DISPLAY MENU DATA (DIPISAH) =====================
void displayMenu() {
    if (current == 0) {
        cout << "Belum ada data menu di etalase bakery!" << endl;
        return;
    }
    
    // 1. TAMPILKAN MENU MAKANAN
    cout << "==========================================" << endl;
    cout << "|         SWEETMUNCH FOOD MENU           |" << endl;
    cout << "==========================================" << endl;
    cout << left << setw(5) << "No"
         << setw(25) << "FOOD NAME"
         << setw(15) << "PRICE" << endl;
    cout << "------------------------------------------" << endl;
    for (int i = 0; i < current; i++) {
        cout << left << setw(5) << (i + 1)
             << setw(25) << menuData[i].food_name
             << "Rp" << menuData[i].food_price << endl;
    }
    cout << "==========================================" << endl << endl;

    // 2. TAMPILKAN MENU MINUMAN
    cout << "==========================================" << endl;
    cout << "|        SWEETMUNCH DRINK MENU           |" << endl;
    cout << "==========================================" << endl;
    cout << left << setw(5) << "No"
         << setw(25) << "DRINK NAME"
         << setw(15) << "PRICE" << endl;
    cout << "------------------------------------------" << endl;
    for (int i = 0; i < current; i++) {
        cout << left << setw(5) << (i + 1)
             << setw(25) << menuData[i].drink_name
             << "Rp" << menuData[i].drink_price << endl;
    }
    cout << "==========================================" << endl;
}

//============ STOCK FOOD & BEVERAGES ========
void displayStock(){
    if(current == 0){
        cout << "belum ada data stok!" << endl;
        return;
    }
    cout << "==========================================" << endl;
    cout << "|    SWEETMUNCH FOOD & DRINK INVENTORY   |" << endl;
    cout << "==========================================" << endl;
    cout << left << setw(5) << "No" 
         << setw(25) << "ITEM NAME" << setw(10) << "STOCK" << endl;
    cout << "------------------------------------------" << endl;
    cout << "[ FOODS ]" << endl;
    for(int i = 0; i < current; i++){
        cout << left << setw(5) << (i + 1)
             << setw(25) << menuData[i].food_name << setw(10) << menuData[i].food_amount << endl;
    }
    cout << "------------------------------------------" << endl;
    cout << "[ DRINKS ]" << endl;
    for(int i = 0; i < current; i++){
        cout << left << setw(5) << (i + 1)
             << setw(25) << menuData[i].drink_name << setw(10) << menuData[i].drink_amount << endl;
    }
    cout << "==========================================" << endl;
}

//================== EDIT DATA =====================
void editBakery() {
    if (current == 0) {
        cout << "Belum ada data menu!" << endl;
        return;
    }
    string target;
    cout << "Masukkan nama makanan atau minuman yang akan diedit: ";
    cin >> ws;
    getline(cin, target);
    bool found = false;

    for (int i = 0; i < current; i++) {
        if (menuData[i].food_name == target || menuData[i].drink_name == target) {
            found = true;
            int chooseEdit;
            cout << "\nData ditemukan! mau edit bagian apa?" << endl;
            cout << "1. Nama & Harga Makanan" << endl;
            cout << "2. Nama & Harga Minuman" << endl;
            cout << "3. Update semua stok" << endl;
            cout << "Pilihan: "; cin >> chooseEdit;
            if(chooseEdit == 1){
                cout << "Nama makanan baru: "; cin >> ws; getline(cin, menuData[i].food_name);
                cout << "Harga makanan baru: "; cin >> menuData[i].food_price;
            } else if(chooseEdit == 2){
                cout << "Nama minuman baru: "; cin >> ws; getline(cin, menuData[i].drink_name);
                cout << "Harga minuman baru: "; cin >> menuData[i].drink_price;
            } else if(chooseEdit == 3){
                cout << "Stok makanan baru: "; cin >> menuData[i].food_amount;
                cout << "Stok minuman baru: "; cin >> menuData[i].drink_amount;
            }
            cout << "Data bakery berhasil diperbarui!" << endl;
            break;
        }
    }
    if (!found) {
        cout << "Menu tidak ditemukan!" << endl;
    }
}

//=================== HAPUS DATA =================
void deleteData(){
    if(current == 0){
        cout << "kosong ini loh, nggak ada yang bisa dihapus!" << endl;
        return;  
    }
    string search;
    cout << "masukin nama makanan/minuman yang mau dihapus sini: ";
    cin >> ws; getline(cin, search);
    bool found = false;
    for(int i = 0; i < current; i++){
        if(menuData[i].food_name == search || menuData[i].drink_name == search){  
            found = true;
            for(int j = i; j < current - 1; j++){
                menuData[j] = menuData[j + 1];
            }
            current--;  
            cout << "udah kehapus dari etalase" << endl;  
            break;
        }
    }
    if(!found) cout << "menu nggak ada woy!" << endl;
}

//================== HELPER: cetak hasil search terpisah =====================
void cetakHasilSearch(int idx, int opsi){  
    cout << "------------------------------------------" << endl;
    if(opsi == 1) {
        cout << left << setw(5) << "No" << setw(25) << "FOOD NAME" << "PRICE" << endl;
        cout << left << setw(5) << (idx + 1) << setw(25) << menuData[idx].food_name << "Rp" << menuData[idx].food_price << endl;
    } else {
        cout << left << setw(5) << "No" << setw(25) << "DRINK NAME" << "PRICE" << endl;
        cout << left << setw(5) << (idx + 1) << setw(25) << menuData[idx].drink_name << "Rp" << menuData[idx].drink_price << endl;
    }
    cout << "------------------------------------------" << endl;
}

//================== SEARCH (TERPISAH) =====================
void binarySearch(string search, int opsi) {
    // bubble sort dulu sesuai field sebelum binary search
    for(int i = 0; i < current - 1; i++){
        for(int j = 0; j < current - i - 1; j++){  
            if((opsi == 1 && menuData[j].food_name > menuData[j + 1].food_name) ||
               (opsi == 2 && menuData[j].drink_name > menuData[j + 1].drink_name)){
                swap(menuData[j], menuData[j + 1]);  
            }
        }
    }
    int low = 0, high = current - 1, mid;
    bool found = false;
    while (low <= high){
        mid = (low + high) / 2;
        string current_name = (opsi == 1) ? menuData[mid].food_name : menuData[mid].drink_name;
        if(current_name == search){
            cetakHasilSearch(mid, opsi);
            found = true; break;
        }
        else if(current_name < search) low = mid + 1;
        else high = mid - 1;
    }
    if (!found) cout << "Data tidak ditemukan" << endl;
}

//========= SORTING (Shell Sort Terpisah) ==========
void shellSort(int field) {  
    int gap = current / 2;
    while(gap > 0){
        for(int i = gap; i < current; i++){
            Data temp = menuData[i];
            int j = i;
            while(j >= gap && (field == 1 ? menuData[j - gap].food_name > temp.food_name
                                          : menuData[j - gap].drink_name > temp.drink_name)){
                menuData[j] = menuData[j - gap];
                j -= gap;
            }
            menuData[j] = temp;
        }
        gap /= 2;
    }
    
    // Tampilkan hasil secara spesifik
    cout << "==========================================" << endl;
    if(field == 1) {
        cout << " Data Terurut (Ascending Food Name)!" << endl;
        cout << "==========================================" << endl;
        cout << left << setw(5) << "No" << setw(25) << "FOOD NAME" << "PRICE" << endl;
        for(int i=0; i<current; i++) {
            cout << left << setw(5) << (i+1) << setw(25) << menuData[i].food_name << "Rp" << menuData[i].food_price << endl;
        }
    } else {
        cout << " Data Terurut (Ascending Drink Name)!" << endl;
        cout << "==========================================" << endl;
        cout << left << setw(5) << "No" << setw(25) << "DRINK NAME" << "PRICE" << endl;
        for(int i=0; i<current; i++) {
            cout << left << setw(5) << (i+1) << setw(25) << menuData[i].drink_name << "Rp" << menuData[i].drink_price << endl;
        }
    }
    cout << "==========================================" << endl;
}

//===== FILE HANDLING ======
void exportData() {
    ofstream fileOut("data_bakery.txt");
    if(!fileOut){
        cout << "Gagal memuat file export!" << endl;
        return;
    }
    fileOut << current << endl;
    for(int i = 0; i < current; i++){
        fileOut << menuData[i].food_name  << endl << menuData[i].food_price  << endl;
        fileOut << menuData[i].drink_name << endl << menuData[i].drink_price << endl;
        fileOut << menuData[i].food_amount << endl << menuData[i].drink_amount << endl;
    }
    fileOut.close();  
    cout << "Data berhasil diexport ke data_bakery.txt" << endl;
}

void importData(){
    ifstream fileIn("data_bakery.txt");
    if(!fileIn){  
        cout << "file tidak ditemukan!" << endl;
        return;
    }
    fileIn >> current;
    for(int i = 0; i < current; i++){  
        fileIn >> ws; getline(fileIn, menuData[i].food_name);
        fileIn >> menuData[i].food_price;
        fileIn >> ws; getline(fileIn, menuData[i].drink_name);
        fileIn >> menuData[i].drink_price;    
        fileIn >> menuData[i].food_amount;
        fileIn >> menuData[i].drink_amount;
    }
    fileIn.close();  
    cout << "Data berhasil diimport! Total data : " << current << " menu." << endl;
}

//================== CASHIER SYSTEM =====================
void cashierSystem() {
    if (current == 0) {  
        cout << "Belum ada menu tersedia!" << endl;
        return;
    }

    displayMenu(); // Menggunakan displayMenu terpisah yang baru

    struct OrderItem {
        string item_name;
        string item_type;
        int item_price;
        int qty;
    };

    OrderItem orders[MAX * 2];
    int orderCount = 0;
    int totalHarga = 0;
    char lanjut = 'y';

    while (lanjut == 'y' || lanjut == 'Y') {
        int pilihMenu;
        cout << "\nPilih nomor paket menu (1-" << current << "): ";
        cin >> pilihMenu;

        if (pilihMenu < 1 || pilihMenu > current) {
            cout << "Nomor menu tidak valid!" << endl;
            continue;
        }

        int pilihItem;
        cout << "Mau pesen apa?" << endl;
        cout << "1. Makanan: " << menuData[pilihMenu-1].food_name  << " (Rp" << menuData[pilihMenu-1].food_price  << ")" << endl;
        cout << "2. Minuman: " << menuData[pilihMenu-1].drink_name << " (Rp" << menuData[pilihMenu-1].drink_price << ")" << endl;
        cout << "Pilihan: ";
        cin >> pilihItem;

        int qty;
        cout << "Jumlah: ";
        cin >> qty;

        if (qty <= 0) {
            cout << "Jumlah tidak valid!" << endl;
            continue;
        }

        orders[orderCount].qty = qty;

        if (pilihItem == 1) {
            if (qty > menuData[pilihMenu-1].food_amount) {
                cout << "Stok tidak cukup! Stok tersedia: " << menuData[pilihMenu-1].food_amount << endl;
                continue;
            }
            orders[orderCount].item_name  = menuData[pilihMenu-1].food_name;
            orders[orderCount].item_type  = "food";
            orders[orderCount].item_price = menuData[pilihMenu-1].food_price;
            menuData[pilihMenu-1].food_amount -= qty;
        } else if (pilihItem == 2) {
            if (qty > menuData[pilihMenu-1].drink_amount) {
                cout << "Stok tidak cukup! Stok tersedia: " << menuData[pilihMenu-1].drink_amount << endl;
                continue;
            }
            orders[orderCount].item_name  = menuData[pilihMenu-1].drink_name;
            orders[orderCount].item_type  = "drink";
            orders[orderCount].item_price = menuData[pilihMenu-1].drink_price;
            menuData[pilihMenu-1].drink_amount -= qty;
        } else {
            cout << "Pilihan tidak valid!" << endl;
            continue;
        }

        totalHarga += orders[orderCount].item_price * qty;
        orderCount++;

        cout << "Tambah item lagi? (y/n): ";
        cin >> lanjut;
    }

    if (orderCount == 0) {
        cout << "Tidak ada item yang dipesan." << endl;
        return;
    }

    string namaPembeli;
    cout << "\nNama pembeli: ";
    cin >> ws;
    getline(cin, namaPembeli);

    int uangBayar;
    cout << "Total belanja: Rp" << totalHarga << endl;
    cout << "Uang bayar  : Rp";
    cin >> uangBayar;

    if (uangBayar < totalHarga) {
        cout << "Uang tidak cukup! Transaksi dibatalkan." << endl;
        return;
    }

    int kembalian = uangBayar - totalHarga;

    cout << endl;
    cout << "     ================================" << endl;
    cout << "     |       SWEETMUNCH BAKERY      |" << endl;
    cout << "     |  Jl. Roti Manis No. 7, DIY   |" << endl;
    cout << "     |   Telp: 0812-XXXX-XXXX       |" << endl;
    cout << "     ================================" << endl;
    cout << "     Nama   : " << namaPembeli << endl;
    cout << "     --------------------------------" << endl;
    cout << "     " << left << setw(18) << "ITEM"
         << setw(5) << "QTY"
         << setw(12) << "HARGA"
         << "SUBTOTAL" << endl;
    cout << "     --------------------------------" << endl;
    for (int i = 0; i < orderCount; i++) {
        int subtotal = orders[i].item_price * orders[i].qty;
        cout << "     " << left << setw(18) << orders[i].item_name
             << setw(5)  << orders[i].qty
             << "Rp" << setw(10) << orders[i].item_price
             << "Rp" << subtotal << endl;
    }
    cout << "     --------------------------------" << endl;
    cout << "     " << left << setw(23) << "TOTAL"     << "Rp" << totalHarga  << endl;
    cout << "     " << left << setw(23) << "BAYAR"     << "Rp" << uangBayar   << endl;
    cout << "     " << left << setw(23) << "KEMBALIAN" << "Rp" << kembalian   << endl;
    cout << "     ================================" << endl;
    cout << "        Terima kasih sudah mampir!   " << endl;
    cout << "           See you next time! :)     " << endl;
    cout << "     ================================" << endl;
    cout << endl;
}

//=================== REKURSI ========================
int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

//=================== FAKTORIAL ======================
long long faktorial(int n) {
    if (n <= 1) return 1;
    return n * faktorial(n - 1);
}

//================= MAIN ===================
int main() {

    if(!loginSystem()) return 0;

    int mainChoose;
    int operationChoose;

    while(true) {
        cout << "======================================================================================" << endl;
        cout << "|                      SWEETMUNCH BAKERY MAIN MENU!                                  |" << endl;
        cout << "======================================================================================" << endl;
        cout << "1. Menu Operation" << endl;
        cout << "2. Food & Drink Stocking" << endl;
        cout << "3. Cashier System" << endl;
        cout << "4. Rekursi" << endl;
        cout << "0. Exit" << endl;
        cout << "Input your choice: "; cin >> mainChoose;
        system("cls");

        switch(mainChoose) {
            case 1: { 
                cout << "==========================================" << endl;
                cout << "             MENU DATA OPERATION          " << endl;
                cout << "==========================================" << endl;
                cout << "1. Input Data Menu Bakery" << endl;
                cout << "2. Display Data Menu Bakery (Terpisah)" << endl;
                cout << "3. Edit Data Menu Bakery" << endl;
                cout << "4. Delete Data Menu Bakery" << endl;
                cout << "5. Search Data (Makanan/Minuman)" << endl;
                cout << "6. Sorting Data (Makanan/Minuman)" << endl;
                cout << "7. Export dan Import Data" << endl;
                cout << "0. Keluar" << endl;
                cout << "============================" << endl;
                cout << "Masukkan choice : ";
                cin >> operationChoose;
                system("cls");

                if(operationChoose == 0) break;  

                switch(operationChoose){
                    case 1: inputMenu(); break;
                    case 2: displayMenu(); break;
                    case 3: editBakery(); break;
                    case 4: deleteData(); break;
                    case 5: {
                        string keyword;
                        int opsiCari;
                        cout << "============================" << endl;
                        cout << "Cari berdasarkan Kategori:  " << endl;
                        cout << "1. Makanan                  " << endl;
                        cout << "2. Minuman                  " << endl;
                        cout << "============================" << endl;
                        cout << "Masukkan pilihan (1-2): "; cin >> opsiCari;
                        cout << "Masukkan Nama Item yang dicari: "; cin >> ws; getline(cin, keyword);
                        binarySearch(keyword, opsiCari);  
                        break;
                    }
                    case 6: {
                        int fieldSort;
                        cout << "Sort berdasarkan:\n1. Makanan (Food Name)\n2. Minuman (Drink Name)\nPilihan: ";
                        cin >> fieldSort;
                        shellSort(fieldSort);  
                        break;
                    }
                    case 7: {
                        int chooseFile;
                        cout << "============================" << endl;
                        cout << "        OPERASI FILE        " << endl;
                        cout << "============================" << endl;
                        cout << "1. Export Data" << endl;
                        cout << "2. Import Data" << endl;
                        cout << "Masukkan pilihan : ";
                        cin >> chooseFile;
                        if (chooseFile == 1) exportData();
                        else if (chooseFile == 2) importData();
                        break;
                    }
                    default: cout << "Pilihan tidak valid!" << endl;
                }
                break; 
            } 

            case 2: displayStock(); break;
            case 3: cashierSystem(); break;

            case 4: {
                int chooseRekursi, n;
                cout << "============================" << endl;
                cout << "            REKURSI          " << endl;
                cout << "============================" << endl;
                cout << "1. Fibonacci" << endl;
                cout << "2. Faktorial" << endl;
                cout << "Masukkan pilihan : ";
                cin >> chooseRekursi;
                cout << "Masukkan angka : ";
                cin >> n;
                if (chooseRekursi == 1)
                    cout << "Hasil fibonacci : " << fibonacci(n) << endl;
                else if (chooseRekursi == 2)
                    cout << "Hasil faktorial : " << faktorial(n) << endl;
                break;
            }

            case 0:
                cout << "Thank you for using our system ia kaka kaka!" << endl;
                return 0;
            default:
                cout << "Menu tidak tersedia!" << endl;
        }

        system("pause");
        system("cls");
    }
}
