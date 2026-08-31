### XSAI

- Bug fixes
  - Fix the MLCT transposed data layout and C MatrixReg read addresses for MSC/MSCT ([XSAI #106](https://github.com/OpenXiangShan/XSAI/pull/106), [CUTE #38](https://github.com/OpenXiangShan/CUTE/pull/38))
  - Fix misdecoding of `msetcfg`/`mgetcfg` ([XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107))
  - Fix state desynchronization between matrix memory-access `AccessAckData` responses and HintQueue ([XSAI #110](https://github.com/OpenXiangShan/XSAI/pull/110), [XSAICache #6](https://github.com/OpenXiangShan/XSAICache/pull/6))
  - Fix missed wakeups for delayed Mx operand writebacks that could permanently block MLS instructions ([XSAI #111](https://github.com/OpenXiangShan/XSAI/pull/111))
- Code quality
  - Remove unused matrix commit and scheduler feedback interfaces ([XSAI #113](https://github.com/OpenXiangShan/XSAI/pull/113))
  - Optimize CI: parallelize EMU and nightly regressions ([XSAI #114](https://github.com/OpenXiangShan/XSAI/pull/114), [XSAI #116](https://github.com/OpenXiangShan/XSAI/pull/116))
- Debugging tools
  - Add AME `mcfg` state comparison to DiffTest ([XSAI #107](https://github.com/OpenXiangShan/XSAI/pull/107), [difftest #944](https://github.com/OpenXiangShan/difftest/pull/944), [NEMU #1172](https://github.com/OpenXiangShan/NEMU/pull/1172))
  - Support 16-byte store checker events ([XSAI #112](https://github.com/OpenXiangShan/XSAI/pull/112))
  - Handle MMA operand retrieval failures and improve AMU event diagnostics ([difftest #926](https://github.com/OpenXiangShan/difftest/pull/926), [difftest #927](https://github.com/OpenXiangShan/difftest/pull/927))
