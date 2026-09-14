### XSAI

- RTL features
  - Propagate matrix prefetch descriptors with CUTE memory requests ([CUTE #39](https://github.com/OpenXiangShan/CUTE/pull/39))
- Bug fixes
  - Sync bug fixes from Kunminghu V2 ([XSAI #123](https://github.com/OpenXiangShan/XSAI/pull/123), [XSAI #129](https://github.com/OpenXiangShan/XSAI/pull/129))
  - Fix a prefetch RequestBuffer livelock ([XSAI #126](https://github.com/OpenXiangShan/XSAI/pull/126), [XSAICache #8](https://github.com/OpenXiangShan/XSAICache/pull/8))
- Code quality
  - Update the nightly regression checkpoint pools and pin matrix jobs to node runners ([XSAI #120](https://github.com/OpenXiangShan/XSAI/pull/120), [XSAI #122](https://github.com/OpenXiangShan/XSAI/pull/122))
- Debugging tools
  - Improve AME DiffTest handling of `mrelease` retirement and ordering against older `mstore` instructions ([XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121), [difftest #953](https://github.com/OpenXiangShan/difftest/pull/953), [XSAI #128](https://github.com/OpenXiangShan/XSAI/pull/128), [difftest #958](https://github.com/OpenXiangShan/difftest/pull/958))
  - Record the correct instruction PC on AME error paths ([XSAI #121](https://github.com/OpenXiangShan/XSAI/pull/121), [difftest #955](https://github.com/OpenXiangShan/difftest/pull/955))
  - Optimize floating-point MMACC in NEMU and improve instruction semantic checks ([NEMU #1189](https://github.com/OpenXiangShan/NEMU/pull/1189), [NEMU #1197](https://github.com/OpenXiangShan/NEMU/pull/1197), [NEMU #1200](https://github.com/OpenXiangShan/NEMU/pull/1200))
