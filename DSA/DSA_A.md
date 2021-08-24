# 真·超浓缩DSA整合攻略（期中篇）

---


## Time complexity
`Comparison-based Sorting Algorithm`

Algorithm|worst-case|average-case|best-case
:-:|:-:|:-:|:-:
Insertion Sort|$\Theta(n^2)$|$\Theta(n^2)$|linear function of $n$
Selection Sort|$\Theta(n^2)$|$\Theta(n^2)$|$\Theta(n^2)$
Merge Sort (general)|$\Theta(n·logn)$|$\Theta(n·logn)$|/
_Merge_|/|$\Theta(n)$|/
[Heap Sort (general)](|$O(n·logn)$/$\Theta(n·logn)$|/|/
buildMaxHeap|/|bottum-up:$O(n)$ one-by-one:$O(nlogn)$|/
_MaxHeapify_|/|$O(logn)$|/
Priority Queue|insert $O(logn)$|remove $O(logn)$|maximum $\Theta(1)$
Quick Sort|$\Theta(n^2)$|Balanced/expected Case  $O(nlogn)$|$\Theta(n·logn)$

>**Notice that the time complexity (in general) of insertion sort is in $O(n^2)$​ but not in $\Theta(n^2)$​**​



`Linear Sorting Algorithm`

Algorithm|worst-case|average-case|
:-:|:-:|:-:|:-:
Counting Sort|$\Theta(k+n)$|$\Theta(k+n)$
Radix Sort|$\Theta(d(n+k))$|$\Theta(d(n+k))$
Bucket Sort|$\Theta(n^2)$|$\Theta(n)$​


----------

## Stability and in-place

Algorithm|stable|in-place|
:-:|:-:|:-:|:-:
Insertion Sort|$\bigodot$|$\bigodot$
Merge Sort|$\bigodot$|$\bigotimes$
Heap Sort|$\bigotimes$|$\bigodot$
Quick Sort|mostly unstable|$\bigodot$
Counting Sort|$\bigodot$|$\bigotimes$
Radix Sort|$\bigodot$ |$\bigotimes$
Bucket Sort|$\bigodot$ depend on the underlying sort|$\bigotimes$​



----------

## Some Definitions

## Bounds

$\Theta$ asymptotic tight bound('$=$')
$O$ asymptotic upper bound('$\leq$')
$\Omega$ asymptotic lower bound('$\geq$')
$o$ asymptotic upper bound not tight('$<$')
$\omega$ asymptotic lower bound not tight('$>$​​')



>**Asymptotic tight bound: $\Theta$**

for $f,g: \mathbb{N} \rightarrow \mathbb{R}^+ :f(n) \in \Theta(g(n))$ if
    $$\exists c,c' > 0 \in \mathbb{R} $$$$\exists n_0 > 0 \in \mathbb{N} $$$$\forall n \in \mathbb{N} : n \geq n_0 \Rightarrow c · g(n) \leq f(n) \leq c' ·g(n)$$

$f(n)$ is eventually '**as large as** $g(n)$' up to constants

We write $f(n) \in \Theta(g(n))$ or also $f(n) = \Theta(g(n))$



Notice that ($\Theta(g(n))$​​ is a set of functions)



>**Asymptotic upper bound: $O$**

for $f,g: \mathbb{N} \rightarrow \mathbb{R}^+ :f(n) \in O(g(n))$ if
    $$\exists c > 0 \in \mathbb{R} $$$$\exists n_0 > 0 \in \mathbb{N} $$$$\forall n \in \mathbb{N} : n \geq n_0 \Rightarrow  f(n) \leq c ·g(n)$$

$f(n)$​ is eventually '**smaller-equal** $g(n)$​' up to constants



>**Properties**

- $f(n) \in \Theta(g(n))$​ if 
  $$f(n)\in O(g(n))$$​ $$and$$​ $$g(n) \in O(f(n))$$​

  

This is the same as:
$a = b$​ if $a\leq b$​ and $b\leq a$​



- Big-O properties:

`large degrees beat lower degrees`
 $n^a\in O(n^b)$ for all $0<a\leq b$   

e.g. $n^2 \in O(n^3)$​



`polynomials beat log`
$log_a(n) \in O(n^b) $ for all $a, b > 0$

e.g. $log n \in O(\sqrt{n})$​



`exponentials beat polynomials`
$n^a \in O(b^n)$ for all $a > 0$ and $b > 1$

e.g. $n^5 \in O(2^n)$​



`logs euqally large`
$log_a n \in O(log_b n)$ for all $a,b > 0$

e.g. $log_2 n \in O(log_3 n)$​



This is because

$$a^{log_a b·log_b n} = (a^{log_a b})^{log_b n} = b^{log_b n} = n$$​



hence we have: $log_a b · log_b n = log_a n$​


----------

## Tree

- Set of nodes with a **parent-child** relation
- A unique distinguished node **root**
- every non-root node has a **unique** ancestor/ predecessor / parent
- a node may have successors / descendants / children
- a node without successors is a **leaf** or **external** (node without children)
- a node with successors is **internal** (node with children)

- the depth of a node is the length of the path to the root (**depth: 该node到root的距离**)
- the height of a node is the maximal length of a path to a leaf (height: **该node到最远leaf的距离**)
- **the height of a tree = the height of the root = maximal depth**
- a **level** or **layer** of a tree consists of all **nodes** of the **same depth**

- number of levels = height of tree + 1


>**binary tree**

- every node has 0, 1 or 2 (ordered) successors
- binary tree is complete if all levels are completely filled
- binary tree is almost or nearly complete if all levels are completely filled 
  except possibly the lowest one which is filled left-to-right

complete $\Rightarrow$ almost complete $\Rightarrow$ normal binary

`an almost complete binary tree corresponds naturally to an array`
![image_1ej0ajlam7tk1s3km7u1sqa95ld1.png-24.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0ajlam7tk1s3km7u1sqa95ld1.png)

- let the height of an almost complete binary tree is $h$
  `if the lowest level contains one element`
  number of element $n = 1 + 2+3+...+2^{h-1} +1 = 2^h -1+1 = 2^h$  
  `if the lowest level is full`
  number of element $n = 1 + 2+3+...+2^h = 2^{h+1} -1$​  

  

so $2^h\leq n\leq 2^{h+1}-1<2^{h+1}$

so $h\leq logn\leq h+1$

so $h = \lfloor logn \rfloor$​



>**parent-children relation in the array**

- i an index in the array

`已知child的index，返回parent的index`
$Algorithm$ $parent(i)$
$return$ $\lfloor i/2\rfloor$​



`已知parent的index， 返回左边child的index`
$Algorithm$ $left(i)$
$return$ $2i$​



`已知parent的index， 返回右边child的index`
$Algorithm$ $left(i)$
$return$ $2i+1$​



>**Decision Tree**


----------

## Heap

- A heap is an almost complete binary tree
- all levels from as full as possible
- if we walk downwards then keys decrease
- 

>**max-heap**

- an almost complete binary tree
- every node is labeled with a key/ label from a totally ordered set
- on every path from the root to a leaf the labels / keys are non-increasing (根最大，越往下越小）

$H[parent(i)]\geq H[i]$

- 如果一个heap所有的node有相同的值，这也是一个max-heap



----------

## Pseudocode

#### Insertion Sort


```javascript
//A: Input Array
//n: Array Size

Alogorithm insertionSort(A,n):
  for j:= 2 to n do
    key := A[j]
    i := j - 1
    while i > 0 and A[i] > key do
      A[i+1] := A[i]
      i := i - 1
    A[i+1] := key
```
![image_1eive5g50110d12hc1kd91e8e1m10p.png-75.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eive5g50110d12hc1kd91e8e1m10p.png)



----------



#### Merge Sort



```javascript
//A: Array
//p: The start index of the array
//r: The end index of the array

Algorithm mergeSort(A, p, r):
  if p < r then
    q := floor((p + r)/2) // take the floor
    mergeSort(A, p, q)
    mergeSort(A, q+1, r)
    Merge(A, p, q, r)
```
```javascript
MERGE(A,p,q,r)
  n1 = q - p + 1 //lhs array size
  n2 = r - q //rhs array size
  let L[1..n1 + 1] and R[1..n2 + 1] be new arrays //array size is 1 place bigger than n1 and n2
  for i = 1 to n1
    L[i] = A[p + i - 1] //copy lhs into L
  for j = 1 to n2
    R[j] = A[q + j] //copy rhs into R
  L[n1 + 1] = infinity //last element be infinity
  R[n2 + 1] = infinity
  i = 1 //reset i and j
  j = 1
  for k = p to r // actual merge starts from here
    if L[i]<= R[j]
      A[k] = L[i]
      i = i + 1
    else A[k] = R[j]
      j = j + 1
```
![image_1eivj34sek2fbsk1vtf2lm194b26.png-110.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivj34sek2fbsk1vtf2lm194b26.png)
![image_1eivj4h7m1emek4o0tep7bpj2j.png-68.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivj4h7m1emek4o0tep7bpj2j.png)





----------



#### Heap Sort

`MaxHeapify`

```javascript
//Maintaining the heap property
//We reconstruct the max-heap property using a down-heap bubble

Algorithm MaxHeapify(A,i):
  l := left(i) //2i return index instead of value
  r := right(i) //2i+1
  if l <= A.heap_size and A[l] > A[i] then //l <= A.heap_size is to make sure l is still an index of A
    largest := l
  else 
    largest := i
    
//Comparison part
  if r <= A.heap_size and A[r] > A[largest] then
    largest := r
    
//swap part  
  if largest != i then
    swap(A[i], A[largest])
    MaxHeapify(A, largest)
```
![image_1eivk54ni1qcf1o5kj071kmj190130.png-94.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivk54ni1qcf1o5kj071kmj190130.png)

`buildMaxHeap`
```javascript
Algorithm buildMaxHeap(H):
  H.heap_size := H.length
  for i = floor(H.length/2 ) downto 1 do //index great than H.leangth/2 are leaves(trivial max heap)
    MaxHeapify(H,i)
```
![image_1eivkg68m13d891o1o911ek1gbk3d.png-62.4kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivkg68m13d891o1o911ek1gbk3d.png)
![image_1eivkgqkr1kc8gca7nhgsm5nn3q.png-62.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivkgqkr1kc8gca7nhgsm5nn3q.png)

`heapsort`
```javascript
Algorithm heapsort(H):
  buildMaxHeap(H)
  for i = H.lenth downto 2 do
    swap H[1] and H[i]
    H.heap_size := H.heap_size - 1
    MaxHeapify(H,1)
```
![image_1eivkigjirjq1vsv1d931suat8e47.png-93.4kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivkigjirjq1vsv1d931suat8e47.png)



----------



#### Priority Queue



`maximum`

```javascript
//H is a max-heap; return the max key
//does not change the heap, both H.size and H.heapsize do not change
//Theta(1)

Algorithm heapMaximum(H): 
  return H[1] 
```
`remove`
```javascript
//H -> max-heap
//remove and return maximum;error omitted
//H.size does not change; H.heapsize decreases
//O(logn)

Algorithm heapExtractMax(H):
  max := H[1]
  H[1] := H[H.heap_size] //swap the first and the last
  H.heap_size := H.heap_size - 1
  maxHeapify(H,1)   //O(logn)
  return max
```
`insert`
```javascript
//H.size stays the same; H.heapsize increases
//O(logn)

Algorithm heapInsert(H,k):
  H.heap_size := H.heap_size + 1
  H[H.heap_size] := -infinity
  HeapIncreaseKey(H,H.heap_size,k)

Algorithm heapIncreaseKey(H,i,k)
  if k < H[i] then
    return error
  H[i] := k
  while i > 1 and H[parent(i)] < H[i] do
    swap(H[parent(i)]), H[i])
    i := parent(i) // floor(i/2)
```
![image_1eivlpeu2sod7841bqvn6d7il4k.png-96.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivlpeu2sod7841bqvn6d7il4k.png)



----------



#### Quick Sort



`partition`
```javascript
//A: Array
//p: first index
//r: last index

Algorithm partition(A,p,r)
  x := A[r]
  i := p - 1
  for j = p to r - 1 do
    if A[j] <= x then
      i := i + 1
      exchange A[i] with A[j]
  exchange A[i+1] with A[r]
  return i + 1
```
![image_1eivnpkv215pv19up1pa8oot1gs95h.png-128.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivnpkv215pv19up1pa8oot1gs95h.png)

`quickSort`
```javascript
//Initial : (A, 1, A.length)

Algorithm quickSort(A,p,r)
  if p < r then
    q := partition(A,p,r) //index of pivot after partition done
    quickSort(A,p,q - 1)
    quickSort(A, q + 1, r)

//recursion stops if p = r
```



----------



#### Counting Sort



```javascript
//A: Input Array
//B: Output Array
//range from 0 up to k

Algorithm countingSort(A,B,k)
  new array C[0...k] //take space
  //init C
  for i:= 0 to k do //init C
    C[i] := 0
  
  //count occurence in A
  for j := 1 to A.length do
    C[A[j]] := C[A[j]] + 1

  //count "up to" occurence
  for i := 1 to k do
    C[i] := C[i] + C[i - 1]
  
  //genarate B
  for j := A.length downto 1 do
    B[C[A[j]]] := A[j]
    C[A[j]] := C[A[j]] - 1
```
![image_1eivp0chffpn10jhviev1i785u.png-79.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivp0chffpn10jhviev1i785u.png)



----------



#### Radix Sort



```javascript
//A: Input Array
//d: dimension

Algorithm radixSort(A,d)
  for i := 1 to d do
  use some stable sort on digit d
```
![image_1eivpcqb316l9894g051qa31p6k6b.png-49.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivpcqb316l9894g051qa31p6k6b.png)



----------



#### Bucket Sort



```javascript
//A: Input Array with 0<=A[i] <= 1 for i = 1,...,A.length

Algorithm bucketSort(A):
  n := A.length
  new array B[0...n-1]
  for i := 0 to n-1 do
    make B[i] an empty list //init B
  for i := 1 to n do
    insert A[i] into list B[floor(n·A[i])]
  for i := 0 to n-1 do 
    insertionSort(B[i])
  concatenate B[0],B[1],...,B[n-1]
```
![image_1eivplu8n1qc56oa16kbs9ahkg6o.png-60.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivplu8n1qc56oa16kbs9ahkg6o.png)



----------

## Time complexity in detail

#### Inserstion Sort

>**Worst Case**

- we excute the whole-loop as many times as possible($A[i] > key$ always succeeds)

- The input is **inverse sorted**

  

$T(n) = \Theta(n^2)$​



![image_1eivsiflnemh13pk5nk1f1t1n7j75.png-102.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivsiflnemh13pk5nk1f1t1n7j75.png)
![image_1eivsn5jkocgjc6l6p1o4h10gi7i.png-46.4kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivsn5jkocgjc6l6p1o4h10gi7i.png)

>**Best Case**

- the best case occurs if $A[i] > key$ always fails
- this is the case if the input is **sorted**

![image_1eivt8q66k4b8c0up8aml1hr77v.png-28.2kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivt8q66k4b8c0up8aml1hr77v.png)




----------

#### Merge Sort

`recursion tree`
![image_1eivtrs4s1fkg1fdg73r4oa1sh18p.png-26.9kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1eivtrs4s1fkg1fdg73r4oa1sh18p.png)

- Time complexity of merging $n$ elements is in $\Theta(n)$
- height is $logn$ for $n$ is the length of the input-array
- number of levels is $(logn) + 1$
- number of leaves is $n$
- total: $c·n·logn$(from the upper n level) $+ d(n)$(from the leaves)
- So the $T(n)$ is in the form of $anlogn + bn$ which is $\Theta(nlogn)$  ([see recurrence](#mergesort_rec))

`For small inputs, insertion sort may be faster because of the constant`




----------
#### Heap Sort

>**MaxHeapify**

- Time complexity of down-heap bubble determined by **height of the heap**

- so in $Olog(n)$​

  

1. with $h$ the height of the heap:
$T(h) = T(h-1) + 1$ if $h>0$ gives $T(h) \in O(h)$
then use $h \in \Theta(logn)$ gives $T(n) \in O(logn)$

2. with $n$ the number of nodes of the heap:
$T(n) = T(\frac{2}{3}n) + 1$ if $n>1$ gives $T(n) \in O(logn)$

`Because in the worst case the bottom level is exactly half full `

>**buildMaxHeap**

- build MaxHeap is in $O(n)$
![image_1ej02cgai1mmksdn8mm16ptquba0.png-109.5kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej02cgai1mmksdn8mm16ptquba0.png)
![image_1ej02aur3eng9bog1k7okalg9j.png-52.9kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej02aur3eng9bog1k7okalg9j.png)

>**heapsort**

- buildMaxHeap in $O(n)$

- $n-1$ calls of MaxHeapify with every call in $O(logn)$

- hence the worst-case running time of heapsort is in $O(n·logn)$

- worst case happens if the list is already **sorted**

  


----------

#### Quick Sort

>**partition**
```javascript
Algorithm partition(A,p,r)
  x := A[r]
  i := p - 1
  for j = p to r - 1 do
    if A[j] <= x then
      i := i + 1
      exchange A[i] with A[j]
  exchange A[i+1] with A[r]
  return i + 1
```

- We do the test for the for-loop (line 4) $r - p + 1$ times

- We execute the inside of the for-loop $r - p$ times

- Worst-case running time proportional to $r - p$

- Linear in number of elements: 
  on input $A[p...r]$​ in $\Theta(n)$​ with $n = r - p + 1$

  

>**Worst Case**

- Worst-case running time if no 'small ones' or no 'big ones'

$T(n) = T(0) + T(n-1) + \Theta(n)$ with $T(0) \in \Theta(1)$ ([see recurrence](#quicksort_rec))

we find: $T(n) \in \Theta(n^2)$​



>**Best Case**

- Best-case running time if as many 'small ones' as 'big ones'

$T(n) = 2·T(\frac{n}{2}) + \Theta(n)$ with $T(0) \in \Theta(1)$

$2·T(\frac{n}{2})$ is from the recursive calls and $\Theta(n)$ from the partition

we find: $T(n) \in \Theta(n·logn)$​ ([see recurrence](#quicksort_rec))



>**Average Case**

- consider ‘good’ splits (we get $\frac{1}{4}$ and $\frac{3}{4}$ or better) and ‘bad’ splits’

- suppose probability of ‘good’ split is $\frac{1}{2}$

- expectation for node in recursion tree on depth $i$:
$\frac{i}{2}$ ancestors are calls with good pivots

- hence: length array on depth $i$ is $\leq(\frac{3}{4})^\frac{i}{2} ·n$
at least half cases are good 

- length 1 is reached for $i = 2log\frac{4}{3}n$

- hence: height is in $O(logn)$

- work per depth: in $\Theta(n)$​​

  ![image_1ej04pvct3hupmd113fnfp1oeqat.png-34kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej04pvct3hupmd113fnfp1oeqat.png)

`with random key as pivot from input sequence`
_Average_ time complexity of quicksort is in $O(nlogn)$
_Expected_ time complexity of quicksort is in $O(nlogn)$




## Recurrence


#### Insertion Sort

![image_1ej0da0t6tif12vomsadueptii5.png-53.4kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0da0t6tif12vomsadueptii5.png)
![image_1ej0dabc77jsemkhrrq891as7ii.png-24.7kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0dabc77jsemkhrrq891as7ii.png)



#### Merge Sort



![image_1ej0d5anok4jg5dbk1kpppa9eu.png-53.3kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0d5anok4jg5dbk1kpppa9eu.png)



#### Quick Sort



`Worst Case (almost the same as Insertion Sort)`

![image_1ej0d76j1p0a1h591kh34p4iq8fr.png-64.9kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0d76j1p0a1h591kh34p4iq8fr.png)



`Best Case (almost the same as Merge Sort)` 

![image_1ej0d81991q0ctv91gj21ec71lrrg8.png-52.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1ej0d81991q0ctv91gj21ec71lrrg8.png)




