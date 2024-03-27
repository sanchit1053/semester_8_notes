# Lecture 6 <div style="text-align:right"> 24/01/2024 </div>

## Pointer Analysis via IDFA(Iterative Data Flow Analysis)

```java
    a = new A(); // O1
    a.f = new B(); // O2
    a.f.g = new C(); // O3
    c = a.f.g;
    d = a;
    e = a.f;
    p = new A(); // O7;
```

### Points to Graph (PTG)

```mermaid
graph LR
    a([a]) & d([d])-->O1
    O1 -->|f| O2 
    e([e]) --> O2
    O2 -->|g| O3 
    c([c]) --> O3
    p([p]) --> O7
```

### Initialization
say that the above code is part of a function which has parameters `p` and `q`;  
∀ parameters `p` create a dummy object for each parameter

```mermaid
graph LR
    p([p]) --> Op
```


<table>
<thead>
<td> statement </td> <td> Existing </td> <td> Generated </td>
</thead>
<tr>
<td> l -> v </td>
<td> 

```mermaid
graph LR
    l([l])
    v([v]) --> O
```

</td>
<td>


```mermaid
graph LR
    l([l]) & v([v]) --> O
```

</tr>
<tr>
<td> l1 = l2.f </td>
<td>


```mermaid
graph LR
    l1([l1])
    l2([l2]) --> O -->|f| O2
```

</td>
<td>

```mermaid
graph LR
    l1([l1]) --> O2
    l2([l2]) --> O -->|f| O2
```

</td>
</tr>

<tr>
<td>
l1.f = l2
</td>
<td>


```mermaid
graph LR
    l1([l1]) --> O1
    l2([l2]) --> O2
```

</td>
<td>

```mermaid
graph LR
    l1([l1]) --> O1-->|f| O2
    l2([l2]) --> O2
```

</td>
</tr>
<tr>
<td>
l = new()
</td>
<td>


```mermaid
graph LR
    l([l])
```

</td>
<td>


```mermaid
graph LR
    l([l])-->O
```

</td>
</tr>
</table>


$\text{OUT}(n) = ([(n)]) \text{IN}(n)$


Possible that there is no object l2.f 
- Two Cases:
    * If it is a dummy object then it should point to another dummy object (case when they are a parameter)
    * Otherwise if we know it is not initialized then it should be NULL;


### Join Operation
```java
    a = new(); // O1
    a.f = new(); // O2
    b = new(); // O3
    if(*){
        b.f = new() // O4     
        r = a;
    }
    else{
        b.f = new() // O5     
        r = b;
    }
    s = r 
    b.f.g = new() //O7
```

True IF STATEMENT

```mermaid
graph LR
    a([a]) & r([r]) --> O1 -->|f| O2
    b([b]) --> O3 -->|f| O4
```

False IF statement

```mermaid
graph LR
    a([a])--> O1 -->|f| O2
    b([b]) & r([r])  --> O3 -->|f| O4
```


We are working with may point to, So we take the **union** of graph


```mermaid
graph LR
    a([a]) & r--> O1 -->|f| O2
    s([s]) --> O1 & O3
    b([b]) & r([r])  --> O3 -->|f| O4 & O5 -->|g| O7
```

## IDFA 
- Initialize all Ins and outs
- process the entry ( create the dummy objects for all non-primitive )
- Initialize a worklist (list containing all the things need to be done)
    * `W U= Nodes`
- While Worklist is not empty do
    * remove a statement n from the worklist `W = W - {n}`
    * Process the statement 
        + `IN(n) = ∀ U OUT(p)` for all predecessors
        + `OUT(n) = ([n])IN(n)`
    * if OUT(n) changed then add all successors that depend on n to W <br> `∀ s ∈ successors(n) W = W U {s}`

The program stops if:
- There are finite number of entries 
- monotonic number of nodes in graph, Graph only increases
