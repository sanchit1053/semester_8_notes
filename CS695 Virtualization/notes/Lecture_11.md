# lecture 12 <div style="text-align"> 16/02/2024 </div>

4 main building blocks of containers

1) namespaces
2) cgroups
3) chroot
4) capabilities

## containers

``` 
    ┌────────────────────────────┐
    │Appliction_1 | Application_2│
    ┌────────────────────────────┐
    │Library_1    |  library_2   │
    ┌────────────────────────────┐
    │OS                          │
    └────────────────────────────┘
```

root file system in application
- dependencies
- utilites
- libraries
- OS-interface / suuupA
- Module Isolation

## Isolation
- resources
- runtime environments (seperation between **1** and **2** )

#### chroot
changes root to a mount point and execute program
- will work if all dependencies of an application are available relative to the new root for the program

###### container world

#### namespaces
- mechanism to provide isolated view of global resources
- atleast 6 different types of namespaces
    * mnt : mount points of file system
    * pid : processes
    * net : netword handling and state
    * ipc : ipc primitives, queues
    * uts : domain/host name
    * user : uid/gid ranges/sets

# Container
- All elements of a container are in teh same namespace
