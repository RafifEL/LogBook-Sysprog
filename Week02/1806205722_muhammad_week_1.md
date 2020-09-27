# Log Week 02

## System Call, User Mode and Kernel Mode

### System Call  
System adalah sebuah interface bagi user untuk melakukan request terhadap service yang disediakan operating system. System call dibutuhkan saat aplikasi meminta resource dari hardware. Jika tidak memakai system call maka terdapat kemungkinan aplikasi dapat merusak operating system.

### Priviledge
 - Kernel Mode
Priviledge dimana CPU dapat bebas mengakses langsung resource komputer
 - User Mode
 Priviledge dimana CPU tidak dapat bebas mengakses resource komputer. Jika ingin mengakses resource harus melalui system call.

### Sytem Call Error Code
System call biasanya memberi nilai return -1 kalau system call itu gagal, akan tetapi tidak semua system call. Cara yang baik untuk mendeteksi system call berhasil / tidak dengan melihat global variables errno, dimana dalam code program harus menginclude file header errno.h. berikut contoh error code dan penjelasannya.
<pre>
errno 		        Error

1 			/* Operation not permitted */

2 			/* No such file or directory */

3 			/* No such process */

4 			/* Interrupted system call */

5 			/* I/O error */

6 			/* No such device or address */

7 			/* Argument list too long */

8 			/* Exec format error */

9 			/* Bad file number */

10 			/* No child processes */

11 			/* Try again */

12 			/* Out of memory */

13 			/* Permission denied */
</pre>

### Contoh System Call
-   fork()  
fork adalah system call yang membuat process baru yang disebut child process. program yang memanggil fork pertama disebut parent process. parent process dan child process akan berjalan secara concurrent. return value fork bergantung terhadap beberapa hal, yaitu:
	-   -1, Jika system call gagal
    
	-   0, Jika process adalah child process
    
	-   Positive value, Jika process parent, nilai return berubah PID child process
-   getpid()
	-System call yang memberi process ID (PID) yang memanggilnya.

### Langkah-langkah System Call
1.  program akan menjalankan baris kode system call di user space
    
2.  system calls user space memiliki mekanisme yang memanggil sebuah trap instruction. 
    
3.  trap instruction akan mengubah mode bit menjadi 0 (ganti priviledge ke kernel space), menyimpan context (old PC, register) di kernel stack, melihat IDT (Interrupt Descriptor Table) dan melakukan jump ke fungsi trap handler 
    
4.  Funsgi trap handler akan memanggil system call kernel.
    
5.  Setelah system call kernel berjalan, trap handler akan mengubah mode bit menjadi 1 (ganti privildge ke user space), mengembalikan context dari CPU register dari kernel stack dan kembali ke code user setelah system call user space.
    
6.  Program lanjut menjalankan code sisanya.

## Library Function
Library function adalah sebuah program yang memanggil system call, biasanya sebagai interface lanjut dari system call yang diberi fungsionalitas tambahan. Pemakaian library function ini dianjurkan karena library function lebih portable, sebagian system call berbeda di tiap sistem sehingga kurang portable. Library Function juga mudah di debug dibandingkan system call karena library function berjalan di user space dan bukan di kernel space.

### Contoh Library Function
1.  fopen()  
fopen() used open() system call to open file. fopen() buffered I/O service to open file while open() doesn’t provide the service.
2.  malloc()  
malloc() calls brk() or sbrk() for memory allocation
3.  printf()  
printf() calls write() system call to write in terminal / command prompt.
