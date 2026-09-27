# NumPy Fundamentals & Hands-on Practice

Welcome to my NumPy learning repository! This repository tracks my step-by-step progress in mastering fundamental data science tools in Python using Jupyter Notebooks.

---

## 📌 Topics Covered

### Module 01: NumPy Basics (`01_numpy_basics.ipynb`)
- **Array Creation & Structure:** Working with 1D, 2D, and 3D NumPy arrays (`np.array`).
- **Indexing & Slicing:** Efficiently accessing elements, full rows, matrices, and slicing multi-dimensional arrays (`[matrix, row, column]`).
- **Data Types (`dtypes`) & Precision:** 
  - Explicitly specifying data types (`int32`, `float32`, `float64`).
  - Analyzing memory and floating-point precision differences between `float32` and `float64`.
  - Comprehensive Dtype Registry (integers, floats, Unicode strings, objects, datetimes).
- **Memory Architecture (`Copy` vs. `View`):**
  - Independent memory buffer allocation using `.copy()`.
  - Shared memory pointers via `.view()` and slicing implications.
  - Verifying array memory ownership using the `.base` attribute.
- **Boolean Masking (Conditional Selection):** Filtering array elements based on logical conditions (e.g., `arr[arr > 15]`).
- **Common Pitfalls & Debugging:** 
  - Resolving `TypeError: 'numpy.ndarray' object is not callable` (using `[]` instead of `()`).
  - Handling variable redefinition issues (`np.array = [...]`) and managing Jupyter Kernel restarts.

---

### Module 02: Array Manipulation & Memory Architecture (`02_array_manipulation.ipynb`)

Focuses on array reshaping, transposing, flipping, joining/stacking, and splitting, with an emphasis on understanding NumPy's underlying **Memory Management Architecture** (Views vs. Deep Copies).

#### 📌 Key Takeaways & Core Concepts

1. **Shape Transformations & Metadata Operations (Views):**
   - Altering the shape or orientation of an array (`reshape`, `transpose`/`.T`, `swapaxes`, `flip`) creates a **View**. 
   - These operations modify only the **metadata** (shape and strides) without moving or duplicating elements in the underlying contiguous memory buffer ($O(1)$ time and memory complexity).

2. **Array Joining & Allocation (Deep Copies):**
   - Combining distinct arrays (`concatenate`, `stack`, `vstack`, `hstack`, `dstack`, `column_stack`) requires allocating a **brand-new contiguous memory block** (**Deep Copy**, $O(N)$ memory complexity).
   - `result.base` evaluates to `None` for joining operations.

3. **Array Splitting & Slicing (Views):**
   - Dividing existing arrays into sub-arrays (`split`, `vsplit`, `hsplit`, `dsplit`) returns **Views** of the parent memory buffer.
   - Modifying a sub-array mutates the original parent array, and `sub_array.base` references the original parent object.

#### 🛠️ Summary of Operations & Memory Behavior

| Operation Category | Functions / Methods | Target Axis / Dimension | Memory Behavior | `.base` Property | Time/Memory Overhead |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Reshaping** | `.reshape()`, `.ravel()` | All axes | **View** (usually) | References Parent | $O(1)$ |
| **Flattening** | `.flatten()` | All axes (to 1D) | **Deep Copy** | `None` | $O(N)$ |
| **Transposing** | `.T`, `.transpose()`, `.swapaxes()` | Axis Permutation | **View** | References Parent | $O(1)$ |
| **Flipping** | `np.flip()` | Specified axis | **View** | References Parent | $O(1)$ |
| **Joining / Stacking** | `np.concatenate()`, `np.vstack()`, `np.hstack()`, `np.stack()`, `np.dstack()`, `np.column_stack()` | Axis 0, 1, 2, or New Axis | **Deep Copy** | `None` | $O(N)$ |
| **Splitting** | `np.split()`, `np.vsplit()`, `np.hsplit()`, `np.dsplit()` | Axis 0, 1, or 2 | **View** | References Parent | $O(1)$ |

#### 📏 Dimensionality Rules Cheat Sheet

- **`np.hstack` vs. `np.column_stack`:**
  - For 1D arrays, `np.hstack` concatenates end-to-end into a **1D array** shape `(N1+N2,)`.
  - `np.column_stack` stacks 1D arrays as columns into a **2D matrix** shape `(N, 2)`.
- **`np.stack` vs. `np.concatenate`:**
  - `np.concatenate` joins along an *existing* axis (dimension count remains unchanged).
  - `np.stack` joins along a *new axis* (dimension count increases by 1).
- **`np.dstack` / `np.dsplit`:**
  - Operates along the 3rd dimension (`axis=2`, depth). 2D arrays stacked via `dstack` become a **3D array** shape `(rows, cols, depth)`.

