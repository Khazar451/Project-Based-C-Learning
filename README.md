# Project-Based-C-Learning

My personal lab for mastering C. Instead of just learning syntax, I'm building the underlying systems that power modern software — from scratch.

---

## Philosophy

The best way to truly understand C is to build real systems with it. This repository contains low-level implementations of fundamental components that are normally hidden behind standard library calls or operating system abstractions. Each project is designed to deepen understanding of memory, systems programming, and the C language itself.

---

## Projects

### 1. Custom Memory Allocator (`memory_allocator.c`)

A from-scratch implementation of the C standard library memory management functions using `sbrk` system calls and a free-list approach.

**Implements:**
- `malloc(size_t size)` — Allocates a block of memory of the given size.
- `free(void *block)` — Frees a previously allocated block; releases memory back to the OS if it sits at the program break.
- `calloc(size_t num, size_t nsize)` — Allocates zero-initialized memory for an array of `num` elements of `nsize` bytes each.
- `realloc(void *block, size_t size)` — Resizes a previously allocated block.

**Key concepts covered:**
- Program break (`sbrk`) and heap management
- Free-list data structure with a linked list of block headers
- Memory alignment (16-byte aligned headers via a union)
- Thread safety using `pthread_mutex_t`
- Multiplicative overflow detection in `calloc`

**How to compile and test:**

```bash
# Compile as a shared library to override the system allocator
gcc -o memory_allocator.so -shared -fPIC memory_allocator.c -lpthread

# Use it with any program via LD_PRELOAD
LD_PRELOAD=./memory_allocator.so ./your_program
```

---

## Prerequisites

- GCC or Clang
- A Linux environment (the allocator uses `sbrk`, which is Linux/Unix-specific)
- POSIX threads (`-lpthread`)

---

## Roadmap

Projects planned or in progress:

- [x] Custom memory allocator (`malloc`/`free`/`calloc`/`realloc`)
- [ ] Shell (command-line interpreter)
- [ ] HTTP server
- [ ] Custom Compiler
- [ ] File I/O library

---

## Resources

- [`sbrk(2)` man page](https://man7.org/linux/man-pages/man2/brk.2.html)
- [Write a Memory Allocator](https://github.com/arjun024/memalloc)
