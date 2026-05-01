# NumPy for Data Analytics — Core Concepts & Operations

> **Complete, practical guide to NumPy covering 11 core topics — array creation, reshaping, slicing, filtering, broadcasting, and real-world DataFrame conversion — with visualizations and a performance benchmark demonstrating NumPy's ~100× speed advantage over Python loops.**

---

## Overview

NumPy (Numerical Python) is the foundational library for scientific computing in Python. Every major data analytics library — pandas, scikit-learn, TensorFlow, PyTorch — builds on NumPy arrays as its core data structure. This notebook demonstrates every core NumPy concept with clean, annotated code, business context, and professional visualizations.

---

## Topics Covered

| # | Section | Key Functions / Patterns |
|---|---|---|
| 1 | **Creating Arrays** | `np.array`, `np.zeros`, `np.ones`, `np.arange`, `np.linspace` |
| 2 | **N-Dimensions** | `.shape`, `.ndim`, `.size`, 1D / 2D / 3D arrays |
| 3 | **Reshape** | `.reshape()`, flattening, dimension conversion, ValueError handling |
| 4 | **Slicing** | `arr[2,3]`, `arr[:,3]`, `arr[0:2,-3:]`, in-place modification |
| 5 | **Filtering** | Boolean masks, compound conditions (`&`, `\|`) |
| 6 | **View vs. Copy** | Memory sharing, `.copy()`, `np.shares_memory()` |
| 7 | **Introspection** | `.max()`, `.min()`, `.sum(axis=0)`, `.mean()`, `.std(axis=1)` |
| 8 | **Element-wise Ops** | Vectorized arithmetic vs. Python loops — speed benchmark |
| 9 | **Data Types** | `dtype`, `int8` constraints, type coercion, dtype reference table |
| 10 | **Broadcasting** | Scalar, 1-D, and 3-D shape compatibility rules |
| 11 | **DataFrames → Arrays** | `.to_numpy()`, `select_dtypes`, `np.nanmean`, `np.nanmax` |

---

## Why NumPy?

NumPy arrays are stored in contiguous memory blocks and operations execute in compiled C — not interpreted Python. This produces two critical advantages for analytics work:

**Memory:** A Python list of 1,000 integers requires ~28,000 bytes. A NumPy int64 array of 1,000 integers requires ~8,000 bytes — 3.5× more memory-efficient.

**Speed:** The speed benchmark in this notebook measures element-wise multiplication of 1,000,000 values:

| Method | Time |
|---|---|
| Python list comprehension | ~120 ms |
| NumPy vectorized | ~1–3 ms |
| **NumPy speedup** | **~50–100×** |

---

## Key Concepts Explained

### View vs. Copy — The Most Common NumPy Bug

```python
data1 = np.arange(24).reshape(4, 6)
data2 = data1[:2, 3:]          # VIEW — shares memory with data1
data2[1, 2] = -1               # modifies data1 too!

data3 = data1[:2, 3:].copy()   # COPY — independent
data3[1, 2] = -1               # data1 unchanged
```

Slicing always returns a **view**. Use `.copy()` when you need independence.

---

### Broadcasting — Arithmetic on Different-Shaped Arrays

```python
A = np.array([[1,2,3],[4,5,6],[7,8,9]])   # shape (3, 3)

A + 1                 # scalar broadcasts to every element
A + np.array([1,1,1]) # 1-D broadcasts across all rows
A + np.array([[1],[1],[1]])  # column vector broadcasts across all columns
```

Broadcasting expands the smaller array logically (no memory copies) to match the larger shape.

---

### Axis Control — Aggregation Direction

```python
data = np.arange(12).reshape(3, 4)
data.sum(axis=0)   # → one sum per COLUMN (collapses rows)
data.sum(axis=1)   # → one sum per ROW (collapses columns)
data.sum()         # → single value (collapses everything)
```
<img width="1415" height="398" alt="image" src="https://github.com/user-attachments/assets/238fe30c-016c-422f-8539-0c00400ed149" />

---

### Filtering with Boolean Masks

```python
arr = np.arange(21).reshape(3, 7)

arr[arr < 5]                          # elements less than 5
arr[(arr < 5) & (arr % 2 == 0)]      # less than 5 AND even
```
<img width="1418" height="398" alt="image" src="https://github.com/user-attachments/assets/725f9803-a5ba-43d6-9e2f-d776e7af0dc4" />

Result is always a **1-D array** of the selected elements.

---

### NaN-Safe Statistics — Real-World Data

When working with real datasets, missing values (`NaN`) propagate through standard aggregations:

```python
num_array.mean(axis=0)      # returns NaN if any column has missing values
np.nanmean(num_array, axis=0)  # ignores NaN — returns column means safely
np.nanmax(num_array, axis=0)   # NaN-safe column maxima
```

---


## Visualizations

| File | Section | Contents |
|---|---|---|
| `np_creation.png` | Sec 1 | arange vs. linspace scatter + memory comparison bar |
| `np_filtering.png` | Sec 5 | Heatmap grid showing three boolean mask conditions |
| `np_introspection.png` | Sec 7 | Array heatmap + column sums + row sums |
| `np_broadcasting.png` | Sec 10 | Three broadcasting patterns: scalar, row, column |
| `np_dataframe_arrays.png` | Sec 11 | Histograms of three Telco churn numerical columns |

<img width="1418" height="454" alt="image" src="https://github.com/user-attachments/assets/8e0fc96a-6f24-4c8d-b3fc-58ca38ec3e64" />

<img width="1418" height="342" alt="image" src="https://github.com/user-attachments/assets/edde3791-1e8f-4d40-8eb1-8193eda3801e" />

---

## Dataset

**Telco Customer Churn** (used in Section 11)

| Property | Value |
|---|---|
| Source | Google Drive (course dataset) |
| Records | 7,043 customers |
| Numerical columns | `tenure`, `MonthlyCharges`, `TotalCharges` |
| Use case | DataFrame → NumPy conversion, `nanmean`, `nanmax` |
<img width="1526" height="454" alt="image" src="https://github.com/user-attachments/assets/5eccf883-9c00-40b1-8989-949d69675bde" />

---

## How to Run

**Google Colab (recommended)**
```
Runtime → Run all
Dataset loads automatically from Google Drive
```

**Local Jupyter**
```bash
pip install numpy pandas matplotlib
jupyter notebook NumPy-for-Data-Analytics-Core-Concepts-Operations.ipynb
```

---

## Skills Demonstrated

`NumPy` `Array Creation` `Reshape` `Boolean Masking` `View vs. Copy` `Broadcasting` `Vectorization` `Axis-Controlled Aggregation` `dtype Management` `NaN-Safe Statistics` `DataFrame to Array Conversion` `Performance Benchmarking` `Python` `pandas` `matplotlib`

---

## Author

**Aketch Adhiambo Okoth**  
MS Business Analytics — Montclair State University  
[LinkedIn](https://linkedin.com/in/your-profile) · [Portfolio](https://your-portfolio-url.com)
