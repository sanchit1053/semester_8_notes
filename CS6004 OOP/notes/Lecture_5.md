# Lecture 5 <div style="text-align:right"> 19/01/2024 </div>

- stack,    
    * map that takes a variable and returns set of obects $V \rightarrow 2^{obj}$
    * a variable can point to a set of objects, eg, if there is a branch
- Heap  
    * $Obj \times F \rightarrow 2^{Obj}$  
    * f is the fields
    
```java
    a = new A(); // O1
    a.f = new B(); // O2
    a.f.g = new C(); // O3
    c = a.f.g;
    d = a;
    e = a.f;
    p = new A(); //O7
```

- `stack[a] = {O1}` | `Heap[O1, f] = {O2}`
- `stack[c] = {O3}` | `Heap[O2, g] = {O3}`
- `stack[d] = {O1}`
- `stack[e] = {O2}`
- `stack[p] = {O7}`

```java
    a = new A(); // O1
    b = new B(); // O2
    c = new C(); // O3
    a = b;
    b = c;
    c = a;
```

- IN[1] : 
- `OUT[1]` → `Stack[a]= {O1}`
- `IN[2] ` → `Stack[a]= {O1}`
- `OUT[2]` → `Stack[a] = {O1}, stack[b] = {O2}`
- `IN[3] ` → `Stack[a] = {O1}, stack[b] = {O2}`
- `OUT[3]` → `Stack[a] = {O1}, stack[b] = {O2}, stack[c] = {O3}`
- `OUT[4]` → `stack[a] = {O2}, stack[b] = {O2}, stack[c] = {O3}`
- `OUT[5]` → `stack[a] = {O2}, stack[b] = {O3}, stack[c] = {O3}`
- `OUT[6]` → `stack[a] = {O2}, stack[b] = {O3}, stack[c] = {O2}`
- No one pointing to O1 so garbage collect it

## Flow Insensitivity 
- Do not care about the steps check all steps seperately 
- so `stack[a] = {O1, O2, O3}`
- so `stack[b] = {O1, O2, O3}`
- so `stack[c] = {O1, O2, O3}`

```
    --------------- FLOW SENSITIVE ------------------

L:  v = new()
    -----------------
    Stack[v] = {OL}

    v = w
    -----------------
    Stack[v] = stack[w]

    v.f = w
    -----------------
    ∀ Ov ∈ Stack[v]   Heap[Ov, f] = stack[w]

    v = w.f
    -----------------
    stack[v] = {}; ∀ Ow ∈ stack[w], stack[v] U= Heap[Ow, f]
```

-- we need to do it again and again till fixed point

```
    --------------- FLOW INSENSITIVE ------------------

L:  v = new()
    -----------------
    Stack[v] U= {OL}

    v = w
    -----------------
    Stack[v] U= stack[w]

    v.f = w
    -----------------
    ∀ Ov ∈ Stack[v]   Heap[Ov, f] U= stack[w]

    v = w.f
    -----------------
    ∀ Ow ∈ stack[w], stack[v] U= Heap[Ow, f]
```

## Field Sensitivity

```java
    a = new A(); // O1
    a.f = new B(); // O2
    a.f.g = new C(); // O3
    c = a.f.g;
    d = a;
    e = a.f;
    p = new A(); //O7
```

field insensitive : Through a we can point to what
- `Stack[a] = {O1, O2, O3}`
- `Stack[c] = Stack[a]`
- `Stack[d] = Stack[a]`
- `Stack[e] = Stack[a]`
- `Stack[p] = {O7}`

```java
    arr = new int[SIZE]; // on heap only one object but with SIZE slots
    arr = new A[SIZE];   // will have slots that point to different objects
    for(i : 1 to SIZE){
        arr[i] = new A(); // O2
    }
```

`Heap(O1,"[]") = {O2}`

