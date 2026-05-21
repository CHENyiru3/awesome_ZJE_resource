---
name: ads2-probability-bayes-markov
description: Use this skill for ADS/ADS2 conditional probability, Bayes theorem, Bayes factors, prior/posterior reasoning, logic-card implication tasks, probability trees, lie-detector/base-rate problems, turtle/beach problems, and Markov-chain simulation. Trigger on Bayes, posterior, prior, conditional probability, Bayes factor, Markov chain, probability tree, lie detector, turtle, or card hypothesis.
---

# ADS2 Probability, Bayes, And Markov Chains

Define events before calculating. Most errors come from confusing `P(A|B)` with `P(B|A)`.

## Conditional Probability

```text
H = hypothesis/event of interest
D = observed data/evidence
P(H|D) = probability of H given D
P(D|H) = probability of observing D if H is true
```

## Bayes Theorem

```text
P(H|D) = P(D|H) P(H) / P(D)
```

For two exhaustive hypotheses:

```text
P(H1|D) = P(D|H1)P(H1) / (P(D|H1)P(H1) + P(D|H2)P(H2))
```

State assumptions about priors.

## Turtles Template

```r
p_west <- 0.5
p_east <- 0.5
p_logger_given_west <- 0.1
p_logger_given_east <- 0.4

p_east_given_logger <- (p_logger_given_east * p_east) /
  (p_logger_given_west * p_west + p_logger_given_east * p_east)
p_east_given_logger
```

Report:

```text
Assuming the ecologist was equally likely to reach either beach and there are no other beaches, the probability of being on East Beach after observing a Loggerhead turtle is 0.80.
```

## Bayes Factor

```text
posterior odds = Bayes factor * prior odds
Bayes factor = P(D|H1) / P(D|H2)
prior odds = P(H1) / P(H2)
```

Use Bayes factor when comparing two hypotheses without needing `P(D)`.

## Logic Card Problems

For implication `A -> B`, only `A and not B` falsifies the hypothesis.

Example: "Every vowel has an even number on the back."

Turn over:

- the vowel card, to check for an odd number;
- the odd-number card, to check for a vowel.

Do not need to turn over consonant or even-number cards.

## Markov Chain Concepts

A Markov chain has:

- states;
- transition probabilities between states;
- outgoing probabilities from each state summing to 1;
- next state depending only on current state.

Exam tasks usually ask to draw states/transitions or simulate hitting time.

## Markov Simulation Skeleton

```r
set.seed(123)

one_run <- function(pattern = c(1, 0, 0, 1)) {
  coin <- rbinom(length(pattern), 1, 0.5)
  pointer <- 1
  while (TRUE) {
    window <- coin[pointer:(pointer + length(pattern) - 1)]
    if (all(window == pattern)) break
    pointer <- pointer + 1
    coin <- c(coin, rbinom(1, 1, 0.5))
  }
  length(coin)
}

times <- replicate(5000, one_run())
mean(times)
quantile(times, c(0.025, 0.975))
```

State your coding, for example `1 = H`, `0 = T`.
