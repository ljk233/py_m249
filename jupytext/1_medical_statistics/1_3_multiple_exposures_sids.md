---
jupyter:
  jupytext:
    formats: jupyter///ipynb,jupytext///md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.11.3
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Case-Control Study: Sleeping Position and Sudden Infant Death Syndrome

## Setup the Notebook

```python
# import the libraries
from opyn.stats import observationalstudies
# set the precison of return floats
%precision 6
```

## Introduction

## Method

The analysis follows that as summarised in M26 Book 1, Part 1.

The data was first plotted as a comaparative bar char and summarised.

Following this, given the nature of the data, a contingency table was used to perform an analysis on the strenght of association.
To perform the analysis, we selected the group including babies who slept on their side as the reference category.
This was an arbitrary choice, as it seemed like a natural choice between sleeping on one's back and on one's front.
An estimate of the odds ratio and a 99% **z**-interval for the odds ratio was calculated in relation to the reference category, after considerations on whether the two exposure groups were independent.

The expected frequencies under a null hypothesis of no association were checked to be all greater than or equal to five, and **chi-sqaured** test of no association was used to test the null hypothesis of no association betwen the exposure and the disease.

```python
# initialise the data
e1 = [30, 24]  # on front
e2 = [82, 509]  # on back
ref = [76, 241]  # on side
```

```python
# load the object
sids = observationalstudies.ThreeExposures(
    exposure1=e1, exposure2=e2, reference=ref
)
```

```python
# labels used for DataFrame outputs
sids.exposure1_label = "Slept on Front"
sids.exposure2_label = "Slept on Back"
sids.reference_label = "Slept on Side (Ref)"
# case-control study, relabel the columns
sids.col_labels = ["Cases", "Controls"]
```

## Results

### Inspecting the Data

The data is shown below in a contingency table.

```python
sids.show_table(incl_col_totals=True)
```

!!! Note Add interpretation and comment on independence.

### Chi-squared Test of No Association

```python
sids.expected_freq(incl_col_totals=True)
```

```python
sids.chi2_contribs()
```

```python
sids.chi2_test()
```

!!! Note Add interpretation

### Measures of Association

An estimate of the odds ratio $\widehat{OR}_{\text{Back}}$ was found to be approximately 3.96, with 99% confidence interval (1.81, 8.67).

```python
sids.table1.conditional_odds(is_cohort=False)
```

```python
# odds ratio, on front
sids.table1.odds_ratio(0.01)
```

An estimate of the odds ratio $\widehat{OR}_{\text{Front}}$ was found to be approximately 0.51, with 99% confidence interval (0.32, 0.81).

```python
sids.table2.conditional_odds(is_cohort=False)
```

```python
# odds ratio, on back
sids.table2.odds_ratio(0.01)
```

!!! Add interpretation

### Discussion

!!! Note Interpret strength of evidence and strength of association
