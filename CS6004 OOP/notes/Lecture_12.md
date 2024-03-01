# lecture 12 <div style="text-align:right"> 21/02/2024 </div>

Constraints for object inlining
- Immutability
- no inheritence
- no synchronization
- fields should either be primitve or also be value classes
- no cycles in type declarations

```java
    class A{ // not value class
        int z;
    }
    class Point{
        int x;
        int y;
        A w;
    }
    class Rectange {
        point p1;
        point p2;
    }
    Rectangle(){ // constructor
        p1_x = p1_y = 0;
        p2_x = p2_y = 0;
        p1.w = new A();
        p2.w = new A();
    }
```

for `x = new Rectangel()` the steps are :-
- alloc(36)
- invoke constructor Rect<init>
- store the ref into r;

Constructor java can run in another thread ?? (didn't realy understand)

## Partial Escape Analysis

```java
    class A{
        int z;
    }
    
    static Map<K, val> map;
    m(){
        A k = new A(); // O1
        if (map.containsKey(k)){ // maybe called multiple times
            return map.val(k); // does not escape
        } else { // will not be used much only once for each 
            val = new V(); // escapes
            map.put(k, val);
        }
    }
```

- First optimize the object away
- move the new statement to the branch where it might escape
- put the values that might have changed before this in the new object
- **partial Escape Analysis** helps as we can optimize most of the time with some overhead when they do escape
