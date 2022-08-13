---
title: Information from randomness
author: tqian
date: 2022-07-08 12:00:00 +0800
categories: [Puzzles]
tags: [probability, math]
math: true
mermaid: true
---

My friend [Maxwell](https://github.com/mzhang2021) introduced me to a puzzle that I found interesting but also very confusing. The official source is [here](https://www.quantamagazine.org/solution-information-from-randomness-20150722/), but I'll restate it here. 
>"I write down two different numbers that are completely unknown to you, and hold one in my left hand and one in my right. You have absolutely no idea how I generated these two numbers. Which is larger? You can point to one of my hands, and I will show you the number in it. Then you can decide to either select the number you have seen or switch to the number you have not seen, held in the other hand, as your final choice. Is there a strategy that will give you a greater than 50 percent chance of choosing the larger number, no matter which two numbers I write down?"

The official solution is to consider a random variable $G$ that is uniformly sampled from the reals. Let's say we randomly with probability $\frac 12$ for each hand reveal a number to be $C$. If $C < G$, then we swap, otherwise, we do not swap. We now analyze the probability of success for this strategy.  Now let's let the two numbers be $A < B$ WLOG. If $G \in (A, B)$, then our strategy succeeds no matter what. Otherwise, our strategy has a $\frac 12$ chance of success. So since we always have at least a $\frac 12$ chance of success, and since $G$ is uniformly random and always has a nonzero probability of being in  $(A, B)$, our overall chance of success is always at least $\frac 12$. We seemingly have used an arbitrary random variable to gain information. Where did the information come from?

The main issue is that the solution is a little misleading. Our assumption is that there's a nonzero probability that $G$ will lie in $(A, B)$. Let's analyze this assumption. An even looser assumption is that there exists some random variable that has a nonzero probability of being in $(A, B)$, and we look at this assumption. Denote this random variable $X$. Let's denote this probability of being in the range $(A, B)$ to be $p > 0$. Now the solution given above glosses over infinitesimal probabilities, which is a pretty bad error. This is like saying an event happening [almost surely](https://en.wikipedia.org/wiki/Almost_surely) and an event happening with probability $1$ are different. So to be concrete, we must be able to assume $p$ is a positive constant. 

Now let's analyze this random variable $X$, what information does it give us? We can view it as an oracle that with probability $p$ will give us a number in the range $(A, B)$, and with probability $1 - p$ give us no information at all. In the former case, this is equivalent to the oracle straight up telling us the answer as we've shown above. In the latter case, the oracle says nothing. So our assumption is equivalent to being given an oracle that with probability $p$ just tells you the answer. So evidently we can beat a $\frac 12$ chance of winning given this oracle, since we can always win with probability $\frac 12$ just by our first random selection of the hand. 

The reason why this was confusing was that the problem was phrased **without** telling us the assumption beforehand. Then they gave us the solution while giving the assumption without any justification or proof. Phrasing the assumption in the form of the oracle interpretation makes it clear why the assumption is very nontrivial, and I do not see in the article a formal justification why this assumption is valid. Of course, there's always a chance that I also made some logical errors, so please let me know if you find any. :)

These types of information theory/game theory types puzzles are always fun for me to think about. I've linked two others that also give this sort of unintuitive flavor: 

- [Lion and lambs](https://theconversation.com/lions-and-lambs-can-you-solve-this-classic-game-theory-puzzle-81288)
- [Blue eyes](https://theconversation.com/lions-and-lambs-can-you-solve-this-classic-game-theory-puzzle-81288)

