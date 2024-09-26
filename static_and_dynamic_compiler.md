# Static compiler and Dynamic compiler

## GCC (GNU Compiler Collection)

- when compile a '.c' file using gcc, there are four 4 steps:

1. Preprocessing. => #include <file> or #define => copy content from files header and paste source code file. remove all comment
2. Compilation. => During the compilation step, the compiler converts the preprocessed output file to `assembly` language.
3. Assembly => make it in machine language
4. Linking => merge files into a single program by linking the files between them.
   - If we used functions stored inside libraries, it will link it to our file so that the program knows where to look at to find said function. There are two types of libraries:
     - Static libraries (.lib, .a): its code is put inside the binary file, which increase its size;
     - Dynamic libraries (.dll, .so): the name of the library is put inside the binary file and is loaded when first called.
   - By default, gcc use dynamic libraries.
     To stop after Preprocessing step => using

```bash
gcc -E file.c
```

To stop after Compilation step => using

```bash
gcc -S file.c
```

To stop after Assembly step => using

```bash
gcc -c file.c
```

- To compile our “.c” file, we either do gcc file.c, the executable output is then called “a.out” by default or we can give a name to our executable by using

```bash
gcc -o exe_name file.c
```

- It is possible to keep a file for each steps by doing

```bash
gcc file.c -save-temps
```

## Static compiler

- static lib: (.a)

* Example:
  - i have a file is isalpha to check if the character is alphabetic while the other checks if the integer is even

```c
// file main.h
#ifdef MAIN_H
#define MAIN_H

// prototypes
int _iseven(int n);
int _isalpha(int c);

#endif /* MAIN_H*/
```

```c
// file isalpha.c
#include "main.h"
int _isalpha(int c) {
    if (condition) {
        return ...
    }
}
```

- similar with file iseven.c
- Then, stop at step assembly with:

```bash
gcc -c *.c # * => all file c
```

- create the static library using:

```bash
ar cr libname.a *.o
```

- explain command:
  - ar: create, modify, and extract from archives
  - r: Insert the files member... into archive (with replacement)
  - c: Create the archive
  - s: Add an index to the archive, or update it if it already exists
- We can look at the function stored inside the library by using `ar -t lib(name).a`
  - ar: create, modify, and extract from archives
  - t: Display a table listing the contents of archive, or those of the files listed in member... that are present in the archive
- to use libname.a => using command `gcc file.c -L. -l(name)` or `gcc file_exe file.c lib`

## Dynamic compiler

- with the extension “.so” for dynamic libraries. Using libraries enable us to call functions without hard coding them inside the source code file as we can call a lot of different functions depending on the program we are creating.

- How to create dynamic lib:

```bash
gcc -c -fPIC *.c
```

- explain command:
  - c: Compile or assemble the source files, but do not link.
  - fPIC: If supported for the target machine, emit position-independent code, suitable for dynamic linking and avoiding any limit on the size of the global offset table.

```bash
# create lib
gcc -shared -o lib(name).so *.o
```

- explain command:

  - shared: Produce a shared object which can then be linked with other objects to form an executable.
  - o: Place output in file file.

- To verify that we did it correctly and have the right functions as dynamic symbols we can use `nm -D libname.so`.
