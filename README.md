# Latent Class Analysis (LCA) application

Task: assigning each startup (characterised by a few dozen category group labels) to a single sector

Notes:
- The likelihood calculation is slightly modified (relative to the original source code @dasirra) to avoid the overflow error (when components in the likelihood calculation are either too large or too close to zero): Only minor changes are made e.g., replacing the calculations with stats.bernoulli.logpmf() and stats.special.logsumexp() to ensure the intemediate steps involve sums of log values (rather than products of raw values)
- For model selection, we use the Integrated Completed Likelihood (ICL) criteria to evaluating model fit, which adds a penalty for posterior uncertainty (-2 * sum of entropies across the data) to the BIC criteria
- BIC and AIC would basically keep falling even when the number of clusters increase well into the 100s, as they do not penalise uncertainty in the posterior distribution of the class assignment among data points
- The best sillouette score is rather low (<0.2), which suggests the data generating process may be misspecified (i.e., the underlying data is generated from a different model than the LCA) and a startup may not neatly belong to a single sector
- Possibly either a product space approach or a mixed membership model would better characterise the data, but I haven't tried either so don't know how well alternative methods will work