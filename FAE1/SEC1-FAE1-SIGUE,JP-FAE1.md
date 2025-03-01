## A malicious spyware can infect a computer system though the Internet or through email. The spyware comes through the Internet 70% of the time and 30% of the time, it gets in through email. If it enters via the Internet the anti-virus detector will detect it with probability 0.6, and via email, it is detected with probability 0.8.

    spyware <- data.frame(detected = c(0.6, 0.8), undetected = c(0.4, 0.2),
                          via = c(.70, .30), row.names = c("Internet", "Email"))
    spyware

    ##          detected undetected via
    ## Internet      0.6        0.4 0.7
    ## Email         0.8        0.2 0.3

### (a) What is the probability that this spyware infects the system?

\*Infect = Undetected

*P*(*I*) = *P*(*I*|*I**n**t**e**r**n**e**t*) ⋅ *P*(*I**n**t**e**r**n**e**t*) + *P*(*I*|*E**m**a**i**l*) ⋅ *P*(*E**m**a**i**l*)

    prob_infect <- round(.4 * .7 + .2 * .3, 4)

    cat("The probability that this spyware infects the system is ", 
        prob_infect * 100, "%", sep = "")

    ## The probability that this spyware infects the system is 34%

### (b) If the spyware is detected, what is the probability that it came through the Internet?

\*P(D) = 1 - P(I)

$$
P(D \vert Internet) = \frac{P(Internet \vert D) \cdot P(Internet)}{P(D)}
$$

    prob_detect <- 1 - prob_infect
    prob_det_int <- round((0.6 * 0.7)/(prob_detect), 4)

    cat("The probability that the spyware detected came from the internet is ", 
        prob_det_int * 100, "%", sep = "")

    ## The probability that the spyware detected came from the internet is 63.64%

## Of the emails you receive 20% are spam on average. Your spam filter is able to detect 90% of them but also misclassifies as spam 15% of the genuine emails.

    email <- data.frame(correct = c(.90, .85), incorrect = c(.10, .15),
                        recieved = c(.20, .80), row.names = c("Spam", "Genuine"))
    email

    ##         correct incorrect recieved
    ## Spam       0.90      0.10      0.2
    ## Genuine    0.85      0.15      0.8

### (a) If an email arrives and is marked spam, what is the probability that it really is spam?

$$
P(S \vert C) = \frac{P(C\vert S)\cdot P(S)}{P(Spam)} \newline
P(Spam) = P(C\vert S)\cdot P(S) + P(I\vert G)\cdot P(G)
$$

    prob_spam <- round((.90 * .20 + .15 * .8), 4)
    prob_spam_c <- round(((.90 * .2)/ prob_spam), 4)

    cat("The probability of an email marked spam that is spam is ", prob_spam_c * 100, "%.", sep = "")

    ## The probability of an email marked spam that is spam is 60%.

### (b) If an email arrives and is not marked spam, what is the probability that it is legitimate?

$$
P(G \vert C) = \frac{P(C\vert G)\cdot P(G)}{P(Genuine)} \newline
P(Genuine) = P(C\vert G)\cdot P(G) + P(I\vert S)\cdot P(S)
$$

    prob_gen <- round((.85 * .80 + .10 * .20), 4)
    prob_gen_c <-round(((.85 * .80)/ prob_gen), 4)

    cat("The probability of an email marked genuine that is genuine is ", prob_gen_c * 100, "%.", sep = "")

    ## The probability of an email marked genuine that is genuine is 97.14%.
