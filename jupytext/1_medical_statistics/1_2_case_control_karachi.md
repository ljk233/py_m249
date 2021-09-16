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

# Case-Control Study: Alcohol Consumption and Fatal Car Accidents

## Set the Notebook

```python
# import the libraries
from opyn.stats import observationalstudies
# set the precison of return floats
%precision 6
```

## Introduction

!!! Note Activity 3.1, pp25.

## Method

!!! Note Rewrite.

```python
# init the data
obs = [[14, 8], [10, 146]]
```

```python
# init object
alcohol_carcrash = observationalstudies.ExposureControl(obs)
```

```python
# labels used for DataFrame outputs
alcohol_carcrash.row_labels = (
    ["Alcohol levels >= 100mg%", "Alcohol levels < 100mg%"]
)
alcohol_carcrash.col_labels = ["Cases", "Controls"]
```

## Results

### Inspecting the Data

The data is shown below in a contingency table.

```python
alcohol_carcrash.show_table(incl_col_totals=True)
```

### Chi-squared Test of No Association

```python
alcohol_carcrash.expected_freq(incl_col_totals=True)
```

```python
alcohol_carcrash.chi2_contribs()
```

```python
alcohol_carcrash.chi2_test()
```

!!! Note Add interpretation.

### Measures of Association

!!! Note Add interpretation on independence.

### Discussion

!!! Note Interpret strength of evidence and strength of association
