# Lecture 2  <div style = 'text-align: right;'> 10/01/2024 </div >

### Runtime Memory Organization
- Stack (last in first out)
- Heap


```Java
class Animal{
    int x;
    int y;
}

Animal a;
a = new Animal(); // then only memory is put on the heap
// alloc
```

- Allocate memory on the heap
- Call the constructor
- Store the reference on the stack

```Java
Animal b = a;
// copy
```

`b` points to the same location as `a`;

if 
```Java
class Animal{
    int x;
    int y;
    A z;
}
```

We do not allocate an object z but just have a pointer stored

```Java
a.z = new A();
// store

A q = b.z // wlll have q on stack
// load
```

```Java
Class Animal {
    int x;
    int y;
    Animal(){
        x = y = 10;
    }
    void speak(){
        System.out.prinln("Animal speak" + y);
    }
    
    void tail() {
        System.out.prinln("Animals tail");
    }
}

Class Monkey extends Animal(){
    int y;
    int z;
    Monkey(){
        x = 20;
        y = 20;
        z = 20;
    }
    void tail() {
        System.out.println("Monkey's tail");
    }
}
``` 


- Field are bound Statically
- Methods are bound Dynamically
