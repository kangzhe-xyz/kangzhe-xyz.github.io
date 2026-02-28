---
date: '2026-03-01T05:16:36+08:00'
draft: false
title: 'Project Dummit and Futon'
---
I have been working on giving my hand at translating Dummit and Foote's *Abstract Algebra* (Third Edition) into Japanese, though rather irregularly. 
In particular, I am trying to translate the second part of the book: on rings and modules.

I have named this project *Project Dummit and Futon*, since "Foote" and "futon" sounded pretty close.

Some examples I did not pay attention to too closely while studying ring theory during the semester were revisited again (because I was forced to read them). 
None of them were particularly exciting.
What my focus was for this project is actually learning how to write mathematics in Japanese.

Since this is me going in blind into translation, with my best sources being other Japanese mathematics textbooks and mimicking them, I highly appreciate any feedback.

In Chapter 7.1 Example (6), the book talks about rings of functions. 
If $X$ is a nonempty set and $A$ is any ring, define the ring of functions  
$$ 
R \coloneqq \\{ f \colon X \to A \mid f \text{ is a function}\\} 
$$
under the operations of pointwise addition and pointwise multiplication
$$
(f+g)(x) = f(x) + g(x), \quad (f \cdot g)(x) = f(x) \cdot g(x).
$$
This example shows how $f$ can transfer the ring properties from $A$ to $R$ due to the structure imposed by the addition and multiplication operations.
My initial attempt at translating it into Japanese is as follows:

> ### 例7.1 (6)
>
> 関数の環を考えれば重要な環の類を得られる．
> $X$ を不空集合として$A$を任意の環をしておく．
>（集合の）関数の全体集合$R$は普通の加法と乗法 $(f+g)(x) = f(x) + g(x)$ と $(fg)(x) = f(x)g(x)$ とともに環になる．
> $R$ が環の条件ごとを満たすことは $A$ の環性からしたがってくる．
> 環 $R$ は単位元が含む可換環であることと $A$ が単位元が含む可換環であることは同値である．
> また，$R$ が単位元を存在することと $A$ が単位元を存在することは同値である（その際，$R$ の $1$ は必ず恒等的に $1$ をとる関数である）．
> 
> $X$ と $A$ にもっと構造が備わっている場合，そういう構造を即する環を作れる．
> 例えば，$A$ は実数の全体集合$\R$で$X$は閉区間 $[0,1]$ であれば，$[0,1]$ から $X$ へのすべての連続関数の環を出来上がる（ここで連続関数の和と積は連結であることを保証するために極限についての基本的な定理が必要）．
> これは単位元が含む可換環である．

My instincts were to send it into ChatGPT for feedback, asking whether the writing was acceptable.
There are some patterns that it suggested, which I will write here as notes for myself.

---

The original text says 
> one important class of rings

which I translated as 
> 重要な環の類

but 「類」 used here is supposedly unnatural, and it was a better choice to have just written 「クラス」 instead.

Also, the tone was not academic enough using the conditional form 「考えれば」. The correct phrase to use was 「考えることで」. After some searching around, I found [this online guide](https://www7a.biglobe.ne.jp/~nifongo/ron/rasii.html), which is a style guide for writing essays or texts in an academic context. 
I will probably read this at some point later on.

The corrected form of the sentence with these suggestions should then be 
> 関数の環を考えることで，重要な環のクラスが得られる．

---

Writing "it follows that ..." is a very common structure, and my initial attempt at writing 
> Each ring axiom for $R$ follows directly from the corresponding axiom for $A$

as
> $R$が環の条件ごとを満たすことは$A$の環性からしたがってくる．

My word choices here were pretty naive, with follows translated directly as 「従ってくる」, and without knowing how to succinctly describe "each ring axiom for $R$," I went for the very clunky phrasing 「$R$が環の条件ごとを満たすこと」, which literally translates to "every condition of rings that has been fulfilled by $R$." — not an inaccurate translation, but I thought it could definitely be less clunky.

It turns out that I could have just used the word 「公理」 for axiom, and there was no need for the 「～くる」 that follows after 「従う」.
Thus the corrected version would be something like 
> $R$が環の公理を満たすことは，$A$が環であることから従う

which is much easier to read.

---

It is also important to write that a set $R$ contains an element $1$.
Here, I used the word 「含む」, which roughly translates to "included."
However, there is a standard way to write that something is contained within a set.
The verb would actually be 「持つ」，or rather, 「もつ」, written in the kana form.
The most naive translation for this word is to "hold," but it can also be used in the sense of "I hold a driver's license." 

The original sentence 
> The ring $R$ is commutative if and only if $A$ is commutative and $R$ has a $1$ if and only if $A$ has a $1$

was originally translated as
> 環 $R$ は可換環であることと $A$ が単位元が含む可換環であることは同値である．

With this piece of feedback however, and some rewriting, I arrived at
> $R$ が $1$ をもつ可換環であることと，$A$ が $1$ をもつ可換環であることは同値である．

I changed 「単位元」 to $1$ to match the original text.

(I was glad that I translated "iff" correctly as 「同値である」.)

---

Admittedly, I am not sure if I will be able to finish this project, since the book is rather thick and I am quite busy these days. 
Nonetheless, I was still rather intrigued by this personal project and I might explore doing translation work in the future (LLMs being able to do this well, considering that I am using one for feedback, is a whole other conversation). 
Of course, a long way to go, but I think it will be rather exciting.