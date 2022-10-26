---
title: Interrupt
BookToC: true
---
# Interrupt

## introduction
An interrupt condition alerts the processor and serves as a request for the processor to interrupt the currently executing code when permitted, so that the event can be processed in a timely manner. If the request is accepted, the processor responds by suspending its current activities, saving its state, and executing a function called an interrupt handler (or an interrupt service routine, ISR) to deal with the event. This interruption is temporary, and, unless the interrupt indicates a fatal error, the processor resumes normal activities after the interrupt handler finishes.(from [wikipedia](https://en.wikipedia.org/wiki/Interrupt))

## some concepts
### Masking
Processors typically have an internal interrupt mask register which allows selective enabling and disabling of hardware interrupts. Each interrupt signal is associated with a bit in the mask register; on some systems, the interrupt is enabled when the bit is set and disabled when the bit is clear, while on others, a set bit disables the interrupt. When the interrupt is disabled, the associated interrupt signal will be ignored by the processor. Signals which are affected by the mask are called maskable interrupts.

Some interrupt signals are not affected by the interrupt mask and therefore cannot be disabled; these are called **non-maskable interrupts (NMI).** NMIs indicate high priority events which cannot be ignored under any circumstances, such as the timeout signal from a watchdog timer.

To mask an interrupt is to disable it, while to unmask an interrupt is to enable it.

## big picture

1. An **interrupt request(IRQ)** happens inside the processor, based on a peripheral (hardware), the software, or a fault in the system.
2. The processor saves where it was (the context, including program counter(PC)). Device is informed that its request has been recognized and the device deactivates the request signal.
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