> ⚠️ **NumPy 2.0 API Note:** `np.row_stack` has been removed. Use `np.vstack` for vertical row-wise stacking.

#### 💡 Rules of Thumb

- **Joining Allocates ($O(N)$):** Combining separate buffers creates a new array (**Copy**).
- **Splitting Slices ($O(1)$):** Slicing/splitting an existing array computes new strided offsets over the parent buffer (**View**).
- **Metadata Is Cheap ($O(1)$):** Reshaping, transposing, and flipping only update shape/stride metadata.

---

### Module 03: Searching & Sorting Operations (`03_searching_and_sorting.ipynb`)

Focuses on vector searching, binary search lookup, conditional evaluation, indexing algorithms, and linear-time partial selection mechanics.

#### 📌 Key Takeaways & Core Concepts

1. **In-Place vs. Out-of-Place Sorting:**
   - `np.sort(a)` returns a sorted **Deep Copy** ($O(N)$ memory), whereas `a.sort()` mutates the array **In-Place** ($O(1)$ auxiliary memory).
   - Indirect sorting with `np.argsort()` yields sorting integer indices, essential for maintaining relational alignment across associated arrays.

2. **Logarithmic Lookup ($O(\log N)$):**
   - `np.searchsorted()` executes a binary search over pre-sorted arrays.
   - The `side` parameter controls insertion bounds for duplicate values (`side='left'` inserts before existing duplicates, `side='right'` inserts after).

3. **Conditional Indexing & Set Membership:**
   - Vectorized ternary branching with `np.where(cond, x, y)` and set evaluation via `np.isin(element, test)` return boolean arrays for memory-efficient masking (`arr[mask]`).
   - `np.nonzero()` and `np.flatnonzero()` extract non-zero array coordinate tuples and linear indices respectively.

4. **Linear-Time Partial Selection ($O(N)$):**
   - `np.partition()` and `np.argpartition()` rearrange arrays around the $k$-th position in linear time $O(N)$, outperforming full sorting $O(N \log N)$ when selecting Top-$K$ or Bottom-$K$ elements.

#### 🛠️ Summary of Operations & Complexity

| Function / Method | Primary Functionality | Average Time Complexity | Auxiliary Space Complexity | Memory Ownership Output |
| :--- | :--- | :--- | :--- | :--- |
| **`np.sort(a)`** | Returns a sorted copy of an array | $O(N \log N)$ | $O(N)$ | **New Array (Copy)** (`.base is None`) |
| **`a.sort()`** | Sorts array directly in-place | $O(N \log N)$ | $O(1)$ | **In-Place Mutation** (Returns `None`) |
| **`np.argsort(a)`** | Returns indices that would sort an array | $O(N \log N)$ | $O(N)$ | **New Array (Copy)** of integer indices |
| **`np.where(cond)`** | Returns index tuple where condition is `True` | $O(N)$ | $O(N)$ | **New Tuple of Arrays** |
| **`np.where(cond, x, y)`** | Element-wise ternary substitution | $O(N)$ | $O(N)$ | **New Array (Copy)** |
| **`np.searchsorted(a, v)`**| Binary search for insertion indices | $O(K \log N)$ | $O(K)$ | **New Array (Copy)** of integer indices |
| **`np.isin(element, test)`**| Vectorized set membership evaluation | $O(N \times M)$ | $O(N)$ | **New Boolean Mask Array** |
| **`np.nonzero(a)`** | Returns tuple of non-zero element indices | $O(N)$ | $O(N)$ | **New Tuple of Arrays** |
| **`np.flatnonzero(a)`** | Returns 1D non-zero indices on flattened view | $O(N)$ | $O(N)$ | **New 1D Array (Copy)** |
| **`np.lexsort(keys)`** | Indirect stable multi-key sort | $O(N \log N)$ | $O(N)$ | **New Array (Copy)** of integer indices |
| **`np.partition(a, kth)`**| Partial sorting around the $k$-th element | $O(N)$ | $O(N)$ | **New Array (Copy)** |

#### 💡 Rules of Thumb

- **In-Place for Memory ($O(1)$):** Use `a.sort()` on large arrays when memory efficiency is primary.
- **Binary Search Needs Sorting ($O(\log N)$):** Always sort base arrays before using `np.searchsorted()`.
- **Top-K Efficiency ($O(N)$ vs $O(N \log N)$):** Never use `np.sort()` if you only need Top-$K$ values; use `np.partition()` instead.

---

## 📁 Repository Structure

```text
numpy-fundamentals/
├── 01_numpy_basics/
│   └── 01_numpy_basics.ipynb       # Module 01 notebook
├── 02_array_manipulation/
│   └── 02_array_manipulation.ipynb # Module 02 notebook
├── 03_searching_and_sorting/
│   └── 03_searching_and_sorting.ipynb # Module 03 notebook
└── README.md                       # Main repository documentation
