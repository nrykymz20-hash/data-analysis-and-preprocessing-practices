# NumPy Fundamentals & Hands-on Practice

Welcome to my NumPy learning repository! This repository tracks my step-by-step progress in mastering fundamental data science tools in Python using Jupyter Notebooks.

## 📌 Topics Covered

### Module 01: `01_numpy_basics.ipynb`
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

### Module 02: `02_array_manipulation.ipynb`
- **Array Reshaping & Dynamic Inference:** 
  - Altering array dimensions using `.reshape()`.
  - Utilizing dynamic dimension calculation with `-1`.
  - Transforming arrays into 1D sequences, Row Vectors `(1, N)`, and Column Vectors `(N, 1)`.
- **Flattening Techniques:** 
  - Collapsing multi-dimensional arrays into a single dimension.
  - Comparing `.flatten()` vs. `.ravel()` vs. `.reshape(-1)`.
- **Memory Ownership Verification:** 
  - Evaluating memory allocation behavior (Copy vs. View) using `.base`.
  - Performance trade-offs between shared memory views and deep copies.

## 🛠️ Key Takeaways & Rules of Thumb

1. **Square Brackets `[...]` for Indexing:** Always use `[]` for slicing and filtering. Round brackets `()` are strictly reserved for function calls.
2. **Slicing Syntax:** Follows `[start:stop:step]` where the `stop` index is excluded.
3. **3D Array Syntax:** Access elements using `[depth/matrix_index, row_index, column_index]`.
4. **Memory Isolation:** Modifying a view mutates the original source array. Use `.copy()` or `.flatten()` when data independence is required.
5. **Flattening Strategy:** Use `.ravel()` or `.reshape(-1)` for fast, memory-efficient operations (View); use `.flatten()` when you need a safe, isolated copy.

---
*Maintained as part of my Data Science learning journey.*
