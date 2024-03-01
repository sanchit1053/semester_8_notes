# lecture 13 <div style="text-align:right"> 21/02/2024 </div>

### Read Papers
- [memmgmt] memory Resources Management in VMware ESX Server
- [livemighta]
    * snapshots
    * Record and replay


### Context 
- overcommit and server consolidation:
    * server consolidation : pack multiple VMS on a single server (PM)
    * overcommit : committed resources greater than physical resources $\sum_{\forall vms} P_{ranges} > m_{range}$
- "Management" Actions
    * allocate memory / generate mapping
    * swap in/swap out (revoke / reclaim)
    * vmmap/deallocate
    * handling fault ← revocation 
    * free page state
    * permissions handling
    * sharing / cow


Shadow page tables for memory virtualisation
- 2 page tables:
    * v2p
    * v2m
- pmap:
    * p2m mapping per vm

### overcommit
increase in (simultaneous) demand
- statistical multiplexing
    * execution entities will have statistically different requirements

Solutions
- avoid memory pressure: increasing memory utility /efficiency
    * cpbs : content based page sharing
- handle memory pressure: swapping paging/demand
    * ballooning

#### Ballooning
- cut memory from the main memory and distribute to the vms
- which 'm' pages to reclaim?
    * Collect meta information about accesses to estimate per page utility
        + high overhead
        + incomplete / wrong decisions
- have many 'm' pages per vm?

###### double paging problem
- vmm swaps out a m page; invalidates p2m mapping
- vm decides to swap out the same p pages
    * rebuild p2m 
    * swap back p to virtual disk

## Solution
### memory ballooning
- guest know state of its memory utility
- approach:
    * co-operative guest OS + balloon inflate/deflate (induce/reduce) memory pressure in the guest
    * balloon driver (LKM) in the guest
    * interacts with a virtual/pseudo device
    * device io is a private channel for the vmm <-> balloon drive:
        + 
        + transfer p info

Balloon Driver Inflate
- alloc memory balloon (kernel) guest OS
- "pin" memory of balloon driver
- convey p-range of balloon to vmm
- invalidate p2m mapping at vmm
- move free pages in the pmap


### Sharing (Avoid Pressure)
- vms : same/similar guest OS,applications,libraries data
- explicit tagging of shareable content
    * bcopy - block IO; hook in vm;n unified disk cache at the VMM block 
    * vdisk1,block#23 <=> vdisk 2, block #46

### cpbs
- content based page sharing
- page identity <=> content
- scan all pages / share identical pages
    * n x n => O(n2)
    * hash based technique
        + 
        + lookup hash for entry
        + if entry exists:
            + rehash the entry
            + byte by byte comparison to confirm match
            + if match : share, copy on write
        + if entry does not match
            + add hash entry to the hash
