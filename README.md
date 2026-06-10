# 8086 Assembly Balloon Game

A game written in 8086 assembly language that renders colored animated balloons in a DOS text-mode screen, using direct video memory manipulation and a hardware timer interrupt.

## What it does

The program writes directly to the CGA video buffer at segment `0xB800` to draw colored rectangular "balloons" that float upward across the screen. Three balloons animate concurrently across three rounds, each with distinct colors (red, blue, green) and digits. A timer ISR increments a tick counter displayed in the top-right corner, and the screen is managed with custom scroll and clear routines.

## Features

- Direct video memory writes (no BIOS/DOS print calls for graphics)
- Hardware timer interrupt (IRQ 0) hooked via IVT for real-time tick display
- Custom subroutines: `print_rectangle`, `erase`, `scrollup`, `clrScr`, `printstr`, `printnum`
- Color-coded attribute bytes set per balloon via `color_checker`
- Three sequential animation rounds with independent balloon speeds
- Stack-based calling convention throughout (`push bp` / `ret N` frames)

## Tech stack

- 8086 assembly (NASM/MASM compatible syntax with `[org 0x0100]`)
- DOS COM executable target
- CGA text-mode video (80x25, segment 0xB800)

## How to run

Assemble with NASM:

```
nasm -f bin cir.asm -o cir.com
```

Run in DOSBox or any 8086 emulator that supports DOS COM files.

## Status

Written as a university project (2021). Single-file implementation; no further development planned.
