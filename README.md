# MURaMKit
Conditioning MURaM data for (potentially) better compression! 

This [header file](https://github.com/shaomeng/MURaMKit/blob/main/include/MURaMKit_CAPI.h) has definitions of all operations in C programming language.

## Supported conditioning operations (C)

### Logarithmatic and exponential transforms
- `int mkit_smart_log()` performs a logarithmatic transform on _any_ input. It does so by 1) keeping the signs of all values in a mask, and then making all negative values positive; and 2) keeping all zero values in a mask, and then applying the log transform on non-zero values. A header including up to two masks is also generated.
- `int mkit_smart_exp()` performs an exponential transform on the input. It also requires the header generated by `int mkit_smart_log()` so that it can properly restore zero and negative values.
- `size_t mkit_log_meta_len()` reads a header produced by `int mkit_smart_log()` and tells its length in bytes. 

This [utility program](https://github.com/shaomeng/MURaMKit/blob/main/utilities/smart_log.c) demonstrates their usage.

### Slice-based normalization
- `int mkit_normalize()` performs a slice-based normalization on a 3D volume. A **slice** is defined by the `dim_mid` and `dim_slow` dimensions of the volume. For each slice, the mean is subtracted from all values, and then all values are normalized by the RMS. A header is also generated to keep track of the mean and RMS of each slice.
- `int mkit_inv_normalize()` performs an inverse normalization. It requires the header generated by `int mkit_normalize()` as an input too.
- `size_t mkit_norm_meta_len()` reads a header generated by `int mkit_normalize()` and tells its length in bytes.

This [utility program](https://github.com/shaomeng/MURaMKit/blob/main/utilities/slice_norm.c) demonstrates their usage.
