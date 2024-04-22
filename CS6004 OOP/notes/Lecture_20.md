# Lecture 20 <div style="text-align:right"> 05/04/2024 </div>

## Speculative Method Dispatch

### Inline Cache (IC)
- At method call site, perform look up to find method, got the address
- remember the address in a cache
- If reciever observed is 'B' then check the cache

```
original code;

rec = x;
call lookup_routine

-------------------------------------

cache 
B -> 100;
-------------------------------------

Generated code;

rec = x;
if rec.type == B:
    call 100
else:
    call lookup_routine
```

lookup_routine: go to object header, go to v-table, lookup 

smart jit compilers do is
```
main code:
...
call 100 // foo location
...


100:
if this.type != B  
    call lookup_routine
foo's body
```

in this case we can start prefetching the instructions in the functions even before performing the check  
if true then we will need to flush, but if false then we saved precious cycles by prefetching 

------

When do we want the inline cache to become polymorphic? 
### Polymorphic inline Cache (PIC)
- say A is 49%, B is 48%, C is 3% times called
- We usually have a small amount of objects that might be called

```
...
rec = x;
goto PIC_stub


--------------------------------------
PIC stub

if rec.type == A:
    call A.foo      // from CACHE
else if rec.type == B:
    call B.foo      // from CACHE
else 
    lookup
```

- usually size of 8 or 10 , till the number of branches is worse than doing lookup,  
- The entries in the stub should be ordered by the frequency  
- the PIC stub is not inlined as if the profile changes then we only need to change the one function and reorder instead of changing in th main code  
- We can also hash the values to find directly, asusming there are very few collisions,  
- We can also do binary search
- Two different callsites can point to the same PIC_stub as pic stub takes more memory


#### Method Inlining based on PIC
```
PIC STUB :

if this.type == A:
    return this.x               // inline A.foo() {return this.x} into the STUB itself
elif this.type == B
    call B.foo()
else
    ...
```

#### RT type info for Method Inlining

Driven by Profiliing INFO
```
if type == A // GUARD
    result = reciever.x
elif type == B // GUARD
    result = reciever.y
else lookup
```
