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

# STM32 OpenOCD Flashing

## Requirements
- STM32F1 device (quest board) + ST-LINK (embedded in the board)  
- OpenOCD + telnet  

## Usage

1. Start OpenOCD:
    ```sh
    openocd -f interface/stlink.cfg -f target/stm32f1x.cfg
    ```

2. Connect:
    ```sh
    telnet localhost 4444
    ```

3. Backup firmware (64 KB from flash):
    ```sh
    dump_image golden.bin 0x08000000 0x00020000
    ```

4. Halt MCU:
    ```sh
    reset halt
    ```

5. Flash firmware:
    ```sh
    flash write_image erase golden.bin 0x08000000
    ```

6. Run MCU:
    ```sh
    reset run
    ```
