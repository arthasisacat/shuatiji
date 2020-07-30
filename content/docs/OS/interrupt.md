---
title: Interrupt
BookToC: true
---
# Interrupt

## big picture

1. An interrupt requestion (IRQ) happensinside the processor, based on a peripheral, the software, or a fault in the system.
2. The processor saves where it was (the context)
3. The processor looks in the interrupt vector table to find the callback function associated with the interrupt.
4. the call back function (ISR/interrupt service routine/interrupt handler) runs

Some interrupts are like small high-priority tasks. e.g. input lines, ADC, timers, peripherals. This is most common. 

Others more like exceptions, handling system fault and never return to normal execution.

## detailed steps

### I. IRQ happens
configure interrupt by writing to register

for a register that sets interrupt handling, setting register directly can cause problems if an interrupt happens between any of 2 steps (read current value - modify - write back). To prevent this race condition, use indirect registers: a register to set, another register to clear/reset. Each acts on a third register. 

multiple sources for one interrupt

interrupt priority

nested interrupts (interrupt within interrupts)

non-maskable interrupts (NMI)

### II. saves the context

save context to stack. context means program counter and a set of processor registers.

interrupt latency the time it takes between IRQ and the ISR. 

Keep interrupt short!!

Re-entrant functions - can be safely called multiple times while it's running. Functions that use static/global variables are non-reentrant.

### III. get ISR from interrupt vector table

Interrupt vector table is a list of function pointers. It is initialized during startup.

Looking up the ISR: 

Each interrupt has an interrupt number, e.g. timer3 interrupt, it's 20. When interrupt happens, it is signaled by just the number. Address of the handler is 20*4 = 80d = 0x50h

|                      | address |                          |
|:--------------------:|:-------:|:------------------------:|
|                      | 0x00    | stack pointer init value |
| exception interrupt  | 0x04    | reset vector             |
| exception interrupt  | 0x08    | NMI vector               |
|                      | \.\.\.  | \.\.\.                   |
| peripheral interrupt | 0x50    | timer3\_IRQHandler       |
| peripheral interrupt | 0x54    | UART0\_IRQHandler        |

### IIII. call ISR

SHORT!!!

Don't call non-entrant functions (because global variables can be corrupted by interrupts)

Turn off other interrupts during the ISR to avoid priority invertion problems!

Disable all interrupts for critical section. If you disable some but not all interrupts, priority inversion happens.

### V. restore the context