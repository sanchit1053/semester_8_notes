# lecture 11 <div style="text-align:right"> 16/02/2024 </div>

## Object Inlining
```java
    class Account {
        int balance;
    }

    class Point{
        int x;
        int y;
    }
    // 2,3 is not same as 4, 3

    class RetNum{
        int n;
        int d;
    }
    // 3/4 is same as 6/8
    // 3/4 is not same as 4/5
```

some objects are tied directly to the fields of the objects, eg :- point can be defined by the fields, but different accounts can have same balance and thus each object is needed

> OPTIMIZATION: use the same point everywhere if it has the same value, like immutable string in JAVA

```JAVA
    class Rectange{
        Point p1;
        Point p2;

        int area(){
            return abs(p1.x - p2.x) * abs(p1.y - p2.y);
        }
        // number of memory loads 
        // this, this.p1, this.p1.x, this.p2, this.p2.x, this.p1.y, this.p2.y
        // = 7 (if this, this.p1, this.p2 are in register)

        // = 9 (if this is in register)
    }
```

this will have a header of 12 bytes 
```
    this ->   ┌─────
              | H  |
              ────── 12
              | p1 |
              ────── 16
              | p2 |
              ────── 
    similarly for p1 and p2
```

Can have 3 cache misses,  
We can directly store the points in the this block, this will remove one level of indirection

```
    this ->   ────────
              | H    |
              ────────12
              | p1.x |
              ────────16
              | p1.y |
              ────────20
              | p2.x |
              ────────24
              | p2.y |
              ────────
    similarly for p1 and p2
```

so using this the function becomes
```java
    int area(){
        t0 = this;
        return abs(t0[12] - t0[20]) * abs(t0[16] - t0[24]);
    }
```

advantages
- Fewer memroy access
- Faster field loads
- Better cache locality

data
- Memory saved for this example = 32/60 
- Cache missed = 3 → 1

#### Constraints for inlinearity
- Objects : immutable
- no "synchronized" on the object
- inherit the class of an initial object X
- determinable structure : no cyclic dependencies
- (**debatable**) inlined fields should contain values  

#### Changes
- Modify the allocation of Rectangle
- Each method are a accessible


```
    
    this ->   ───────────
              | H       |
              ──────────
              | p1 head |
              ──────────
              | p1.x    |
              ──────────
              | p1.y    |
              ──────────
              | p2 head |
              ──────────
              | p2.x    |
              ──────────
              | p2.y    |
              ───────────
```

- (**Object Colocation**) Garbage collectors should move them apart
