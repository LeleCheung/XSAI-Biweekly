### XSAI

- Code quality
  - Switch CI nightly random regression to the RVA23 non-vector SPEC checkpoint pool ([XSAI #130](https://github.com/OpenXiangShan/XSAI/pull/130))
- Debugging tools
  - Add a joint CUTE-L2 test top and provide write-request observation interfaces ([CUTE #40](https://github.com/OpenXiangShan/CUTE/pull/40), [CUTE #41](https://github.com/OpenXiangShan/CUTE/pull/41))
  - Improve NEMU's CUTE controller-mode callbacks and matrix synchronization support ([NEMU #1225](https://github.com/OpenXiangShan/NEMU/pull/1225))
  - Fix the layout mismatch between AME event structures in DiffTest batch mode and NEMU ([difftest #962](https://github.com/OpenXiangShan/difftest/pull/962))
  - Fix `coreid` and PC sampling in CUTE DiffTest events ([CUTE #42](https://github.com/OpenXiangShan/CUTE/pull/42))
  - Restrict comparisons for NEMU matrix load results to avoid false positives caused by unwritten regions ([NEMU #1217](https://github.com/OpenXiangShan/NEMU/pull/1217))
  - Add checks in NEMU for missing synchronization before matrix memory accesses and reads from undefined matrix-register regions ([NEMU #1212](https://github.com/OpenXiangShan/NEMU/pull/1212), [NEMU #1224](https://github.com/OpenXiangShan/NEMU/pull/1224))
