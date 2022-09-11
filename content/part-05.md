+++
weight = 5
+++

<!-- Start vertical slides -->
{{% section %}}

# Special

Enhanced the coverage of special functions in CuPy.
- APIs covered:
  - [x] `log_ndtr` [PR #6776](https://github.com/cupy/cupy/pull/6776)
    - For more details: https://khushi-411.github.io/GSoC-week1/
  - [x] `log_softmax` [PR #6823](https://github.com/cupy/cupy/pull/6823)
  - [x] `logsumexp` [PR #6773](https://github.com/cupy/cupy/pull/6773)
    - [ ] `support multiple output args in reduction kernel` [PR #6813](https://github.com/cupy/cupy/pull/6813)
  - [x] `expn` [PR #6790](https://github.com/cupy/cupy/pull/6790)
    - GitHub repository for more details: https://github.com/khushi-411/expn
  - [x] `softmax` [PR #6890](https://github.com/cupy/cupy/pull/6890)
- [x] Documentations and tests
- [x] Performance Benchmark

---

### Universal Functions

- Implemented in `log_ndtr` & `expn` (both numerically stable)
- Wraps into C++ snippet for speedy implementation.

```python
# universal function
log_ndtr = _core.create_ufunc(
    'cupyx_scipy_special_log_ndtr',
    (('f->f', 'out0 = log_ndtrf(in0)'), 'd->d'),
    'out0 = log_ndtr(in0)',
    preamble=log_ndtr_definition, # C++ function call
    doc="""
    ....
    """
)
```

---

### Custom Kernels (ReductionKernel)

- Similar to `map` & `reduce` operations in python.
- Wraps into C++ snippet for speedy implementation.

```python{1-5|8-16}
# function call
def(...):
    ...
    _log_softmax_kernel(tmp, axis=axis, keepdims=True)
    return ...

# ReductionKernel
_log_softmax_kernel = cp._core.ReductionKernel(
    'T x1',
    'T y',
    'exp(x1)',
    'a + b',
    'y = log(a)',
    '0',
    name='log_softmax'
)
```

---

### Kernel Fusion (Experimental)

- Compiles into a single kernel instead of series of kernels
- Experimental implementation to *fuse* `softmax` function
- Drawback here: does not generate competitive codes, therefore, switched to the normal implementation

```python{1-9}
def make_expander(shape, axis):
    axis = internal._normalize_axis_indices(axis, len(shape))
    expander = []
    for i, s in enumerate(x.shape):
        if i in axis:
            expander.append(None)
        else:
            expander.append(slice(None))
    return tuple(expander)
```
*TODO*: Add `shape` method in cupy.fusion, to use `make_expander` inside fusion kernel

---

```python{1-9|12-15}
@_util.memoize(for_each_device=True)
def _softmax_fuse(shape, axis):
    expander = make_expander(shape, axis)
    @_core.fusion.fuse()
    def softmax_fuse(x):
        x_max = cupy.amax(x, axis=axis)
        exp_x_shifted = cupy.exp(x - x_max[expander])
        return exp_x_shifted / cupy.sum(exp_x_shifted, axis=axis)[expander]
    return softmax_fuse


def softmax(x, axis=None):
    fused_softmax = _softmax_fuse(shape=x.shape, axis=axis)
    return fused_softmax(x)
```

<!-- End vertical slides -->
{{% /section %}}
