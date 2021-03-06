|[< Previous (Debugging)](Debugging.md) | [Day3](../README.md)| [Next (Modules) >](Modules.md) |
|----|----|----|

# Functions

In programming, we may need to do the same calculation (or activity) multiple times. To encapsulate this calculation or activity, we use a function. A function takes zero or more input arguments, processes those arguments and returns zero or more values. Functions are also known as subroutines, routines, procedures in other programming languages.

In general, many programming problems are easier to solve when decomposed into smaller problems or steps. Even if we do not need to call a particular function more than once, just decomposing the problem into smaller functions or sub-steps, improves the readability of the code.

Functions can be thought of as black-boxes. They might be written by other people. We do not need to know how they work (though it is good to know), but only be concerned what what goes in (inputs) and what comes out (return values or outputs).

Python gives you many built-in functions like print(), etc. but you can also create your own functions. These functions are called *user-defined functions*.



# Function: Temperature Conversion

Temperature is commonly represented in degrees in units of Fahrenheit (F) or Celsius (C). Below are formulas for converting between the units.

## Conversion formulas

Celsius to Fahrenheit:
```
T(°F) = T(°C) × 9/5 + 32
```

Fahrenheit to Celsius:
```
T(°C) = (T(°F) - 32) × 5/9
```

## Python Code to Convert Fahrenheit to Celsius

```python
def convertFtoC(temperatureF):
    temperatureC = (float(temperatureF) - 32) * (5.0/9.0)
    return temperatureC
```

The keyword ```def``` defines the function name: ```convertFtoC```.
```temperatureF``` is an input argument to the function. We will call this function with different values.
```return temperatureC``` is the syntax to send the calculation back to the calling program.
In the above example, the input argment ```temperatureF``` is a string type. The ```float()``` operator is used to convert the string to a float before performing the conversion calculation.

After defining the function, we can use it to perform calculations.
## Python Code to call the conversion function

```python
freezing = convertFtoC('32')
print('freezing =', freezing, 'C')
```


### Exercise

Create a new file, temperatureConversion.py. Copy the function definition code above to your file. Add some calls to convert selected temperatures and print the results.



------



# Function: Quadratic roots

A  [quadratic equation](https://en.wikipedia.org/wiki/Quadratic_equation) can be represented as

![](http://latex.codecogs.com/gif.latex?ax%5E2%20&plus;%20bx%20&plus;%20c%20%3D%200)

Such an equation has two roots, given by:

![](http://latex.codecogs.com/gif.latex?x%20%3D%20%5Cfrac%7B-b%20%5Cpm%20%5Csqrt%7Bb%5E2%20-%204ac%7D%7D%7B2a%7D)



We will write a Python program to ask the user to input the values of coefficients a, b and c. Then we will calculate and print the two values of x (the roots). For the purpose of simplicity and understanding in class, we will use a very simple equation with non-imaginary roots. 



Let us consider the mathematical expression :
![](http://latex.codecogs.com/gif.latex?x%20%3D%20%5Cfrac%7B-b%20%5Cpm%20%5Csqrt%7Bb%5E2%20-%204ac%7D%7D%7B2a%7D)

In Python, this mathematical expression can be written as two separate expressions

```python
x1 = (-b + (b ** 2 - 4*a*c) ** 0.5) / (2 * a)
x2 = (-b - (b ** 2 - 4*a*c) ** 0.5) / (2 * a)
```

Note that the ```**``` symbols is the exponentiation or "Raise to the power of" operator. Consequently, the square root of y, mathematically expressed as ![](http://latex.codecogs.com/gif.latex?%5Csqrt%7By%7D), is written in Python as ```y ** 0.5```.

Alternatively, we can also use Python's built in Math library's ```math.sqrt()``` function, as shown below

```python
import math

x1 =(-b + math.sqrt(b ** 2 - 4*a*c)) / (2 * a) 
x2 =(-b - math.sqrt(b ** 2 - 4*a*c)) / (2 * a) 
```



To avoid clutter, we can further breakdown and write

```python
import math

y = math.sqrt (b ** 2 - 4 *a*c)
x1 = (-b + y) / (2 * a)
x2 = (-b - y) / (2 * a)
```



Finally, we can put this into a function and write a program (e.g. quadroots.py)

```python
import math

# Function to compute quadratic roots
def quad_roots(a, b, c):
    y = math.sqrt(b ** 2 - 4 * a * c)
    x1 = (-b + y) / (2 * a)
    x2 = (-b - y) / (2 * a)

    # Return a list containing the two roots
    return [x1, x2]

# Main part of the program
print("Solve for the quadratic equation ax^2 + bx + c = 0")
a = input("Enter the value of a : ")
b = input("Enter the value of b : ")
c = input("Enter the value of c : ")

# Convert the user inputs from string to float
a = float(a)
b = float(b)
c = float(c)

roots = quad_roots(a, b, c)
print("Roots are:", roots[0], roots[1])
```


### Exercise

Test your program with the following inputs : a = 1, b = -8, c = 15. You should get roots of 5.0 and 3.0 (similar to what is shown below)

```
Solve for the quadratic equation ax^2 + bx + c = 0

Enter the value of a : 1

Enter the value of b : -8

Enter the value of c : 15

Roots are: 5.0 3.0

Process finished with exit code 0

```

----


# The "Main" of a Python Program

So far we have just run one python file at a time. As projects get complex, you may have several functions and put the definitions in separate files. When you want to run them, one file needs to be the starting point. This is __main__. To include code to run only when the file is the starting point add a section checking if this is the main program like this:

```python
if __name__ == "__main__":
    print('this is the main program')
```

### Exercise
1. Move the calls to the temperature function into a __main__ section. Leave the def part of the function outside the if statement block. Run this program.

2. Create a new program with just an if __name__ == "__main__": block. Put different code in this main section. Some suggestions:
   Create a loop to ask the user for input values and then call the convert function.

3. Use conditionals to print comment about the temperatures, like "that is cold!", "that is a nice temperature for playing golf", "that is hot, let's go swimming", etc.
   Divide the function and main into two python files and run again.

4. Run this program and see the different output. 

5. Write a program that calls two functions ```simpint()``` and ```compint()``` to calculate the Simple Interest and Compound Interest on a (common) Principal Amount, Rate of Interest and Number of Years. Print both the interest values and the difference between them.

   ![](http://latex.codecogs.com/gif.latex?Simple%20Interest%20%3D%20%5Cfrac%7BP%20*%20R%20*%20N%7D%7B100%7D)

   ![](http://latex.codecogs.com/gif.latex?CompoundInterest%20%3D%20P%281&plus;%5Cfrac%7BR%7D%7B100%7D%29%5EN)

   where 

   P = Principal amount

   R = Rate in % (e.g 5, 6.7, 9 etc)

   N = No of time periods (assume years for simplicity) over which the interest accrues

   ​

   ​

|[< Previous (Debugging)](Debugging.md) | [Day3](../README.md)| [Next (Modules) >](Modules.md) |
|----|----|----|
