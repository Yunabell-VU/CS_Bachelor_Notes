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

> **Terminating / Strongly normalizing:**
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
(λx. x x)(λfy.(f y)) is strongly normalizing and hence also weakly normalizing because all its reductions are finite.
We have 
	(λx. x x)(λf. λy.(f y)) →β (λf. λy.(f y)) (λf. λy.(f y)) →β
	λy.(λf. λy.(f y)) y →β 
	λy' λy. y' y 
which ends in normal form, and there is no other reduction sequence possible. 
So self-application does not necessarily leads to non-termination.
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
 
We can see this by reducing the term using the leftmost-outermost reduction strategy 
	(λx. x Ω) (λy. y) →β (λy. y) Ω → Ω → Ω → . . ..
If the leftmost-outermost reduction strategy yields an infinite reduction, then the initial term does not have a normal form.
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

#### Q1

**Show that Curry’s fixed point combinator**  

​	`λf.(λx. f (x x)) (λx. f (x x))`

**and Turing’s fixed point combinator**

​	`T = (λx. λy. y (x x y)) (λx. λy. y (x x y))`

**are indeed fixed point combinators.**



##### Definition

> **Fixed point:**
>
> (待补)

> **Fixed point combinator:**
>
> (待补)



##### Solution:

```
We show: 
	for every λ-term F we have Y F =β F (Y F).

Let 
	F be an arbitrary λ-term. 
We have :
	Y F = (λf.(λx. f (x x)) (λx. f (x x))) F
		→β (λx. F (x x)) (λx. F (x x))
		→β F ((λx. F (x x)) (λx. F (x x)))
		←β F ((λf.(λx. f (x x)) (λx. f (x x))) F)
		= F (Y F)
So indeed
	F (Y F) =β Y F


Now we consider Turing’s fixed point combinator T = (λx. λy. y (x x y)) (λx. λy. y (x x y)).

We aim to show: 
	for every λ-term F we have TF =β F (TF ). 
Take 
	an arbitrary λ-term F. 

We use 
	t = λx. λy. y (x x y). 

We have:
	TF = (λx. λy. y (x x y)) (λx. λy. y (x x y)) F
		→β (λy. y (t t y)) F
		→β F (tt F )
		= F (TF )
So we indeed
	TF =β F (TF )

We even have
	TF →∗β F (TF )

Remark: 
	if we have to show that a λ-term P is a fixed point combinator, we have to show that P F =β= F (P F) for every λ-term F. 
	So the reasoning starts with taking an arbitrary λ-term.
```



****

#### Q2

**Reduce Y (λa. b) and T(λa. b) to obtain a fixed point of λa. b.**



##### Solution

```
We consider Y (λa. b):
	Y (λa. b) = (λf.(λx. f (x x)) (λx. f (x x))) (λa. b)
		→β (λx.(λa. b) (x x)) (λx.(λa. b) (x x))
		→β (λa. b) ((λx.(λa. b) (x x))) ((λx.(λa. b) (x x)))
		→β b
		
Alternatively: 
we use that we already know 	
	Y F =β F (Y F), for any F, from the previous question. 

That gives, 
taking 
	λa. b for F:
		Y (λa. b) =β (λa. b) (Y (λa. b)) →β b
Here we get β-equality.

For the question show β-equality of Y (λa. b) and b both approaches are correct. 
For the question reduce Y (λa. b) only the first approach is correct.

But of course the point is to see that for the specific example of the function that gives back b for any input, 
the term b is a fixed point, which is indeed found using the fixed point combinator Y.


Now we consider T(λa. b):
first explicitly, 
using again 
	t = λx. λy. y (x x y)

first explicitly:
	T(λa. b) = (λx. λy. y (x x y)) (λx. λy. y (x x y)) (λa. b)
		→β (λy. y (t t y)) (λa. b)
		→β (λa. b) (tt(λa. b) )
		→β b

Alternatively, and faster: 
we know from the previous question that 
	TF →∗β
	F (TF ) for any F. 
So we have
	T(λa. b) →∗β (λa. b) (T(λa. b) ) →β b

```

- 注意，在上面的解法中，我们使用了 abbreviation 替换（t = λx. λy. y (x x y)）来方便计算，使用这种方法时注意被替换的 term 最好是 closed term （不包含 free variable 的 term），否则会很麻烦。比如，如果 term 中包含一个 free variable y，那么我们替换时，需要写做 `t(y) = ...` 表示 y 是一个 argument，替换后的项会跟着 argument 变动。

