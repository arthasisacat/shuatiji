# Memory management

## Computer memory hiararchy
![image info](../memory_management.png)

1. external memory or secondary memory
    Comprising of Magnetic Disk, Optical Disk, Magnetic Tape i.e. peripheral storage devices which are accessible by the processor via I/O Module.
2. internal memory or primary memory
   Comprising of Main Memory, Cache Memory & CPU registers. This is directly accessible by the processor.

## introduction to memory and memory units
memories are made up of registers.

1 word = 8 bits = 1 byte

## RAM (random access memory)
- SRAM (static -) 
  retain contents as long as powered on
- DRAM (dynamic -) 
  short data lifetime ~4ms, DRAm controller rrefreshes it so it works just like SRAM.

SRAM is faster than DRAM, more expensive than DRAM, consumes more power than DRAM,  low packaging density.

## Partition Allocation Methods
Single contiguous allocation: 

Simplest allocation method used by MS-DOS. All memory (except some reserved for OS) is available to a process.

Partitioned allocation: 

Memory is divided in different blocks or partitions.Each process is allocated accroding to the requirment.

Paged memory management: 

Memory is divided into fixed sized units called page frames, used in a virtual memory environment.

Segmented memory management: 

Memory is divided in different segments (a segment is a logical grouping of the process’ data or code).In this management, allocated memory doesn’t have to be contiguous.

Most of the operating systems (for example Windows and Linux) use Segmentation with Paging. A process is divided into segments and individual segments have pages.
