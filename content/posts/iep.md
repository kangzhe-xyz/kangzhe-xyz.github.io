---
date: '2026-09-01T21:43:58+08:00'
draft: false
title: 'Inclusion–Exclusion Principle'
---

> This is a repost of a note I wrote two years ago on the inclusion--exclusion principle when I was taking a class on Probability. 

> The en-dash (–) in the title was AI-generated, because I searched for "en-dash" and the first thing that popped out was Google's AI overview. I just copied the symbol from its output.

In this article, the conjunction (intersection) of events is written as $E_1 \cap E_2 = E_1 E_2$.

**Theorem (Inclusion--Exclusion Principle).**
To find the probability of the union of events $E_1, \dots, E_n$, 
$$
\begin{align*}
    P(E_1 \cup E_2 \cup \cdots \cup E_n) &= \sum_{i=1}^n P(E_i) - \sum_{i_1 < i_2} P(E_{i_1} E_{i_2}) + \cdots \\\\
& \quad + (-1)^{r+1} \sum_{i_1 < i_2 < \cdots < i_r} P(E_{i_1} E_{i_2} \cdots E_{i_r}) \\\\
& \quad \quad \\\\
& \quad \quad \quad + \cdots + (-1)^{n+1} P(E_1 E_2 \cdots E_n).
\end{align*}
$$

To tackle a problem using the inclusion--exclusion principle, divide the number of ways to do a task into subtasks that are indexed by a _size parameter_ $k \in \left\\{0, 1, 2, \dots\right\\}$.

## Example 1

> Suppose that each of $N$ men at a party throws his hat into the center of the room.
> The hats are first mixed up, and then each man randomly selects a hat.
> What is the probability that none of the men selects his own hat?

**Idea.** The task is to permute the hats, and the _size parameter_ is whether $k$ men are getting back their own hats.
You do not need to care about the remaining $n - k$.

**Strategy.** Introduce events $E_i$ indexed by the names of the men from 1 to $n$.

What we want is to compute $P(E_1^C E_2^C \cdots E_N^C) = P(\bigcap_{1 \leq i \leq n} E_i^C)$, where $E_i^C$ is the complement of the event $E_i$.
However, this is annoying and difficult to deal with, so we use de Morgan's law to rewrite this as $P\left((\bigcup_{1 \leq i \leq n} E_i)^C\right)$.
The union allows us to make use of the IEP.

### Solution
Denote by $E_i$ for $i = 1, 2, \dots, N$, the event that the $i$th man selects his own hat.
We want to find $P(E_{i_1} \cdots E_{i_k})$, in other words, we want to give out $N - k$ hats to $N - k$ men, so that these $N - k$ men get their own hats back.

The total possible outcomes are $N!$, and permuting $N - k$ men getting their hats has $(N - k)!$ outcomes.
This means that 
$$
P(E_{i_1} \cdots E_{i_k}) = \frac{(N - k)!}{N!}.
$$
Now since there are ${N \choose k}$ terms in $\sum_{i_1 < i_2 < \cdots i_k} P(E_{i_1} \cdots E_{i_n})$, it follows that 
$$
\sum_{i_1 < i_2 < \cdots < i_k} P(E_{i_1} \cdots E_{i_k}) = {N \choose k} \frac{(N - k)!}{N!} = \frac{1}{k!}.
$$
Thus, the probability that none of the men selects his own hat is 
$$
P(E_1^C \cdots E_N^C) = 1 - 1 + \frac{1}{2!} - \frac{1}{3!} + \cdots + \frac{(-1)^N}{N!} = \sum_{i=0}^N \frac{(-1)^i}{i!}.
$$

## Example 2

> Compute the probability that if 10 married couples are seated at random at a round table, then no wife sits next to her husband.

### Solution
Since there are 20 people in total, there are a total of $(20 - 1)! = 19!$ possible seating arrangements.

Now let $E_i$ denote the event where the $i$th couple sits together, where $1 \leq i \leq 10$.
We now want to find $P(E_{i_1} \cdots E_{i_k})$ for any $k \leq 10$.

Since there are now $k$ couples, there are $20 - 2k$ people left to arrange around the table.
This makes it $20 - 2k + k$ groups to be arranged around a table, which is equal to $2^k (20 - k - 1)!$ possible seating arrangements; the $2^k$ term is there because there are $k$ couples and there are two ways each couple can be seated.

We see that there are ${10 \choose k}$ terms in $\sum_{i_1 < i_2 < \cdots < i_k} P(E_{i_1} \cdots E_{i_k})$. 
Therefore,
$$
\sum_{i_1 < i_2 < \cdots < i_k} P(E_{i_1} \cdots E_{i_k}) = {10 \choose k} \frac{2^k (20 - n - 1)!}{19!}.
$$
Then to answer the question,
$$
P(E_1^C \cdots E_{10}^C) = P\left( (E_1 \cup \cdots \cup E_{10})^C\right)
$$ 
by De Morgan's law.
It follows that 
$$
\begin{align*}
1 - \Bigg(&{10 \choose 1}\frac{2(20 - 1 - 1)!}{19!} \\\\
&- {10 \choose 2}\frac{2^2(20 - 2 - 1)!}{19!} \\\\
&+ {10 \choose 3}\frac{2^3(20 - 3 - 1)!}{19!} - \cdots \Bigg)
\end{align*}
$$
which we can evaluate with a calculator.

Writing a simple piece of Python code 

```Python
from math import comb, factorial

def summand(k):
    return ((-1)**k) * comb(10, k) * (2 ** k) * factorial(19 - k) 
    / factorial(19)

sum = 0
for k in range(0, 11):
    sum += summand(k)

print(sum)
```

gives us around 0.3395.
