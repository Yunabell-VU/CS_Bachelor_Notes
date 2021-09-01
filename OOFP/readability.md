# Readability



---

## Example of Readable code

```scala
class InterestRate {
  //example: 0.2% interest rate daily means 107.3% yearly in non-leap year
  def dailyToYearlyInterestRate(year: Int, dailyInterestRate:Double) = {
    val dailyInterestFactor = rateToFactor(dailyInterestRate)
    val yearlyInterestFactor = Math.pow(dailyInterestFactor, daysInYear(year))
    factorToRate(yearlyInterestFactor)
  }

  def rateToFactor(rate : Double) = 1.0 + rate //0.02 rate means factor 1.02
  def factorToRate(factor: Double) = factor - 1.0 //factor 1.02 means 0.02rate

  def daysInYear(year: Int) : Int = if(isLeapYear(year)) DaysInLeapYear else DaysInYear

  def isLeapYear(year : Int) : Boolean =
    divisibleBy(year, 400)||(divisibleBy(year,4) && !divisibleBy(year,100))

  def divisibleBy(n : Int, div : Int) : Boolean = n % div == 0

  val DaysInYear = 365
  val DaysInLeapYear = DaysInYear + 1
}

```
#### Good Code

- Use constants  
- Meaningful names  
- Functions that do one thing  
- One level of abstraction expanded at a time  
- Comments explain things that which cannot be expressed in code

#### Constants

Use constants instead of "Magic numbers"

- Easier to understand
- Easier to change value of constant 

```scala
def widthInPixels = 40 * 10
def cellIndexX(pixelX : Int) = pixel / 10
```
```scala
val WidthInNrCells = 40
val CellWidthInPixels = 10
def widthInPixels  = WidthInNrCells * CellWidthInPixels
def cellIndexX( pixelX : Int) = pixelX / CellWidthInPixels 
```
---
### Naming example

**Better naming**
```scala
val StatusIndex = 0
val Flagged = 4
def getFlaggedCells: ArrayBuffer[Array[Int]] = {
  val flaggedCells = new ArrayBuffer[Array[Int]]()
  for (cell <- gameBoard){
    if (cell(StatusIndex) == Flagged) flaggedCells += cell  
  }
  return flaggedCells
}
```
**Good naming**
```scala
def getFlaggedCells: ArrayBuffer[Cell] = {
  val flaggedCells = new ArrayBuffer[Cell]
  for(cell <- gameBoard) {
    if(cell.isFlagged()) flaggedCells += cell
  }
  return flaggedCells
}
```
**Good name for function**
You do not have to read the function definition to know what a function does -- only its name!
```scala
def getFlaggedCells: List[Cell]
```
**Abbreviation**
Ok if standard & clear from context
```scala
def greatestCommonDivisor(a : Int, b : Int) : Int
```
vs
```scala
//euclids greatest common divisor
def gcd(a : Int, b : Int) : Int
```
**Names & Scopes**
small scope = short name
large scope = long name
```scala
def changeDir(d : Direction) : Unit = {
  currentState = currentState.changeDir(d)
}
```
```scala
case class Rational(
  n : Int, // numerator
  d : Int, // denominator
  ){
}
```
**Names - use pronounceable names**
- make sure you can talk about code
```scala
var genymdhms : Date
var modymdhms : Date
val pszqint : String
```
```scala
var generationTimestamp : Date
var modificationTimestamp : Date
val recordld: String
```
---
### Comments
prefer self-explanatory code over comments

```scala
//Check to see if the employee is eligible for full benefits
if((emplyer.flags & HOURLY_FLAG)&&
  (employee.age > 65))
```
```scala
if(employee.isEligibleForFullBenefits())
```
Do not do this:
```scala
x += 1; //increase x
if(s == "test") {//Check if s equals test
    test = true; //Set test to true
}
```
**Good comments**
Explain things which cannot be expressed in code

```scala
//implement algorithm described in paper "O(nlogn) KDTree traversal"
//This fixes bug #4325
//TODO: Refactor this code
```

---
### Functions

- Work at one level of abstraction
- Do on thing
- Descriptive Names

**Mixing levels of abstractions**
Details of many concepts expanded at same time:

```scala
def yi(y : Int, i : Double) : Double = {
    val ifc = 1.0 + i
    if(y % 4 == 0 && (y % 100 != 0 || y % 400 == 0))
        Math.pow(ifc, 366) - 1
    else Math.pow(ifc, 365) - 1
}
```
- How many days in a year?
- What is a leap year
- How to convert interest rate to factor

**Example of expanding mutiple levels of abstractions at the same time**  

![image_1eibo477teme2vd1vg3g7u1rbj1m.png-336.9kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eibo477teme2vd1vg3g7u1rbj1m.png)  


![image_1eibomb4a1n0u9lc1ojn1ou41uni9.png-322.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eibomb4a1n0u9lc1ojn1ou41uni9.png)

**Symptoms of expading mutiple levels of abstraction**

- Long functions (> 10 lines)
- Duplicated code (otherwise the repeated functionality would be grouped in its own function, and then called multiple times)
- Nested control structures(if in while in for)

**Better**

```java
public static String renderPageWithSetupsAndTeardowns(
    PageData pageData, boolean isSuite)throws Exception{
    if (isTestPage(pageData))
        includeSetupAndTeardownPages(pageData,isSuite);
    return pageData.getHtml();
}
```

![image_1eibp096jsks1udeglp11he154cm.png-188.1kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eibp096jsks1udeglp11he154cm.png)  

