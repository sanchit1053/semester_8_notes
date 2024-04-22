# Lecture 19 <div style="text-align:right"> 03/04/2024 </div>


## Deoptimization Infrastructure
Upon Deoptimization, (guard failure)
- Where to resume execution (in the interpretor)
- How to reconstruct the state of the baseline (interpretor)

```java
fooSAFE(x, y, z){
    d = 1;
#1: a = x * y;
    if(z!= 7) goto #1
    b = x*x;
    c = y*y;
    if(z != 7) returx a;
    else return b + c + d
}
```

Optimized version 
```java
fooOPT(x, y, z){
    // learned that z == 7 and x == 75
    guard(z == 7, x == 75)
    d = 1; // Remove, used in end
    a = x * y; // not being used can be ignored
    b = 5625 // Remove, used in end
    c = y * y;
    return c + 5626;
}
```


## FRAME STATE
```java
void x(){
    int i = 1;
    int j = 1;
    classA.a = 2; // FS [i = 1, j = 1]
    i = ClassA.b
    j = 3
    classA.c = 4; // FS[ i = 0, j = 1]
}
```


```java
void x(){
    int i = 1;
    int j = 2; // FS [i = 1, j = 2];
    y();                  ↑
}                         |
void y(){                 |
    int i = 3;            |
    classA.a = 0; // FS [i = 3]
}

```


## Guard and Anchoring
```java
void x(){
    i = classA.b
}
```

it is equivilant to 
```java
void x(){
    if(classA != null){
        i = classA.b;
    }
    else{
        throw NullPointerException;
    }
}
```

After putting up a guard
```java
void x(){
    guard(classA != null);
    i = classA.b;
}
```

insert the guard till the furthest dominator (code that will definatly run before the code)

```
if(c1){
    if(c2){
        S1 ← anchor for guard
        S2
        S3 ← guard
        S4
    }
}
```

Variable scope should be valid
