# Peer Review of Disruptive Papers: Sample Data

This repository contains a 200 paper sample dataset used in a study of how disruptive papers are evaluated during peer review. The data link PLOS ONE public peer review histories with citation-based disruption scores and sentence-level classifications of reviewer comments.

The full study is based on 24,547 accepted biomedical PLOS ONE articles. This public sample is provided for transparency and to illustrate the data structure.

## Files

| File | Level | Description |
|---|---|---|
| `paper_level_dataset_sample.csv` | Paper | Paper metadata, disruption scores, review-process measures, and controls. |
| `round_level_dataset_sample.csv` | Review round | Round-level timing, reviewer counts, comment counts, and author-response timing. |
| `reviewer_comment_aspects_sample.csv` | Sentence | Reviewer-comment sentences with aspect and sentiment labels. |

All files can be linked by `doi`. The round-level and sentence-level files also include `review_round`.

## Main Variables

- `disruption`: citation-based disruption score.
- `high_disruption`: equals 1 for papers in the top decile of the disruption-score distribution.
- `review_round_count`: total number of review rounds.
- `review_comment_round_count`: number of rounds with reviewer comments.
- `total_review_days`: days from initial submission to acceptance.
- `reviewer_editor_processing_days`: reviewer/editor-side processing time.
- `author_response_days_total`: author-side revision time.
- `aspect`: reviewer-comment aspect label.
- `sentiment`: `positive`, `negative`, or `neutral`.

The `aspect` label has eight categories: `Summary`, `Motivation/Impact`, `Originality`, `Soundness/Correctness`, `Substance`, `Replicability`, `Meaningful Comparison`, and `Clarity`.

## Sample

The sample contains 200 papers, including 20 high-disruption papers. It covers publication years 2019-2024. Papers were selected to have complete links across the three files, non-missing core metadata, valid aspect/sentiment labels, and readable reviewer-comment text.

## Quick Start

```python
import pandas as pd

paper = pd.read_csv("paper_level_dataset_sample200.csv")
rounds = pd.read_csv("round_level_dataset_sample200.csv")
comments = pd.read_csv("reviewer_comment_aspects_sample200.csv")

negative_aspects = (
    comments[comments["is_negative"] == 1]
    .groupby(["high_disruption", "aspect"])
    .size()
    .reset_index(name="n")
)
```

## Notes

This is a sample dataset for inspection and transparency, not the full replication dataset. The full analysis in the paper uses 24,547 articles.

Reviewer comments come from PLOS ONE public peer review histories. Disruption scores were linked from SciSciNet using DOI identifiers.

If using this sample, please cite the associated paper and:

Lin, Z., Yin, Y., Liu, L., & Wang, D. (2023). SciSciNet: A large-scale open data lake for the science of science research. *Scientific Data, 10*, 315. https://doi.org/10.1038/s41597-023-02198-9
