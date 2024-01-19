# Lecture 5 <div style="text-align:right"> 19/01/2024 </div>

## recap:
- trap and emulate
- binary translation / trap - and - emulate

## Design 3 : paravirtualized approach for CPU virtualization  
- Guest OS knows about the VMM VM abstraction
    * Not Issue problem / priveleged instruction
- Enabled via a mechanism: **hypercall** 

### Hypercall
- Similar to the system call interface
- interface between guestOS (abstraction VM) and the hypervisor (provider of abs)
- explicit invocation
    * `int 0x80`, interrupt  → x86 system call
    * `int 0x82`, → hypercall (xen)

#### Idea
on any critical work, 
> critical : anything that needs hypervisor intervention

explicitly make a hypercall;  
eg: `mmu_update(va, pa, pte_details)`  
say we do `guest va → pa`, guest os knows pa is not real physical address

1) trying to update the page table
2) setup the IDTR (interrupt descriptor table);

## Design 4 : hardware associated virtualization support for cpu 
- hardware architecture redesign/upgrade to support system-level virtualization
- **key Idea** programmatic control/config of traps 
- x86 ISA
    * vms modes of operation
    * vmx instructions
    * vmx state(context & config)

#### vmx modes
| Column1    | vmx non-root modes    | vmx root mode    |
|---------------- | --------------- | --------------- |
| Ring3    | Application    |     |
|     |     |     |
|    |    |    |
| Ring0   | OS   | VMM  |

non-root to root by VM_exit.  
root to non-root by VM_entry

## VMCS virtual machine control structure
- guest state/ area
    * all guest execution state, CPU_registers, saves on exit restored on entry
- host area
    * save vmms execurtion status - saved on entry to VM unsed on exit from VM
- vm execution control
    * behaviors in non-root mode (exit conditions)
- vm entry control fields
    * what state to restore on entry : **interrupt injection** 
- vm exit control fields
    * what state to restore on exit
- vm exit information
    * exit status / details

HW new priveleged instructions
- vm read, vm write, vmclear, vmldptr, vm resume, vmx on, vmx off, vm launch
- per-cpu vmcs ptr(registers)

order of operation
```
    root vmm     non-root vm    root vm      non-root
  |------------|--------------|------------| ----------|
vmx on      vm launch       vm exit     vm resume   vm exit
                    | 
                   syscall - int
```
