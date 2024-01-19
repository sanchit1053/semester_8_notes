# Lecture 2 <div style="text-align: right;"> 10/01/2024 </div>


A. What is the secrets "sauce" for all computing (developing programs, embedding logic, do work)
- Abstrations
    * specification of functionality
    * accessed via an interface / API
    * interface has a beckend for implementation


Computing World Stack
```
- Applications (Programs like tetris)
-=========================================== API
- Libraries (C, C++, Rust)
-=========================================== ABI (system calls)
- OS (Process, file, address space)
-=========================================== ISA
- Hardware
    (Transistors, gates, logic units, flip-flops, interconnects)
```

## process
- Effiecient use of resources by scheduling

## Process Context
- The state of the CPU due to process execution
- CPU registers
    * eax, ebx, ecx → General Purpose
    * esp, ss, ebp → stack ptr
    * pc, eip → instruction pointer
    * flags → flags regs
- context : Save and restore
- context switch : saves process 1, restore proess 2

-----------

## PCB (process control block)
- pid, status,
- stack info
- context
- page table info
- files

## Virtualization
- multiplexing sharing
- Virtual Machines (VMs)

| Process-View   | Os/System-view    |
|--------------- | --------------- |
| zero-starting address space   | CPUs, cputypes   |
| CPU ownership    | ISA   |
| files            | all CPU char. (address true width)|
| sockets          | Physical memory available|
| device endpoints | external devices (types)|

## Virtualization / VM's
- provide the OS view (system-view, machine) as an abstraction (software defined)





