# Logic and Modeling 考点整理



## Propositional logic

### Natural deduction rules (Sytax)

> **Main Question : Given a list of hypothesis, can I derive a particular formula?**

- Know the natural deduction proof rules, and be able to create derivations on your own.

![image_1f6aihekf16kg12lh8c1t2oppr9.png-11.3kB](http://static.zybuluo.com/Yunabell/8wx50hj79ud69uusmvz4rhqv/image_1f6aihekf16kg12lh8c1t2oppr9.png)
![image_1f6aij3kn4fqkmt3f7103r88rm.png-40.1kB](http://static.zybuluo.com/Yunabell/cj414lxeslmr86utezoliaqn/image_1f6aij3kn4fqkmt3f7103r88rm.png)
![image_1f6aijr948vt1ht2ovf1i0bm5613.png-43.8kB](http://static.zybuluo.com/Yunabell/x7797blenvw4x4vfn9l5k34h/image_1f6aijr948vt1ht2ovf1i0bm5613.png)

---

### Sematics of Propositional Logic (Semantics)

> **Main Question: Given a truth assignment for propositional letters, is a particular formula true or false?**

- Be able to use and reason with truth tables.

`Example of Truth table`

![image_1f6aj0r2pk8o18m7sehekmju41g.png-18.8kB](http://static.zybuluo.com/Yunabell/2w1h682sw89a6qask7bu4trr/image_1f6aj0r2pk8o18m7sehekmju41g.png)

- Be able to evaluate formulas as true or false, given a truth assignment for variables.
- Come up with truth assignments to make a formula true or false.
- Understand, be able to reason with, and apply the concepts:
    - Satisfiability, contradiction, validity (tautology) of formulas
    - Semantic entailment |=
    - Logical equivalence ≡
    - Consistency and inconsistency of sets of formulas
    - Soundness and completeness (you don't need to know the proofs of these theorems)

**Logical equivalence：**
:   Two propositions are Logically equivalent if they have identical truth table

**Provable (syntactic notion):**
:     A propositional formula is said to be provable if there is a formal proof of it in that system.

**Tautology / Valid (semantic notion):**
:    A propositional formula is said to be a tautology, or valid, if it is true under any truth assignment.

**Soundness:**
:   The statement that every provable formula (|-) is valid (|=) is known as soundness.

**Comleteness:**
:   The converse, which says that every valid (|=) formula is provable (|-), is known as completeness.

**Logical Consequence:**
:   If Γ is a set of propositional formulas and A is a propositional formula, then A is said to be a logical consequence of Γ if, given any truth assignment that makes every formula in Γ true, A is true as well.
In this extended setting, **soundness** says that if A is provable from Γ, then A is a logical consequence of Γ. 
**Completeness** runs the other way: if A is a logical consequence of Γ, it is provable from Γ.

In symbolic terms, we write **Γ ⊢ A** to express that A **is provable** from the formulas in Γ (or that Γ proves A), and we write **Γ ⊨ A** to express that A **is a logical consequence of Γ** (or that Γ entails A). 

With this notation, **soundness** says that for every propositional formula A and set of propositional formulas Γ, if **Γ ⊢ A then Γ ⊨ A,** 
and **completeness** says that for every A and Γ, if **Γ ⊨ A then Γ ⊢ A.**

---

### 利用Soundness和Completeness证明unprovable

![image_1f6ckmh66p8415ujk711dn0c7d13.png-139.9kB](http://static.zybuluo.com/Yunabell/q7tqr9cwpdv932zdb7vbfg23/image_1f6ckmh66p8415ujk711dn0c7d13.png)

![image_1f6ckekmr1dr5t7oh841nv5aug9.png-77.9kB](http://static.zybuluo.com/Yunabell/tkjuegw7hdecghhjz9gnowaa/image_1f6ckekmr1dr5t7oh841nv5aug9.png)
![image_1f6ckja2a1all1mf61uhn4021cdjm.png-82.5kB](http://static.zybuluo.com/Yunabell/aaoo3iktowm68et4sk315cw1/image_1f6ckja2a1all1mf61uhn4021cdjm.png)

---

## Predicate logic

- Know the natural deduction proof rules, and be able to create derivations on your own.

### Natural deduction (First Order Logic)

![image_1f6ak7te51mdsch13hk169jcrn9.png-10.4kB](http://static.zybuluo.com/Yunabell/976mokzzxvbbiekefmtz3fxd/image_1f6ak7te51mdsch13hk169jcrn9.png)
![image_1f6ak8bqm1skk1v501lf9b0cs02m.png-11.9kB](http://static.zybuluo.com/Yunabell/zqyqka0tbnknv8pissa5yjky/image_1f6ak8bqm1skk1v501lf9b0cs02m.png)
![image_1f6ak8t7716bo1r5cakenh110v213.png-15.1kB](http://static.zybuluo.com/Yunabell/z15k50kkg95d5wkyg10gvobp/image_1f6ak8t7716bo1r5cakenh110v213.png)

### Models for First Order Logic

- Come up with models or counter models for a given formula

if A is an assertion and M is a model of the language of A, we write **M |= A** to mean that **A evaluates to T in M,** and M ̸|= A to mean that A evaluates to F. (You can read the symbol |= as “models” or “satisfies” or “validates.”)

- Interpret formulas in a model

![image_1f6clgifs1jebgtr1er5v3l1si11g.png-62.9kB](http://static.zybuluo.com/Yunabell/eabbx64uppn4a59m1dx0r1wj/image_1f6clgifs1jebgtr1er5v3l1si11g.png)
![image_1f6clgrt9l511ogektq50t1abv1t.png-60.6kB](http://static.zybuluo.com/Yunabell/xwx61txekngh7ji5baf0q3lm/image_1f6clgrt9l511ogektq50t1abv1t.png)
![image_1f6clho9d1a7vurb1fn5368ojk2q.png-142.6kB](http://static.zybuluo.com/Yunabell/jpgvgtpnjjemf15ly9oxzyqt/image_1f6clho9d1a7vurb1fn5368ojk2q.png)
![image_1f6clob8h1qmj1sjrmf21behd7l47.png-42.8kB](http://static.zybuluo.com/Yunabell/ns265emf5rjhxap9rx26qvwv/image_1f6clob8h1qmj1sjrmf21behd7l47.png)

`Example`

![image_1f6clsg1s1jq31ou41tda14131h4v54.png-49kB](http://static.zybuluo.com/Yunabell/4w0yl8vtx0shwat11ykbxbd5/image_1f6clsg1s1jq31ou41tda14131h4v54.png)
![image_1f6cltddjfkko0i12r1110s14iv61.png-56.8kB](http://static.zybuluo.com/Yunabell/3mvcj6vts6rte56itmv2o6bu/image_1f6cltddjfkko0i12r1110s14iv61.png)
![image_1f6cltt4k1efc1sui1aef6jkh4g6e.png-118.5kB](http://static.zybuluo.com/Yunabell/hyov52ch2x84v4dgq6dgxkvs/image_1f6cltt4k1efc1sui1aef6jkh4g6e.png)

#### M |= $\phi$ 的interpreting



![image_1f6cmijss9gf1k1k1vpt1mfaapi6r.png-113.6kB](http://static.zybuluo.com/Yunabell/xyqwlib0f8ddhvaxwtgn1hdq/image_1f6cmijss9gf1k1k1vpt1mfaapi6r.png)
![image_1f6cmnj0i1o3a1teb18r45o5roq78.png-74.6kB](http://static.zybuluo.com/Yunabell/hfvngx1zilwn4fedqzqk91of/image_1f6cmnj0i1o3a1teb18r45o5roq78.png)

`Environment`

![image_1f6cmt7351l5k1rdbojc4ub7ie85.png-88kB](http://static.zybuluo.com/Yunabell/qk4m3s2xndf35t4gmrzmo51c/image_1f6cmt7351l5k1rdbojc4ub7ie85.png)
![image_1f6cmtn9m1hc31gkfc1m1c5q7st92.png-117.2kB](http://static.zybuluo.com/Yunabell/4snv8vs9z4j2tlcwlspxlsk4/image_1f6cmtn9m1hc31gkfc1m1c5q7st92.png)

![image_1f6cnl55713kaki112sigeb1rcv9.png-125.4kB](http://static.zybuluo.com/Yunabell/hswsuf7w1uuird0b0cbt5eh3/image_1f6cnl55713kaki112sigeb1rcv9.png)

**Sentence :**
:   A formula φ is a **sentence** if φ **does not have free variables**.


![image_1f6cnrnl69io13jkfmh14bcn0t16.png-36.4kB](http://static.zybuluo.com/Yunabell/704lc3l08luwp0r5s3kot23f/image_1f6cnrnl69io13jkfmh14bcn0t16.png)

---

### Translation into Predicate Logic

- Translate simple sentences from natural language to predicate logic and back

![image_1f6crtm6bsir53cret1ro1n8l5e.png-123.4kB](http://static.zybuluo.com/Yunabell/h3pn7b8g3x0qf2obvqta9wgm/image_1f6crtm6bsir53cret1ro1n8l5e.png)

![image_1f6cslcn26jaqajgasmk210em6b.png-60.6kB](http://static.zybuluo.com/Yunabell/o5rxpnor8z92832upda9rhdp/image_1f6cslcn26jaqajgasmk210em6b.png)

![image_1f6csnm0r15u878skuah6e1usg6o.png-109.9kB](http://static.zybuluo.com/Yunabell/y9yq6chcs236519791oxdscw/image_1f6csnm0r15u878skuah6e1usg6o.png)
![image_1f6csstnp10b053upds93bvn7i.png-69.9kB](http://static.zybuluo.com/Yunabell/8o9hgx0yyat3vnjc0rb1kc2m/image_1f6csstnp10b053upds93bvn7i.png)

![image_1f6ct1q0u3vqj121o1navo9d7v.png-69.1kB](http://static.zybuluo.com/Yunabell/ub0y526nyjbl8euv3q9jwmvp/image_1f6ct1q0u3vqj121o1navo9d7v.png)


---

### Model Cardinality

- Express model properties like "at least," "at most," "exactly" using predicate logic with =

**Exercise 6 最后一题**

![image_1f6d50hotgg7rt1le57ea835gj.png-81.5kB](http://static.zybuluo.com/Yunabell/lgk7p7g9lr5fbm14tadtxrcc/image_1f6d50hotgg7rt1le57ea835gj.png)


### Order Relations

- Understand the important first order theories of partial orders and total orders

#### Partial Order

> To distinguish an ordinary partial order from a strict one, an ordinary partial order is sometimes called a **weak partial order**.

![image_1f6akragpuo61km7ou81ifc1ba81g.png-36.8kB](http://static.zybuluo.com/Yunabell/svmrb3nngptqw1t7h21fkyar/image_1f6akragpuo61km7ou81ifc1ba81g.png)

#### Total Order

![image_1f6akshtglh360j18etcl164d1t.png-22.2kB](http://static.zybuluo.com/Yunabell/a11drlqb6fz3v21ofiyfnoaj/image_1f6akshtglh360j18etcl164d1t.png)

#### Strict Partial Order

![image_1f6aktsl21oibikv3o24r41c8p2a.png-27.7kB](http://static.zybuluo.com/Yunabell/yexra1mvwkww6rq9nheldq3y/image_1f6aktsl21oibikv3o24r41c8p2a.png)

#### Strict Total Order

![image_1f6akupou14p6mq1vh79fnpjs2n.png-21.6kB](http://static.zybuluo.com/Yunabell/kba64ajahd1g68yyn3lx44iz/image_1f6akupou14p6mq1vh79fnpjs2n.png)

![image_1f6al1b7kngahbk1s14o81djv34.png-37.4kB](http://static.zybuluo.com/Yunabell/xtuqmawjpxhivaasblmmhd8g/image_1f6al1b7kngahbk1s14o81djv34.png)

#### Minimum and Minimal

**Minimum:**
:   Say an element y is minimum for a partial order if it is less than or equal to any other element, that is, if it takes the place of 0 in the first statement.

**Minimal:**
:   Say that an element y is minimal for a partial order if no element is less than it, that is, if it takes the place of 0 in the second statement.

![image_1f6al566h9jh192q12tdvsc10o33h.png-52.3kB](http://static.zybuluo.com/Yunabell/bi6uidjwdnfbmt7tqd5520vw/image_1f6al566h9jh192q12tdvsc10o33h.png)

#### Equivalence and Equality

![image_1f6al7tat1djn9qd8q9ahe1fbo3u.png-45.2kB](http://static.zybuluo.com/Yunabell/dbtkutoqdzojwzspvee7ulhy/image_1f6al7tat1djn9qd8q9ahe1fbo3u.png)

### Consistency and Soundness (First Order Logic)
- Understand, be able to reason with, and apply the concepts:
    - Satisfiability, contradiction, validity (tautology) of formulas
    - Semantic entailment |=
    - Logical equivalence ≡
    - Consistency and inconsistency of sets of formulas
    - Soundness and completeness (you don't need to know the proofs of these theorems)

![image_1f6crl43mg3s17sl1a1g1lnk12ca51.png-102.3kB](http://static.zybuluo.com/Yunabell/25o2u3t718sh9h5q19lq85wm/image_1f6crl43mg3s17sl1a1g1lnk12ca51.png)

Consistency:
:    A set of sentences is said to be consistent if you cannot prove a contradiction from those hypotheses.

> **Theorem**. Every consistent set of sentences has a model.

---

### Semantic Entailment |=

![image_1f6co147q1kbvau81eci1upk18ei1j.png-101kB](http://static.zybuluo.com/Yunabell/lgkgz6awaiqumsow3xuptrjk/image_1f6co147q1kbvau81eci1upk18ei1j.png)
![image_1f6co3jvh10561qhe17cl1un0vg720.png-47.4kB](http://static.zybuluo.com/Yunabell/7rxpddp6xno9kwbvn8bp3vjh/image_1f6co3jvh10561qhe17cl1un0vg720.png)

#### Prove Semantic Entailment

![image_1f6co4q99pngde01d6hb841pv42d.png-93.9kB](http://static.zybuluo.com/Yunabell/sb6ap7c8gcndrzzf2cs0prxh/image_1f6co4q99pngde01d6hb841pv42d.png)
![image_1f6co63lo1ne1mm213mbf501t082q.png-79.5kB](http://static.zybuluo.com/Yunabell/kcp8vhtcbok4hzbcenu72tvd/image_1f6co63lo1ne1mm213mbf501t082q.png)


---

### Logical Equivalence

![image_1f6codd9r1i9k1bevbcq1p0114b73n.png-65.1kB](http://static.zybuluo.com/Yunabell/n9chnjjo2yo565vfs72fclsx/image_1f6codd9r1i9k1bevbcq1p0114b73n.png)
![image-20210824211814019](http://yunabell-image-repository.oss-cn-shanghai.aliyuncs.com/img/image-20210824211814019.png)


---

## Modal logic

### Kripke Models

- Understand the concepts of Kripke models and frames

![image_1f6cvuc5ffod9b98751ilg11op8c.png-65.5kB](http://static.zybuluo.com/Yunabell/komeckp2pje7c5r01osiczii/image_1f6cvuc5ffod9b98751ilg11op8c.png)

- Come up with Kripke models and counter models for formulas

#### Definition of Truth in Worlds

- Be able to evaluate the truth of a formula in (a world of) a Kripke model

![image_1f6d37ahh1191k2q13dp1m061ovu8p.png-45.1kB](http://static.zybuluo.com/Yunabell/1bmg7ha87ibw32zu0mobpxvv/image_1f6d37ahh1191k2q13dp1m061ovu8p.png)

![image_1f6d38jk714nsqeh35c15o4hd196.png-71.6kB](http://static.zybuluo.com/Yunabell/0s7hvmzuet52xlyvunhng9sb/image_1f6d38jk714nsqeh35c15o4hd196.png)

![image_1f6d39vj0sdi1euu1kop1fjc1mn89j.png-28.7kB](http://static.zybuluo.com/Yunabell/h126epb2vjweaif7qcqwgwgz/image_1f6d39vj0sdi1euu1kop1fjc1mn89j.png)

![image_1f6d3bvl61v4s12ck1mon14tq1m4va0.png-27.1kB](http://static.zybuluo.com/Yunabell/kmkuo4nrqqi80onw9za7bq3r/image_1f6d3bvl61v4s12ck1mon14tq1m4va0.png)

![image_1f6d3dktk1jci1724f1jgam19s4ad.png-11.9kB](http://static.zybuluo.com/Yunabell/opjvnttr2p0p1v2u36wkb8xj/image_1f6d3dktk1jci1724f1jgam19s4ad.png)

- Understand the concepts of validitity of formulas, semantic entailment, and logical equivalence
- Formulas and frame properties:
    - Understand important properties of relations/frames: reflexive, symmetric, transitive
    - Understand correspondence of formulas with properties of frames
    - Know the correspondences covered in lecture
    - Be able to prove correspondences

#### Kripke Logic Equivalence

![image_1f6d3ipjt1mk91hpe1b2gpsq1jsjaq.png-59.8kB](http://static.zybuluo.com/Yunabell/x6jyk03cbezv8gwpnw3r0bg9/image_1f6d3ipjt1mk91hpe1b2gpsq1jsjaq.png)

#### Kripke Models Frame

![image_1f6d3mdh0dg1nfkndr1qun104ob7.png-78.6kB](http://static.zybuluo.com/Yunabell/nzufid19wxzvybzojw79sw1h/image_1f6d3mdh0dg1nfkndr1qun104ob7.png)


![image_1f6d3ofu3199gn9tcgm18or11b0bk.png-47.9kB](http://static.zybuluo.com/Yunabell/x9km1n7vy2dyw7u3bgktv7tv/image_1f6d3ofu3199gn9tcgm18or11b0bk.png)

#### Properties of Frame

![image_1f6d3qgni97thr51701ogiel7c1.png-88.4kB](http://static.zybuluo.com/Yunabell/43rj0dqv2gw1mt1h1ajcqwsl/image_1f6d3qgni97thr51701ogiel7c1.png)

`Correspondence of Formulas and Frame Properties`

![image_1f6d3tqso1fd6jc7rhfhs6vf4ce.png-86.1kB](http://static.zybuluo.com/Yunabell/zxtwkcu69xu4i5uwwxo9d6mt/image_1f6d3tqso1fd6jc7rhfhs6vf4ce.png)
![image_1f6d3uvoc22o1hu51vau3u7tpncr.png-74.6kB](http://static.zybuluo.com/Yunabell/8e1xihg1zld6km6zytm9c4ie/image_1f6d3uvoc22o1hu51vau3u7tpncr.png)


---

## Meta-theorems of first order logic

### Meta-theorems of Predicate Logic 

- Know the formulations of and understand the soudness and completeness, consistency, compactness theorems. (You don't need to know the proofs.)

`Soundness & Completeness`
![image_1f6d47ivfcn21hh91c0a1n9td8id8.png-111.6kB](http://static.zybuluo.com/Yunabell/v3w8kdqgg23v359eop83box1/image_1f6d47ivfcn21hh91c0a1n9td8id8.png)

`Consistency and Syntactical Consistency`
![image_1f6d4e779ok15mh3n81nfm1rhqdl.png-94kB](http://static.zybuluo.com/Yunabell/edwqxov0fpayckiu2actoeny/image_1f6d4e779ok15mh3n81nfm1rhqdl.png)

![image_1f6d4hq2b1cht18jc1ieu1p401b7mei.png-59.6kB](http://static.zybuluo.com/Yunabell/oosmq62japnzc7qy7rmto4qm/image_1f6d4hq2b1cht18jc1ieu1p401b7mei.png)
![image_1f6d4inh73ju1r5kdu2gjrghhev.png-27kB](http://static.zybuluo.com/Yunabell/x15yxgh6g3vrfjb1e0k9jrws/image_1f6d4inh73ju1r5kdu2gjrghhev.png)

`Compactness`
![image_1f6d4mus011eh1p3do0j1vrfv4dfc.png-85.5kB](http://static.zybuluo.com/Yunabell/mbsem63v5d6hqi46xt3v7h8j/image_1f6d4mus011eh1p3do0j1vrfv4dfc.png)
![image_1f6d4o6jodi9jpb6un1lh912djfp.png-125.7kB](http://static.zybuluo.com/Yunabell/wj0uir0n798ihhrs3hqlpoax/image_1f6d4o6jodi9jpb6un1lh912djfp.png)

- Know the definition of a decision problem, decidability, and undecidability, and be able to give examples

---

### Definability and Undefinability

![image_1f6eungcf13r8at3ubu1d1419qi9.png-59.7kB](http://static.zybuluo.com/Yunabell/p2qptl9j5tcqae1osolla8g9/image_1f6eungcf13r8at3ubu1d1419qi9.png)


#### Definable Frame Properties in Predicate Logic and Modal Logic

![image_1f6d4uo4q149lf5a1d7u1421eh6g6.png-86.5kB](http://static.zybuluo.com/Yunabell/nr7l1etvof40a4o5aqwld4ru/image_1f6d4uo4q149lf5a1d7u1421eh6g6.png)


- Undecidability theorems for validity, provability of formulas in first order logic: know the formulations and be able to apply them in easy situations

---

#### Reachable

![image_1f6d5oqt81hbn1ei71sa2c09n1uh0.png-104.6kB](http://static.zybuluo.com/Yunabell/s5vlvs0pq6e51nrxcejmlcde/image_1f6d5oqt81hbn1ei71sa2c09n1uh0.png)
![image_1f6d5t52sqn6541cmn1a061p4fhd.png-104.5kB](http://static.zybuluo.com/Yunabell/9h5s9fuarc43nkozl30wmu67/image_1f6d5t52sqn6541cmn1a061p4fhd.png)

---

### Decision Problems

#### Decidable

![image_1f6d66qv7bf1ocrnpp16qn1qg1in.png-112.3kB](http://static.zybuluo.com/Yunabell/wo0k2x3w6b5otpef7tsph9bo/image_1f6d66qv7bf1ocrnpp16qn1qg1in.png)

![image_1f6d683kgu0lm9r16j3108m19fdj4.png-75.6kB](http://static.zybuluo.com/Yunabell/unp8qcb1nmss4di4rdyo3ic9/image_1f6d683kgu0lm9r16j3108m19fdj4.png)

