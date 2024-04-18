[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.




**MY ANSWER:**

The recurrence relation can be expressed as $T(n) = 3T(n/3) + n^5$ as the function makes 3 recursive calls of size n/3, and there are $n^5$ loop iterations.

We can use the base case T(1) = $O$(1) to solve our recurrence relation.

Now we can solve by substitution:

$T(n) = 3(3T(n/9) + (n/3)^5) + n^5$

$= 9T(n/9) + n^5/81 + n^5$

Generalization:

$= 3^iT(n/3^i) + (n/3^i)^5$

For $i = \log_{3} n$:

$= nT(1) + 1$

Since T(1) = $O$(1), we get n * $O$(1) + 1

We can ignore the n and the +1. Thus, we are left with our big- $O$ bound of $O$ (1)
