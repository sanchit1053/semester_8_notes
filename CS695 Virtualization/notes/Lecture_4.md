# Lecture 4 <div style="text-align:right"> 17/01/2024 </div>

## Designs of VMMs/Hypervisor
- Native: Os is the owner of all resources, interrups, LDE, system calls
- Challenges to VMM design: Who is the owner? , ownership resolution

## Types of VMMs
1) Bare-metal (vmware, ) __vs__ hosted (qemu, kvm, virtualbox)
2) Full virtualization (guest OSis unaware of the VMM) __vs__ para-virtualization (Guest OS knows about the VMM)

## Design principles of VMM
1) efficiency - minimum VMM overhead
2) resouces control - VMM is the owner of all resources
3) equivalence - application should execute identically on VMs and PMS

## Design 1 : Trap and Emulate
| | Native | Vm|
|----|----|----|
| Ring 3 | Application | Application |
| | | |
| | | OS| 
| Ring 0| OS | VMM|




__TODO__

i) sidt ~ reads the IDTR into memory address
        - Works even if the privilege level > 0
        - Guest OS read read successds => IDT<sub>G != IDTR
        -                              => knows aout the hypervisor IDT
ii) PL > 0 read code segment register to determine CPL, guest OS CPL > 0


## Design 2 : Scan-and-Patch
- binary translation
- used by vmware

- scan instructions of critical instructions
- replace with explicit traps to VMMs 
- make critical instructions privileged

- from a instruction in trap with interrupt vector, with the instruction pointer mapped to the instruction arguments
