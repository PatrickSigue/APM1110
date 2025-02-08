## 3. An experiment consists of rolling a die. Use R to simulate this experiment 600 times and obtain the relative frequency of each possible outcome.

    possible <- c(1,2,3,4,5,6)

    experiment <- sample(possible, 600, replace = TRUE)

    results <- data.frame(
               Outcome = possible,
               Frequency = c(sum(experiment == 1), sum(experiment == 2), sum(experiment == 3), 
                             sum(experiment == 4), sum(experiment == 5), sum(experiment == 6)))

    brplt <- barplot(results$Frequency, names.arg = possible, main = "Frequency of Die Roll Result",
            xlab = "Outcomes", ylab = "Frequency", ylim = c(0,max(results$Frequency)), col = "#FFC300")

    text(brplt, results$Frequency, labels = results$Frequency, 
         cex = 1, pos = 1)

![](SEC-1-FA2-GROUP-1-SIGUE,-JP-FA2_files/figure-markdown_strict/unnamed-chunk-1-1.png)

### Hence, estimate the probability of getting each of 1, 2, 3, 4, 5, and 6.

    rel_freq <- round(results$Frequency / 600 * 100, 2)

    relative_frequency <- data.frame(Outcomes = c(possible, "Total"), 
                          "Probability(%)" = c(rel_freq, sum(rel_freq)))

    print(relative_frequency)

    ##   Outcomes Probability...
    ## 1        1          16.17
    ## 2        2          20.33
    ## 3        3          16.00
    ## 4        4          15.50
    ## 5        5          16.17
    ## 6        6          15.83
    ## 7    Total         100.00
