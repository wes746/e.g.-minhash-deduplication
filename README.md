# High-Performance MinHash LSH Data Deduplication Pipeline

## Overview
This repository provides a scalable, multiprocessing Python pipeline for identifying and removing near-duplicate documents from large text datasets. 

In the context of training Large Language Models (LLMs), training on raw, duplicate-heavy web data degrades model reasoning and increases computational overhead. This pipeline utilizes MinHash Locality-Sensitive Hashing (LSH) to efficiently filter high-volume datasets, ensuring high-quality inputs for model fine-tuning and pre-training.

## Mathematical Foundation
Identifying exact duplicates is computationally simple. Identifying *near-duplicates* (e.g., a text with a few altered words) across millions of documents using standard string comparison requires $O(N^2)$ time complexity, which is unscalable. 

This script solves this using two concepts:

1.  **Jaccard Similarity:** A mathematical measure of similarity between two sets. It is defined as the size of the intersection divided by the size of the union of the sample sets:
    $$J(A,B) = \frac{|A \cap B|}{|A \cup B|}$$
    
2.  **MinHash LSH:** Instead of comparing every document to every other document, the text is broken into overlapping 3-word chunks (shingles). The algorithm generates a compressed "signature" (MinHash) for each document. LSH then groups these signatures into "buckets." Documents that hash to the same bucket are flagged as near-duplicates, reducing the search space to $O(N)$.

## Requirements and Installation
This pipeline requires Python 3.7+ and the `datasketch` library.

```bash
pip install datasketch
