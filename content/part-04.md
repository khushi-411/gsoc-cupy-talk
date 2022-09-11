+++
weight = 4
+++

<!-- Start vertical slides -->
{{% section %}}

# Interpolate

Introduced `interpolate` module in CuPy.

Before:
```python{1|2|4-7}
import cupy
from cupyx.scipy import interpolate

# throws error
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ImportError: cannot import name 'interpolate' from 'cupy' (/home/khushi/Documents/cupy/cupy/__init__.py)
```

Now:
```python{1|2|4}
import cupy
from cupyx.scipy import interpolate

# works well
```

---

- APIs covered:
  - [x] `BarycentricInterpolator` [PR #6958](https://github.com/cupy/cupy/pull/6958)
  - [x] `barycentric_interpolate` [PR #6958](https://github.com/cupy/cupy/pull/6958)
  - [x] `KroghInterpolator` [PR #6990](https://github.com/cupy/cupy/pull/6990)
  - [x] `krogh_interpolate` [PR #6990](https://github.com/cupy/cupy/pull/6990)
- [x] Documentations and tests
- Performance Benchmark
  - [x] NVIDIA Nsight System

---

## `BarycentricInterpolator` & `barycentric_interpolate`

Paper: https://people.maths.ox.ac.uk/trefethen/barycentric.pdf

<br/>

- [x] Added **`_Interpolator1D`** class: deals with common features for all interpolation functions (implemented in CPU, due to a smaller number of points). It supports the following methods:

  - [x] *`__call__`*: use to call the next points
  - [x] *`_prepare_x`*: change into a 1-D array
  - [x] *`_finish_y`*: reshape to the original shape
  - [x] *`_reshape_yi`*: reshape the updated yi values to a 1-D array
  - [x] *`_set_yi`*: if y values are not provided, this method is used to create a y-coordinate
  - [x] *`_set_dtype`*: sets the dtype of the newly created yi point
  - [x] *`_evaluate`*: evaluates the polynomial, but for reasons of numerical stability, currently, it is not implemented.

---

- [x] Added **`BarycentricInterpolator`** class: constructs polynomial. It supports the following methods:
  - [x] *`set_yi`*: update the next y coordinate, implemented in CPU due to smaller number of data points
  - [x] *`add_xi`*: add the next x value to form a polynomial, implemented in CPU due to smaller number as mentioned in the paper
  - [x] *`__call__`*: calls the *_Interpolator1D* class to evaluate all the details of the polynomial at point x
  - [x] *`_evaluate`*: evaluate the polynomial

- [x] Added **`barycentric_interpolate`** wrapper

---

## `KroghInterpolator` & `krogh_interpolate`

<br/>

- [x] Added **`_Interpolator1DWithDerivatives`** class: calculates derivatives. Its' parent class is `_Interpolator1D`. It supports the following methods:

  - [x] *`derivatives`*: evaluates many derivatives at point x
  - [x] *`derivative`*: evaluate a derivative at point x

---

- [x] Added **`KroghInterpolator`** class: constructs polynomial and calculate derivatives. It supports the following methods:
  - [x] *`_evaluate`*: evaluates polynomial
  - [x] *`_evaluate_derivatives`*: evaluates the derivatives of the polynomial

- [x] Added **`krogh_interpolate`** wrapper 

<!-- End vertical slides -->
{{% /section %}}
