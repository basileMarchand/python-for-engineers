---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.1
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

+++ {"lang": "en"}

# Course exercises

**Basile Marchand (Centre des Matériaux - Mines ParisTech/CNRS/Université PSL)**

+++ {"lang": "fr"}

## Exercise on slicing

   1. create the string: J'adore Python et Numpy !
   1. access the first and last character of the string 'j' and '!'
   1. slice the string to keep only "adore"
   1. reverse the string: ! ypmun te nohtyp eroda'j
   1. cut the string to keep only "jaoepto tnmy!"

+++ {"lang": "fr"}

## Exercises on strings

### Exercise 1
   1. create a string in python
   1. print the string and its length using an f-string
   1. create another string
   1. concatenate the two strings
   1. capitalize the result

### Exercises 2

   1. create a multi-line string and display it
   1. split the string to obtain a list of lines (method **split**)
   1. display each line with a for loop by prefixing it with its number

+++ {"lang": "en"}

## Exercise on lists

   1. build a list containing an integer, a string, a float, a boolean
   1. modify the first element of the list
   1. slice the list so as to keep only one element out of 2 from the beginning
   1. test if an element is in the list
   1. create a new list containing itself a list
   1. concatenate the two lists
   1. print with a **for** the elements of the list

+++ {"lang": "en"}

## Exercise on dictionaries

   1. create a dictionary with pairs of people described by their name and age
   1. display the type of a dictionary
   1. test if a person is in the dictionary and if so modify his age
   1. Apply the **items** function to the dictionary, what does it return ?
   1. print with a **for** the names and the age of all the people in the dictionary

+++ {"lang": "fr"}

## Exercises on functions

+++ {"lang": "en"}

### Exercise 1

+++ {"lang": "en"}

The objective of this first exercise is to realize a Python program allowing an elementary analysis of a large number of experimental results. The experimental tests in question are tensile tests on specimens.

The points of interest that are addressed in this exercise are the following:

1. Modularity of the code.
1. Text file processing
1. Simple mathematical functions

The expected operation of the program is as follows:

1. The user provides as input the path to the folder containing all the experimental files
1. The program lists all the files contained in this folder
1. For each file:
    * Reading of the file data
    * Identification of the maximum stress and strain at break
    * Storage of these quantities in a container
1. Calculate the average of the maximum stress and strain at break
1. Calculation of the variances of the maximum stress and strain at break
1. Display of the results in the console (with a clean layout)
1. Writing the results in a text file.


The files containing the experimental data can be downloaded at the following address http://bmarchand.fr/download/data/tp1.tar.gz

+++ {"lang": "en"}

### Exercise 2

+++ {"lang": "fr"}

In this second exercise the objective is to define a function `evalPolynom` which should allow : 

1. Evaluate a polynomial of any order, defined by its coefficients, at a given value `x`.
2. Return, if requested by the user, the values of `M` successive derivatives of this polynomial evaluated in `x` as well. 
3. Display via the `help` function a clear help message

+++ {"lang": "en"}

## Exercises on classes

+++ {"lang": "fr"}

### Exercise 1

+++ {"lang": "fr"}

In this first exercise you will define a class `Vector2D` and `Vector3D` having :

