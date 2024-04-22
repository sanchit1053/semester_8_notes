# Lecture 23 <div style="text-align:right"> 17/04/2024 </div>

## Imprecisise Call Graphs
- inheritence
- some function overloading (such as variable number of arguments)
- conditionals (the language will not be expressive though)


## Reflection
get the name of the classes in the program 

```java

class A{
    void play(int p){
        // ...
    }
}


class M{
    void m(String c) throws Exception{
        Class<?> cls = Class.forName(c);
        Method mtd = cls.getDefaultMethod("play", null /* int.class | float.class*/ ); // argument_name, which does not take any arguments
        Object obj = cls.newInstance();
        mtd.invoke(obj, 10) // obj.play(10)
    }
}
```

The correct method would be say any function can be called at `invoke`, This is not scalabale

## Eval
- It takes a string and executes the code 

```javascript
x = 2
y = x + 5
print(y)

// We can reduce the code to just print 7
// But if we have

x = 2
eval(z)
y = x + 5
print(y)
```

`eval(z)` can change the code in a lot of ways, say `z = "x = 10"` then the output is different 
- Conservative way is to stop all optimizations

## Solutions
1. Prohibit the features
2. reflection aware static analysis
    1. Propogate string constants
    2. Propogate other args
    3. backward propogation (If later same object is used in other way, we get hint into what the object is and what method can be called)
        a. PTA, forward flow, pointer analsis
3. Profile Guided analysis and transformation
    1. Instrument, log, patch (Tamiflex + soot)
    2. Instrument, log, guards

```java
p = eval (arg + x);

---------------------------------
// can be changed to, if we profile that arg is "window", x is "height"

guard(arg = "window", x = "height")
p = window.height


---------------------------------
// nested guards

guard(arg == "window", x == [H])
p = window[x];

```

