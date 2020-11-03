# Log Week 7

## Shell Scripting

Shell script adalah sebuah program yang dituliskan untuk dijalankan oleh Unix/Linux shell. Penulisan program sama logikanya dengan bahasa pemrograman biasa, akan tetapi shell scripting dapat menyertakan command-command dan fitur-fitur yang terdapat di dalam Unix/Linux shell.

### Command-Command Dasar

```shell
echo ##Untuk mencetak string ke terminal
read $VARIABLE ## Membaca input dari user
export ## Menambah variabel ke Environment Variable
```

### Variable

Variable dalam shell script biasanya dituliskan dengan dengan huruf kapital dan saat melakukan assignment ke dalam variable tersebut tanda '=' harus tidak ada whitespace dengan variabel dan value yang mau diassign. Dari yang saya pelajari, Data type dasar shell script adalah String, Numeral dan String tersebut dapat juga menjadi List dengan whitespace dalam string sebagai delimiter

```shell
STRING="Hello World"
## Variable STRING diatas juga merupakan List dengan element "Hello" dan "WORLD"
```

Shell Script Juga mendukung string formatting dengan variabel

```shell
STRING="Hello World"
echo "HALO $STRING"
echo "HALO ${STRING}"
### Kedua output perintah echo sama, yaitu "HALO Hello World"
```

Saat Menjalankan Shell Script di terminal, shell script dapat menerima argumen. argumen dalam shell script disimpan dalam variabel khusus, yaitu $N yang dimana N adalah argumen Ke-N.

```shell
## file tes.sh
echo $1
## Command : ./tes.sh tes
#output :
tes
```

### Conditional Branches

Conditional Branches didukung dalam shell scripting seperti bahasa pemrograman biasanya. berikut contoh conditional branches dalam shell script.

```shell
if [ -z $1 ]; then 
    echo "No file path args"
elif [ -f $1 ]; then
    jq "." $1 > "$( dirname $1)/CLEAN_$( basename $1 )"
else 
    echo "File not exist"
fi
```

Dalam menulis condition, condition berada di dalam "[ ]" dan harus ada whitespace antara condtion dan tanda "[ ]". Untuk menulis body dari if dan elif statement, harus ada tanda  ";" setelah if/else statement dan then, lalu body dari if statement dapat dituliskan. else statement tidak perlu menyertakan hal tersebut. Setiap conditional statement harus ditutup dengan kata fi.

#### Arithmetic Comparisons

| -lt  | <    |
| ---- | ---- |
| -gt  | >    |
| -le  | <=   |
| -ge  | >=   |
| -eq  | ==   |
| -ne  | !=   |

#### String Comparisons

| =     | equal                  |
| ----- | ---------------------- |
| !=    | not equal              |
| <     | less then              |
| >     | greater then           |
| -n s1 | string s1 is not empty |
| -z s1 | string s1 is empty     |

#### Bash File Testing

| -b filename      | Block special file                                         |
| ---------------- | ---------------------------------------------------------- |
| -c filename      | Special character file                                     |
| -d directoryname | Check for directory existence                              |
| -e filename      | Check for file existence                                   |
| -f filename      | Check for regular file existence not a directory           |
| -G filename      | Check if file exists and is owned by effective group ID.   |
| -g filename      | true if file exists and is set-group-id.                   |
| -k filename      | Sticky bit                                                 |
| -L filename      | Symbolic link                                              |
| -O filename      | True if file exists and is owned by the effective user id. |
| -r filename      | Check if file is a readable                                |
| -S filename      | Check if file is socket                                    |
| -s filename      | Check if file is nonzero size                              |
| -u filename      | Check if file set-ser-id bit is set                        |
| -w filename      | Check if file is writable                                  |
| -x filename      | Check if file is executable                                |

### For loop

```shell
# bash for loop
for f in $VARIABLE; do
	echo $f
done 
```

for loop seperti loop pada biasanya, hanya saja body dari for loop dimulai dengan do dan diakhiri dengan done.



### Redirection

``` shell
COMMAND_1 | COMMAND_2 ## Piping menyeragkan output COMMAND_1 menjadi input COMMAND_2

COMMAND_1 > FILE_PATH ## Output Command dibuat menjadi file (Truncate)

COMMAND_1 >> FILE_PATH ## Mengappend file dengan output COMMAND_1

COMMAND_1 < FILE_PATH ## menjadikan file menjadi input ke command
```
Source : https://linuxconfig.org/bash-scripting-tutorial
