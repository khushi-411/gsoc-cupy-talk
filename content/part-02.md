+++
weight = 2
+++

<!-- Start vertical slides -->
{{% section %}}

# The Project

### Project 1: [CuPy coverage of NumPy/SciPy functions](https://github.com/cupy/cupy/wiki/GSoC-2022-Project-Ideas#project-1-cupy-coverage-of-numpyscipy-functions)

Mentor: [Masayuki Takagi](https://github.com/takagi)

[Issue #6324](https://github.com/cupy/cupy/issues/6324)

<br/>

#### Expected Outcomes

{{% fragment %}} Optimized GPU implementation of NumPy/SciPy APIs {{% /fragment %}}
{{% fragment %}} Documentation and tests {{% /fragment %}}
{{% fragment %}} Performance Benchmarking (use NVIDIA Nsight System) {{% /fragment %}}

---

### Functions I Proposed & Accomplished

{{% grid middle %}}


{{< g 1 >}}

#### Interpolate

{{% fragment %}} BarycentricInterpolator {{% /fragment %}}
{{% fragment %}} KroghInterpolator {{% /fragment %}}

{{< /g >}}


{{< g 1 >}}

#### Special

{{% fragment %}} log_ndtr {{% /fragment %}}
{{% fragment %}} expn {{% /fragment %}}
{{% fragment %}} softmax {{% /fragment %}}
{{% fragment %}} log_softmax {{% /fragment %}}

{{< /g >}}


{{< g 1 >}}

#### Stats

{{% fragment %}} boxcox_llf {{% /fragment %}}
{{% fragment %}} zmap {{% /fragment %}}
{{% fragment %}} zscore {{% /fragment %}}

{{< /g >}}


{{% /grid %}}

<!---
<style>
  table {
    border-collapse: collapse;
  }
  th, td {
    border: 1px solid #ccc;
    padding: 10px;
    text-align: left;
  }
  tr:nth-child(even) {
    background-color: #eee;
  }
  tr:nth-child(odd) {
    background-color: #fff;
  }            
</style>

<table>

<tr>
<th>Function</th>
<th>Module</th>
</tr>

<tr>
<td>BarycentricInterpolator</td>
<td>interpolate</td>
</tr>

<tr>
<td>KroghInterpolator</td>
<td>interpolate</td>
</tr>

<tr>
<td>log_ndtr</td>
<td>special</td>
</tr>

<tr>
<td>expn</td>
<td>special</td>
</tr>

<tr>
<td>softmax</td>
<td>special</td>
</tr>

<tr>
<td>log_softmax</td>
<td>special</td>
</tr>

<tr>
<td>boxcox_llf</td>
<td>stats</td>
</tr>

<tr>
<td>zmap</td>
<td>stats</td>
</tr>

<tr>
<td>zscore</td>
<td>stats</td>
</tr>

</table>
-->

---

### Other Goals Accomplished (apart from proposed functions)

{{% fragment %}} Add complex number support for `nanvar` & `nanstd` {{% /fragment %}}
{{% fragment %}} logsumexp {{% /fragment %}}
{{% fragment %}} barycentric_interpolate {{% /fragment %}}
{{% fragment %}} krogh_interpolate {{% /fragment %}}

<br/>

### WIP PR

{{% fragment %}} support multiple output args in ReductionKernel {{% /fragment %}}

<!-- End vertical slides -->
{{% /section %}}
