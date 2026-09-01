# NumPy Fundamentals & Hands-on Practice

Welcome to my NumPy learning repository! This repository tracks my step-by-step progress in mastering fundamental data science tools in Python using Jupyter Notebooks.

## 📌 Topics Covered in `01_numpy_basics.ipynb`

- **Array Creation & Structure:** Working with 1D, 2D, and 3D NumPy arrays (`np.array`).
- **Indexing & Slicing:** Efficiently accessing elements, full rows, matrices, and slicing multi-dimensional arrays (`[matrix, row, column]`).
- **Data Types (`dtypes`) & Precision:** 
  - Explicitly specifying data types (`int32`, `float32`, `float64`).
  - Analyzing memory and floating-point precision differences between `float32` and `float64`.
- **Boolean Masking (Conditional Selection):** Filtering array elements based on logical conditions (e.g., `arr[arr > 15]`).
- **Common Pitfalls & Debugging:** 
  - Resolving `TypeError: 'numpy.ndarray' object is not callable` (using `[]` instead of `()`).
  - Handling variable redefinition issues (`np.array = [...]`) and managing Jupyter Kernel restarts.

## 🛠️ Key Takeaways & Rules of Thumb

1. **Square Brackets `[...]` for Indexing:** Always use `[]` for slicing and filtering. Round brackets `()` are strictly reserved for function calls.
2. **Slicing Syntax:** Follows `[start:stop:step]` where the `stop` index is excluded.
3. **3D Array Syntax:** Access elements using `[depth/matrix_index, row_index, column_index]`.

---
*Maintained as part of my Data Science learning journey.*
