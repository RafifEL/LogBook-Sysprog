# Log Week 04

## WS 6 - Make, Stdio, and Buffering

### MakeFile
MakeFile adalah suatu script yang membantu proses building program yang berisi shell command. make adalah utility dari unix yang mengeksekusi script make file.

Komponen dalam make file:

 1. Variables  
 menyimpan variables yang dibutukan makefile
 format:
 ```
		LINUX_EXE = large_file
 ```
 2. Target, prequisite, dan recipe      	
 target adalah command yang dipanggil yang berisi recipe yang berupa command-command shell. Target dapat memiliki prequisite yang akan dieksekusi sebelum recipe target dijalankan.
 format:
 ```
		target: prerequisites  
		<TAB> recipe
 ```
 3. .PHONY  
 special target

### Buffer
Buffer adalah suatu area memory (RAM) yang berfungsi menyimpan data sementara dalam waktu singkat dimana data tersebut dibutuhkan untuk melakukan suatu operasi (biasanya operasi yang berhubungan dengan read and write data di secondary storage)

 #### Cara Buffer bekerja (Read & Write)
![buffer_works](https://i2.wp.com/img-blog.csdnimg.cn/20200608083946806.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3d1amlhbmluZ18xMTAxMTc=,size_16,color_FFFFFF,t_70)  
Buffer bekerja sebagai penampung data dari operasi yang melibatkan secondary storage. Gambar diatas menggambarkan proses menuliskan user data ke dalam secondary storage. User data yang akan dituliskan dapat melalui 2 cara, melalui stdio library call dan melalui I/O system call. Proses melalui stdio library call pada ujungnya akan memanggil I/O, perbedaannya stdio library call dan system call ini adalah library call menampung datanya terlebih dahulu di stdio buffer untuk meminimalisir penggunaan I/O system call (I/O system call mahal karena memerlukan switch dari user space kernel space). Write akan memindahkan data ke kernel buffer cache dan kemudian kernel akan menuliskan data ke secondary storage dari kernel buffer cache tersebut. Untuk proses read hampir sama, hanya dibalik saja urutannya.
 
#### Buffer Size dan Performanya
Semakin besar buffer size, semakin singkat elapsed time dan CPU time dari  system call I/0 dan semakin berkurang CPU usage sampai ke suatu ukuran buffer size dimana penambahan ukuran buffer size tidak mempersingkat elapsed I/0 system call dan mengurangi CPU usagenya, hal ini disebabkan beberapa faktor seperti kecepatan read/write suatu secondary storage, filesytem block size, dll.
![Read time](https://www.javamex.com/tutorials/io/buffer_size_performance.png)

![CPU USAGE](https://www.javamex.com/tutorials/io/buffer_size_cpu.png)

### STDIO
STDIO adalah sebuah library standard input output yang dimiliki oleh C. 
contoh library call.

Contoh library call STDIO:
1. printf()
mencetak string ke terminal
2. fwrite()
menulis string ke suatu file yang ditunjuk file pointer / file stream
3. fflush()  
memaksa mem-flush buffer pada file stream ke system call write
