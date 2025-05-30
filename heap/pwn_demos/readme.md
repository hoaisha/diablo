## Primitives

### Malloc

<details>
<summary><strong>Overlapping chunk</strong></summary>
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

abc


## Techniques


