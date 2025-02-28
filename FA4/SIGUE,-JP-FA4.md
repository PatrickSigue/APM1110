## A geospatial analysis system has four sensors supplying images. The percentage of images supplied by each sensor and the percentage of images relevant to a query are shown in the following table.

    images <- data.frame(sensor = 1:4, Supplied = c(0.15, 0.2, 0.25, 0.4), Relevant = c(0.5,
        0.6, 0.8, 0.85))
    images

    ##   sensor Supplied Relevant
    ## 1      1     0.15     0.50
    ## 2      2     0.20     0.60
    ## 3      3     0.25     0.80
    ## 4      4     0.40     0.85

### What is the overall percentage of relevant images?

\*R = Relevant, S = Supplied

*P*(*R*) = *P*(*R*|*S*<sub>1</sub>) ⋅ *P*(*S*<sub>1</sub>) + *P*(*R*|*S*<sub>2</sub>) ⋅ *P*(*S*<sub>2</sub>) + *P*(*R*|*S*<sub>3</sub>) ⋅ *P*(*S*<sub>3</sub>) + *P*(*R*|*S*<sub>4</sub>) ⋅ *P*(*S*<sub>4</sub>)

    prob_rel <- sum(images$Supplied * images$Relevant)

    cat("The overall percentage of relevant images is ", prob_rel * 100, "%.", sep = "")

    ## The overall percentage of relevant images is 73.5%.

## A fair coin is tossed twice. Let *E*<sub>1</sub> be the event that both tosses have the same outcome, that is *E*<sub>1</sub> = (*H**H*, *T**T*). Let *E*<sub>2</sub> be the event that the first toss is a head, that is, *E*<sub>2</sub> = (*H**H*, *H**T*). Let *E*<sub>3</sub> be the event that the second toss is a head, that it, *E*<sub>3</sub> = (*T**H*, *H**H*). Show that *E*<sub>1</sub>, *E*<sub>2</sub>, and *E*<sub>3</sub> are pairwise independent but not mutually independent.

### Sample Space

*S* = *H**H*, *H**T*, *T**H*, *T**T*

Since the coin is fair, each outcome has an equal probability:
$$P({HH}) = P({HT}) = P({TH}) = P({TT}) = \frac{1}{4}$$

### Events and Their Probabilities

1.  *E*<sub>1</sub> = (*H**H*, *T**T*)
    -   $P(E\_1) = P(HH) + P(TT) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$
2.  *E*<sub>2</sub> = (*H**H*, *H**T*)
    -   $P(E\_2) = P(HH) + P(HT) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$
3.  *E*<sub>3</sub> = (*T**H*, *H**H*)
    -   $P(E\_3) = P(TH) + P(HH) = \frac{1}{4} + \frac{1}{4} = \frac{1}{2}$

### Check for Pairwise Independence

Events *A* and *B* are independent if:
*P*(*A* ∩ *B*) = *P*(*A*)*P*(*B*)

1.  $E\_1 \text{ and } E\_2 \newline E\_1 \cap E\_2 = \\HH\\ \newline  P(E\_1 \cap E\_2) = P(HH) = \frac{1}{4} \newline P(E\_1) P(E\_2) = \frac{1}{2} \times \frac{1}{2} = \frac{1}{4}\newline$
    Since
    *P*(*E*<sub>1</sub> ∩ *E*<sub>2</sub>) = *P*(*E*<sub>1</sub>)*P*(*E*<sub>2</sub>),
    *E*<sub>1</sub> and *E*<sub>2</sub> are independent.

2.  $E\_1 \text{ and } E\_3 \newline E\_1 \cap E\_3 = \\HH\\ \newline  P(E\_1 \cap E\_3) = P(HH) = \frac{1}{4} \newline P(E\_1) P(E\_3) = \frac{1}{2} \times \frac{1}{2} = \frac{1}{4}\newline$
    Since
    *P*(*E*<sub>1</sub> ∩ *E*<sub>3</sub>) = *P*(*E*<sub>1</sub>)*P*(*E*<sub>3</sub>),
    *E*<sub>1</sub> and *E*<sub>3</sub> are independent.

3.  $E\_2 \text{ and } E\_3 \newline E\_2 \cap E\_3 = \\HH\\ \newline  P(E\_2 \cap E\_3) = P(HH) = \frac{1}{4} \newline P(E\_2) P(E\_3) = \frac{1}{2} \times \frac{1}{2} = \frac{1}{4}\newline$
    Since
    *P*(*E*<sub>2</sub> ∩ *E*<sub>3</sub>) = *P*(*E*<sub>2</sub>)*P*(*E*<sub>3</sub>),
    *E*<sub>2</sub> and *E*<sub>3</sub> are independent.

### Check for Mutual Independence

*E*<sub>1</sub>, *E*<sub>2</sub>, …, *E*<sub>*k*</sub> are mutually
independent if:
*P*(*E*<sub>*i*<sub>1</sub></sub> ∩ *E*<sub>*i*<sub>2</sub></sub> ∩ ⋯ ∩ *E*<sub>*i*<sub>*k*</sub></sub>) = *P*(*E*<sub>*i*<sub>1</sub></sub>)*P*(*E*<sub>*i*<sub>2</sub></sub>)⋯*P*(*E*<sub>*i*<sub>*k*</sub></sub>)

From the sets:
$\newline E\_1 \cap E\_2 \cap E\_3 = \\HH\\ \newline P(E\_1 \cap E\_2 \cap E\_3) = P(HH) = \frac{1}{4}$

Calculate *P*(*E*<sub>1</sub>)*P*(*E*<sub>2</sub>)*P*(*E*<sub>3</sub>):
$\newline P(E\_1)P(E\_2)P(E\_3) = \frac{1}{2} \times \frac{1}{2} \times \frac{1}{2} = \frac{1}{8}\newline$

Since
*P*(*E*<sub>1</sub> ∩ *E*<sub>2</sub> ∩ *E*<sub>3</sub>) ≠ *P*(*E*<sub>1</sub>)*P*(*E*<sub>2</sub>)*P*(*E*<sub>3</sub>),
the events are not mutually independent.
