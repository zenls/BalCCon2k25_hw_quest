# BalCCon2k25_hw_quest

Binary dumps from an STM32F103 (Cortex-M3). Your task: reverse-engineer and extract the answers.

## Tools

- Ghidra — static analysis / decompilation (ARMv7-M, Thumb).
- ImHex — hex + pattern definitions for structures.

## Quick start

Open quest_?.bin in Ghidra → set language to ARM LE Cortex, base 0x08000000, use Reset_Handler as entry, run analysis with `ARM Aggressive Instruction Finder`.

```
Flash: 0x0800_0000 -> 0x0020_0000   (128 Kbytes)
SRAM:  0x2000_0000 -> 0x0005_0000   ( 20 Kbytes)
```