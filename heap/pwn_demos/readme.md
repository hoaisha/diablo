## Primitives

Various "pure (heap's) primitives" we can (ab)use for futher exploitation.

### Malloc

<details>
<summary><strong>Overlapping chunk via consolidation</strong></summary>
<p>

- **Foward consolidation**
	- link
	> abc

- **Backward consolidation**
	- link
	> abc

- **Overlapping consolidation**
	- link
	> abc

- **Top consolidation**
	- link
	> abc

- **Overlapping mmap**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Unlinking</strong></summary>
<p>

- **Unsafe unlink**
	- link
	> abc

</p>
</details>

### Tcache

<details>
<summary><strong>Tcache linked list attack</strong></summary>
<p>

- **Tcache poisoning**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Tcache double free</strong></summary>
<p>

- **Tcache key double**
	- link
	> abc

- **Tcache fastbin double**
	- link
	> abc

- **Tcache size double**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Free custom tcache chunk</strong></summary>
<p>

- **Tcache fake chunk**
	- link
	> abc

</p>
</details>

### Fastbin

<details>
<summary><strong>Fastbin linked list attack</strong></summary>
<p>

- **Fastbin poisoning**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Fastbin double free</strong></summary>
<p>

- **Fastbin double**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Free custom fastbin chunk</strong></summary>
<p>

- **Fastbin fake chunk**
	- link
	> abc

</p>
</details>

### Unsortedbin

<details>
<summary><strong>Overlapping chunk via unsortedbin</strong></summary>
<p>

- **Unsortedbin exact fit**
	- link
	> abc

- **Unsortedbin last remainder**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Unsortedbin linked list attack</strong></summary>
<p>

- **Unsortedbin poisoning**
	- link
	> abc

- **Unsortedbin attack (?)**
	- link
	> abc

</p>
</details>

<details>
<summary><strong>Free custom unsortedbin chunk</strong></summary>
<p>

- **Unsortedbin fake chunk**
	- link
	> abc

</p>
</details>

### Largebin

<details>
<summary><strong>Largebin linked/skip list attack</strong></summary>
<p>

- **Largebin linked poisoning**
	- link
	> abc

- **Largebin skip poisoning**
	- link
	> abc

</p>
</details>

### Smallbin

<details>
<summary><strong>Smallbin linked list attack</strong></summary>
<p>

- **Smallbin poisoning**
	- link
	> abc

</p>
</details>

---
## Techniques

Leverage heap's bugs/primitives to get code execution.

### Remote code execution

<details>
<summary><strong>Targetting</strong></summary>
<p>

- **libc GOT entries**
	- [docs](/heap/pwn_demos/targetting/got_libc/readme.md)
	> similar to GOT overwrite...

</p>
</details>

<details>
<summary><strong>Houses</strong></summary>
<p>

- **House of botcake**
	- [docs](/heap/pwn_demos/houses/house_of_botcake/readme.md)
	> **double free primitive**, bypass tcache dbf's key check, making overlapping chunk, return arbitrary allocation...

</p>
</details>