* for private attributes :
    * `values` a list of doubles (2 values for `Vector2D` and 3 values for ̀`Vector3D`
    * `size` an integer specifying the size of the vector
    
The desired behavior for these two objects is as follows: 

1. Be able to display the vector cleanly using print.
2. Return the size via the `len` function
3. Access the values contained in the `values` attribute 
4. Have all the usual operations 
    * Sum of two ̀`Vectors`
    * Difference of two ̀`Vector`
    * Term to term multiplication of two ̀`Vector`
    
5. Do broadcasting, i.e. the sum of a `Vector2` and a `Vector3` must return a `Vector3` for which the last component is unchanged.

+++ {"lang": "en"}

### Exercise 2

+++ {"lang": "fr"}

**Note**:

Don't you think the previous exercise has a lot of copy and paste in it? You should anyway!!! 

The objective of this exercise is to redo exercise 1 using the *inheritance* concept in order to minimize the copy-paste.

+++ {"lang": "en"}

## Numpy exercise

+++ {"lang": "en"}

### Data manipulation 

The objective here is to repeat exercise 1 on functions, now using numpy as much as possible

+++ {"lang": "fr"}

### Image manipulation (thanks to V. Roy for the subject)

```{code-cell} ipython3
import numpy as np
from matplotlib import pyplot as plt
```

+++ {"lang": "fr", "tags": ["framed_cell"]}

**notions involved in this tutorial**

on arrays `numpy.ndarray`
* `reshape()`, tests, boolean masks, *ufunc*, aggregation, linear operations on `numpy.ndarray`
* other notions used are recalled (very briefly)

for reading, writing and displaying images
* use `plt.imread`, `plt.imshow`.
* use `plt.show()` between two `plt.imshow()` in the same cell

**note**

* we use the basic functions on `pyplot` images for simplicity
* we don't mean that they are the best ones at all  
for example `matplotlib.pyplot.imsave` does not allow you to give the quality of the compression  
whereas the `save` function in `PIL` does
* you are free to use another library like `opencv` if you know it well enough to handle it  
  if you know it well enough to do it yourself (and install it), the images are just a pretext

**don't forget to use the help in case of problem.**

+++ {"lang": "en"}

#### Sum of the RGB values of an image

+++ {"lang": "fr"}

0. Read the image `the-mines.jpg`

1. Create a new array `numpy.ndarray` by summing **with the operator `+`** the RGB values of the pixels in your image  

2. Display the image (not great), its maximum and its type

3. Create a new array `numpy.ndarray` by summing **with the aggregation function `np.sum`** the RGB values of the pixels in your image

4. Display the image, its maximum and its type

5. Why the difference? Use the `np.sum` help

6. Switch the image to 8-bit unsigned integer grayscale  
(in the way you prefer)

7. Replace in the grayscale image,   
values >= 127 with 255 and those below with 0  
Display the image with a grayscale color map  
you can use the `numpy.where` function

8. with the `numpy.unique` function  
look at the different values you have in your black and white image

+++ {"lang": "en"}

#### Sepia image

+++ {"lang": "fr"}

To change the R, G and B values of a pixel to sepia  
(encoded here on an 8 bits unsigned integer)  

1. we transform the values $R$, $G$ and $B$ by the transformation  
$0.393\, R + 0.769\, G + 0.189\, B$  
$0.349\, R + 0.686\, G + 0.168\, B$  
$0.272\, R + 0.534\, G + 0.131\, B$  
(attention the calculations must be done in floats not in uint8  
to avoid having, for example, 256 becoming 0)  
1. then we threshold the values which are greater than `255` to `255`.
1. of course the image must then be put back in a correct format  
(uint8 or float between 0 and 1)

+++ {"lang": "en"}

**Exercise**

1. Make a function that takes as argument an RGB image and renders a sepia RGB image  

1. Switch your patchwork to sepia  
Read the file `media/patchwork-all.jpg` if you don't have a custom file
2. Change the image `media/the-mines.jpg` to sepia

+++ {"lang": "en"}

#### Compress the image with SVD

+++ {"lang": "fr"}

In this exercise the objective is to compress a grayscale image using an SVD (Singular Value Decomposition). The image to be compressed is the following :

+++

![](data/carrie_fisher.png)

+++ {"lang": "en"}

As a reminder, the SVD decomposition of a matrix $\mathbf{A} \in \mathbb{R}^{mathtimes n}$ is written as follows: 

$$ \mathbf{A} = \mathbf{U}cdot\mathbf{Sigma}cdot\mathbf{V} $$

With $\mathbf{U}\in \mathbb{R}^{m\times m}$, $\mathbf{\Sigma}\in \mathbb{R}^{m\times n}$ a diagonal matrix of singular values and $\mathbf{V} \in \mathbb{R}^{n\times n}$.

+++ {"lang": "fr"}

**Question 1:** 

Load the image of Carrie Fisher (you will find in the data folder a file carrie_fisher.npy containing the image in the form of an np.ndarray) and calculate its decomposition into singular values. 

**Question 2 :**

Draw the evolution of the singular values of the image. 

**Question 3 :**

For different truncations ($k=\lbrace 1,5,10,15,20,30,50,100 \rbrace$) reconstruct the image, display it and compute the compression ratio obtained.

+++ {"lang": "fr"}

#### Solving a system of N springs

```{code-cell} ipython3
from IPython.display import IFrame

IFrame("./media/spring.pdf", width=600, height=300)
```

+++ {"lang": "fr"}

The objective is to determine by a matrix approach the response of the system to an effort $F$. 

The formulation of the problem must therefore be reduced to the resolution of a problem of the form 

$$ \mathbf{K} \cdot \mathbf{u} = \mathbf{F}$$ 

With $\mathbf{K} \in \mathbb{R}^{M}$, $\mathbf{u} \in \mathbb{R}^{M}$, $\mathbf{F} \in \mathbb{R}^{M}$ and $M$ the number of points in the system.

+++ {"lang": "fr"}

For this we recall that the potential energy of the system can be expressed in the following form: 

$$ E_p = \frac{1}{2} \sum_{i=1}^{N} \left( u_{i,1} - u_{i,0} \right)\cdot k_{i} \cdot \left( u_{i,1} - u_{i,0} \right) $$

With $u_{i,0}$ the displacement of the first attachment node of the $i$-th spring and $u_{i,1}$ the displacement of the second attachment node of the $i$-th spring.

This potential energy can be written in the following matrix form: 

$$ E_p = \frac{1}{2} \mathbf{U}^T \cdot \mathbf{K} \cdot \mathbf{U} $$ 

Using then the potential energy theorem we can write that 

$$ \mathbf{K} \cdot \mathbf{U} = \mathbf{F} $$

+++ {"lang": "fr"}

**Question 1:** 


From the expression of the potential energy of a spring, define the elementary stiffness matrix.

+++ {"lang": "fr"}

**Question 2 :** 

Use the stiffness matrix of a spring to construct the global $\mathbf{K}$ matrix. To do this, use the notion of connectivity table. As a reminder, the connectivity table is a list $L$ such that the $i$-th element of $L$ is the doublet of the indices of the spring's attachment points.

+++ {"lang": "en"}

**Question 3:**

Construct the second member $F$.

+++ {"lang": "fr"}

**Question 4 :** 
    
Solve the linear system

+++ {"lang": "fr"}

**Bonus :** 

Using matplotlib, visualize the profile of the matrix $\mathbf{K}$:  

``python 
import matplotlib.pyplot as plt 
plt.imshow( K ) 
plt.colorbar()
plt.show()
```

What can we conclude from this? What improvement can be made to speed up the resolution of the problem?

+++ {"lang": "en"}

## Scipy exercises

+++ {"lang": "fr"}

### EDO solution

+++ {"lang": "fr"}

Consider a classical RC circuit defined by the following differential equation: 

$$ RC \frac{du}{dt} + u = u_e $$ 

$$ \frac{du}{dt} = \frac{u_e - u }{RC} $$


With $R=1000\Omega$, $C=10^{-6}F$ and $u(t=0) = 0$.

+++ {"lang": "fr"}

**Question 1:** 

In the case where $u_e(t) = U_0$ with $U_0=10\,V$ calculate the solution of the differential equation on the interval $[0, 0.005]$.

**Question 2:** 

In the case $u_e(t) = U_0 \sin \left( 2\pi f t \right)$ with $U_0=10\,V$ and $f=100\,Hz$ calculate the solution of the differential equation on the interval $[0, 5/f]$.

+++ {"lang": "fr"}

### Solve a system of differential equation

+++ {"lang": "fr"}

Consider a classical RLC circuit defined by the following differential equation: 

$$LC\frac{d^2u}{dt^2} + RC \frac{du}{dt} + u = u_e $$

+++ {"lang": "fr"}

**Question 1:**

Transform this second order equation into a system of two first order equations.

+++ {"lang": "fr"}

**Question 2 :**

Determine the evolution of $u(t)$ on the interval $t \in [0, 0.02]$ for $R=1000\,\Omega$, $F=10^{-6}\,F$. It is up to you to choose the value of $L$ to solve: (i) pseudo-periodic; (ii) aperiodic; (iii) critical.

+++ {"lang": "fr"}

As a reminder: 
$$q = \frac{1}{R} \sqrt{ \frac{L}{C} } \; ; \begin{cases} 
q = \dfrac{1}{2} & critical
q < \dfrac{1}{2} & aperiodiue 
q > \dfrac{1}{2} & pseudo-periodic 
\end{cases}
$$

+++ { "lang": "fr"}

If you want to use `ipywidgets` (you have to install it via conda) you can make an interactive graph with the value of $L$.

+++ {"lang": "fr"}

### Find the zero of a scalar function

+++ {"lang": "fr"}

Consider the Kepler equation: 

$$ x - e\cdot \sin x = m $$

+++ {"lang": "fr"}

**Question 1:** 

Using `scipy` find the solution of the Kepler equation in the case where $e=frac{1}{2}$ and $m=1$. Check that the solution found by scipy is correct.

+++ {"lang": "fr"}

### Parameter assignment --- RC circuit

+++ {"lang": "fr"}

Let's consider the RC circuit previously studied. 

We will try to identify the parameter R of the system from "experimental" data. 
The experimental data in question are given in the file `notebook/data/exp_data_rc.dat`. If we represent these data we obtain the following curve:

``{code-cell} ipython3
import matplotlib.pyplot as plt 
import numpy as np
import pathlib as pl 

data = np.loadtxt(str(pl.Path(".") / "data" / "exp_data_rc.dat"))

plt.plot( data[:,0], data[:,1])
plt.xlabel("Time (s)")
plt.ylabel("U (V)")
plt.show()
```

+++ {"lang": "en"}

This data is obtained with the following configuration: 

$$ u_e = 10\,V\, ; \, C=10^{-6}\,F\, ; \, R=?? $$

+++ {"lang": "fr"}

**Question 1:**
Formulate the optimization problem to be solved to identify the parameter R ? 

**Question 2:** 
Using `scipy.optimize` identify the value of the R parameter. 

**Question 3:** 
Plot on the same graph the experimental data and the model result for the identified value of $R$.
