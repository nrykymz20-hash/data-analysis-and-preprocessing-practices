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

## 📁 Repository Structure

```text
numpy-fundamentals/
├── 01_numpy_basics/
│   └── 01_numpy_basics.ipynb       # Module 01 notebook
├── 02_array_manipulation/
│   └── 02_array_manipulation.ipynb # Module 02 notebook
└── README.md                       # Main repository documentation
