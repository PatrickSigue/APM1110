## An email message can travel through one of three server routes. The percentage of errors in each of the servers and the percentage of messages that travel through each route are shown in the following table. Assume that the servers are independent.

    email <- data.frame(Messages = c(0.4, 0.25, 0.35), Errors = c(0.01, 0.02, 0.015),
        row.names = c("Server 1", "Server 2", "server 3"))
    email

    ##          Messages Errors
    ## Server 1     0.40  0.010
    ## Server 2     0.25  0.020
    ## server 3     0.35  0.015

### What is the probability of receiving an email containing an error?

*P*(*E*) = *P*(*E*|*S*<sub>1</sub>)*P*(*S*<sub>1</sub>) + *P*(*E*|*S*<sub>2</sub>)*P*(*S*<sub>2</sub>) + *P*(*E*|*S*<sub>3</sub>)*P*(*S*<sub>3</sub>)

    prob_err <- round(sum(email$Messages * email$Errors), 4)

    cat("The probability of recieving an email containing an error is ", prob_err * 100,
        "%.", sep = "")

    ## The probability of recieving an email containing an error is 1.42%.

### What is the probability that a message will arrive without error?

*P*(*E*<sup>*C*</sup>) = 1 − *P*(*E*)

    prob_wo_err <- round((1 - prob_err), 4)

    cat("The probability of recieving an email without an error is ", prob_wo_err * 100,
        "%.", sep = "")

    ## The probability of recieving an email without an error is 98.58%.

### If a message arrives without error, what is the probability that it was sent through server 1?

$$P(S\_1 \vert E^C) = \frac{P(E^C\vert S\_1)P(S\_1)}{P(E^C)}$$

    prob_wo_s1 <- round((((1 - 0.01) * 0.4)/prob_wo_err), 4)

    cat("The probability of recieving an email without an error from server 1 is ", prob_wo_s1 *
        100, "%.", sep = "")

    ## The probability of recieving an email without an error from server 1 is 40.17%.

## A software company surveyed managers to determine the probability that they would buy a new graphics package that includes three-dimensional graphics. About 20% of office managers were certain that they would not buy the package, 70% claimed that they would buy, and the others were undecided. Of those who said that they would not buy the package, only 10% said that they were interested in upgrading their computer hardware. Of those interested in buying the graphics package, 40% were also interested in upgrading their computer hardware. Of the undecided, 20% were interested in upgrading their computer hardware.

-   Let A denote the intention of not buying, B the intention of buying,
    C the undecided, and G the intention of upgrading the computer
    hardware.

<!-- -->

    survey <- data.frame(Group = c("A", "B", "C"), Probability = c(0.2, 0.7, 0.1), G = c(0.1,
        0.4, 0.2))

    survey

    ##   Group Probability   G
    ## 1     A         0.2 0.1
    ## 2     B         0.7 0.4
    ## 3     C         0.1 0.2

## Calculate the probability that a manager chosen at random will not upgrade the computer hardware ($P(\overline{G})$)

$$P(\overline{G}) = P(A \vert\overline{G}) P(A) + P(B\vert\overline{G}) P(B) + P(C\vert\overline{G}) P(C)$$

    survey$"~G" <- 1 - survey$G

    prob_neg_g <- round(sum(survey$Probability * survey$`~G`), 4)
    cat("The probability that a manager chosen at random will not upgrade the computer hardware is ",
        prob_neg_g * 100, "%.", sep = "")

    ## The probability that a manager chosen at random will not upgrade the computer hardware is 68%.

## Explain what is meant by the posterior probability of *B* given *G*, *P*(*B*|*G*).

This tells us how likely a manager is to buy the graphics package if we
already know that they are interested in upgrading.

## Construct a tree diagram and use it to calculate the following probabilities: $P(G), P(B\vert G), P(B\vert \overline{G}), P(C\vert G), P(\overline{C}\vert \overline{G})$

    survey$pathString <- paste("Survey", survey$Group, sep = "/")
    tree <- as.Node(survey)

    print(tree, "Probability", "G", "~G")

    ##   levelName Probability   G  ~G
    ## 1    Survey          NA  NA  NA
    ## 2     ¦--A          0.2 0.1 0.9
    ## 3     ¦--B          0.7 0.4 0.6
    ## 4     °--C          0.1 0.2 0.8

    prob_g <- (1 - prob_neg_g)
    prob_b_g <- round((tree$B$G * tree$B$Probability)/prob_g, 4)
    prob_b_neg_g <- round((tree$B$"~G" * tree$B$Probability)/prob_neg_g, 4)
    prob_c_g <- round((tree$C$G * tree$C$Probability)/prob_g, 4)
    prob_neg_c_neg_g <- round((tree$A$"~G" * tree$A$Probability + tree$B$"~G" * tree$B$Probability)/prob_neg_g,
        4)

    cat("P(G) = ", prob_g * 100, "%\nP(B|G) = ", prob_b_g * 100, "%\nP(B|~G) = ", prob_b_neg_g *
        100, "%\nP(C|G) = ", prob_c_g * 100, "%\nP(~C|~G) = ", prob_neg_c_neg_g * 100,
        "%", sep = "")

    ## P(G) = 32%
    ## P(B|G) = 87.5%
    ## P(B|~G) = 61.76%
    ## P(C|G) = 6.25%
    ## P(~C|~G) = 88.24%

## A malicious spyware can infect a computer system through the Internet or through email. The spyware comes through the Internet 70% of the time and 30% of the time, it gets in through email. If it enters via the Internet the anti-virus detector will detect it with probability 0.6, and via email, it is detected with probability 0.8.

    spyware <- data.frame(Via = c(0.7, 0.3), Detect = c(0.6, 0.8), row.names = c("Internet",
        "Email"))
    spyware

    ##          Via Detect
    ## Internet 0.7    0.6
    ## Email    0.3    0.8

### What is the probability that this spyware infects the system?

*P*(¬*D*) = *P*(¬*D*|*V*<sub>*I*</sub>)*P*(*V*<sub>*I*</sub>) + *P*(¬*D*|*V*<sub>*E*</sub>)*P*(*V*<sub>*E*</sub>)

    spyware$"~Detect" <- 1 - spyware$Detect

    prob_neg_d <- round(sum(spyware$`~Detect` * spyware$Via), 4)
    cat("The probability that the spyware infects the system is ", prob_neg_d * 100,
        "%.", sep = "")

    ## The probability that the spyware infects the system is 34%.

### If the spyware is detected, what is the probability that it came through the Internet?

$$P(D\vert V\_I) = \frac{P(V\_I\vert D) P(V\_I)}{P(D)}$$

    prob_det_int <- round(((spyware$Detect[1] * spyware$Via[1])/(1 - prob_neg_d)), 4)

    cat("The probability that the spyware detected came from the internet is ", prob_det_int *
        100, "%.", sep = "")

    ## The probability that the spyware detected came from the internet is 63.64%.
