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

### Recurrence Relation

At the beginning of the function, there is a check for the base case ($n \le 1$). This just
causes a return statement, meaning $T(1) = 1$ for $n \le 1$

When n is greater than 1, the function calls itself with n/3. It declares and intiializes a variable
to 0, which doesn't affect the asymptotic complexity, then makes another call to itself with n/3. Next, 
there are three nested for loops. The first iterates by 1 from 0 to $n^2$. The next loop iterates by 1 
from 0 to $n$. The inner-most loop iterates by 1 from 0 to $n^2$. The only thing this loop does is 
increment the previosuly initialized variable, which does not affect the asymptotic complexity. Finally 
there is another recursive call with a value of n/3. Therefore, ignoring constants, when n is greater 
than 1, we have:

$T(n) = T(\frac{n}{3}) + T(\frac{n}{3}) + n^2 \cdot n \cdot n^2 + T(\frac{n}{3}) = 3T(\frac{n}{3}) + n^5$

This gives us a final recurrence relation of:

$$ T(n) =
    \begin{cases}
        1 & n \leq 1\\
        3 T\left(\frac{n}{3}\right) + n^5 & n > 1
    \end{cases}
$$

### Time Complexity

#### Expand the Relation

$3 T\left(\frac{n}{3}\right) + n^5 = 3(3T\left(\frac{n}{3^2}\right) + \left(\frac{n}{3}\right)^5) + n^5 = 3^2 T\left(\frac{n}{3^2}\right) + \left(\frac{n^5}{3^4}\right) + n^5 = 3^3 T\left(\frac{n}{3^3}\right) + \left(\frac{n^5}{3^8}\right) + \left(\frac{n^5}{3^4}\right) + n^5$

#### Simplify

$3^i T\left(\frac{n}{3^i}\right) + n^5\displaystyle\sum_{k=0} ^{i-1}{(\frac{1}{3})^{4k}}$

