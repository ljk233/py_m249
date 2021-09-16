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
    display_name: PyM249
    language: python
    name: pym249
---

# Cohort Study: Seat Belts and Children's Safety in Car Accidents

## Set the Notebook

```python
# import the libraries
from opyn.stats import observationalstudies
# precison of return floats
%precision 6
```

## Introduction

The aim of this study is to analyse whether there is an association between children not wearing a seatbelt (the *exposure*) and the sustaining at least moderately severe injuries (the *disease*) as a result of being involved in serious accidents.

> *Data were obtained on 85 children aged from 4-14 years sitting in the left-hand back seat of cars (so behind the driver) involved in serious accidents.*
>
> *The numbers sustaining at least moderately severe injury among children who were wearing seat belts at the time of the accident and among children who were not wearing seat belts were counted.*
>
> ***M269, Open University***

The data was provided by *M249* *(Open University, 2021)* *M249*, who in turn sourced it from Halman, I., Chipman, M., Parkin, P.C. and Wright, J.G. *(British Medical Journal, 2002).*

For simplicity (and brevity), we shall refer to the the not wearing of a seatbelt as *exposed*, and the suffering of at least moderately severe injuries as *disease*.

## Method

!!! Todo Rewrite

```python
# load the data
obs = [[14, 19], [13, 39]]
seatbelts = observationalstudies.ExposureControl(obs)
```

```python
# labels used for DataFrame outputs
seatbelts.row_labels = ["Not wearing a seat belt", "Wearing a seat belt"]
seatbelts.col_labels = ["At least moderately severe injury",
                        "Less that moderately severe injury"]
```

## Results

*Add comment on independence of exposure groups.*

### Inspecting the Data

The results of the study are shown below in a **2x2** contingency table.

```python
seatbelts.show_table(incl_row_totals=True)
```

An estimate for the probability of suffering the disease whilst exposed, $P(D|E)$, was

```python
float(seatbelts.obs[0][0] / seatbelts.obs[0].sum())
```

Whilst the probability of suffering the disease whilst not being exposed, $P(D|E^{c})$, was estimated to be

```python
float(seatbelts.obs[1][0] / seatbelts.obs[1].sum())
```

So the probability of suffering at least moderately severe injuries whilst not wearing a seatbelt does seem higher compared to when wearing a seatbelt.
However, we note that this could be down random variation, so no conclusions should be reached just yet.

### Chi-sqaured Test of No Association

A **chi-squared** test of no association was carried out.
The frequencies expected under the null hypothesis of no association are shown in the table below.

```python
seatbelts.expected_freq(incl_row_totals=True)
```

There does not seem to be that much difference between the observed frequencies and the expected frequencies.
This suggests that there may not be an association between not wearing a seatbelt.
*(Or at least not a strong association.)*

The test yielded a test statistic $\chi^{2} = 2.8278$ with 1 degree of freedom, with a **p**-value of approximately **0.0926.**
*(Note, a table of **chi-squared** contributions is included at the bottom of the note.)*

```python
seatbelts.chi2_test()
```

Given a **0.05** $<$ **p** $\leq$ **0.10**, there is weak evience against the null hypothesis.
The study provides weak evidence that there is an association between a child not wearing a seatbelt and their sustaining of at least a moderately severe injury as a result of being involved in serious car accident.

### Measures of Association

#### Relative risk

An estimate of the relative risk was found to be approximately **1.70,** with 99% confidence interval **(0.76, 3.81).**

```python
seatbelts.relative_risk(alpha=0.01)
```

#### Odds and odds ratio

The odds of suffering the disease whilst being exposed $\widehat{OD}(D|E)$ was **0.74**, and of suffering the disease whilst not exposed $\widehat{OD}(D|E^{c})$ was **0.33**.

```python
seatbelts.conditional_odds(is_cohort=True)
```

Finally, an estimate of the odds ratio was **2.21,** with 99% confidence interval **(0.65, 7.53).**

```python
seatbelts.odds_ratio(0.01)
```

A relative risk of approximately **1.70** suggests that children not wearing seatbelts were 70% more likely to suffer from at least a moderately severe injury compared to other simular children who were wearing a seatbelt.

The point estimates of both the relative risk and odds ratio are both greater than **1**, suggesting there may be a positve association between the exposure and the disease.
However, given both measure's confidence intervals include **1**, it is **plausible** that the true value of the measures could equal **1**, so we cannot conclude that there is an association between the exposure and ther disease.

```python
seatbelts.chi2_contribs()
```

### Discussion

!!! Note Interpret strength of evidence and strength of association
