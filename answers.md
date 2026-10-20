# CMPS 2200 Assignment 4

## Answers

**Name:** Chuong Hoang Pham

---

Place all written answers from `assignment-04.md` here for easier grading.

**1 Quicksort probabilities**

- **1a. (5 pts)** What is the probability that Quicksort does $\Omega({n^2})$
  comparisons?

Consider $X$ is a random variable such that $X$ is the total comparisons executed by `Quicksort`.

Then, $\mathbb{E} [X] = c_1 \cdot n \log n \in O(n \log n ) $.

Therefore,

$$
P[X \ge n^2] \le \frac{c_1 n \log n}{c_2 \cdot n^2} = \frac{c_2 \log n}{n} \\[8pt]
\Rightarrow P[X = \Omega(n^2)] \le \frac{c_1}{c_2} \frac{\log n}{n} = O(\frac{\log n}{n})
$$

- **1b. (5 pts)** What is the probability that Quicksort does $10^c n \lg n$
  comparisons, for a given $c>0$? What does this say about the
  deviation of the actual work from the expected work for Quicksort?

Let $X$ be a random variable for the number of comparisons Quicksort performs, with $\mathbb{E}[X] = c_1 \cdot n \lg n = O(n \lg n)$. Set $\alpha = 10^c \cdot n \lg n$. By Markov's inequality:

$$
\mathbb{P}[X \geq 10^c n \lg n] \leq \frac{c_1 n \lg n}{10^c n \lg n} = \frac{c_1}{10^c} = O(10^{-c})
$$

So the probability that Quicksort performs $10^c n \lg n$ comparisons is at most $O(10^{-c})$. This means the actual work deviates from the expected work by a factor of $10^c$ with exponentially small probability in $c$ — large deviations from $O(n \lg n)$ are very unlikely, and with high probability Quicksort's work stays close to its expectation.

**2 From "Maybe" to "Definitely"**

- **2a. (10 pts)** Give an algorithm to improve the guaranteed success probability and state its work.

- **2b. (6 pts)** Show how to convert $\mathcal{A}$ into an
  algorithm that always produces the correct result, but has an
  expected runtime that depends on $w(n)$ and a success probability
  $\epsilon$.

**3 Determinism versus Randomization in Quicksort**

- **3b. (8 pts)** Compare running times using `compare-qsort` between variants of
  Quicksort and the provided implementation of selection sort (`ssort`).

- **3c. (8 pts)** Compare the fastest of your sorting implementations to the Python sorting function `sorted`, conducting the tests in 3b above.
