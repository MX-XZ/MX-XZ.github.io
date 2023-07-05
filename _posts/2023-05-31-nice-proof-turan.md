---
title: My (new) favourite proof of Turán's theorem
author: Xiangxiang Michael Zheng
layout: post
---

Hey, life's been mostly good. **Anyway**, let's talk about math. 

Actually, talking about good things that are math-related, there was a joint seminar today between the graph theory groups (yes, plural since extremal have their own research seminar for some reason) of the University of Hamburg and the discrete math group from the TUHH. The talk was given by Dhruv Mubayi on ''Ramsey theory constructions from hypergraph matchings''. I mean, not that surprising given that 
Mubayi is an expert on the field, but the talk was really enjoyable, full of surprises really, including the following: 

- Connections from Roth's Theorem (my preparatory project topic) to hypergraph and design stuff. 
- Axenovich was mentioned twice or three times which made me kinda proud. 
- The Theorem by Frankl and Rödl on Hypergraph coverings (proved using the Nibble method), which we actually saw in class last week, was one of the fundamental tools today. 

Yeah, so really enjoyable. *Anyway*, one other thing I am excited about is the ''Summer of Math Exposition 3'' (SoME3) this year. 
I suggested to my friend some fundamental theorems in graph theorems, one of which I kinda hiddenly found on the SoME3 Discord server: 

"Consider the following graph $G = (V,E)$. Assing probabilities $p_i$ to each vertex $i$ such that each $p_i \geq 0$ and $\sum_{i \in V} p_i = 1$. We wish to maximize $\sum_{ij \in E} p_i p_j$. What is the maximum value, and what probability distribution achieves it?" <cite>— Akiva on Discord</cite>

It was given as a *challenge problem* (because nerds will be nerds) with a graph that, for the discussion here, isn't really important. 

Instead, I want to sketch a way how you may solve this problem. First, it is good to have in mind, what the problem *means*. Akiva gives a fairly straight-forward interpretation: "I will choose two vertices independently at random according to your probability distribution. You win if those vertices are distinct and joined by an edge. I win if the vertices are either equal, or are distinct and not joined by an edge. How do you maximize your chance of winning?" 

Technically, the probability of you winning is the sum with an extra factor of 2, but that doesn't matter. 

Anyway, the first thing to try is maybe calculate the optimal distribution for *simpler* graphs. And what's simpler than a clique? 
Here we get the following: 

**For $K_n$, the optimal distribution is the uniform one, i.e. where every vertex has probability $1/n$.**


We prove the claim by induction on $n \in \mathbb{N}$. For simplicity sake, the vertices of $K_n$ will always be $v_1, \dots, v_n$. If $n = 1$, the claim is trivial. If $n = 2$, we would essentially maximize $p \cdot (1-p)$ under the constraint $p \in [0,1]$, so using calculus one gets that $p \cdot (1-p)$ is maximized if $p = 1/2$:

$$ \left( \frac{\text{d}}{\text{d} p} p \cdot (1-p) = 1 - 2p \overset{!}{=} 0 \implies p = \frac{1}{2} \right) \land \left( \frac{\text{d}^2}{\text{d} p^2} p\cdot (1-p) = -2 < 0 \right).$$

Now, for the induction step $n \rightsquigarrow n+1$, let $0 \leq p \leq 1$ be the probability of $v_{n+1}$, i.e. $\sum_{1 \leq i \leq n} p_i = 1-p$. By splitting the sum into a sum on those edges incident to $v_{n+1}$ and the remaining edges, we get that the sum is equal to 

$$p \cdot (1- p) + \sum_{1 \leq  i < j \leq n} p_i p_j.$$ 

In other words, for the vertices $v_1, \dots, v_n$, we can take the optimal solution for a clique on $n$ vertices! This gives us, by the induction hypothesis, that the sum (under fixed $p$) has maximal value $$p \cdot (1- p) + \binom{n}{2} \left( \frac{1-p}{n}\right)^2=p \cdot (1- p) + \frac{n-1}{2n} (1-p)^2.$$ 

