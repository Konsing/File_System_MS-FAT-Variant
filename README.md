
---

# **📄 MS-FAT Variant Filesystem**
🚀 **A simple FAT-like filesystem implemented in C.**  
This project implements a **Minimalist FAT-style File System (MS-FAT)** that manages files efficiently using a **block-based virtual disk**.

---

## **📌 Features**
✔ **Virtual Disk Implementation** – Uses a block-based virtual disk for file operations.  
✔ **File Creation & Management** – Supports creating, opening, writing, reading, and deleting files.  
✔ **Custom Disk I/O Operations** – Reads/writes blocks using `disk.c` and `disk.h`.  
✔ **Error Handling & Debugging** – Includes built-in assertions and logging for debugging.  
✔ **Shell Utilities** – `simple_writer.c` and `simple_reader.c` for testing file operations.  

---

## **📂 Project Structure**
```
MS-FAT/
│── apps/                # Applications to test filesystem
│   ├── Makefile         # Makefile for building test programs
│   ├── fs_make.x        # Utility for formatting the filesystem
│   ├── fs_ref.x         # Reference filesystem implementation
│   ├── simple_reader.c  # Reads files from MS-FAT
│   ├── simple_writer.c  # Writes files to MS-FAT
│   ├── test_fs.c        # Filesystem test cases
│   ├── tester_grade.sh  # Automated testing script
│
│── libfs/               # Core filesystem implementation
│   ├── Makefile         # Makefile for building filesystem library
│   ├── disk.c           # Virtual disk implementation
│   ├── disk.h           # Disk I/O function prototypes
│   ├── fs.c             # Core filesystem logic
│   ├── fs.h             # Filesystem function prototypes
│
│── Makefile.txt         # Main Makefile (may need renaming)
```
---

## **🛠️ Building the Filesystem**
### **1️⃣ Clone the Repository**
```sh
git clone https://github.com/YOUR_GITHUB/MS-FAT.git
cd MS-FAT
```

### **2️⃣ Compile the Filesystem**
Navigate to `libfs/` and compile the filesystem library:
```sh
cd libfs
make
```
Navigate to `apps/` and compile test applications:
```sh
cd ../apps
make
```

---

## **📄 Filesystem Components**
### **🗃️ Virtual Disk (`disk.c`, `disk.h`)**
- Implements **low-level block operations** (`block_read`, `block_write`).
- Provides **disk mounting/unmounting** functionality.
- Ensures **data integrity** with error handling.

### **📁 Filesystem Core (`fs.c`, `fs.h`)**
- Implements **file operations**: `fs_create`, `fs_open`, `fs_write`, `fs_read`, `fs_delete`.
- Manages **directory structure** and **free block allocation**.
- Handles **filesystem mounting/unmounting**.

---

## **📝 Example Usage**
### **🔹 Writing to a File (`simple_writer.c`)**
This program:
1. **Mounts the disk**.
2. **Creates four files** (`myfile`, `myfile2`, etc.).
3. **Writes data** to the files.
4. **Deletes them** after writing.

```c
ret = fs_create("myfile");
ASSERT(!ret, "fs_create");

fd = fs_open("myfile");
ASSERT(fd >= 0, "fs_open");

fs_lseek(fd, fs_stat(fd));
ret = fs_write(fd, abc, 7176);
ASSERT(ret == 7176, "fs_write");

fs_close(fd);
fs_delete("myfile");
fs_umount();
```

### **🔹 Reading from a File (`simple_reader.c`)**
This program:
1. **Mounts the disk**.
2. **Creates a file (`myfile`)**.
3. **Writes a test string (`abcdefghijklmnopqrstuvwxyz`)**.
4. **Reads the data back**.

```c
fd = fs_open("myfile");
ASSERT(fd >= 0, "fs_open");

ret = fs_write(fd, data, sizeof(data));
ASSERT(ret == sizeof(data), "fs_write");

fs_close(fd);
fs_umount();
```

---

## **📌 Running the Tests**
1️⃣ **Create a virtual disk image**  
```sh
./fs_make.x disk.img 1024  # Creates a 1024-block disk image
```
2️⃣ **Run the filesystem tests**  
```sh
./test_fs disk.img
```
3️⃣ **Use the reader and writer utilities**  
```sh
./simple_writer disk.img
./simple_reader disk.img
```

---

## **📜 License**
This project is licensed under the **MIT License**.

---