## A binary communication channel carries data as one of two sets of signals denoted by 0 and 1. Owing to noise, a transmitted 0 is sometimes received as a 1, and a transmitted 1 is sometimes received as a 0. For a given channel, it can be assumed that a transmitted 0 is correctly received with probability 0.95, and a transmitted 1 is correctly received with probability 0.75. Also, 70% of all messages are transmitted as a 0. If a signal is sent, determine the probability that:

\*R = Received, T = Transmitted

    binary_comm <- data.frame(correct = c(0.95, 0.75), error = c(0.05, 0.25),
                              sent = c(0.70, 0.30), row.names = 0:1)
    binary_comm

    ##   correct error sent
    ## 0    0.95  0.05  0.7
    ## 1    0.75  0.25  0.3

### a 1 was received

*P*(*R* = 1) = *P*(*R* = 1|*T* = 0) ⋅ *P*(*T* = 0) + *P*(*R* = 1|*T* = 1) ⋅ *P*(*T* = 1)

    prob_get1 <- round((0.05 * 0.7 + .75 * 0.3), 4)
    cat(prob_get1 * 100, "%", sep = "")

    ## 26%

### a 1 was transmitted given then a 1 was received

$P(T = 1 | R = 1) = \frac{P(T = 1) \cdot P(R = 1 | T = 1)}{P(R = 1)}$

    prob_send1_get1 <- round(((0.3 * 0.75) / prob_get1), 4)
    cat(prob_send1_get1 * 100, "%", sep = "")

    ## 86.54%

## There are three employees working at an IT company: Jane, Amy, and Ava, doing 10%, 30%, and 60% of the programming, respectively. 8% of Jane’s work, 5% of Amy’s work, and just 1% of Ava‘s work is in error.

    work <- data.frame(runs = c(0.92, 0.95, 0.99), errors = c(0.08, 0.05, 0.01),
                       load = c(0.10, 0.30, 0.60), row.names = c("Jane", "Amy", "Ava"))
    work

    ##      runs errors load
    ## Jane 0.92   0.08  0.1
    ## Amy  0.95   0.05  0.3
    ## Ava  0.99   0.01  0.6

### What is the overall percentage of error?

*P*(*E*) = *P*(*E*|Jane) \* *P*(Jane) + *P*(*E*|Amy) \* *P*(Amy) + *P*(*E*|Ava) \* *P*(Ava)

    error <- round((0.08 * 0.1 + 0.05 * 0.3 + 0.01 * 0.6), 4)
    cat(error * 100, "%", sep = "")

    ## 2.9%

### If a program is found with an error, who is the most likely person to have written it?

$P(E|\text{Employee}) = \frac{P(E|\text{Employee}) \cdot P(\text{Employee})}{P(E)}$

    e_jane <- round(((0.08 * 0.1) / error), 4)
    e_amy <- round(((0.05 * 0.3) / error), 4)
    e_ava <- round(((0.01 * 0.6) / error), 4)

    e_likely <- max(c(e_jane, e_amy, e_ava))

    cat("Most likely to cause an error is Amy with ", e_amy * 100, "%.\n\n", sep = "")

    ## Most likely to cause an error is Amy with 51.72%.

    cat("Jane:", e_jane * 100, "%\n", sep = "")

    ## Jane:27.59%

    cat("Amy:", e_amy * 100, "%\n", sep = "")

    ## Amy:51.72%

    cat("Ava:", e_ava * 100, "%\n", sep = "")

    ## Ava:20.69%
