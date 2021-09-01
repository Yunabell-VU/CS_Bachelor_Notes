# Pattern Matching

This chapter includes:

- Pattern matching
- Tail recursion
- List

---

## Pattern matching VS Dynamic dispatch

```scala
abstract class Expression {
  def eval(bindings : Map[String,Int]) : Int
}

//advantage of dynamic dispatch is that, if you don't have access to this object file, 
//you can still make a new subtype of expression to add extra case
case class Const(i : Int) extends Expression {
  override def eval(bindings: Map[String, Int]): Int = i //dynamic 
}

case class Var(s : String) extends Expression {
  override def eval(bindings: Map[String, Int]): Int = bindings(s)
}

case class Negate(arg : Expression) extends Expression {
  override def eval(bindings: Map[String, Int]): Int = -arg.eval(bindings)
}

case class Operator(lhs : Expression, operatorName : String, rhs : Expression) extends Expression {
  override def eval(bindings: Map[String, Int]): Int = {
    val l = lhs.eval(bindings)
    val r = rhs.eval(bindings)
   PatterMatch.operatorByName(l,operatorName,r)
  }
}
```

```scala
//examples
//x
object PatterMatch {
  def operatorByName(l: Int, name : String, r: Int) : Int = {
    name match {
      case "+" => l + r
      case "-" => l - r
      case "*" => l * r
      case "/" => l / r
    }
  }

//did exactlly the same thing as eval() defined in abstract class
//but in abstract class we need to define in each sub class the operation is(dynamic dispatch)
//pattern matching is more readable
  def eval(bindings : Map[String, Int], exp : Expression) : Int =
    exp match {
      case Const(i) => i
      case Var(s) => bindings(s)
      case Negate(arg) => -eval(bindings,arg)
      case Operator(lhs,op,rhs) =>
        operatorByName(eval(bindings,lhs),op,eval(bindings,rhs))
    }

  //x
  val ex1 = Var("x")
  val evalEx1 = ex1.eval(Map("x"->1)) //give 1

  //2
  val ex2 = Const(2)
  val evalEx2 = ex2.eval(Map()) //give 2

  //-(-x)
  val ex3 = Negate(Negate(Var("x")))
  val evalEx3 = ex3.eval(Map("x" -> 3)) //gives 3

  //2 * x
  val ex4 = Operator(Const(2),"*",Var("x"))
  val evalEx4 = ex4.eval(Map("x" ->3)) //gives 6

  //(x/y) * 2 + 1
  val ex5 =
    Operator(
      Operator(
        Operator(Var("x"), "/", Var("y")),
        "*", Const(2)),
      "+", Const(1))

  val evalEx5 = ex5.eval(Map("x" -> 6, "y" -> 3)) //gives 5
}
```

## Pattern matching More examples

suppose we need to simplify the expressions

```scala
//rules :
// -(-e) => e
// e + 0 => e
// e * 1 => e
```
this would be extremely difficult to do with dynamic dispatching... so we choose pattern matching 
```scala
def simplify(exp : Expression) : Expression =
    exp match{
      case Negate(Negate(e)) => simplify(e)
      case Operator(e, "+", Const(0)) => simplify(e)
      case Operator(e, "*", Const(1)) => simplify(e)
      case Negate(e) => simplify(e)
      case Operator(l,op,r) => Operator(simplify(l),op,simplify(r))
      case _ => exp
    }
```
**Examples:**

```scala
  //-(-3) ->3
  val simpEx1 = simplify(Negate(Negate(Const(3))))

  //-(-3) + 0 -> 3
  val simpEx2 = simplify(Operator(Negate(Negate(Const(3))), "+", Const(0)))

  //((x * x) * 1) / ((y + 3) + 0) -> (x * x) / (y + 3)
  val simpEx3 = simplify(
    Operator(
      Operator(Operator(Var("x"), "*", Var("x")), "*", Const(1)),
      "/",
      Operator(Operator(Var("y"), "+", Const(3)), "+", Const(0)),
    )
  )
```
**Result :**

```scala
scala> import PatterMatch._
import PatterMatch._
scala> simpEx1
res1: Expression = Const(3)
scala> simpEx2
res0: Expression = Const(3)
scala> simpEx3
res1: Expression = Operator(Operator(Var(x),*,Var(x)),/,Operator(Var(y),+,Const(3)))
```


