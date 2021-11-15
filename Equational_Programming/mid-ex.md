# EP Exercises 详解 -- 期中篇（Lambda Calculus）



## Exercise1

#### Q1

**Write as a λ-term the function that takes one input and maps it to the constant 0 as λ-term.**

##### Solution:

```
λx. 0
```



****

#### Q2

**Write as a λ-term the function that takes two inputs and maps them to the constant 0.**

##### Solution:

```
λx. λy. 0
```



****

#### Q3

**Write the following λ-term in the notation with all parentheses and all λs:**

`(λxy. x (y z)) λx. y x x`.

##### Solution:

```
((λx.(λy.(x (y z)))) (λx.((y x) x)))
```



****

#### Q4

**Write the following λ-term in the notation with as few parentheses and λs as possible:**

`((λx.(λy.((((x y) z) u) (v w)))) (λx.(y (x x))))`.

##### Solution:

```
 (λx. λy. x y z u (v w)) λx. y (x x)
```



****

#### Q5

**Draw the term tree of the following λ-term, and indicate which variables are bound, and by which λ they are bound:**

`(λxy. x x y) (λzu. u (u z)) λw. w`

##### Solution:  



![image-20211115165406830](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115165406830.png)  



****

#### Q6

**Indicate for all pairs of λ-terms below whether or not they are α-convertible:**

(a) x and y, 

(b) λx. x x and λy. y y, 

(c) λu. u u' and λu' . u' u', 

(d) (λxyz. y (x y z)) λvw. v w and (λx'yz' . y (x ' y z' )) λvw' . v w' , 

(e) (λx. x) x and (λy. y) y,



##### Definition

>  **α-convertible**:
>
> - Two terms M and N are said to be α-equivalent if they are identical up to the renaming of bound variables.
> - The renaming of bound variable is called α-convertible.



##### Solution

(a) x and y

```
not α-convertible
```

- variable 不可以随意改名



(b) λx. x x and λy. y y

```
α-convertible
```

- bound 的 variable 必须随绑定的 λ 一起改名



(c) λu. u u' and λu' . u' u' 

```
not α-convertible
```

- and 左边的 u' 是 free variable (argument)，不能与  λ 一致。



(d) (λxyz. y (x y z)) λvw. v w and (λx'yz' . y (x ' y z' )) λvw' . v w'

```
α-convertible
```



(e) (λx. x) x and (λy. y) y

```
not α-convertible
```

- 左边返回 x， 右边返回 y，不一致。



****

#### Q7

**Calculate the following substitutions:**

(a) (x y)[y := u w] 

(b) (x y)[x := u w] 

(c) (λx. x y)[x := u w] 

(d) (λx. x y)[y := u w] 

(e) (λx. x y)[y := x x]

(f) ((λx. x) x (λy. x u))[x := y]



##### Definition

> **β-reduction:**
>
> - (λx. M) N $\rightarrow _\beta$​​​ M[x := N]
> - The expression on the left-hand side of the arrow means: the term M in which all **free** occurrences of *x* are replaced by the term N.



> **Substitution:**
>
> - (λx. M) N $\rightarrow _\beta$​ M[x := N]
> - 单独的 substituion 是指对 abstraction body （这里是 M）根据 β-reduction rule （箭头右侧）把 body 进行替换的行为。
> - 注意，如 Q7 所示的题型，题干都只是 $\rightarrow _\beta$ 右侧的一部分，而不是完整的 $\lambda$​-term, 注意不要混淆。​
>
> **Substitution遵循两个原则：**
>
> - 只替换 abstraction body 里的 free variable；
> - 如果替换后和 bound variable 重名，则需给 bound variable 和其绑定的 lambda 改名。



##### Solution：

(a) (x y)[y := u w] 

```
(x y)[y := u w] = x (u w)
```

- the parentheses are needed



(b) (x y)[x := u w] 

```
(x y)[x := u w] = (u w) y = u w y
```



(c) (λx. x y)[x := u w] 

