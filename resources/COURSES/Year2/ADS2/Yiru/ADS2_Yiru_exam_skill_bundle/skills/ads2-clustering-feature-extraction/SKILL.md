---
name: ads2-clustering-feature-extraction
description: Use this skill for ADS/ADS2 k-means clustering, neuron-type classification from numeric features, comparing clusters to known labels, elbow plots, adjusted Rand index, simple feature extraction from image-like matrices, MNIST-style row/column summaries, or classification feature preparation. Trigger on kmeans, k-means, clustering, neuron type, hap1, hap2, feature extraction, MNIST, pixels, classification, or cluster validation.
---

# ADS2 Clustering And Feature Extraction

Use for the ADS2 neuron-classification style task and lower-priority feature extraction practice.

## K-Means Workflow

1. Import and check data.
2. Plot original labels if available.
3. Select numeric features.
4. Scale features if ranges differ.
5. Choose `k`; use known class count if supplied.
6. Run `kmeans` with `set.seed()` and `nstart`.
7. Plot clusters.
8. Compare to original labels with a contingency table.

## K-Means Template

```r
dat <- read.csv("vmndata.csv")
str(dat)
head(dat)
colSums(is.na(dat))
sum(duplicated(dat))

plot(dat$hap1, dat$hap2, col = as.factor(dat$type), pch = 19,
     xlab = "hap1", ylab = "hap2", main = "Original classification")

features <- dat[, c("hap1", "hap2")]
features_scaled <- scale(features)

set.seed(123)
km <- kmeans(features_scaled, centers = 5, nstart = 25)
dat$cluster <- factor(km$cluster)

plot(dat$hap1, dat$hap2, col = dat$cluster, pch = 19,
     xlab = "hap1", ylab = "hap2", main = "K-means clusters")

table(dat$type, dat$cluster)
```

## Elbow Plot

```r
wss <- sapply(1:10, function(k) {
  kmeans(features_scaled, centers = k, nstart = 25)$tot.withinss
})
plot(1:10, wss, type = "b", xlab = "Number of clusters", ylab = "Within-cluster SS")
```

## Adjusted Rand Index

Only use if a package is already available. Do not waste exam time installing packages.

```r
library(mclust)
adjustedRandIndex(dat$type, dat$cluster)
```

Fallback: use `table(dat$type, dat$cluster)` and visual comparison.

## Feature Extraction From 28x28 Images

```r
raw <- read.csv("mnist_train.csv", header = FALSE)
labels <- raw[, 1]
pixels <- raw[, -1]

get_features <- function(row_pixels) {
  mat <- matrix(as.numeric(row_pixels), nrow = 28, byrow = TRUE)
  c(rowMeans(mat), colMeans(mat))
}

features <- t(apply(pixels[1:1000, ], 1, get_features))
features <- data.frame(label = labels[1:1000], features)
```

## Interpretation

```text
The k-means clustering produced [k] clusters. Comparing the clusters with the original labels using a contingency table shows [degree of agreement]. The clustering is [good/moderate/poor] because [specific pattern], but cluster labels themselves are arbitrary.
```