- 注意上面解法中有出现 $\rightarrow _\beta*$ 和  $\rightarrow _\beta$，这代表精确的reduction步骤数，具体解释参考 `Exercise 1 -> Q8 -> Definition -> β-reduction sequence`。



****

#### Q3

**Suppose P is a fixed point combinator (we do not know which one).** 

**Show that P (S I) is also a fixed point combinator.** 

**We use S = λx. λy. λz.(x z) (y z) and I = λx. x.**



##### Solution

```
We use Assume a fixed point combinator P, 
so we know that
	P F =β F (P F) for any F. 
We aim to show that 
	P (S I) is a fixed point combinator. 

Therefore, we take 
	an arbitrary λ-term F, 
and we aim to show
	(P (S I)) F =β F ((P (S I)) F), 
	or, 
	using fewer parentheses: 
		P (S I) F =β F (P (S I) F). 
We have:
	P (S I) F =β (S I) (P (S I)) F
			= (λx. λy. λz.(x z) (y z))I(P (S I)) F
			→∗β (I F) ((P (S I)) F)
			→β F ((P (S I)) F)

In the first step we use that P is a fixed point combinator. 
In the second step we unfold the definition of S. 
In the third step we do three β-reduction steps. 
In the fourth step we reduce I F to F in one step. 

So indeed
	P (S I) F =β F (P (S I) F).
```

- This exercise illustrates that from a fixed point combinator we can build another fixed point combinatory by applying it to S I. 
- With  'another’we mean‘not β-equal’. 
- Note that we did not show that they are not β-equal.



****

#### Q4

**Give the reduction graphs of the following terms:** 

(a) (I x) (I x); 

(b) I(I I); 

(c) (λx.x x)(I z);



##### Solution:

(a) (I x) (I x);   

![image-20211115225650521](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225650521.png)  



(b) I(I I);   

![image-20211115225706917](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225706917.png)  

- both are correct

- similar as the following example:

  ![image-20211115225733945](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225733945.png)  



(c) (λx.x x)(I z);  

![image-20211115225807089](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225807089.png)  





****

#### Q5

与 `Exercise 1 -> Q13` 一致 （同一题）



****

#### Q6

**Consider the term M = (λx.((λu. u) x) (λz. x Ω)) λy. z.**

(a) Depict the term tree of M. (Unfold the definition of Ω.) 

(b) Give two different α-equivalent renderings of M. 

(c) Reduce M using the leftmost-innermost (call-by-value) strategy. 

(d) Reduce M using the leftmost-outermost (call-by-need) strategy.



##### (没有答案 + 课上没讲， 待补充)



****

#### Q7

**Consider the term**

​	`(λx. λy. x (I I)) (λz. v z) Ω`.

**Reduce is according to the leftmost-innermost strategy, according to the leftmost-outermost to normal form (if possible),** 

**and according to the lazy reduction strategy to weak head normal form (if possible).**



##### Definition

> **Call by value:**
>
> (待补)

> **Call by need:**
>
> (待补)

> **Lazy reduction:**
>
> (待补)

> **Weak head normal form:**
>
> (待补)



##### Solution:

- Leftmost-innermost:

  ![image-20211115225855883](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225855883.png)  

  

- Leftmost-outermost:

  ![image-20211115225931321](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20211115225931321.png)  

  

****

#### Q8

**Reduce in the term** 

​	`(λx. f (x Ω I)) (λu. λv. v w)` 

**repeatedly the lazy redex until a WHNF is reached.**



##### Solution:

```
(λx. f (x Ω I)) (λu. λv. v w) → f ((λu. λv. v w) Ω I)

We stop here, because the variable f applied to the term 
	((λu. λv. v w) Ω I)
is a weak head normal form.
```



****

#### Q9

**Reduce the following term in a minimum number of steps to normal form:** 

​	`(λx.(λy. z y y) (I I)) (I I)`.



##### Solution:

```
Reading from left to right, the first redex 
	I I will be substituted for y
so it will be copied twice,  and the second redex 
	I I will be substituted for x
so it will be erased (or copied zero times). 

Therefore, we minimize the number of β-reduction steps 
if we reduce the first 
	I I to I
before it is substituted for y
and we do not reduce the second 
	I I
but just let it be erased by substituting it for x.

(λx.(λy. z y y) (I I)) (I I) →β (λy. z y y) (I I)
				→β (λy. z y y)I
				→β z I I

```



