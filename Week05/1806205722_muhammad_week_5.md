## Memory and Process

### Process
Berikut bagian-bagian dari proses, yaitu:

 1. Text (Program code)  
    Bagian dari process memory yang menyimpan instruksi eksekusi program yang akan dijalankan process

2.  Initialized data  
    Bagian process memory yang menyimpan global dan static variables yang diinisialisasi oleh programmer.

3.  Uninitialized data  
    Bagian process memory yang menyimpan global dan static variables yang tidak diinisialisasi secara eksplisit oleh programmer

4.  Stack  
    Bagian process memory yang berguna saat sebuah fungsi dipanggil yang akan menaruh stack frame ke dalam stack. Stack frame ini berisi local variable fungsi, address return dari fungsi dan argumen fungsi.

5.  Heap  
Bagian process memory dimana alokasi memory resource secara dinamis terjadi. Heap akan melebar dan mengecil sesuai dengan kebutuhan memory yang dibutuhkan dari proses.

### Reference Locality
Reference locality adalah suatu kecenderungan prosesor mengakses set dari lokasi memory yang sama untuk beberapa saat.

Terdapat dua jenis locality of reference, yaitu:

 1. Spatial Locality  
Spatial locality adalah suatu kondisi dimana sebuah data yang diambil atau instruksi yang dieksekusi kemungkinan besar tetangga dari data / instruksi tersebut akan diambil atau dieksekusi.

 3. Temporal Locality
Temporal locality adalah suatu kondisi dimana sebuah data yang diambil atau instruksi yang dieksekusi kemungkinan besar akan dieksekusi kembali.

```javascript
let arr = [1,2,3]

let sum = 0

for(ii=0; i<arr.length; ii++){

	sum += arr[ii]
}
```
Dari kode diatas menunjukkan temporal locality dan spatial locality. Temporal locality terlihat pada variabel sum yang diakses terus-menerus dalam program. Spatial locality terlihat saat melakukan for loop, setiap loop mengakses sebuah data array sebuah indeks dan loop setelahnya akan mengambil data dari indeks tetangga dari indeks array sebelumnya, yaitu nilai array pada indeks + 1.

 

### Virtual Memory
Virtual memory adalah sebuah teknik manajemen memory dimana OS mensimulasikan secondary storage menjadi main memory. Virtual memory digunakan apabila OS kekkurangan resource memory untuk menjalankan aplikasi. Saat OS membutuhkan resource memory tambahan, OS akan menyimpan bagian memory yang jarang diakses ke dalam virtual memory, Lalu OS akan men-load data baru yang dibutuhkan memory segera. Saat bagian memory yang disimpan dalam virtual memory dibutuhkan, Memory akan melakukan swap dari virtual memory ke physical memory. Terlalu banyak proses swapping disebut **thrashing**.

Kelebihan Virtual memory:
1.  Lebih murah ketimbang meningkatkan kapasitas physical memory
    
2.  Lebih banyak process yang dijalankan di main memory karena prinsip swapping dari virtual memory, alokasi memory yang dibutuhkan process dapat dipecah dalam physical memory dan virtual memory
    
3.  Dapat menjalankan process yang membutuhkan memory lebih tinggi, alasan sama dengan nomor 2

Kekurangan Virtual Memory:
4.  Ukuran secondary storage yang dapat digunakan berkurang akibat dialokasikan sebagai virtual memory
    
5.  Aplikasi berjalan lambat karena kemungkinan aplikasi harus melalui proses swapping paging file di secondary storage ke main memory (Kondisi ini kemungkinan besar terjadi apabila komputer menjalankan banyak aplikasi / menjalankan aplikasi besar sehingga resource main memory tidak cukup). Kondisi swapping memory terlalu sering disebut thrashing.
    
6.  Dapat mengurangi jangka waktu hidup (lifespan) dari secondary storage karena proses swapping melibatkan banyak proses write pada secondary storage.

### Memory Leak
Memory leak adalah sebuah kondisi dimana suatu process yang sudah selesai memakai resource yang dialokasikan (heap) tetapi lupa membebaskannya / dealokasi sehingga resource tersebut tetap ditahan untuk process tersebut.

Contoh Kondisi yang menyebabkan Memory Leak:

 -   Program yang lupa mendealokasikan resource memory-nya, terutama program yang memiliki tujuan sebagai daemon, karena program bertujuan tidak pernah terminate OS tidak dapat mendealokasikan memory secara otomatis (OS Modern)
    
-   Pada program java, penggunaan static variabel yang berlebih (static variable menyimpan value yang besar) dapat menyebabkan memory leakage karena Java garbage collector tidak dapat mendealokasi memory yang dipakai static variable.

### Memory Allocation
#### System Call:
1. brk()  
brk() adalah system call yang men-set address akhir dari data segment (program break) dari suatu proses sesuai parameter address yang diberikan. brk() akan me-return value 0 apabila system call berhasil dan -1 dan error ENOMEM apabila gagal.
2. sbrk()
sbrk() adalah system call yang meng-increment address dari akhir dari suatu proses sesuai dengan parameter increment yang diberikan. sbrk() akan mengembalikan pointer address program break setelah increment apabila berhasil (jika increment yang dimasukkan 0 akan mengembalikan akhir dari data segment proses tanpa increment) dan apabila gagal akan me-return hal yang sama dengan brk().

#### Library Call
1. Malloc()  
malloc adalah library call yang digunakan untuk mengalokasi memory sesuai dengan parameter size yang dimasukkan ke dalam fungsi malloc(). malloc akan bekerja mencari free block list yang sesuai dengan parameter sizenya di dalam heap. Apabila heap tidak cukup, malloc akan mengimplementasikan system call sbrk() untuk menambah ukuran heap (menambah address program break). malloc akan mengembalikan pointer ke allocate memory apabila berhasil dan NULL apabila gagal.
	 - Malloc menjaga konsistensi free block list dengan menjaga konsistensi next pointer dan previous pointer pada free block list

2. Free()
Free adalah library call yang mengembalikan allocated memory kembali kedalam free block list. free menerima parameter pointer address allocated memory. Pemanggilan free tidak menjamin mengurangi address program break karena bisa saja memory yang dialokasikan berada di tengah heap.

	- Untuk Alokasi memory, pemanggilan free lebih disarankan daripada brk() karena alasan berikut:
		-   Memory block yang dibebaskan biasanya berada di tengah-tengah heap daripada di akhir heap sehingga menurunkan program break tidak dimungkinkan
    
		-   Menurunkan penggunaan system call sbrk() untuk meningkatkan performa (pemanggilan banyak system call menyebabkan banyak melakukan switch processor mode (kernel dan user))
    
-   Di beberapa program yang mengalokasikan memory yang besar cenderung menahan memory yang sudah dialokasikan atau secara berulang melepaskan dan mengalokasikan kembali memory dibanding melepaskannya secara langsung dan lanjut menjalankan tugasnya
