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

**Write the following λ-term in the notation with all parentheses and all λs:  **

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

