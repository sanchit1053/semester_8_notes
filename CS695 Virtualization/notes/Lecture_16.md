# lecture 16 <div style="text-align:right"> 15/03/2024 </div>

## High Availability via Asynchronous VM Application
- Highly availaible:
    * service is availaible (for use/access) at all/most times
    * TTR - (Time to recovery/restart) small 
    * failure recovery model:
        + relate to state exposure
        + What is visible to the external world
        + External visible should be consisitent


## Crash Consistency
- file system of native OS (bare metal)
- `fd = fopen("helloworld.txt")`
- open → fd table → fs struct → fnode → dentry → read blocks from disk

## Journaling

```
   transaction start                            end 
    -----------------------------------------------
                read write descriptions
```

## Application centric model
- applications that are critical 
- HA in-live with application logic code

## remus
- system wide replication (application agnostic)
- generalizability  : all applications
- transparent       : seamless in usage
- consistent failure model

### System Wide replication
- in memory state of the system has replicas:
    * in memory : run time execution context that is ready to go on failure
- Solution trajectories:
    * reproduce input on multiple instances
    * instruction replay and io event injection → record and replay

## Memory snapshot/check points
- similar to live migration - service for all VMs
- copies memory states across machines (primary and backup)
- has an active(primary) and a passive(backup) instance (multiple vms)

1. normal execution : buffer all external state
2. checkpoint
3. transfer checkpoint
4. ack checkpoint and release externally
