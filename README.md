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

For adition information you can check [this]([url](https://docs.google.com/presentation/d/1cdKOSSeUj7wjjbe4AN3h3LsnMcJIFCdbmSi1o4zBcXU/edit?slide=id.p#slide=id.p)) presrntdtion - before with 51 slide

## STM32 OpenOCD Read & Flash

1. Start OpenOCD (reconnect if failed):
    ```sh
    openocd -f interface/stlink.cfg -f target/stm32f1x.cfg
    ```

2. Connect to OpenOCD:
    ```sh
    telnet localhost 4444
    > dump_image golden.bin 0x08000000 0x00020000
    > reset halt
    > flash write_image erase golden.bin 0x08000000
    > reset run
    ```

3. Connect GDB to Openicd
    ```sh
    - `arm-none-eabi-gdb` – start GDB  
    - `(gdb) target remote localhost:3333` – connect to OpenOCD GDB server  
    - `(gdb) monitor reset halt` – reset + halt MCU  
    ```

## GDB cheat sheet

### Navigation
- `ni` – next instruction  
- `si` – step instruction  
- `j *addr` – jump to address  
- `fin` – finish current function  
- `c` – continue execution  
- `f` – show current frame/PC  
- `q` – quit  

### Breakpoints
- `b *addr` – set breakpoint at address  
- `b n` – delete breakpoint n  
- `i b` – list breakpoints  

### Data & Registers
- `set $r0 = 1` – write to register r0  
- `x/10x addr` – show 10 words at address  
- `display/10i $pc-0x5` – show ASM around PC  

### Aliases
- `alias rr = monitor reset halt` – quick halt
