# Database-iSubmit解题思路


---

## Normalisation

### Cover

**只要是从初始entity能连接到的，都往里面塞**

![image_1f6k2uq9010tirra1vu6s17psd9.png-61.6kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6k2uq9010tirra1vu6s17psd9.png)  


----------


### Determinants

![image_1f6k822tf13t41mvkois1a0ake9m.png-171.9kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6k822tf13t41mvkois1a0ake9m.png)  

如， 

```
C->A
A,B,D->C
C->A,B
D->A
C,D->B
```

求{B,C}的determinants，

1.检查所有的FD的右侧，看B和C是否有出现在右侧，如果没有，记入set，如果都出现过，则用空集开始。

```
{}
```
2.将其他元素单独成子集，记入set

```
{{A}, {B},{C}, {D}}
```

3.挑选一个最小的子集，如{C}, 计算C的cover, 如果该子集的cover覆盖{B,C}，则将该子集列入答案。如果cover中不包含，则分别用其他元素extend子集。

```
{{A}, {B},{C}, {D}}
{C}+ = {A,B,C}
//这里可以看出单独一个C可以determine B，C，将{C}列入答案
```
```
{C} //答案

{A}+ = {A} //不包含{B,C}

{{B},{D}, {A,B}, {A,C}, {A,D}} //extend {A}
//这里因为{C}已经是determinants,所以{A,C}不再需要，可以去除

{{B},{D}, {A,B},{A,D}}

```
4.继续将所有子集和extend后的子集都计算cover，直到子集包含所有元素。


----------

### Minimal Key

1.先检查右侧有没有没有出现过的元素，有的话加入start set {}
2.find start set的cover
3.extend start set （与determinants类似）
4.目标是子集的cover可以涵盖所有的元素。

----------


### Canonical functional dependencies

1.将题目先copy到答题框，右侧元素都拆分成单个

```
A，D-> B,C
=>
A,D->B
A,D->C
```

2.检查所有的transitivity，如A->B,B->C, A->C, 我们已经直到从A能推到C,所以A->C多余，删掉。不确定的项就先确定左侧的cover （不包括那一项本身），如果没有这一项，cover也有右侧的内容，则这项多余。

3.最小化左侧，检查如果去除左侧某个元素，仍然能获得该元素和右侧，如果可以，去掉该元素

4.检查剩下的FD，如果去掉这个FD，是否还能获得右侧。


----------

### BCNF

所有FD只允许以下两种情况

1. 右侧是左侧的子集
或者
2. 左侧包含minimal key

**FD转为BCNF形式：**
1. 转成Canonical functional dependencies
2. 将右侧化为最大：计算左边的cover，替换右侧
，注意只将右侧替换成左侧没有的部分
3. 检查所得的所有FD，是否和已有R set冲突(不符合BCNF)

注意： 遇到以下这种，有冲突 但右边不全在R里的情况：
B-> C,G 
R（ABC）
只需将R里有的部分挑出来split
结果为：
R1(AB), R2(BC)

```
E -> A,B,D
B,D -> A //B,D不是R的key，而且BDA和R有overlap，所以需要split B,D
A,C -> B,D

R(A,B,C,D,E)

//split B,D -> A
R(B,C,D,E), R2(B,D,A) //移除R中的A，建立新关系

//split E->A,B,D
R(C,E), R2(B,D,A), R3(E,B,D)

//AC->BD 该关系在新的R set里丢失，没有关系

```

----------

### 3NF

满足**BCNF**则自动满足**3NF**

3NF需满足以下任意一点：

1. 右边属于左边
2. 左边包含key
3. 右边每一个元素都是某minimal key中的一个元素

**FD转为3NF形式：**
1. 转成Canonical functional dependencies
2. 合并左边相同的FD （不要max右边）
3. 将每一个已有的FD转化成Relation （如： A -> B,D 转成 R(A,B,D)）
4. 现有Relations如果没有包含minimal key，将minimal key中选择一个转成Relation
5. 检查有没有relation是另一个的subset，如果有，删除


----------

## Transactions

### Precedence Graphs

有冲突的项：

- RW
- WW
- WR

![image_1f6nal8ig1qk113givleaeq1ek59.png-26.8kB](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image_1f6nal8ig1qk113givleaeq1ek59.png)  

**If there is no cycle in the precedence graph, the schedule is conflict-serializable!**

If the precedence graph contains no cycles, then the schedule is conflict serializable. Then an equivalent serial schedule is obtained by a topological sort of the precedence graph.

Recall, a topological sort of a directed graph G = (V,E) is an ordering of its nodes as v1, v2, …​, vn such that for every edge vi → vj, it holds that i < j.


----------


### Two Phase Locking (Pessimistic)

**Lock-based Concurrency Control: Transactions must lock objects before using them.**

- Shared lock (S-lock): 可以共享，用在 Read前
- Exclusive lock (X-lock): 不可共享，用在Writing前。当Y上有别的transaction上的任何种类的lock时，X-lock不可用在Y上

- 一个Transaction的Unlock开始后，不可以再上任何一种lock
- 2 Phase Locking （2PL）下的schedule是 confilict-serializable的

In **strict two phase locking (strict 2PL)**, we additionally require that: a transaction releases all locks only when the transaction is completed (i.e. when performing commit/rollback).

----------


### Cascading Rollbacks

当一个Transaction commit失败，并被废除，读取它Write数据的其他Transaction也应该被废除，并一级级往后排查。
