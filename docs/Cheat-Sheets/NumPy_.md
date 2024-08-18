---
title: NumPy (Cheat Sheet)
description: A cheat sheet of NumPy (The fundamental package for scientific computing with Python). Specifically made for data science interviews

# NumPy

[TOC]

NumPy, which stands for Numerical Python, is a free, open-source Python library for working with arrays. It's one of the most popular packages for scientific computing in Python, and is used for data manipulation and analysis, including data cleaning, transformation, and aggregation.

```Python
import numpy as np
```


- Official Website: https://numpy.org/
- Installation:  (https://numpy.org/install/)
    ```shell
    pip install numpy
    ```
- Documentation: https://numpy.org/doc
- GitHub: https://github.com/numpy/numpy


## Array Creation

### From Lists, Tuples, and Buffers
```python
np.array([1, 2, 3])
np.array((1, 2, 3))
np.frombuffer(b'Hello World', dtype='S1')
```

### Zeros, Ones, and Empty Arrays
```python
np.zeros((2, 3))  # 2x3 array of zeros
np.ones((2, 3))   # 2x3 array of ones
np.empty((2, 3))  # 2x3 empty array
```

### Ranges and Random Numbers
```python
np.arange(0, 10, 2)  # Array from 0 to 9 with step 2
np.linspace(0, 1, 5) # 5 equally spaced numbers from 0 to 1
np.random.rand(2, 3) # 2x3 array with random numbers between 0 and 1
```

### Identity and Diagonal Matrices
```python
np.eye(3)          # 3x3 identity matrix
np.diag([1, 2, 3]) # Diagonal matrix from a list
```

### Structured Arrays
```python
dt = np.dtype([('age', np.int32), ('name', np.str_, 10)])
arr = np.array([(21, 'Alice'), (25, 'Bob')], dtype=dt)
```

### Using `np.full` and `np.tile`
```python
np.full((2, 3), 7)   # Create a 2x3 array filled with the value 7
np.tile([1, 2], (2, 3))  # Repeat [1, 2] in a 2x3 grid
```

## Array Inspection

### Shape and Size
```python
arr.shape  # Dimensions of the array
arr.size   # Total number of elements
arr.ndim   # Number of dimensions
```

### Data Type
```python
arr.dtype  # Data type of elements
arr.astype(float)  # Convert to another type
```

### Memory Layout
```python
arr.itemsize  # Size of one element in bytes
arr.nbytes    # Total memory used by array
arr.flags     # Memory layout information
```

### Checking for `NaN` and `Inf` Values
```python
np.isnan(arr)  # Check for NaN values
np.isinf(arr)  # Check for infinity values
np.isfinite(arr)  # Check for finite values
```

## Array Mathematics

### Basic Operations
```python
arr + 1       # Add 1 to each element
arr * 2       # Multiply each element by 2
np.add(arr1, arr2)  # Add arrays element-wise
np.subtract(arr1, arr2)  # Subtract arrays element-wise
```

### Aggregate Functions
```python
np.sum(arr)       # Sum of all elements
np.mean(arr)      # Mean of elements
np.max(arr)       # Maximum value
np.min(arr)       # Minimum value
np.prod(arr)      # Product of elements
np.cumsum(arr)    # Cumulative sum of elements
np.cumprod(arr)   # Cumulative product of elements
```

### Exponentials and Logarithms
```python
np.exp(arr)       # Exponential of each element
np.log(arr)       # Natural logarithm
np.log10(arr)     # Base-10 logarithm
np.expm1(arr)     # Compute exp(x) - 1
```

### Trigonometric Functions
```python
np.sin(arr)       # Sine of each element
np.cos(arr)       # Cosine of each element
np.tan(arr)       # Tangent of each element
np.arcsin(arr)    # Inverse sine
np.arccos(arr)    # Inverse cosine
np.arctan(arr)    # Inverse tangent
```

### Rounding and Precision Control
```python
np.round(arr, decimals=2)  # Round to 2 decimal places
np.floor(arr)              # Floor operation
np.ceil(arr)               # Ceiling operation
np.trunc(arr)              # Truncate elements to integers
```

## Array Manipulation

### Reshaping
```python
arr.reshape((3, 2))  # Reshape to 3x2 array
arr.flatten()        # Flatten the array to 1D
np.ravel(arr)        # Return a flattened array
```

### Transposing
```python
arr.T            # Transpose of the array
np.transpose(arr, (1, 0, 2))  # Custom transpose
```

### Joining and Splitting Arrays
```python
np.concatenate((arr1, arr2), axis=0)  # Join along axis 0
np.hstack((arr1, arr2))  # Horizontal stack
np.vstack((arr1, arr2))  # Vertical stack
np.split(arr, 3)         # Split into 3 equal parts
np.hsplit(arr, 2)        # Split horizontally
np.vsplit(arr, 2)        # Split vertically
```

### Changing Dimensions
```python
np.expand_dims(arr, axis=0)  # Expand dimensions
np.squeeze(arr)              # Remove single-dimensional entries
```

### Array Repetition
```python
np.tile(arr, (2, 3))  # Repeat array
np.repeat(arr, 3)     # Repeat elements of an array
```

### Rotating and Flipping Arrays
```python
np.rot90(arr)        # Rotate array by 90 degrees
np.fliplr(arr)       # Flip array left to right
np.flipud(arr)       # Flip array upside down
```

## Linear Algebra

### Dot Product and Matrix Multiplication
```python
np.dot(arr1, arr2)       # Dot product
np.matmul(arr1, arr2)    # Matrix multiplication
arr1 @ arr2              # Matrix multiplication using @
```

### Solving Linear Equations
```python
np.linalg.solve(A, b)    # Solve linear equations Ax = b
```

### Eigenvalues and Eigenvectors
```python
np.linalg.eig(arr)       # Eigenvalues and eigenvectors
```

### Inverse and Determinant
```python
np.linalg.inv(arr)       # Inverse of a matrix
np.linalg.det(arr)       # Determinant of a matrix
```

### Singular Value Decomposition (SVD)
```python
U, S, V = np.linalg.svd(arr)  # Singular Value Decomposition
```

### Norms and Condition Numbers
```python
np.linalg.norm(arr)      # Compute matrix or vector norm
np.linalg.cond(arr)      # Compute the condition number of a matrix
```

## Statistics

### Descriptive Statistics
```python
np.mean(arr)             # Mean
np.median(arr)           # Median
np.var(arr)              # Variance
np.std(arr)              # Standard deviation
```

### Percentiles
```python
np.percentile(arr, 50)   # 50th percentile (median)
```

### Correlation and Covariance
```python
np.corrcoef(arr1, arr2)  # Correlation coefficient
np.cov(arr1, arr2)       # Covariance
```

### Histogram
```python
np.histogram(arr, bins=10)  # Histogram of an array
```

### Binned Statistics
```python
from scipy import stats
stats.binned_statistic(arr, values, statistic='mean', bins=10)  # Compute binned statistics
```

## Broadcasting

### Basic Broadcasting
```python
arr + 5       # Add 5 to all elements
arr + [1, 2, 3]  # Add array [1, 2, 3] to each row
```

### Advanced Broadcasting
```python
arr * np.array([1, 2, 3])  # Element-wise multiplication with broadcasting
np.expand_dims(arr, axis=0) + arr  # Broadcasting with dimension expansion
```

## Indexing and Slicing

### Basic Indexing
```python
arr[0]         # First element
arr

[-1]        # Last element
arr[0, 2]      # First row, third column
```

### Slicing
```python
arr[1:3]       # Elements from index 1 to 2
arr[:, 1:3]    # All rows, columns 1 and 2
```

### Fancy Indexing
```python
arr[[0, 2], [1, 3]]  # Elements (0,1) and (2,3)
```

## Boolean Masking and Advanced Indexing

### Boolean Masking
```python
arr[arr > 0]   # Elements greater than 0
```

### Advanced Indexing with Conditions
```python
np.where(arr > 0, arr, -arr)  # Replace negative values with their absolute value
```

### Setting Values
```python
arr[arr > 0] = 0   # Set all positive elements to 0
```

### Advanced Indexing with np.ix_
```python
np.ix_([1, 3], [2, 4])  # Create a mesh grid from indexing arrays
```

## Random

### Random Numbers
```python
np.random.rand(2, 3)       # Uniform distribution (0, 1)
np.random.randn(2, 3)      # Standard normal distribution
np.random.randint(0, 10, size=(2, 3))  # Random integers between 0 and 9
```

### Random Permutations
```python
np.random.permutation(arr)  # Randomly permute an array
```

### Sampling and Distributions
```python
np.random.choice(arr, size=3, replace=False)  # Random sample without replacement
np.random.binomial(n=10, p=0.5, size=10)  # Binomial distribution
np.random.poisson(lam=3, size=10)         # Poisson distribution
```

### Setting Seed
```python
np.random.seed(42)  # Set random seed for reproducibility
```

## I/O with NumPy

### Reading and Writing Files
```python
np.save('array.npy', arr)    # Save array to binary file
np.load('array.npy')         # Load array from binary file
np.savetxt('array.txt', arr) # Save array to text file
np.loadtxt('array.txt')      # Load array from text file
```

### Saving and Loading Multiple Arrays
```python
np.savez('arrays.npz', arr1=arr1, arr2=arr2)  # Save multiple arrays to a compressed file
npzfile = np.load('arrays.npz')               # Load multiple arrays from a compressed file
```

### Reading and Writing CSV Files
```python
np.genfromtxt('data.csv', delimiter=',')  # Load data from CSV file
np.savetxt('data.csv', arr, delimiter=',') # Save data to CSV file
```

### Reading and Writing with Pandas
```python
import pandas as pd
df = pd.read_csv('data.csv')  # Load data into a Pandas DataFrame
df.to_csv('output.csv')       # Save DataFrame to a CSV file
```

## Polynomials

### Polynomial Operations
```python
p = np.poly1d([1, 2, 3])  # Define a polynomial p(x) = 1x^2 + 2x + 3
p(2)                      # Evaluate polynomial at x = 2
p.roots                   # Find roots of the polynomial
```

### Polynomial Fitting
```python
np.polyfit(x, y, deg=2)  # Fit a polynomial of degree 2 to data points (x, y)
```

### Polynomial Derivatives and Integrals
```python
p.deriv()  # Derivative of the polynomial
p.integ()  # Integral of the polynomial
```

## Advanced Array Operations

### Vectorize Functions
```python
vectorized_func = np.vectorize(some_function)  # Apply a function element-wise to an array
```

### Meshgrid
```python
X, Y = np.meshgrid(x, y)  # Create a coordinate grid from 1D arrays x and y
```

### Broadcasting with Advanced Indexing
```python
np.add.at(arr, idx, 1)  # Increment elements at indices `idx` by 1
```

### Sorting Arrays
```python
np.sort(arr)            # Sort array
np.argsort(arr)         # Indices of the sorted array
```

### Searching and Counting Elements
```python
np.where(arr > 0)       # Indices where the condition is met
np.count_nonzero(arr)   # Count non-zero elements
```

## Memory Management

### Memory Layout and Optimization
```python
arr.flags           # Check memory layout (C_CONTIGUOUS, F_CONTIGUOUS)
np.ascontiguousarray(arr)  # Convert to C-contiguous array
np.asfortranarray(arr)     # Convert to Fortran-contiguous array
```

### Memory Mapping Files
```python
np.memmap('data.dat', dtype='float32', mode='w+', shape=(1000, 1000))  # Memory-mapped file
```

### Copying and Views
```python
arr_copy = arr.copy()  # Create a deep copy of the array
arr_view = arr.view()  # Create a view of the array (shallow copy)
```

## Advanced Indexing

### Using `np.take` and `np.put`
```python
np.take(arr, [0, 2])   # Take elements at indices 0 and 2
np.put(arr, [0, 2], [-1, -2])  # Set elements at indices 0 and 2
```

### Using `np.choose`
```python
np.choose([0, 1], [arr1, arr2])  # Construct an array from elements chosen from `arr1` and `arr2`
```

### Using `np.lexsort`
```python
np.lexsort((arr2, arr1))  # Sort by `arr1`, then by `arr2`
```

## Matrix Operations

### Determinant, Rank, and Trace
```python
np.linalg.det(arr)   # Determinant of a matrix
np.linalg.matrix_rank(arr)  # Rank of a matrix
np.trace(arr)  # Sum of diagonal elements (trace)
```

### Kronecker Product and Outer Product
```python
np.kron(arr1, arr2)  # Kronecker product of two arrays
np.outer(arr1, arr2) # Outer product of two arrays
```

### Solving Systems of Linear Equations
```python
np.linalg.solve(A, b)   # Solve Ax = b for x
np.linalg.lstsq(A, b)   # Solve Ax = b using least squares
```

## Data Types

### Specifying Data Types
```python
arr = np.array([1, 2, 3], dtype=np.float32)  # Specify data type
```

### Converting Data Types
```python
arr.astype(np.int32)  # Convert array to specified data type
```

### Complex Data Types
```python
arr = np.array([1+2j, 3+4j], dtype=np.complex64)  # Complex data type
```

### Checking Data Types
```python
arr.dtype    # Check data type
np.issubdtype(arr.dtype, np.number)  # Check if the data type is a subtype of `np.number`
```

---
