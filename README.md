Custom task: A simple scientific (ha-ha) tool with a console user interface. Additional challenge: use no ";" to join lines.

The resulting code can do three things:

1. Generate prime numbers
2. Generate Pascal's pyramid
3. Calculate the Fibonacci sequence

Why does the code work? Let's format it a bit now:
```
(
    lambda f:
        print(f'''Result: {
            str(
                (lambda n: [x for x in range(2,n) if all(x%i for i in range(2,int(x**0.5)+1))]) (int(input('Set the upper limit: ')))
                ).replace('[', '').replace(']', '')
            }''')

        if f==1 else
    
            (
                [
                    globals().__setitem__("a", lambda n: [[1 if i==0 or i==k else a(n-1)[k-1][i-1]+a(n-1)[k-1][i] for i in range(k+1)] for k in range(n)])
                    if x==0 else
                    print("Result: \n" + '\n'.join(str(lst) for lst in a(min(7, int(input("How many layers of the pyramid you want? (>=7): "))))))
                  
                    for x in range(2)
                ]

                if f==2 else

                print("Result: " +
                   str(
                       (lambda n: __import__('functools').reduce(lambda x,_: x+[x[-1]+x[-2]], range(n-2),[0,1])[:n])(int(input("How many numbers do you want? ")))
                    ).replace("[", "").replace("]", ""))
            )
)
(int(input("Prime number generator - 1\nCreate Pascal's pyramid - 2\nCalculate Fibonacci sequece - 3\n>")))
```

Now you can see how the code works much better. Let's review why it's bad, section by section.

The first and most important thing to notice is the main lambda. It is used to store user input in a variable to use it in two places (because we can't use input() multiple times, as it would ask for input each time it's called). Do you see where we call it? Yes, at the end, by doing: `(int(input("Prime number generator - 1\nCreate Pascal's pyramid - 2\nCalculate Fibonacci sequece - 3\n>")))`

Okay, now onto the next two sections. We have if f==1 else separating them. If f (the user's input) is 1, we call the first print(), which is the prime number generator. It's a lambda function that is called right after it's created.

The next chunk is a bit more interesting. It contains two other functionalities: Pascal's pyramid and the Fibonacci sequence:

```
[
    globals().__setitem__("a", lambda n: [[1 if i==0 or i==k else a(n-1)[k-1][i-1]+a(n-1)[k-1][i] for i in range(k+1)] for k in range(n)])
    if x==0 else
    print("Result: \n" + '\n'.join(str(lst) for lst in a(min(7, int(input("How many layers of the pyramid you want? (>=7): "))))))
                  
    for x in range(2)
]

if f==2 else

print("Result: " +
    str(
        (lambda n: __import__('functools').reduce(lambda x,_: x+[x[-1]+x[-2]], range(n-2),[0,1])[:n])(int(input("How many numbers do you want? ")))
    ).replace("[", "").replace("]", ""))
```

As you can see, if `f==2` else checks whether the user wants option 2 (Pascal's pyramid) or 3 (the Fibonacci sequence). As you may have noticed, it will run the Fibonacci sequence for any input except 1 or 2, not strictly for 3 as it should. Why? You're right—because the code is intentionally bad, as it should be.

The first section is what's interesting here. The lambda NEEDS to be in a separate variable because it calls itself, but we can't do a = lambda n... due to the if else structure. So yes, we use globals().__setitem_ because it's a function call and doesn’t interfere with the if else. Okay, but we also need to run two lines of code, and we can't use semicolons. There's a workaround for this: we use a for loop with range(2) to run the if else structure twice, and inside it, we determine which line to run.

Finally, we have a simple Fibonacci sequence generator using a single lambda function with no variables—it's simple.

And to make the code even worse, three different formatting methods were used: 

**f"Text: {str().replace().replace()}"**

**"Text" + str().replace().replace()**

**f"Text: " + "".join()**

Why? Yep, because the code is intentionally shit.
