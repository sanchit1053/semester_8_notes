# Lecture 3             <div style="text-align: right;"> 12/01/2023 </div>

## Why VMS
- isolation soundbones on a single main computer
- Server consolidation (Sharing / multiplexing PM with severlsas VMS)
- portability - trick!
- elastic resources
- muli-os system on single machine
- testing & debugging
- New Mechanisms
    * snapshot
    * record - replay
    * ballooning

### In x86
- CR3 (control register) point to the page table
- page table walk to translate va → pa
- ldcr3 
    * load value to CR3 register

### OS building blocks
Ensure that the OS is the sole owner/ arbitrator of all resources
i. LDE - Limited Direct Execurtion
ii. interrupts/ interrupt driven execution
iii. System call interface

PL: Privilege level
__execute all non-OS instrution directly on the CPU, interject when critical / sensitive updates are to be made__ 
- privilige levels of execution
    - CPU execute in a PL 
    - every instruction of the ISA has min PL for correct execution semantics

## Challenges of hypervisor design?
- Who is the owner? of all resources
    * Guest OS believes that it is the owner
    * multiple guest OSs
    * Current Privelige level CPL ~ bit mask of the CS (Code Segment )/ CR0 (Control register)
- System Call handling
    * App (fopen, API CAll) → Lib (Libstd) (Open | System Call) → syscall handler → Interrupt vector, Interupt Handler, Syscall number
    * Sowftware mades from user to kernel
    * save user state
    * jump to Interupt handler <- IDT <- IDTR
- Resource Virtualization ( CPU, Memory, IO )
    * eg (CR3)
- Device Virtualization
