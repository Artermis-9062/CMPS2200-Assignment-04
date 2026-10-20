# CMPS 2200 Assignment 4

## Answers

**Name:** Chuong Hoang Pham

---

Place all written answers from `assignment-04.md` here for easier grading.

**1 Quicksort probabilities**

- **1a. (5 pts)** What is the probability that Quicksort does $\Omega({n^2})$
  comparisons?

Let $X$ be a random variable for the number of comparisons `Quicksort` performs, with $\mathbb{E}[X] = c \cdot n \lg n = O(n \lg n)$.

The event that Quicksort does $\Omega(n^2)$ comparisons means $X \geq k \cdot n^2$ for some constant $k > 0$. Set $\alpha = k n^2$. By Markov's inequality:

$$
\mathbb{P}[X \geq k n^2] \leq \frac{c \cdot n \lg n}{k \cdot n^2} = \frac{c}{k} \cdot \frac{\lg n}{n} = O\left(\frac{\lg n}{n}\right)
$$

So the probability that Quicksort performs $\Omega(n^2)$ comparisons is at most $O(\lg n / n)$.

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

$\mathcal{A}'(\mathcal{I}, \delta)$ runs $\mathcal{A}$ on $\mathcal{I}$ repeatedly and verifies each output with $\mathcal{C}$ until one passes, returning the first correct output; if none of the $k$ attempts succeed, it reports failure. Each attempt costs $O(w(n) + v(n)) = O(w(n))$ work since $v(n) \in O(w(n))$.

We want $\mathcal{A}'$ to succeed with probability at least $\delta$, so we need $k$ attempts such that
$$1 - (1-\epsilon)^k \ge \delta \Rightarrow k \cdot \ln(1-\epsilon) \le \ln(1-\delta)$$
This gives us $k \ge \frac{\ln(1-\delta)}{\ln(1-\epsilon)}$ (since $\ln(1-\epsilon) < 0$).

So the work of $\mathcal{A}'$ with success probability $\delta$ is:
$$W(n) = \frac{\ln(1-\delta)}{\ln(1-\epsilon)} \cdot O(w(n))$$

- **2b. (6 pts)** Show how to convert $\mathcal{A}$ into an
  algorithm that always produces the correct result, but has an
  expected runtime that depends on $w(n)$ and a success probability $\epsilon$.

Run $\mathcal{A}$ on $\mathcal{I}$ repeatedly, verifying each output with $\mathcal{C}$, and return the first output that passes verification. Since $\mathcal{C}$ is deterministic and always correct, this algorithm always returns the correct result — it never returns an incorrect output; it only keeps trying until $\mathcal{A}$ succeeds.

Let $T$ be the random variable for the number of trials until the first successful run of $\mathcal{A}$. Since each run succeeds independently with probability $\epsilon$, $T$ follows a geometric distribution with parameter $\epsilon$, so $\mathbb{E}[T] = 1/\epsilon$.

Each trial costs $O(w(n) + v(n)) = O(w(n))$ work (run $\mathcal{A}$ then verify with $\mathcal{C}$). Therefore the expected total work is:

$$\mathbb{E}[W] = \mathbb{E}[T] \cdot O(w(n)) = \frac{1}{\epsilon} \cdot O(w(n)) = O\left(\frac{w(n)}{\epsilon}\right)$$

**3 Determinism versus Randomization in Quicksort**

- **3b. (8 pts)** Compare running times using `compare-qsort` between variants of
  Quicksort and the provided implementation of selection sort (`ssort`).

- **3c. (8 pts)** Compare the fastest of your sorting implementations to the Python sorting function `sorted`, conducting the tests in 3b above.
