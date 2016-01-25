
Assembly and low-level programming
==================================

List of Linux system calls (Ubuntu) : ::

    /usr/include/x86_64-linux-gnu/asm/unistd_32.h

Assembling and linking with NASM : ::

    nasm -f elf64 test.s
    ld -s -o test test.o

Compiling C program step by step : ::

    # Preprocessing
    cpp dick.c dick.i
    # Code generation
    /usr/lib/gcc/x86_64-linux-gnu/5/cc1 dick.i -o dick.s
    # Assembling (64 bits)
    as --64 dick.s -o dick.o
    # Linking (64 bits)
    # -lc : link with libc (/usr/lib/x86_64-linux-gnu/libc.a)
    # -e main : program entry point (default is _start)
    # -dynamic-linker [...] : use the 64 bits linker
    ld -lc -e main -o dick -dynamic-linker /lib64/ld-linux-x86-64.so.2 dick.o

