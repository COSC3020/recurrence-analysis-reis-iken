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

Base case: T(n) = 1 for n $\le$ 1

The recurrence relation can be expressed as $T(n) = 3T(n/3) + n^5$ as the function makes 3 recursive calls of size n/3, and there are 3 nested loops in which the upper bounds are n * n, n, and n * n (resulting in n^5).

Let's expand:

$T(n) = 3(3T(n/9) + (n/3)^5) + n^5$
$= 9T(n/9) + n^5 + 3(n/3)^5$
$= 27T(n/27) + n^5 + n^5/3^4 + n^5/9^4$

Now let's make a generalization:

$T(n) = 3^iT(n/3^i) + n^5/3^{4(i-1)} + n^5/3^{4(i-2)} + ... + n^5$

Substituting in $i = \log_{3} n$:

$= nT(1) + n^5/(n^4 * 3^{-4}) + n^5/(n^4 * 3^{-8}) + ... + n^5$

$= n + (3^4(n)) + (3^8(n)) + ... + n^5$

Since we have a dominant term of $n^5$, we can conclude that our big $O$ bound is $O(n^5)$.
