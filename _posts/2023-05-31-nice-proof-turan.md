---
title: My (new) favourite proof of Turán's theorem
author: Xiangxiang Michael Zheng
layout: post
---

Hey, life's been mostly good. **Anyway**, let's talk about math. 

Actually, talking about good things that are math-related, there was a joint seminar today between the graph theory groups (yes, plural since extremal have their own research seminar for some reason) of the University of Hamburg and the discrete math group from the TUHH. The talk was given by Dhruv Mubayi on ''Ramsey theory constructions from hypergraph matchings''. I mean, not that surprising given that 
Mubayi is an expert on the field, but the talk was really enjoyable, full of surprises really, including the following: 

- Connections from Roth's Theorem (my preparatory project topic) to hypergraph and design stuff. 
- Axenovich was mentioned twice or three times which we made me kinda proud. 
- The Theorem by Frankl and Rödl on Hypergraph coverings (proved using the Nibble method), which we actually saw in class last week, was one of the fundamental tools today. 

Yeah, so really enjoyable. *Anyway*, one other thing I am excited about is the ''Summer of Math Exposition 3'' (SoME3) this year. 
I suggested to my friend some fundamental theorems in graph theorems, one of which I kinda hiddenly found on the SoME3 Discord server: 

"Consider the following graph $G = (V,E)$. Assing probabilities $p_i$ to each vertex $i$ such that each $p_i \geq 0$ and $\sum_{i \in V} p_i = 1$. We wish to maximize $\sum_{ij \in E} p_i p_j$. What is the maximum value, and what probability distribution achieves it?" <cite>— Akiva on Discord</cite>

It was given as a *challenge problem* (because nerds will be nerds) with a graph that, for the discussion here, isn't really important. 

Instead, I want to sketch a way how you may solve this problem. First, it is good to have in mind, what the problem *means*. Akiva gives a fairly straight-forward interpretation: "I will choose two vertices independently at random according to your probability distribution. You win if those vertices are distinct and joined by an edge. I win if the vertices are either equal, or are distinct and not joined by an edge. How do you maximize your chance of winning?" 

Technically, the probability of you winning is the sum with an extra factor of 2, but that doesn't matter. 

Anyway, the first thing to try is maybe calculate the optimal distribution for *simpler* graphs. And what's simpler than a clique? 
Here we get the following: 

$$\text{For $K_n$, the optimal distribution is the uniform one, i.e. where every vertex has probability $1/n$.}$$

