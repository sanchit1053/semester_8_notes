# Lecture 7 <div style="text-align:right;"> 31/01/2024 </div>

### Assignment 2
- using the KVM interface to setup and control guest VMs

## Recap
- v2p and p2m
- guest virtual → psuedo physical → Machine


1) 
2) Shadow Paging ( full virtualized VMs)
    1) Guest vmware of the vmm
    2) create a copy of page table in host

Key: is to ride on trap on CR3 update
    - mark all guest page table pages as read only

## Page Fault
- Guest Fault
    * no v2p 
    * inject fault and let guest page handler set up v2p mapping
    * update to PTs will result in trap and update Spt
- VMM's fault swap in page via vmm pg fault handler update v2m
