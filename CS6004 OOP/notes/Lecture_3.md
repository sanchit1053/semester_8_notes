# Lecture 3  <div style = 'text-align: right;'> 11/01/2024 </div >

## Object Layouts & Method Dispatch

    = a.x
    relative address of the right field

#### Method → Functions
```Java
class A{
    int x; int y;
    int m1(int z){
        int t1 = x + y + z;
        return t1;
    }

    int m2(){
        return x; // this.x
    }

    void m3(){
        
    }

    void m3(){

    }
}
```

Changes to 

```Java
int A_m1(A mthis, int z){
    int t1 = mthis.x + mthis.y + z;
    return t1;
}

int A_m2(A mthis){
    return mthis.x;
}
```


#### Translating constructors
- Allocating a Object
    * Header 
        + for 64 bytes machines header is of size 12 Bytes
        + there are 2 words (4 bytes) of marks and 1 word of Klass
        + Marks
            + INfo about locks, GC, identitiy
        + Klass
            + Metadata about class A
    * Payload 
        + Depends on the fields of the object like 4 bytes of x and 4 bytes of y

```Java
A a = new A();
```

- `x1 = alloc(20)` 12 from header 8 from fields
- `x1[12] = 0` Default value of int x will be 0
- `x1[16] = 0` Default value of int y will be 0
- `x2 = alloc(16)` Vtable space
    - store the address of `A_m1, A_m2, A_m3, A_m4`
    - it is not created for every object initialization (once for class __OPTIMIZATION__)
    - `x2[ 0] = &A_m1`
    - `x2[ 4] = &A_m2`
    - `x2[ 8] = &A_m3`
    - `x2[12] = &A_m4`
- store the vtable in klass of object `x1[8] = x2`
- `a = x1` store the created object in *a* 

The Function changes to 

```Java
int A_m1(A mthis, int z){
    int t1 = mthis[12] + mthis[16] + z;
    return t1;
}

int A_m2(){
    return mthis[12];
}
```

### Methods are bound dynamically
```Java
int r = a.m1(5)
```

so we can break the procedure address
```Java
    z = a[8] // vtable
    r = z[0](a, 5);
```

With Inheritence
```Java
Class B extends A{
    int x; 
    int z;
    int m1(int p){
        int t2 = m2();
        int t3 = 2 * x + y - p + t2;
        return t3;
    }

    int set(int a, int b){
        x = a;
        z = b;
    }
}
```

Allocating B
- Class B header
    * 8 bytes Mask
    * 4 bytes Klass
    * 4 bytes `A.x`
    * 4 bytes `A.y`
    * 4 bytes `B.x`
    * 4 bytes `B.z`
- Vtable (This table is only for B, A will have a different Vtable)
    * &B.m1
    * &A.m2
    * &A.m3
    * &A.m4
    * &B.set

```Java
int B_m1(B mthis, int p){
    int t2 = mthis[8][4](mthis); // vtable -> m2 function
    int t3 = 2 * mthis[20] /* B.x */ + mthis[16] /* A.y */ - p + t2;
    return t3;
}
```

when A's m2 function is called the field is bound statistically so the `mthis[12]` will be called which is `A.x`

The Vtable is given by the object that is calling it so if B object calls m1 then the Klass will send it to B's Vtable, where m1 was overwritten  
Other wise if object of type A calls it then original is called