****

#### Q10

**Consider the function** `foldr`:

`foldr f b [] = b` 

`foldr f b (h:t) = f h (foldr f b t)`

**Use it to give a definition of the function myconcat that takes as input a list of lists,** 

**and that gives back as output the concatenation of those lists.** 



**Example:**

```haskell
*Main> myconcat [[1,2,3] , [4,5,6]] 
[1,2,3,4,5,6]
```

**Give the first four steps of the evaluation of** 

​	`myconcat [[1,2,3] , [4,5,6]]`

**using informal equational reasoning.**



##### Solution:

```
We define:
	myconcat = foldr append []
	append [] k = k
	append (h : t) k = h : (append t k)
	
We now evaluate 
	myconcat[[1, 2, 3], [4, 5, 6]]:

myconcat[[1, 2, 3], [4, 5, 6]] = foldr append [] [[1, 2, 3], [4, 5, 6]]
					= append [1, 2, 3] (foldr append [] [[4, 5, 6]])
					= 1 : append [2, 3],(foldr append [] [[4, 5, 6]])
					= 1 : 2 : append [3],(foldr append [] [[4, 5, 6]])
					= 1 : 2 : 3 : append [],(foldr append [] [[4, 5, 6]])
					= 1 : 2 : 3 : (foldr append [] [[4, 5, 6]])
					= 1 : 2 : 3 : (append [4, 5, 6] (foldr append [] []))
					= 1 : 2 : 3 : 4 : (append [5, 6, ] (foldr append [] []))
					= 1 : 2 : 3 : 4 : 5 : (append [6],(foldr append [] []))
					= 1 : 2 : 3 : 4 : 5 : 6 : (append [](foldr append [] []))
					= 1 : 2 : 3 : 4 : 5 : 6 : (foldr append [] [])
					= 1 : 2 : 3 : 4 : 5 : 6 : []
					= [1, 2, 3, 4, 5, 6]
```

- 考试时不会出需要 evaluate 这么多步骤的题目，但基础思想不变。



****

#### Q11

**Show the following:** (ite : if - then - else)

​	ite true P Q $\rightarrow _\beta$ P



#### Definition

> **Booleans:**
>
> (待补)



##### Solution

```
Note that P and Q are arbitrary λ-terms.

ite true P Q 				= 		(unfold the definition)
(λx. λy. λz. x y z) true P Q 	 →β
(λy. λz.true y z) P Q 		    →β
(λz.true P z) Q 			→β
true P Q 				     = 		   (unfold the definition)
(λx. λy. x) P Q 			 →β
(λy. P) Q 				     →β
P
```

- Note that P and Q are not necessarily closed, but by the variable convention free variables in P or in Q are not captured by substituting P or Q below a λ.



****

#### Q12

**Show the following:** 

​	or true false $\rightarrow _\beta$ true.



##### Solution

```
or true false 				= 	(unfold the definition)
(λx. λy. x true y)true false 	  →β
(λy.true true y)false 		     →β
true true false 			 = 	(unfold the definition)
(λx. λy. x)true false 		      →β
(λy.true)false 				 →β
true
```



****

#### Q13

**Show that** 

​	Suc $c_1$ $\rightarrow _\beta$ $c_2$, 

**with Suc defined as**  `λxsz. s (x s z)`.



##### Definition

> **Successor (Suc):**
>
> - Successor and Church numerals, check CourseNotes_Lambda_Calculus -> 4.4 Church numerals



##### Solution:

```
Suc c1 					= 	(unfold the definition)
(λxsz. s (x s z)) c1 		    →β
λs. λz. s (c1 s z) 			  =      (unfold the definition)
λs. λz. s ((λu. λv. u v) s z)       →β
λs. λz. s ((λv. s v) z)		      →β
λs. λz. s (s z) 			= 	 (fold the definition)
c2
```



****

#### Q14

**Show that** 

​	$Plus\  c_1\  c_2\  \rightarrow _\beta\  c_3$​ 

**with Plus defined as** `λmn. λsz. m s (n s z)`.



##### Solution:

```
Plus c1 c2 						= (unfold the definition)
(λmn. λsz. m s (n s z)) c1 c2 		   →β
(λn. λsz. c1 s (n s z)) c2 			    →β
λsz. c1 s (c2 s z) 				       = (unfold the definition)
λsz. c1 s ((λu λv. u (u v)) s z) 		→β
λsz. c1 s ((λv. s (s v)) z) 		      →β
λsz. c1 s (s (s z)) 				= (unfold the definition)
λsz.(λu λv. u v) s (s (s z)) 		      →β
λsz.(λv. s v) (s (s z)) 			    →β
λsz. s (s (s z)) 				       = (fold the definition)
c3
```



