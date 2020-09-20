# Log Week 01

## System Programming dan Application Programming

System Programming  
Programming yang menggunakan bahasa low-level, seperti C, Assembly, dll yang bertujuan untuk menciptakan program yang mengelola hardware computer. Hasil dari system programming ini juga menjadi jembatan antara application program dan hardware agar dapat dijalankan.

Application Programming
Programming yang menggunakan bahasa high-level, seperti Java, Python, Ruby, dll yang bertujuan untuk menciptakan program yang menjalakan tugas khusus bagi user secara langsung. 

## Programming Language
Programming Language ada dua jenis berdasarkan cara menjalankannya, compiled language dan scripting language.
*  Compiled Language  
	Bahasa Pemrogaman yang perlu di compile terlebih dahulu menjadi bahasa mesin sebelum dijalankan. 
* Scripting Language  
	Bahasa Pemrogaman yang tidak perlu di-compile menjadi bahasa mesin sebelum dijalankan, scriptnya akan diterjemahkan secara langsung menjadi bahasa mesin oleh intrepeter. Akibatnya runtime scripting language lebih lambat dibanding compiled language

## Kernel dan Operating System

Kernel  
Inti dari operating system yang mengontrol semuanya yang ada di system. Kernel berfungsi sebagai jembatan antara system sofware dan hardware agar system software dapat berjalan.

Operating System  
Operating System merupakan program yang mengelola system resource, hardware dan layanan-layanan inti dari sebuah computer. OS merupakan jembatan antara user dan hardware (komputer) yang memudahkan user untuk "Berkomunikasi" dengan komputer.

## Program dan Process
Program  
Program adalah himpunan instruksi komputer untuk menjalankan suatu tugas. Program disimpan di dalam secondary storage (HDD, SDD, dll).

Process  
Process adalah sesuatu yang dibuat oleh operating system saat Program akan dieksekusi yang berfungsu menyediakan resource agar program tersebut berjalan.

### Process Part

 1. Code  
 Code mengandung program code yang sudah di-compile dan code library yang dibutuhkan oleh program.
 2. Data  
 Data mengandung global variables dan static variabel yang dibutuhkan program
 3. Stack  
 Stack berisi local variabel yang telah dideklarasikan.
 4. Heap  
 Heap Mengandung memory resource dinamis yang dialokasikan oleh process dan dapat dipanggil dengan command new, delete, malloc, etc.
 6. Shared Heap  
 Shared mengandung jenis alokasi memori lainnya, seperti shared memory dan mapped memory.
 
 # Linux

## Absolute Path dan Relative Path

Absolute Path : Path yang dimuali dari root (/)  
Relative Path : Path yang dimulai dari current working directory

## Linux FHS
FHS adalah struktur directory default bagi Unix-Like OS.

1. / (Root)  
Directory utama dari FHS, mengandung semua file dan direktori)

2.  /bin and /sbin
Tempat menyimpan code command-command do linux, perbedaannya command /sbin biasanya membutuhkan superuser priviledge.

3.  /boot  
Tempat menyimpan file yang diperlukan untuk boot seperti bootloader file, etc.

4.  /dev  
Tempat khusus menyimpan device file computer (Storage, mouse, keyboard, dll)

5.  /home  
Tempat menyimpan file personal user, seperti user settings, file personal, etc.

6.  /lib  
tempat menyimpan libraries yang dibutuhkan oleh command yang ada /sbin dan /bin

7.  /media 
mounting point untuk eksternal storage.

8.  /mnt  
mounting point sementara, biasanya diapakai saat ingin mengurus masalah partisi.

9.  /opt  
direktori untuk menyimpan package tamabahan software, biasanya dari software vendor.

10.  /srv  
tempat menyimpan site-specific-data yang dikirim oleh sistem ini, akan terisi apabila sistem linux dijadikan sebuah web server, ftp server dan server lainnya.

11.  /tmp  
menyimpan file sementara yang dibutuhkan oleh program atau file download sementara

12.  /usr  
Hirarki kedua, menyimpan shared read-only data untuk user yang banyak, seperti binaries, libraries, etc.

13.  /proc  
virtual file system yang memberi informasi process, kernel dalam bentuk sebuah file.

14.  /etc  
menyimpan jenis file-file lain seperti file config, file socket, dll. 
