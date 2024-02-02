# Lecture 6 <div style="text-align:right"> 24/01/2024 </div>

## memory virtualizaion with VMS
- Native:
    * Virtual memory / address space  ( abstraction )
        + 0 starting
        + linear and continous
        + per-process
        + "full" address space
    * throught v2p , via page tables
        + isolation
        + permissions
        + elastic provisioning (alloc) of memory

Giving VMs some memory which they think is the total memory available and map their virtual memory to the given memory  
the given memory is mapped to the actual memory

```
guest virtual address (gva)  ------------> psuedo physical address (ppa) ---------------> machine physical memory(mpa) 
                            guest-managed                               hypervisor managed
                                v2p                                         p2m
```

nested page tables
- if the mapping is static then cannot generalize
- constraint : MMU only has single page table walk

## Solution 1 Direct mapping (Para Virtualized VMS)
- Guest has page tables per process (v2p)
- vmm has a mapping from p to m
- mmu points to the page table of the process
- Process
    * maintain a simple v2m mapping 
    * mmu walks v2m for consistent translation
- How to build the v2m mapping
    * eg:- Page fault in guest
    * update mapping via hypercall
    * `update_pgtable(gva,ppa,pgd)`
    * vmm : ppa → mpa
    * __TODO__
    1) update_pgtable(gva, pqa, pgd)
- Key steps
    * Guest does not update pg tables directly, only via hypercall
    * All page table pages are marked read only

## Shadow 2 Shadow Paging (full virtualized VMS)

- VMMS have a full page table that is a shadow of the Guest page tables
- mmu points to this page table which mapps from v to m
- 
