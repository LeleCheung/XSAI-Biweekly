### XSAI

- RTL features
  - Integrate a matrix-guided L2 prefetcher ([XSAI #124](https://github.com/OpenXiangShan/XSAI/pull/124), [XSAICache #7](https://github.com/OpenXiangShan/XSAICache/pull/7))
  - Implement a standalone transpose load engine with double-group buffering to support multi-channel transpose loads ([CUTE #43](https://github.com/OpenXiangShan/CUTE/pull/43), [XSAI #132](https://github.com/OpenXiangShan/XSAI/pull/132))
- Bug fixes
  - Synchronize bug fixes from KMH-V2 ([XSAI #131](https://github.com/OpenXiangShan/XSAI/pull/131), [XSAICache #9](https://github.com/OpenXiangShan/XSAICache/pull/9))
- Debugging tools
  - Fix the matrix completion event stride in DiffTest under MinimalMatrixConfig ([difftest #976](https://github.com/OpenXiangShan/difftest/pull/976))
  - Fix stale CSR values exported by NEMU after implicit state updates ([NEMU #1237](https://github.com/OpenXiangShan/NEMU/pull/1237))
  - Fix NEMU's handling of large zstd image reads ([NEMU #1239](https://github.com/OpenXiangShan/NEMU/pull/1239))
  - Support hash comparison of matrix register contents ([CUTE #45](https://github.com/OpenXiangShan/CUTE/pull/45), [difftest #978](https://github.com/OpenXiangShan/difftest/pull/978), [NEMU #1238](https://github.com/OpenXiangShan/NEMU/pull/1238), [XSAI #133](https://github.com/OpenXiangShan/XSAI/pull/133))