****

#### Q15

**Show that for arbitrary P and Q we have the following:** 

​	$π_1\  (π\  P\  Q)\ \rightarrow _\beta\  P$.



#### （没有答案，待补）



****

#### Q16

**We represent lists using** 

​	`nil := λxy. y` and `cons := λht. λz. z h t = π` 

**Give a λ-term for empty (the function that takes as input a list and yields true if the list is empty and false otherwise), and show that empty nil reduces to true.**



#### (没有答案，待补）



****

#### Q17

**We define** 

​	`τ = λx1. λx2. λx3. λz. z x1 x2 x3`. 

**This λ-term can be used to build triples:** 

​	$τ\ P_1\  P_2\ P_3\ \rightarrow _\beta\ λz.\ z P_1\ P_2\ P_3$. 

**Now define λ-terms τ1, τ2 and τ3 representing the first, second, and third projection.** 

**Show that they have the right behaviour, that is:** 

​	$τ_1\ (τ\ P_1\ P_2\ P_3)\ \rightarrow _\beta\ P_1, $

​	$τ_2\ (τ\ P_1\ P_2\ P_3)\ \rightarrow _\beta\ P_2, $​​

​	$τ_3\ (τ\ P_1\ P_2\ P_3)\ \rightarrow _\beta\ P_3. $​



##### Solution:

```
The idea is to adapt the first and second projection from the pairing operator to this case of triples. 
We define the following:
	τ1 = λy. y (λx1. λx2. λx3. x1)
	τ2 = λy. y (λx1. λx2. λx3. x2)
	τ3 = λy. y (λx1. λx2. λx3. x3)

We now show that these terms have the right behaviour. 

Take 
	arbitrary terms P1, P2, P3. 

We have the following:
	τ1 (τ P1 P2 P3) = τ1 ((λx1. λx2. λx3. λz. z x1 x2 x3) P1 P2 P3)
				→∗β τ1 (λz. z P1 P2 P3)
				= (λy. y (λx1. λx2. λx3. x1)) (λz. z P1 P2 P3)
				→β (λz. z P1 P2 P3) λx1. λx2. λx3. x1
				→β (λx1. λx2. λx3. x1) P1 P2 P3
				→∗β P1

```



****

#### Q18

**a. Give a specification for the operation exclusive or, notation xor, that takes two booleans as input and yields true if exactly one of the inputs is true.** 



##### Solution:

```
The (to be found) term xor should satisfy the following:
	xor true true =β false
	xor true false =β true
	xor false true =β true
	xor false false =β false
```



**b. Give a λ-term for xor.** 



##### Solution:

```
We define 
	xor = λx. λy. x (not y) y, with not = λx. x false true.

A bit of intuition: 
	xor takes two inputs, 
more intuitively: two booleans as input (something which cannot be enforced in the untyped λ-calculus). 
Hence the start with two abstractions. 

If the first input is or evaluates to true, 
then from the first two lines of the specification we see that we should return the negation of the second input. 

Hence the first argument of x, the one that is returned if x is true, is not y.

If the first input is or evaluates to false, then from the last two lines of the specification we see that we should return the second input.
Hence the second argument of x, the one that is returned if x is false, is y.

More straight forward:

xor = λx λy. ? 
(two arguments)

true = λx. λy . x
false = λx. λy. y

xor = λx. λy. x ① ②
if ① true, 
then, return not ②,
because:
	x true false = true
	x true true = false

therefore, 
	xor = λx. λy. x (not y) ②
if ① false,
then, return ②,
because:
	x false true = true
	x false false = false
 
 therefore,
	xor = λx. λy. x (not y) y
```



**c. Show for one of the four possible inputs that xor satisfies the specification.**



##### Solution:

```
xor false true 
= (λx. λy. x (not y) y)false true
→∗β false (not true)true
= (λx. λy. y) (not true)true
→∗β true

More detailed version:

xor true false
= ( λx. λy. x (not y) y) true false
->-> true (not false) false
= (λx. λy.x) (not false) false
->-> not false
= (λx.x false true) false
-> false false true
= (λx. λy. y) false true
->-> true
```

