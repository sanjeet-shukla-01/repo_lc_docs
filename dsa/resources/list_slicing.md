# Python List Slicing & Sub-setting Cheat Sheet

Python list slicing follows the core syntax: **`sequence[start:stop:step]`**
* **`start`**: The index where the slice begins (inclusive).
* **`stop`**: The index where the slice ends (exclusive).
* **`step`**: The increment value (stride) between elements.

---

### 1. Basic Slicing
* `arr[a:b]` – Items from index `a` up to (but not including) `b`.
* `arr[a:]` – Items from index `a` to the very end of the list.
* `arr[:b]` – Items from the beginning up to (but not including) `b`.
* `arr[:]` – Creates a shallow copy of the entire list.

### 2. Negative Indexing (Counting from the End)
* `arr[-1]` – The last item in the list.
* `arr[-n:]` – The last `n` items of the list.
* `arr[:-n]` – All items except the last `n` items.

### 3. Stepping (Strides)
* `arr[::2]` – Every second item in the list (indices 0, 2, 4...).
* `arr[1::2]` – Every second item starting from index 1 (indices 1, 3, 5...).
* `arr[::-1]` – Reverses the entire list.

### 4. In-Place Modification (Overwriting Lists)
* `arr[a:b] = [x, y]` – Replaces the segment from `a` to `b` with new elements.
* `arr[:] = ...` – Modifies the original list in-place without changing its memory reference.
* `del arr[a:b]` – Deletes a specific slice from the list.
