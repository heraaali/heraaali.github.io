+++
categories = ["math monday"]
date = "2020-07-06"
description = ""
title = "Math Monday: Introducing A Visual Proof"
type = "post"
katex = true
markup = "mmark"
+++

In mathematics, a proof is an argument to convince the reader that something holds true in all conditions, beyond any doubt. There are more examples of artful proofs than I could possibly document, so I chose a visual proof that should be easy to grasp. Let's prove the following:

$$\sum_{n=1}^\infty\frac{1}{2^n} = 1$$

A refresher on summations: $$\sum_{n=1}^\infty\frac{1}{2^n}$$ is a shorthand way to describe adding the terms, where, starting from n=1, $$\frac{1}{2^1} + \frac{1}{2^2} + \frac{1}{2^3} + ... $$ theoretically for an infinite amount of terms.

But there is no way for us to actually write out the "sum from 1 to infinity".  What we are really asking is "what value (if any) does the sum approach as we add more and more terms?"

As _n_ gets closer to infinity, this sum **converges** (adds up) to 1. But don't take my word for it! The picture below also demonstrates this. 

![proof](/proof.png)

Say this triangle started out white. Take 1/2 of the triangle and color it red. Then, take half of the resulting triangle $$(1/2 * 1/2 = 1/4)$$ and color that red. Then take half of THAT triangle $$(1/2 * 1/2 * 1/2 = 1/8)$$ and continue coloring it red. And so on and so on and so on until there is a point where there is no more whitespace and the entire triangle is red, meaning the amount of white space is 0 and the amount of red is 1.


Congrats! You've just proved the original statement: that the summation tends to 1.


**Disclaimer**: while visual proofs can be a powerful tool, there are plenty of visually deceptive "proofs" out there. Take the following incorrect cancellation:

$$\frac{64}{16} = \frac{\cancel{6}4}{1\cancel{6}} = 4$$

Clearly, this is not mathematically sound, despite the fact that the answer is correct. An illogical proof _can_ get you to the right answer -- but this method of division does not hold true for every case, which is the requirement for a proof. A **counterexample** is a specific case which shows that a general statement is false. Here's the counterexample to this illogical method of division:

$$\frac{60}{6} = \frac{\cancel{6}0}{\cancel{6}} \neq 0$$

And there is a quick demonstration of the power of a visual proof!