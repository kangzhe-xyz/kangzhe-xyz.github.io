---
date: '2026-07-06T12:27:52+09:00'
draft: false
title: 'Getting Back into Programming'
---
The other day my friend gave me a "coding interview", after hearing that I wanted to get back into programming.

He gave me two tasks: to add and multiply very large (positive) numbers.

Since these numbers are potentially very large, I am not allowed to directly cast them with `int()`; instead the inputs and outputs have to be strings.
I am however allowed to cast one digit at a time.

Effectively, I am asked to implement manual addition in code, and given that I have not written a piece of code by hand without AI at all for around a year, I was quite happy that I was able to sit down to work through the problem and finish both tasks within around an hour.

# `addbignum()`
As the name of the function suggests, two numbers will be given as strings, and I have to output a string that is the sum of the two large numbers.
This is my implementation:

```python
def addbignum(x,y):
    output = ""
    carry_flag = 0
    d = len(x) - len(y)
    if d < 0:
        for _ in range(-d):
            x = "0" + x
    elif d > 0:
        for _ in range(d):
            y = "0" + y
    
    for i in range(len(x)-1,-1,-1):
        a = str(int(x[i]) + int(y[i]) + carry_flag)
        if int(a) < 10:
            carry_flag = 0
        else:
            carry_flag = 1
            a = str(int(a) % 10)
        output = a + output 
    if carry_flag == 1:
        output = "1" + output
    return output
```

My good friend Way Yan has kindly provided me feedback.
One of them that stuck with me is 

> instead of `int(x[i])` you can do `ord(x[i])-ord('0')` which computes the ASCII offset of the ASCII digit `x[i]` relative to the ASCII digit `'0'`

and this trick works because 

> each character has an ASCII code
>
> and it happens that the ASCII characters 0-9 have contiguous codes

I am admittedly not sure how much faster `ord()` is compared to casting with `int()`.
My intuition tells me that `ord()` is doing a lookup, so it should be $O(1)$, and maybe that is why it is preferred. 
But that is just a wild guess.

Nonetheless, I am happy that this function worked!

# `multbignum()`
As the function name suggests, I need to now multiply two positive integers.
However, I am allowed to use `addbignum()`.
Here is my implementation.

```python
def bunchofzeroes(n):
    string = ""
    for _ in range(n):
        string += "0"
    return string
        
def multbignum(x,y):
    output = ""
    if x == "0" or y == "0":
        return "0"
    for i in range(len(x)-1,-1,-1):
        ypower = y + bunchofzeroes(len(x) - i - 1)
        for j in range(int(x[i])):
            output = addbignum(ypower,output)
    return output
```

I realised I would need the `bunchofzeroes()` function to deal with shifting across the place values in the number, so I wrote that halfway through writing the solution.

The variable name `ypower` was admittedly born out of a strange idea. 
Since I was moving through the place values, I thought that it would be a good idea to explicitly work with the exponent of the digit $10^n$. 
This however ended up to be quite clunky, and defeats the point making this function work with very big numbers, so I eventually gave up on that idea. 
However, I did not change this variable name.

# Other Comments 
Given that I have lost my touch with writing code, I also forgot many rules on style for writing good code. 
One of them that my friend told me was 

> also one more comment, the meta for naming in python is to use snake case, so like `add_big_num`
> 
> anything in general except for classes
> 
> which are named `LikeThis`

I also wrote a little snippet for test cases:
```python
array_x = [123,456,678,1234,23462345,0]
array_y = [12345123,23423,1234,2354,234,123]
for i in range(len(array_x)):
    if int(multbignum(str(array_x[i]), str(array_y[i]))) - (array_x[i] * array_y[i]):
        print("fail")
    else:
        print("pass")
```
and one might probably be very grossed out by the `if` statement — understandably so.
I was so focused on making the condition evaluate to zero to make use of the "truthy" and "falsey" properties of Python booleans. 
However, this could have been done much cleaner. 
I forgot that `!=` existed.

> I think using != instead of - is clearer, it is a slight miracle of python syntax that your code works

# Final Thoughts
This exercise was a nice confidence booster, where I reminded myself that I still have some programming skills, such as working through an idea, tracing code, debugging, considering edge cases, and so on.
Perhaps now I just have not seen or written enough code yet, so my repertoire is still small.

In the next semester, I am intending to take programming classes again after five semesters.
I plan to take [CS2030 Programming Methodology II](https://nusmods.com/courses/CS2030/programming-methodology-ii) and [CS2040 Data Structures and Algorithms](https://nusmods.com/courses/CS2040/data-structures-and-algorithms).

Generative AI and the likes have made it very easy to write code fast, and I do not deny that they are good tools. 
However, I would also like to put myself through learning programming again properly. 
I quite like [this video](https://www.youtube.com/watch?v=HTUh0OO6Kmo) from JetBrains; one of the key messages I would like to bring forward in the things I do is that if I am using AI, I should have the confidence to be able to write that code myself in the first place.

{{< youtube HTUh0OO6Kmo >}}

I am excited to learn more! 

---

> me: i am irrationally proud of addbignum()

> way yan: not a trivial function!