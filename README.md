# Numerical-methods
## Program and algorithm
- Set of algorithms along with statements for user interactions.
- Algorithms are predefined operations to convert input to output.
## Types of NM
1) Direct
   -fixed algorithms with fixed elementary steps.
   - Error is due to computer precision like rounding off

2) Itirative
   - Requires initial guess for the final solution.
   - Value is given as an input and then the algorithm would repeat until the input and output are equal.

3) Heuristic
   -Based on experience.
   -Does not guarantee a solution

## Fixed root iteration
- initial value x
- g(x)= {x + A/x}/2
 -  where A is the number whose sq root we want to find
 - g(x) value becomes the next x
 - when x is equal to g(x), that g(x) is the square root

 with for loop:
 ```
def g(x,A):
    val=(x+(A/x))/2
    return val
# Number, whose square root we want to find
A=5

# Maximum number of steps
MaxIter=4

# Start with a guess
xold=1

# Iterate
for n in range(MaxIter):
    xnew=g(xold,A)
    output = "{val1:5d} {val2:15.8f} {val3:15.8f}"
    print(output.format(val1=n, val2=xold, val3=xnew))
    xold=xnew
```

with while loop and maxiter value not known
```
def g(x,A):
    val=(x+(A/x))/2
    return val
# Number, whose square root we want to find
A = 5

# Tolerance for stopping the iteration
tolerance = 1e-6

# Start with a guess
xold = 1

# Initialize iteration counter
n = 0

# Iterate using a while loop until the tolerance is met
while True:
    xnew = g(xold, A)
    print(n, xold, xnew)

    # Check if the difference is smaller than the tolerance
    if abs(xnew - xold) < tolerance:
        break

    xold = xnew
    n += 1
```
## Range:
In Python, the range() function is a built-in function that generates a sequence of numbers. It is commonly used in for loops to iterate over a sequence of numbers. The general syntax of the range() function is as follows:
 ```
range([start], stop[, step])
```
    start: (optional): The starting value of the sequence. If not specified, the sequence starts from 0.
    stop: The end value of the sequence. The sequence generates numbers up to, but not including, this value.
    step (optional): The step or increment between each pair of consecutive numbers in the sequence. If not specified, the default step is 1.

# Mean value theorem

 
 ## Jupyter notebook of fixed root iteration
'http://localhost:8888/notebooks/fixed_root_iteration.ipynb'
