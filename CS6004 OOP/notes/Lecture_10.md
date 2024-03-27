# lecture 10 <div style="text-align:right"> 14/02/2024 </div>

```java
    public class Test{
        public static Node global;
        public static void main(String[] args){
            foo();
        }
        public static Node foo(){
            Node x = new Node(); // O1
            x.f = new Node(); // O2
            x.f.g = new Node();
            Node y = new Node(); // O3
            node z = new Node(); // O4
            y.f = z;
            bar(x.f, y);
            return y.f;
        }

        public static void bar(Node p1, Node p2){
            Node w = new Node(); // O5
            w.f = new Node(); // O6
            p2.f = w.f;
        }
    }
```

Objects on the stack possible
- for Bar
    * O4
- for foo
    * O1
    * O2, O3 for interprocedural (we know nothing happens in bar so put in stack)


## Scalar Replacement
```java

    class Circle{
        float r;
        Circle(float r){
            this.r = r;
        }
    }

    float foo(float d){
        Circle c = new Circle(d/2);
        return c.r * c.r * PI; // area
    }
```

remove the object entirely, so the code changes to 

```java
    float foo(float d){
        float c_r = d / 2;
        return c_r * c_r * PI;
    }
```

Scalar replacement can be done if 
- The object does not escape
- object not passed as parameter `foo(a)`
- no typechecking `a instanceof T`
- no reference equality `a==b`
- no null check `a==null`
- no typecast `(T)a`

```java
    a = new A();
    b = new A(10, 20); // O2; 
    a = b;
```

if we scalar replace b, then we can scalar replace a as `a_x = b_x; a_y = b_y`  
Need to make sure that if `b.x, b.y` change then `a.x, a.y` should also change


## Field Privatization

```java
    o = new (); // o escapes
    while(*){
        temp = o.f // for something
        // ......
        o.f = something;
    }
```

the code block can be very big, so break the oject and then recreate it

```java
    t = o.f;
    while(*){
        temp = t;
        //......
        t = something
    }
    o.f = t;
```

- o hasn't escaped untl the loop body
- o is not redefined in the loop
