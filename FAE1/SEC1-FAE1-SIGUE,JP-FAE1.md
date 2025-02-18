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
P(D \vert Internet) = \frac{P(D \vert Internet) \cdot P(Internet)}{P(D)}
$$

    prob_detect <- 1 - prob_infect
    prob_det_int <- round((0.6 * 0.7)/(prob_detect), 4)

    cat("The probability that the spyware detected came from the internet is ", 
        prob_det_int * 100, "%", sep = "")

    ## The probability that the spyware detected came from the internet is 63.64%