```
(λx. x y)[x := u w] = λx. x y
```



(d) (λx. x y)[y := u w] 

```
(λx. x y)[y := u w] = λx. x (u w)
```



(e) (λx. x y)[y := x x]

```
(λx. x y)[y := x x] = λx'. x' (x x)
```



(f) ((λx. x) x (λy. x u))[x := y]

```
((λx. x) x (λy. x u))[x := y] = (λx. x) y (λy'. y u)
```



****

#### Q8

**Indicate whether the following λ-terms are in β-normal form:**

(a) 5 (λx. x x) 3, 

(b) λx.(λy. y) 3, 

(c) (λx. x) (λy. y) x, 

(d) λx. x ((λy. y) x)



##### Definition

> **β-redex:**
>
> - β-redex is defined as term of the form **(λx. M) N**
>   - redex - stands for reducible expression
>   - reducible - 指可以进行 β-reduction 

>**β-normal form:**
>
>- A $\lambda$​-term that does not contain a β-redex is said to be a normal form of β-normal form.

> **β-reduction sequence:**
>
> - A sequence that consisting of zero, one, or more β-reduction  steps 
> - Notice that, if exactly one β-reduction step, we use the notation $\rightarrow _\beta$
> - $\rightarrow _\beta*$  stands for zero, one or more steps
> - $\rightarrow$ $\rightarrow$  stands for two steps



##### Solution:



(a) 5 (λx. x x) 3  





![image-20211115174449645](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115174449645.png)  

```
 There exists no β-redex, so is in β-normal form.
```

- 注意橙色框部分，application 左边是 constant / varibale 且右边是 normal form的情况下，可以判定此 @ 是 normal form，因为任何 $\lambda$-term 都不能对 constant / variable 进行带入。



(b) λx.(λy. y) 3  



![image-20211115174803553](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115174803553.png)  

```
Not in β-normal form.
The term can be reduced to λx. 3
```



(c) (λx. x) (λy. y) x    





![image-20211115174910195](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115174910195.png)  



```
Not in β-normal form.
The term has the following β-reduction to normal form:
(λx. x) (λy. y) x →β (λy. y) x →β x
```



(d) λx. x ((λy. y) x)    



![image-20211115175103743](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115175103743.png)  





```
Not in β-normal form.
The term can be reduced to β-normal form:
λx. x ((λy. y) x) →β λx. x x
```



****

#### Q9

**Consider the function double in Haskell:**

```haskell
double x = x + x
```

**Use equational reasoning to compute double (double 4). Explain every step. Give at least one alternative computation.** 



##### Solution

```
double (double 4) = {unfold inner double}
double (4 + 4) = {do built-in addition}
double 8 = {unfold double}
8 + 8 = {do built-in addition}
16
```

**An alternative computation:**

```
double (double 4) = {unfold outer double}
(double 4) + (double 4) = {unfold left double}
(4 + 4) + (double 4) = {do built-in addition}
8 + (double 4) = {unfold double}
8 + (4 + 4) = {do built-in addition}
8 + 8 = {do built-in addition}
16
```



##### Extension

**Reduction Graph**:  



![image-20211115192500642](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115192500642.png)  







****

#### Q10

**Depict the following terms as trees, and clearly indicate all β-redexes.**

(a) K I Ω ;

(b) M1 = (λf. f 3) (λx.(λy. y) x); 

(c) M2 = (λx.((λu. u) x) (λz. x Ω)) λy. z



##### Solution:

![image-20211115192730087](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115192730087.png)  



![image-20211115192745137](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115192745137.png)  

  ![image-20211115192855971](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115192855971.png)  

![image-20211115192907735](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115192907735.png)  



****

#### Q11

**(a) Give λ-terms M and N such that M and N are β-normal forms but M[x := N] is not a β-normal form.**



##### Solution

```
Take for example 
	M = x y, 
	N = λu. u. 
Then M and N are both in β-normal form, 
but 
	M[x := N] = (λu. u) y -> y
is not in β-normal form.
```



