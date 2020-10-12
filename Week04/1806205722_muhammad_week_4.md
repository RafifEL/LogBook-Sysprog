# Log Week 04

## Process

### Program, Process, and PID

 - Program  
 Program adalah sebuah himpunan instruksi untuk melaksanakan tugas tertentu yang terletak di dalam disk (secondary drive)
 - Process  
Process adalah suatu instansi pelaksanaan dari instruksi-instruksi yang ada di program. Instruksi dari program dimasukkan ke dalam memory dan dijalankan menjadi sebuah process. Umumnya, process tidak dapat berbagi resources satu sama lain (kecuali hasil fork() yang memanfaatkan tekhnik copy-on-write). 
 - Thread  
Thread adalah satuan unit sebuah process yang menjalankan suatu tugas spesifik tertentu untuk process. Sebuah process dapat memiliki banyak thread. thread yang dimiliki oleh process yang sama dapat berbagi resource karena resource yang diambil dari process yang sama.

### PID dan PPID
PID adalah ID untuk mengidentifikasi suatu process.
PPID adalah Process ID dari parent process sebuah ID.

PID dan PPID dibutuhkan sebagai sebuah representasi dari hirarki dari semua process yang aktif dan apabila ada sebuah process yang memakan terlalu banyak resoureces, kita dapat melakukan "kill" pada process tersebut. PPID juga berguna untuk menghilangkan zombie process dengan melakukan "kill" pada parent process.

### Zombie, Orphan dan Daemon process

 - Zombie  
Zombie process adalah suatu process diamana process tersebut sudah menyelesaikan instruksinya akan tetapi parent process belum membaca status exit dari proses tersebut yang menyebabkan process tersebut masih terdapat di process table, walaupun resourcesnya sudah dialokasikan ke process yang lain. Terlalu banyakzombie dapat menyebabkan process table penuh dan tidak dapat memuat process lain.
**Cara mencegah zombie process :**
 Menggunakan system call wait() untuk parent process
 Mengabaikan signal childprocess dengan **signal(SIGCHLD,SIG_IGN)**
 Membuat custom handler untuk signa; **SIGCHLD**
 - Orphaned Process  
 Orphaned process adalah process dimana parent process sudah menyelesaikan eksekusi dan terminate, sedangkan proses tersebut belum melakukan terminate. Process akan tidak memiliki parent yang kemudian akan diadopsi oleh **init** process
 - Daemon process  
 Process yang disengaja dibuat menjadi orphaned agar dapat berjalan sebagai background proses (tidak terikat dengan terminal, hanya terikat pada init process)
 
### Command PS
PS adalah command terminal linux untuk mengetahui informai tentang proses-proses yang aktif yang dapat membantu dalam manajemen resource
opsi. 
tips dan trik berguna untuk menggunakan command PS:  
https://www.tecmint.com/ps-command-examples-for-linux-process-monitoring/

Penjelasan field dalam command PS:
-   PID : Process ID number
    
-   USER : username of who owned the process
    
-   PR : Value of priority number value, it shows process actual priority in kernel space. Range from 1(highest priority) until 140(lowest priority).
    
-   NI: nice value, it shows process priority in user space concept. Number range from -20 (Highest priority) and 20 (lowest priority)
    
-   VIRT: Showing full size of memory (Virtual )that used by task, whether its on ram or disk(shared objects, mmaped files, swap area) in KiB format.
    
-   RSS : resident set size, it shows how much memory allocated in physical space (RAM) for the process in KiB
    
-   %CPU : showing CPU utilization of the process in percentage
    
-   %MEM : showing ratio of the process resident set size to the physical memory.
    
-   TIME+ : showing cpu time used on a process with format “minutes:seconds.hundredths”

### fork()
-   fork()  
fork adalah system call yang membuat process baru yang disebut child process yang identik dengan parent process. Parent process dan child process akan berjalan secara concurrent. return value fork bergantung terhadap beberapa hal, yaitu:
	-   -1, Jika system call gagal
    
	-   0, Jika process adalah child process
    
	-   Positive value, Jika process parent, nilai return berubah PID child process
 
 Fork menerapkan teknik copy-on-write dimana apabila melakukan fork, ponter resource yang diberikan pada child dan parent sama sampai salah satu dari process tersebut melakukan modifikasi isi pada resource, child process akan diberikan copy dari resource yang sama dari parent.
