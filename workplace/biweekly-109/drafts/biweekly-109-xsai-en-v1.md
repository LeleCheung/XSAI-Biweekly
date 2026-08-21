### XSAI

- RTL features
  - Support e8/e16/e32 multi-precision transposed loads for tile registers ([CUTE #35](https://github.com/OpenXiangShan/CUTE/pull/35))
- Bug fixes
  - Fix DiffTest support for multi-channel CUTE and optimize area ([XSAI #93](https://github.com/OpenXiangShan/XSAI/pull/93), [CUTE #33](https://github.com/OpenXiangShan/CUTE/pull/33))
- Debugging tools
  - Implement MMA batching in DiffTest to reduce kernel launches ([difftest #920](https://github.com/OpenXiangShan/difftest/pull/920))
  - Implement backpressure to prevent unbounded queue growth when the MMA backend has insufficient throughput ([difftest #923](https://github.com/OpenXiangShan/difftest/pull/923))
