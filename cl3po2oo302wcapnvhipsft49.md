## Understanding Closures in JavaScript

# Introduction
According to our friendly neighborhood teacher MDN Docs: 

**A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment).
**

> Function + it's lexical environment = Closure

# First things first
Now, we know what a function is and in order to understand Closures completely, we first need to understand Lexical Environment. 

If you already understand Lexical Environment lets move ahead, if not then I already have a dedicated blog explaining Lexical Scope and Environment from scratch, to read it [click here ↗️ ](https://maitrakhatri.hashnode.dev/understanding-lexical-scope-in-javascript)

So now you know how lexical scope works.

TL;DR - inner functions can use parent/outer function's variables and functions.

This can be shown by very simple example: 

```
function greet() {
  const userName = "Maitra";
  function greetMsg() {
    console.log("Welcome,", userName);
  }
  greetMsg();
}
greet(); //output: Welcome, Maitra
```

Now, what if I need to extract the inner function and use it like an independent function. Will then it be able to access the `userName` variable from its parent function ?

The answer is YES !! and the reason is Closures !!!!

# Closures
You don't believe me ? Try it yourself: 

```
function greet() {
  const userName = "Maitra";
  return function greetMsg() {
    console.log("Welcome,", userName);
  };
}
const displayMsg = greet();
console.log(displayMsg); //output: ƒ greetMsg() {}
console.log(displayMsg());//output: Welcome, Maitra
```

As you can see, `displayMsg` is nothing but the function `greetMsg` but the interesting thing here is that the function `displayMsg` has no mention of the constant `userName`, still when called it prints its value.

Although, we we extract an inner function and we can see that the function is alone, but it always comes with its lexical environment (i.e its own lexical scope + its parent's lexical scope) 

That's it, the simplest explanation of what Closure is. We can also say that: 

> Closure is a function that remembers the variables from the place where it was defined, regardless of where it is executed later.

# Little fun ft. Doremon
Now I wanna have some fun and that's why I have prepared this fun example that uses closure.

```
function pocket() {
  const strengthPill = true;
  function doremon() {
    return function nobita() {
      function fightGian() {
        if (strengthPill) {
          console.log("win");
        } else {
          console.log("lose");
        }
      }
      fightGian();
    };
  }
  return doremon();
}
const nobitaAlone = pocket();
console.log(nobitaAlone); //output: ƒ nobita() {}
console.log(nobitaAlone()); //output: win
```

Here, we can see that only if `nobita` has the `strengthPill` then he can win against `Gian`. And as usual `nobita` is under the protection of `doremon` and has access to the `strengthPill`. But what if he has been extracted out and he is alone ???

As we can see in the function `nobitaAlone`, we only have the function `nobita` and no mention of the `strengthPill`, so technically he should lose. But thanks to Closure `nobita` still has access to the `strengthPill` and can defeat Gian 🥳  

I hope you learned something new and enjoyed the fun in the end. If you did then do checkout:

- [my other blogs](https://maitrakhatri.hashnode.dev/)
- [my projects](https://github.com/maitrakhatri)

And don't forget to follow me :)