We again employ some basic calculus: 

$$\frac{\text{d}}{\text{d} p} \left( p \cdot (1- p) + \frac{n-1}{2n} (1-p)^2 \right) = 1 - 2p  + \frac{n-1}{n} (1-p) \overset{!}{=} 0 \implies p = \frac{1}{+1}.$$

As we also have 

$$\frac{\text{d}^2}{\text{d} p^2} \left( p \cdot (1- p) + \frac{n-1}{2n} (1-p)^2 \right)  = -2 + \frac{n-1}{n} < 0 ,$$

we see that $p = 1 / (n+1)$ maximizes the sum under all $p$ and thus we get that, again, the uniform distribution is optimal with value 

$$\binom{n+1}{2} \left( \frac{1}{n+1}\right)^2 = \frac{n}{2(n+1)}$$

for $n+1$ vertices. 

Now, here is where I got stuck. I had a conjecture in mind, which turned out to be true, but couldn't see a good argument for why it should hold. I considered next $P_3$ and saw that for all stars any distribution where the center vertex has value $1/2$ is optimal. 

Also, one can generalize Theorem 1 in such a way to show that, essentially, the same is true for complete multipartite graphs: Given $n$ partition classes, as long as each partition class has overall weight $1 /n$, this distribution will be optimal. 

I also imagined that one can probably algorithmically determine it for all cographs via a similar argument (and spoiler, the graph given by Akiva wasn't a cograph). But it's $P_4$ where I really got stuck and then decided to just go to bed. In the next morning, someone ("noahballz") was then able to fully answer the question by basically considering what would happen if we didn't have a clique.

The other fundamental insight is that, morally speaking, the support of the distribution **needs** to be a clique. Formally, let's assume that $p_1, \dots, p_n$ is an optimal distribution for a graph on $n$ vertices such that the "support", i.e. the number of $i$'s such that $p_i \neq 0$, is minimal. Assume that the support doesn't induce a clique, i.e. there are non-adjacent vertices $i$ and $j$ with $p_i , p_j >0$. Let's now imagine increasing one by $x > 0$ and decreasing the other by that same amount. Then, the sum we're trying to minimize is linear. In particular, either the maximum is at one of the endpoints, so our distribution was not optimal, or we may choose one of them to have value $p_i + p_j$ while the other has value zero, and that distribution would give the sum the same value but have a smaller support. Either way, a contradiction!

Hence, we get:

**For every $n$-vertex graph $G$, the maximum is attained by considering an $\omega(G)$-clique in $G$ and considering the uniform distribution on that clique. In particular, the sum has then maximum value $(\omega(G) -1)/(2 \omega(G)).$**

Now, let's just for fun consider a graph $G = (V,E)$ with $\omega(G)$ bounded by $k \in \mathbb{N}$. If $n$ is the number of vertices and $m$ the number of edges and just consider the uniform distribution on all vertices, we get 

$$ \frac{k-1}{2k} \geq \frac{m}{n^2} \implies m \leq \left(1 - \frac{1}{k}\right) \frac{n^2}{2}.$$

In other words, if $G$ is *$K_{k+1}$-free*, it has at most that many edges! Tada, Turán's Theorem! By closer inspection, apart from the density, it seems that one can also argue what the structure of the Turán graph must look like.  

According to Wikipedia, this is known as the <a href="https://www.wikiwand.com/en/Tur%C3%A1n%27s_theorem#Lagrangian" title="Lagrangian method">*Lagrangian method*</a>. I asked Schacht about it and he said that it lead to some discoveries on hypergraphs, but is now mostly considered a dead-end. Sad, especially since this proof of Turán's Theorem may be my favorite. (The proof via the <a href="https://www.wikiwand.com/en/Tur%C3%A1n%27s_theorem#Probabilistic_Method" title="probabilistic method">*probabilistic method*</a> is also good though.)

A good reference for all of this is also *Proofs from THE BOOK* by Aigner and Ziegler.