----------

## Pattern Matching Odds and Ends

### Match vs Switch

Match generalizes switch(C/C++/Java), differences:

- Match is an expression
- Match can match deeply
- Match can match case classes
- Match can bind variables
- No fallthrough or break statement



### Linear Pattern

Patterns must be linear : each variable occurs only once

Example below is **NOT ALLOWED!**
```scala
//e + e => 2 * e

//NOT ALLOWED
def simplifyTop(expr : Expr) ： Expr = expr match{
  case BinOp(e, "+", e) => BinOp(Number(2),"*",e)
  case _ => expr
}
```



### Pattern Guards
Pattern `case p if c` only matches if c is true

Example below is what you **CAN DO!**

```scala
//e + e => 2 * e

//Correct way to implement pattern match
def simplifyTop(expr : Expr) ： Expr = expr match{
  case BinOp(l, "+", r) if l ==r => BinOp(Number(2),"*",l)
  case _ => expr
}
```



#### Types of patterns - wildcards/dontcares(_)

wildcard or dontcares " _ " : match whatever is in there, we don't care what _ is, no binding to the variable.

```scala
def describe(expr : Expr) : String = expr match{
  case Var(_) => "A variable"
  case Number(_) => "A number"
  case UnOp(_,_) => "A unary operator"
  case BinOp(_,_,_) => "A binary operator"
}
```

#### Types of patterns - constants

Any constant can be used as pattern

```scala
def describe(x : Any) = x match {
  case 5 => "five"
  case true => "truth"
  case "hello" => "hi!"
  case Nil => "the empty list"
  case _ => "something else"
}
```

#### Types of patterns - variables

Matches anything, binds value to variable

```scala
expr match {
  case 0 => "zero"
  case somethingElse => "not zero:" + somethingElse
}
```

#### Types of patterns - Constructors

```scala
expr match {
  case BinOp(e, "+", Number(0)) => println("a deep match")
  case _=>
}
```

#### Types of patterns - list patterns

```scala
expr match {
  case List(_,_) => "A list with 2 elements"
  case List(_,_,3) =>"A list with 3 elements ending in 3"
  case List(1,_*) => "A list with more than one element starting with 1" 
  //"_*" indicates any number of elements
  case List(_*) => "Some list"
}
```

#### Types of patterns - tuples patterns

```scala
def tupleDemo(expr : Any) =
expr match{
  case (a,b,c) => println("matched" + a + b + c)
  case_ =>
}
```



### Pattern in value definitions