- Side Effect (initialize session) not in name
- Does not do one thing

![image_1eibp2nem6661ov0tru2ml1j613.png-261.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eibp2nem6661ov0tru2ml1j613.png)  



![image_1eibp37b11lvk1aom2ab1bqb79l1g.png-247.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eibp37b11lvk1aom2ab1bqb79l1g.png)

---

### Conclusion

- Simplicity is hard, complexity is easy
- Readability is the most important aspect of software
- Good code explains itself so well, that it seems obvious when reading
    * Use constants
    
    * Meaningful names
    
    * Comments explain that which cannot be expressed in code
    
    * Short functions that do one thing
    
    * One level of abstraction expanded at a time
    
      

## Common coding pitfalls

- Reinventing the wheel
- Premature optimization
- Premature generalization

#### Do not reinvent the wheel

- use built in datastructures, algorithms!

**Do Not**

- Implement your own linked list
- Implement your own sort function
- etc



### Premature optimization
Structuring your code to hopefully make it faster without necessity.  


**What is costly?**

What is fast and what is slow is extremely hard to predict  

- Layers of compilers
- Java virtual machine performs optimizations at runtime  

Need **measurements** to optimize performance  
Your assumptions about what is costly and what is cheap are probably wrong

All optimization is premature unless:

- Your program is too slow
- You have a measurement showing that the optimization could improve things

#### Premature generalization
Structuring your code to make it more general without necessity.  
It is premature if it makes the code more difficult to read.  

#### YAGNI - You ain't gonna need it

_"Always implement things when you actually need them, never when you just foresee that you may need them."_



## Code Style Guide

This section describes how we will grade your code style in assignments 2.3 (Snake reverse mode), 3 (Tetris) and 4 ( Repls). You will also use these guidelines yourself, in the peer review of assignment 2.2.

For these assignments, we want you to make the simplest and most readable implementation possible as explained in the readable code lectures. We will grade your implementation based on your code style and hence implementations of students should be as comparable as possible. This means you should NOT implement additional functionality beyond what is needed for the tests. If the implementation of one student has much more functionality or is much more generic than that of another student, they become incomparable. We do encourage you to implement extra functionality with as many bells and whistles as possible in the bonus assignment.

To keep your submissions somewhat comparable, please make sure to adhere to the
following mantras:

- Make the code as simple and readable as possible.
- Implement only what is asked in the assignment, nothing more (extra functionality is encouraged - in the bonus assignment).
- Use only the abstractions you actually need. Do not make your code generic to
- accommodate possible future extensions or reuse.

Some things that will we penalize are (this list is not exclusive, there may be ways of producing unreadable code not listed below).

###Repeated code
Copying a bit of code and changing it a little is easy but results in lengthy code that is hard to maintain (making 1 conceptual change means changing all copies). If you need to copy code you are missing an abstraction: the
repeated code should be grouped in its own function, and then called multiple times.

### Multiple levels of abstraction expanded at once
As explained in the readable code lectures, multiple levels of abstraction expanded at once means that you fail to make a separate abstraction for a concept. For example, you might use:

```scala
user.hasDrivingLicense() && !user.isIntoxicated()
```
instead of the easier to understand:
```scala
user.legallyAllowedToDrive()
```
Another example: Using 
```scala
y % 4 == 0 && (y % 100 != 0 || y % 400 == 0)
```
instead of:
```scala
isLeapYear(y)
```
A very minor (and common) example is using x % 2 == 0 instead of isEven(x)

####  Unclear names
The easest fault to make as well as the most frequent one. As discussed, a name should be such that you can understand what it means without looking up its definition. 
Some examples of unclear names and their penalty are:

- Name describes only part of what is going on. For example, we saw methods called reset without it being clear what was being reset. Better would be to call it resetBlock (if it resets the block).
- Side effects unclear from name. Example: checkPassword instead of checkPasswordAndInitSession
- The name describes how it is doing it,  instead of what is doing, e.g. scanGrid instead of freePositions.

#### Function does more than one thing at a time
If a function (unexpectedly/surprisingly) does more than one thing at a time, it usually also poorly named. Some examples:

- A method called getCellType(x,y) also initializes a variable when needed. If you are reading the code.
- Another example we saw is that getCellType(x,y) also performs a side effect to maintain some state which is needed when placing a random apple and the correctness of this also depends on the order of getCellType calls. This is pretty unexpected when you are ready the code.

#### Variables which are conceptually grouped are not together in a class

This is similar to expanding multiple levels of abstraction at a time and repeating code, but on a higher level than function implementations. For example Use of (centerX, centerY, radius) instead of a class Circle. Another example we saw last year was someone using a 3-tuple (Bool, Array[Array[Bool]], (Int, Int)) instead of a class called  GameState class which contains a gameOver field, a GameBoard instance, and an applePosition. This tuple definition was repeated a lot in the code.

#### Re-implements basic data structures instead of using a library
While implementing your own linked-list or other basic data structure is a nice exercise for a data structures course, you should not do so when actually programming something (unless you’re writing a collections library, obviously).

#### Using variables to pass information instead of method results/arguments
This we also saw frequently last year, instead of using method arguments and results, wide-scope variables are used to pass information. An exaggerated example of this is:

```scala
class Ex {
    var x = 0
    var y = 0
    var z = 0
    def add : Unit  =  z = x + y
    def usage : Int = {
        x = 2
        y = 2
        z
    }
}
```
instead of 
```scala
class Ex {
    def add(x : Int, y : Int) : Int  = x + y
    def usage : Int  = add(2,3)
}
```
