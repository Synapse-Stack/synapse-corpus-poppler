# synapse-corpus-poppler

Isolated Poppler-focused stress-testing corpora extracted and normalized from the PDF Association SafeDocs Stressful PDF Corpus.

This repository contains the largest and most resource-intensive subset of the SafeDocs ecosystem and is intentionally isolated from standard CI workloads.

Designed for:

* deep parser stress testing
* renderer interoperability validation
* large-scale fuzzing
* memory exhaustion analysis
* long-running scheduled validation
* infrastructure-scale regression testing

---

# Overview

The Poppler corpus represents one of the largest entities within the SafeDocs Stressful PDF Corpus.

Due to its size and extraction cost, this dataset is separated into its own dedicated repository to:

* prevent blocking lightweight CI pipelines
* reduce GitHub Actions disk pressure
* isolate infrastructure-heavy workloads
* allow targeted scheduled execution
* improve reproducibility for parser research

---

# Included Corpora

Current datasets include:

* poppler
* poppler-gitlab

Each dataset is packaged independently as a normalized `.zip` archive for selective retrieval during automated workflows.

---

# Repository Structure

```txt id="44kgrr"
synapse-corpus-poppler/
├── README.md
├── LICENSE
├── manifest.json
├── SHA256SUMS
├── poppler.zip
└── poppler-gitlab.zip
```

---

# Why This Repository Exists

The original upstream archives are extremely large and unsuitable for repeated CI execution inside standard pull request pipelines.

This repository exists to:

* isolate infrastructure-heavy corpora
* enable scheduled validation workflows
* reduce runner storage exhaustion
* simplify targeted downloads
* improve reproducibility for parser testing and fuzzing

---

# Usage Example

```bash id="w1j1cx"
mkdir -p tests/assets/corpus/poppler

curl -L \
  https://media.githubusercontent.com/media/YOURORG/synapse-corpus-poppler/main/poppler.zip \
  -o poppler.zip

unzip -q poppler.zip -d tests/assets/corpus/poppler/

rm poppler.zip
```

---

# GitHub Actions Example

```yaml id="jlwm2n"
- name: Fetch Poppler Corpus
  run: |
    mkdir -p tests/assets/corpus/poppler

    curl -L \
      https://media.githubusercontent.com/media/YOURORG/synapse-corpus-poppler/main/poppler.zip \
      -o poppler.zip

    unzip -q poppler.zip -d tests/assets/corpus/poppler/

    rm poppler.zip
```

---

# Recommended CI Strategy

Because of the repository size and extraction overhead, the recommended execution model is:

* scheduled workflows
* manual dispatch execution
* dedicated runners
* monthly or weekly validation

Example workflow trigger:

```yaml id="mjlwm0"
on:
  workflow_dispatch:

  schedule:
    - cron: "0 6 1 * *"
```

---

# Optimization Notes

Each archive was normalized to:

* reduce extraction overhead
* remove redundant upstream artifacts
* eliminate nested archive duplication
* improve CI decompression speed
* minimize temporary disk consumption

Only normalized archives are stored.

Raw upstream distributions and temporary extraction artifacts are intentionally excluded.

---

# Provenance

The original datasets originate from:

* PDF Association SafeDocs Stressful Corpus
* https://labs.pdfa.org/stressful-corpus/

This repository redistributes normalized subsets strictly for testing, interoperability research, parser validation, fuzzing, and CI reproducibility purposes.

All rights remain with their respective upstream authors and projects.

---

# Integrity Verification

SHA256 hashes are provided inside:

```txt id="1o67sh"
SHA256SUMS
```

Verification example:

```bash id="dh79qg"
sha256sum -c SHA256SUMS
```

---

# Intended Usage

Recommended use cases include:

* parser stress testing
* malformed PDF analysis
* renderer compatibility validation
* differential parser testing
* infrastructure-scale fuzzing
* regression benchmarking
* memory pressure testing
* security research

---

# License

Repository tooling, manifests, and packaging:
MIT

Corpus contents:
Owned by their respective upstream projects and contributors.

```
```
