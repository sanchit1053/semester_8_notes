## Lecture 1  <div style = 'text-align: right;'> 05/01/2024 </div >

### Object Oriented Programming

- Polymorphism 
- abstraction
- Encapsulation
- Inheritance
- Objects
- Classes

Example:-  
1. Function need to store the rational numbers (each rational number requires 2 variables)  
2. We can create a class called Rational with two variables and then we do not need to worry about mixing numerator of one with denominator of other ___encapsulation___
3. We can also reuse the variable name ( say x and  y) in another class like "Point"  
4. It will also stop cases like `rational_1 = rational_2 + point_1`
5. Now we need a class of 3dPoint, it will have 3 components, Inheritance will allow to say that 3d point extend 2d point and then we can reuse `x` and `y` 
6. each of 2dPoint, 3dPoint can have same function like addPoints ___Polymorphism___


### Lets's summarize the costs (for Java)
- Field access through objects involves indirection
- Method overloading complicates virtual calls
- Type safety requires checks 
- Throwing exceptions instead of crashing requires many many checks
- Collecting garbage requires runtime analysis

### But OO programs run fast enough
- OO language dominate the software development industry
- OO code is written for everything ranging from satellites to handheld devices
- People are even writing virtual machines and kernels using OO languages


```Java
public class Rectange {
    private int h;
    private int w;
    
    public int area() {
        return w*h;
    }

    public boolean sameArea(Rectangle other){
        return this.area() == other.area();
    }

    public static void main(final String[] arg){
        \*
            Makes about 500,000,000 rectanges 
            and then compare if they have the same area
        *\
    }
}
```

The oop code is not very slow then direct code but if the optimizations are turned off it becomes slower

### What does this course include 

- Fundamentals 
    - OO abstraction
    - memory organisation
- Heap analysis
     - Points-to information
     - field- and flow-sensitivity
     - intra- and inter-procedural analysis
     - alias analysis
     - heap cloning
- Optimization involving allocation, field access and deallocation
    - escape analysis and stack allocation
    - scalar replacement
    - field privatization
    - value types and object inlining
    - object collocations
    - control-sensitive analysis
    - garbage collection
- Optimization involving method dispatch
    - class hierarchy analysis
- Optimizations involving method dispatch
- Speculative optimizations
- Recent Developments
