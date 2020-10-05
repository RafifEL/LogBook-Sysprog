# Log Week 03

## Sytem Call Stat

### Stat
Stat adalah system call yang mengembalikan infromasi sebuah file seperti permission, ukuran file, terakhir dimodifikasi, dll. Informasi tersebut dikelmbalikan dalam bentuk structure / struct di bahasa C bernama stat. berikut isi dari structure stat.
```C
struct  stat {

dev_t  st_dev; /* ID of device containing file */

ino_t  st_ino; /* Inode number */

mode_t  st_mode; /* File type and mode */

nlink_t  st_nlink; /* Number of hard links */

uid_t  st_uid; /* User ID of owner */

gid_t  st_gid; /* Group ID of owner */

dev_t  st_rdev; /* Device ID (if special file) */

off_t  st_size; /* Total size, in bytes */

blksize_t  st_blksize; /* Block size for filesystem I/O */

blkcnt_t  st_blocks; /* Number of 512B blocks allocated */

/* Since Linux 2.6, the kernel supports nanosecond

precision for the following timestamp fields.

For the details before Linux 2.6, see NOTES. */

struct  timespec  st_atim; /* Time of last access */

struct  timespec  st_mtim; /* Time of last modification */

struct  timespec  st_ctim; /* Time of last status change */

#define st_atime st_atim.tv_sec  /* Backward compatibility */

#define st_mtime st_mtim.tv_sec

#define st_ctime st_ctim.tv_sec
};
```
### Macam-Macam Stat
1. stat()  
system call stat yang menerima argumen berupa pathname ke sebuah file. Jika file terbeut berupa symbolic link akan mengembalikan informasi tentang file target dari symbolic link tersebut
2. lstat()    
Serupa dengan stat(), akan tetapi jika menerima path dari sebuah file berupa symbolic link, akan mengembalikan informasi tentang symbolic link tersebut
3. fstat()  
Serupa dengan stat() tetapi menerima argumen berupa file descriptor

### Open File table
Sytem call open() adalah system call yang membuka file dan mengembalikan file descriptor tersebut. System call open() biasanya dibarengi dengan system call close() yang menutup file descriptor

Istilah:
1.  File Descriptor  
File descriptor adalah sebuah integer positive yang memiliki reference sebagai index di open file table yang berisi file description. 
2. File Description
File description adalah sebuah structure bernama file yang menyimpan informasi dari suatu file dan sebagai sebuah abstraksi untuk mendapatkan informasi di Inode Table
3. Inode
Inode adalah sebuah struktur data yang disimpan di disk yang berisi metadata dari sebuah file dan direktori. metadata berisi informasi file / direktori seperti permission, block size, dll.

Unix-Like OS menjunjung universiality of I/O sehingga seluruh input, output, error, process, dll dianggap sebuah file (dirpresentasikan dalam sebuah file) sehinggap kebanyakan memiliki file descriptor. Akan tetapi ada beberapa hal yang tidak memiliki file descriptor, seperti beberapa daemon (biasanya untuk menghindari kasus zombie process)

### System Call open(), close(), read(), write(), lseek()
1. open()  
Membuka file dan mengembalikan file descriptor.  
Flags :  
https://www.gnu.org/software/libc/manual/html_node/Open_002dtime-Flags.html
2. close()  
Menutup file descriptor
3. read()  
read adaslah system call yang berguna untuk membaca file kedalam memory. menerima tiga argumen file, yaitu file descriptor, buffer dan count. buffer adalah memory penempatan data file yang mau dibaca.
4. write()  
write adalah system call yang berguna untuk menulis ke sebuah file. argumen yang diterima sama seperti read(). data dalam buffer read() akan ditulis kedalam file sesuai dengan byte yang diminta.
5. lseek  
lseek adalah system call yang berfungsi mengganti nilai offset dari suatu open file. offset ini yang menentukan dimana file akan mulai di read() / write(). 

keterangan lanjut
https://www.geeksforgeeks.org/input-output-system-calls-c-create-open-close-read-write/  
https://www.tutorialspoint.com/unix_system_calls/lseek.htm  
