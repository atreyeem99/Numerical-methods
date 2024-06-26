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
```
import numpy as np
import math

def g(x,A=5):
    val = 5 * (1 - math.exp(-x))
    return val
xold=0.1
error_threshold=0.001
error=float('inf')
i=0
while error>error_threshold:
      xnew=g(xold)
      error=abs(xnew-xold)
      print(i,xnew,xold,error)
      xold=xnew
      i+=1
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
# Bisection method
```
def bisection_method(a, b, tolerance):
    iterations = 0
    while (b - a) > tolerance:
        midpoint = (a + b) / 2
        if midpoint**2 - 5 == 0:
            return midpoint, iterations
        elif (midpoint**2 - 5) * (a**2 - 5) < 0:
            b = midpoint
        else:
            a = midpoint
        iterations += 1
    return (a + b) / 2, iterations

def fixed_point_iteration(initial_guess, tolerance):
    iterations = 0
    x = initial_guess
    while abs(x**2 - 5) > tolerance:
        x = (x + 5 / x) / 2
        iterations += 1
    return x, iterations

if __name__ == "__main__":
    # Bisection method
    a, b = 1, 3
    tolerance_bisection = 0.001
    result_bisection, iterations_bisection = bisection_method(a, b, tolerance_bisection)

    # Fixed-point iteration method
    initial_guess = 2
    tolerance_fixed_point = 0.001
    result_fixed_point, iterations_fixed_point = fixed_point_iteration(initial_guess, tolerance_fixed_point)

    print(f"Bisection method result: {result_bisection}")
    print(f"Number of iterations for bisection method: {iterations_bisection}")

    print(f"\nFixed-point iteration method result: {result_fixed_point}")
    print(f"Number of iterations for fixed-point iteration method: {iterations_fixed_point}")
```
# Cobweb
- x=cosx oscillatory convergence
- x=sinx monotonous convergence
# Upper triangular matrix
Solvig an upper triangular matrix
# Flop count
# stressen multiplication
```
def strassen_matrix_multiply(A, B):
    n = len(A)

    # Base case: If the matrices are 1x1
    if n == 1:
        return [[A[0][0] * B[0][0]]]

    # Splitting matrices into quarters
    mid = n // 2
    A11 = [row[:mid] for row in A[:mid]]
    A12 = [row[mid:] for row in A[:mid]]
    A21 = [row[:mid] for row in A[mid:]]
    A22 = [row[mid:] for row in A[mid:]]

    B11 = [row[:mid] for row in B[:mid]]
    B12 = [row[mid:] for row in B[:mid]]
    B21 = [row[:mid] for row in B[mid:]]
    B22 = [row[mid:] for row in B[mid:]]

    # Strassen's recursive steps
    S1 = [[B12[i][j] - B22[i][j] for j in range(mid)] for i in range(mid)]
    S2 = [[A11[i][j] + A12[i][j] for j in range(mid)] for i in range(mid)]
    S3 = [[A21[i][j] + A22[i][j] for j in range(mid)] for i in range(mid)]
    S4 = [[B21[i][j] - B11[i][j] for j in range(mid)] for i in range(mid)]
    S5 = [[A11[i][j] + A22[i][j] for j in range(mid)] for i in range(mid)]
    S6 = [[B11[i][j] + B22[i][j] for j in range(mid)] for i in range(mid)]
    S7 = [[A12[i][j] - A22[i][j] for j in range(mid)] for i in range(mid)]
    S8 = [[B21[i][j] + B22[i][j] for j in range(mid)] for i in range(mid)]
    S9 = [[A11[i][j] - A21[i][j] for j in range(mid)] for i in range(mid)]
    S10 = [[B11[i][j] + B12[i][j] for j in range(mid)] for i in range(mid)]

    # Intermediate matrices
    P1 = strassen_matrix_multiply(A11, S1)
    P2 = strassen_matrix_multiply(S2, B22)
    P3 = strassen_matrix_multiply(S3, B11)
    P4 = strassen_matrix_multiply(A22, S4)
    P5 = strassen_matrix_multiply(S5, S6)
    P6 = strassen_matrix_multiply(S7, S8)
    P7 = strassen_matrix_multiply(S9, S10)

    # Computing result submatrices
    C11 = [[P5[i][j] + P4[i][j] - P2[i][j] + P6[i][j] for j in range(mid)] for i in range(mid)]
    C12 = [[P1[i][j] + P2[i][j] for j in range(mid)] for i in range(mid)]
    C21 = [[P3[i][j] + P4[i][j] for j in range(mid)] for i in range(mid)]
    C22 = [[P5[i][j] + P1[i][j] - P3[i][j] - P7[i][j] for j in range(mid)] for i in range(mid)]

    # Combining result submatrices
    C = [[0] * n for _ in range(n)]
    for i in range(mid):
        for j in range(mid):
            C[i][j] = C11[i][j]
            C[i][j + mid] = C12[i][j]
            C[i + mid][j] = C21[i][j]
            C[i + mid][j + mid] = C22[i][j]

    return C

# Example usage:
A = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12], [13, 14, 15, 16]]
B = [[17, 18, 19, 20], [21, 22, 23, 24], [25, 26, 27, 28], [29, 30, 31, 32]]

C = strassen_matrix_multiply(A, B)
for row in C:
    print(row)
```
# scipy 
 # function approximation (Model making)
 ## Jupyter notebook of fixed root iteration
 # vondermonde matrix
 # iterative interpolation
 # Lagrange interpolation
 # Integration      ( Rieman integration)
 # 11th exam
 # ODE
 # differential equations
 # how to make scatter plot square
'http://localhost:8888/notebooks/fixed_root_iteration.ipynb'