Can use any pattern after val
```scala
val tuple = ("x",2,1,0)
val(a,b,_) = tuple //distruct tuple by assigning it like (a,b,_)
```
Most useful for tuples.
Also can do case classes, how ever, 
if match fail =>entire program crash (won't crash in the case of tuple)



### Sealed classes

Sealed class = no extension of class possible outside of current file.

```scala
sealed abstrct class Expr
case class Var(name : String) extends Expr
case class Number(num : Double) extends Expr
case class UnOp(operator : String, arg : Expr) extends Expr
case class BinOp(lhs : Expr, operator : String, rhs : Expr) extends Expr
```
If Expr is not sealed, describe needs **a default case** or you will get a warning : `match is not exhaustive!`
```scala
def describe(expr : Expr) : String = expr match {
    case Var(_) => "A variable"
    case Number(_) => "A number"
    case UnOp(_,_) => "A unary operator"
    case BinOp(_,_,_) => "A binary operator" //don't need default case if all the cases are sealed
}
```


----------



## Null, Option and Either

### Aside: The problem with null

Null values, Called "the billion dollar mistate" by its inventor

- Each reference may be `null` -> adds lot of cases to be handled
- No way to say that a reference cannot be null



### Example : Option type
There are alternatives to use `null`.

```scala
sealed abstract class Option[A]
case class Some[A](a:A) extends Option[A]
case class None[A]() extends Option[A]
```
Aka Maybe[A], used to singal that something may fail. Prefer over using `null`.

```scala
calss Map[A,B]{
    def get(a:A) : Option[B] //If "a" doesn't exist, then return B
}
```
```scala
val capitals = Map("France"->"Paris","Japan"->"Tokyo")
capitals get"France"//Some("Paris")
capitals get"North pole" //None()
```

```scala
//In standard Scala library, if return None, there's no parentheses behind.
sealed abstract class Option[+A]
case class Some[A](a:A) extends Option[A]
case class None extends Option[Nothing]
```

Rework the `eval` function:
```scala
def eval(bindings : Map[String, Int], exp : Expression) : Option[Int] =
    exp match {
      case Const(i) => Some(i)
      case Var(s) => bindings.get(s) //will return an Option already
      case Negate(arg) => eval(bindings,arg) match {
        case Some(x) => Some(-x) //if there's some result then negate it
        case None => None
      }
      case Operator(lhs,op,rhs) =>
        (eval(bindings,lhs),eval(bindings,rhs)) match {
            case (Some(l), Some(r)) => Some(operatorByName(l,op,r))
            case _ => None
        }
    }
```

Using standard library we can change the `eval` to :
```scala
//the sealed class here just to show how the standard libray works, no need to add this in your code
sealed abstract class Option[+A]{
    def map[B](f : A=> B) : Option[B]//transfer A to B and return Option[B]
}
case class Some[A](a:A) extends Option[A] {
    def map[B](f : A=> B) : Option[B] = Some(f(a)) 
    //if there's something there, then we return a function
}
case class None extends Option[Nothing] {
    def map[B](f : Nothing => B) : Option[B] = None
    //if there's nothing, then we return nothing
}

def eval(bindings : Map[String, Int], exp : Expression) : Option[Int] =
    exp match {
      case Const(i) => Some(i)
      case Var(s) => bindings.get(s) //will return an Option already
      case Negate(arg) => eval(bindings,arg).map(-_) 
      case Operator(lhs,op,rhs) =>
        eval(bindings,lhs).flatMap(l=>
            eval(bindings,rhs).map(r => operatorByName(l,op,r)))
    }
```

You can define a method for the general pattern where you only apply some functions if the lhs and rhs is `Some()` :
```scala
//pattern match both lhs and rhs
def zipWith(lhs : Option [A], rhs : Option[B], f : (A,B => C) : Option[C] =
    (lhs,rhs) match {
        case (Some(l),Some(r)) => Some(f(l,r))
        case _ => None
    }

def eval(bindings : Map[String, Int], exp : Expression) : Option[Int] =
    exp match {
      case Const(i) => Some(i)
      case Var(s) => bindings.get(s) //will return an Option already
      case Negate(arg) => eval(bindings,arg) match {
        case Some(x) => Some(-x) //if there's some result then negate it
        case None => None
      }
      case Operator(lhs,op,rhs) =>
        zipWith(eval(bindings,lhs),eval(bindings,rhs),operatorByName(_,op,_)) 
    }

```



### Null and Option in other languages

>Haskell

- There is no `null`.
- `Option` is called `Maybe`, always used to signal nonexistence.

>C++

- Use `null` to signal nonexistence

>Java

- Typically use null to signal nonexistence, in Java 8 a `Option[A]` was added to stdlib

>Scala

- `Null` is considered a wart inherited from Java.

- Next version of 3 will probably not allow `null` without explicit an type annotation

  

### Example : Either type
Another alternative to `Option` where instead of `None`, we can pass some information of `type A`(for example `String`). Can be used as an alternative to exceptions.

```scala
sealed abstract class Either[A,B] // e.g. Either[String, Int]
case class Left[A,B](a : A) extends Either[A,B] //If failed, then return Left
case class Right[A,B](b: B) extends Either[A,B] //If went well, then return Right
```


----------

## Tail Recursion

Two codes here compute exactly the same thing:

```scala
def approximateLoop(initialGuess : Double) : Double = {
    var guess = initialGuess
    while(!isGoodEnough(guess))
        guess = improve(guess)
    guess
}
```

```scala
def approximate(guess : Double) : Double = 
    if (isGoodEnough(guess) guess
    else approximate(improve(guess))
```


**Which is faster?**
The answer is they are equally fast. Because approximate is tail-recursive.

>**Tail-recursive** : recursive call is directly after "`return`"

```scala
def approximate(guess : Double) : Double = 
    if (isGoodEnough(guess) guess
    else approximate(improve(guess)) //recursive call in tail position
```



### Why tail recursion?

In Haskell, Scheme, Lisp, ML, F# there is no `for` or `while` loop, use tail recursion instead.

### Example : Factorial

```scala
def factorial(n : Int) : Int = {
    var res = 1
    for(i <- 2 to n) res* = i
    res
}

def factorial(n : Int) : Int = n match {
    case 0 => 1
    case _ => n * factorial(n-1) 

    //after factorial() you need to multiply with n, so factorial is not the last thing you do
    //so this is not tail recurvise. It's a little slower than for loop above
}
```
What happens in the second function:
```scala
factorial(6)
6 * factorial(5)
6 * (5 * factorial(4))
6 * (5 * (4 * factorial(3)))
6 * (5 * (4 * (3 * factorial(2))))
6 * (5 * (4 * (3 * (2 * factorial(1)))))
6 * (5 * (4 * (3 * (2 * 1))))
6 * (5 * (4 * (3 * 2)))
6 * (5 * (4 * 6))
6 * (5 * 24)
6 * 120
720

Stack depth : 6
```



#### Factorial tail recursion - accumulating parameter

```scala
def factorial(n : Int) : Int = {
    def facTailRec(n : Int, accum : Int) : Int = n match{
        case 0 =>accum
        case n = facTailRec(n-1, accum * n) //tail recursive
    }
    facTailRec(n,1)
}
```
What happens in the function: 
```scala
factorial(6)
facTailRec(6,1)
facTailRec(5,6)
facTailRec(4,30)
facTailRec(3,120)
facTailRec(2,360)
facTailRec(1,720)
720

Stack depth : 1
```
**accumulating parameter = loop**



### Avoid the problem : use fold

```scala
def factorial(n : Int) = (1 until n).fold(1)(_*_) //standard defined tail recursion
```


----------


## List

### Concatenate two lists, add element, reverse

```scala
//our own list
sealed abstract class Listt[A] {
  def fold(i : A)(f : (A,A) => A) : A =
    this match {
      case Cons(h,t) => t.fold(f(i,h))(f)
      case NNil() => i
    }

    def ++(rhs : Listt[A]) : Listt[A] = {
      this match {
        case Cons(h,t) => Cons(h,t ++ rhs) //not tail recursive
        case NNil() => rhs
      }
    }

  //add element to the back of the list
  def addToBack(a : A) : Listt[A] = {
    this match {
      case Cons(h,t) => Cons(h,t.addToBack(a)) //not tail recursive
      case NNil() => Cons(a,NNil())
    }
  }

  def reverse : Listt[A] = {
    this match {
      case Cons(h,t) =>(t.reverse).addToBack(h) //not tail recursive
      case NNil()=> NNil()
    }
  }
  
}

//written infix :: for list from standard library
case class Cons[A](head : A, tail : Listt[A]) extends Listt[A]
//called Nil in standard libray
case class NNil[A]() extends Listt[A]
```
make `reverve` tail recursive:
```scala
def reverseTail : Listt[A]= {
    def reverseAccum(l:Listt[A], accum : Listt[A]) : Listt[A] = {
      l match {
        // if the list is not empty, reverse the tail of the list 
        // then we add head to the accum parameter
        case Cons(h,t) => reverseAccum(t,Cons(h,accum))
        case NNil() => accum
      }
    }
    reverseAccum(this, NNil())
  }
```

#### map

```scala
//Not tail recursive version
  def map[B](f : A => B) : Listt[A] = {
    this match{
      case Cons(h,t) => Cons(f(h), t.map(f))
      case NNil() => NNil()
    }
  }
```

```scala
//Tail recursive version
def mapTail[B](f : A => B) : Listt[B] = {
   def mapAccum(l : Listt[A], accum : Listt[B]) : Listt[B] = {
     l match {
       case Cons(h,t) => mapAccum(t,Cons(f(h),accum))
       case NNil() => accum
     }
   }
    mapAccum(this,NNil()).reverse 
    //because the mapAccum is tai recursive, it reverse our list which we don't want.
  }
```