**(b) Give λ-terms M and N such that M and N both have a β-normal form, but M[x := N] does not have a β-normal form.**



##### Definition

> **Has normal form:**
>
> - We say that a term has a normal form if it can be β-reduced in zero, one or more steps to a normal form.
> - A normal form itself can also be considered as normal form.
>
> Example:
>
> - x has a normal form
> - (λu.u )y has a normal form
> - (λx.λy.x)w has a normal form
>
> Notice that $\Omega$​ does not have a normal form, since every reduction gets the same result.  
>
> ![image-20211115202746238](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115202746238.png)  



##### Solution

```
Take for example 
	M = x (λu. u u), 
	N = λu. u u
Then 
	M and N are in β-normal form (so in particular they have a β-normal form),
but 
	M[x := N] = (λu. u u) (λu. u u) = Ω does not have a β-normal form.
```



**(c) Give terms M, N, P such that (M[x := N])[y := P] $\ne$ (M[y := P])[x := N].**



```
Take for example 
	M = x, 
	N = y, 
	P = z. 
Then 
	(M[x := N])[y := P] = P = z 
whereas 
	(M[y := P])[x := N] = N = y.
```



****

#### Q12

**Reduce (λx. x x) (λs.λz. s z) to β-normal form.**



##### Solution:



````
(λx. x x) (λs.λz. s z) →β
(λs. λz. s z) (λs. λz. s z) →β
λz.(λs. λz. s z) z →β
λz. λz'. z z'
````

  

![image-20211115203337760](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115203337760.png)  

![image-20211115203359030](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115203359030.png)  



****

#### Q13

**Are the following terms terminating and/or weakly normalizing?**

(a) (λx. x x)(λfy.(f y)) 

(b) (λx. x Ω) (λy. z) 

(c) (λx. x Ω) (λy. y) 

(d) (λx. x x x) (λx. x x x)



#### Definition

> **Strongly normalizing:**
>
> - A term P is said to be terminating or strongly normalizing (SN) if **all** reduction sequences starting in P are finite. 
> - That is: P is not the start of an infinite reduction.
> - β-normal forms are terminating.
> - Notice that a term that is not strongly normalizing has a an infinite reduction sequence.
>
> Example:
>
> - (λx. y) ((λx. x) z)
> - (λx. x) (λy. y)

> **Weakly normalizing:**
>
> - A term that admits a reduction sequence to normal form, we also say that the term has a normal form, is said to be weakly normalizing (WN).
> -  A strongly normalizing term is weakly normalizing.
> - There are weakly normalizing terms that are not strongly normalizing.
>
> Example:
>
> - (λx. y) Ω →$_\beta$ y  (WN not SN because can also be reduced as: (λx. y) Ω →$_\beta$ (λx. y) Ω →$_\beta$ . . .. )



##### Solution



(a) (λx. x x)(λfy.(f y)) 

```
(λx. x x)(λfy.(f y)) is strongly normalizing and hence also weakly normalizing.
```



(b) (λx. x Ω) (λy. z) 

```
(λx. x Ω) (λy. z) is weakly normalizing because it has a reduction to β-normal form:
	(λx. x Ω) (λy. z) →β (λy. z) Ω →β z. 

The term (λx. x Ω) (λy. z) is not strongly normalizing, 
because it has Ω as subterm, which reduces in one step to itself.
```



(c) (λx. x Ω) (λy. y) 

```
 (λx. x Ω) (λy. y) is not weakly normalizing and hence not strongly normalizing.
 
The reducts of (λx. x Ω) (λy. y) are (λx. x Ω) (λy. y) itself, and (λy. y) Ω, and Ω.
```



(d) (λx. x x x) (λx. x x x)

```
(λx. x x x) (λx. x x x) is not weakly normalizing and hence not strongly normalizing. 
Using the 
	A = λx. x x x, 
the reduction sequence is
A A →β A A A →β A A A A →β . . .¿ 
(non-termination)
```



****

## Exercise 2

