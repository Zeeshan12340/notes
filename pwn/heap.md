# heap
heap involves dynamically allocated memory which is allocated with malloc/mmap. `malloc()` allocates some memory and `free()` frees a prior allocated chunk. Every non-trivial programs uses the heap, some C functions use heap. ptmalloc doesn't use mmap.

`brk(addr)` expands the end of the data segment to `addr`. The first time heap is used in libc, the data segment is setup. Using malloc adds a `[heap]` section to process mappings.

Bugs
----

If memory isn't explicitly freed, it stays there even if the pointers or references to it are gone.

### Use after free:

When you call free on a pointer which points to a memory region from malloc, it is still there. When memory is freed, it can be reused by the allocator which leads to the program(previous pointer) using previously stored incorrect data/memory