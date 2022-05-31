## Understanding Lexical Scope in JavaScript

# Introduction

Remember the time when you're writing some code, you try to access an variable but it throws an error that `variable is not defined`. But you can clearly see that you have defined it and used it multiple times in the function above. That's exactly where **Lexical Scope** comes in the picture.

# Lexical Scope

Let's understand this by an example :

```
const name = "Maitra";

function helloWorld() {
    console.log("Hello World !! I'm", name);
}

helloWorld(); //Output: Hello World !! I'm Maitra
```

Here you have declared a variable in Global and can use anywhere in the code, inside many nested function and it will still work. But it does not work vice versa.

```
function user() {
    const userName = "Maitra";    
}
user();

console.log("Hello World!! I'm",userName); //Output: Uncaught ReferenceError: userName is not defined
```

This happens because `userName` is not present in the Global Scope, it's only present in the lexical scope of the function `user`.

In very simple words lexical scope means **the places in your code where a certain variable/function is accessible and you can use it.**

Now let's talk about what all things comes under the lexical scope of a function, lexical scope of any function has two things:

1. It's own local memory
2. Lexical Scope of the Parent

It means a function can access all the variables & functions that are defined inside itself and in it's parent.

> Lexical Scope = Local Memory + Lexical Scope of Parent

Example: 

```
const greetings = "Good Morning !!"

function greetUser() {
    const userName = "Maitra"
    console.log(greetings, userName)
}

greetUser();//Output: Good Morning !! Maitra
```

Note: by default `global` is the parent of all functions.

Trivia: `global` also has a parent, it points to `null`, so when the program reaches to the global's parent it exits. 

# Scope Chain

Now here comes the interesting part, a function can not just access it's parents variables & functions but all the ancestor's too (Ancestors are parent's parent). Let's understand this by a very simple yet effective example: 

```
const a = "This"
function scopeChain() {
    const b = "is a"
    function x() {
        const c = "simple yet"
        function y() {
            const d = "effective example"
            function z() {
                const e = "of Scope Chain"
                console.log(a,b,c,d,e)
            }z()
        }y()
    }x()
}

scopeChain() //Output: This is a simple yet effective example of Scope Chain
```

This is how the above example works: 

1. function `z` looks for `a` `b` `c` `d` `e` inside itself.
2. It finds `e` but not others, so it goes into it's parents (`y`) lexical scope and looks for them
3. There it finds `d` but not other, so it goes to it's parents lexical scope
4. And this loop continues until all the variables are found

> The entire process of searching inside local memory/own lexical scope, if not found then go to parent's lexical scope and repeat is know as **Scope Chain**

Remember here I said illustrated all the examples using variables but all of this rules applies to functions too, as functions are first class citizens in JS.

I hope this helped you, if it did then do let me know and also share it with your friends because knowledge is the only wealth that increases on sharing :)



