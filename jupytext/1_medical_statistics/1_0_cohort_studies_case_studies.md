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

# Cohort studies

## Keywords

#association #epidemiology #cohortstudies #exposure #control #contingencytable #relativerisk #odds #oddsratio

## What are cohort and case-control studies?

**Cohort studies** and **case-control studies** are studies of the association between an exposure $E$ and a disease $D$ *(pp8, pp23-24)*.

In a cohort study, $E$ is known and $D$ is unknown.
Alternatively, in a case-control study, it is $D$ that is known prior to the study, and $E$ is unknown *(pp24)*.

A **retrospective** cohort study is one which occurs after both the outcome has happended.
The analysis then looks back to the time the outcome happeneded to determine their exposure *(pp11 and [Boston University School of Public Health, 2017](https://sphweb.bumc.bu.edu/otlt/mph-modules/ep/ep713_analyticoverview/ep713_analyticoverview3.html))*.

The controls in a case-control study should be chosen from the same population as that of the cases.
After that, then the exposure category can be determined *(pp24)*.

Both can be analysed by a two-by-two **contingency table**.
Contingency table for a cohort study *(pp10):*

|           | D   |   Not D | Total   |
|-----------|-----|---------|---------|
| **E**     | *a* | *b*     | *n1*    |
| Not **E** | *c* | *d*     | *n2*    |

Contingency table for a cohort study *(pp23-24):*

|           | Cases   | Control   |
|-----------|---------|-----------|
| **E**     | *a*     | *b*       |
| Not **E** | *c*     | *d*       |
| **Total** | *m1*    | *m2*      |

## Measures of association

A **measure of association** is a means to quantify the strength of an association *(pp7)*.

### Relative risk

The **relative risk**, $RR$, is the ratio of having the disease and being exposed, to having the disease and not being exposed *(pp11-12)*.

It can be estimated using

$$\widehat{RR} = \frac{\hat P (D|E)}{\hat P (D|\text{not } E)}.$$

It cannot be directly estimated in a case-control study *(pp25)*, but it can be indirectly estimated from the the odds ratio *(pp15)*.

The relative risk is a good measure to use when communicating some findings to the general public. *(pp15).*

### Odds and the odds ratio

The **odds of an event**, $OD$, is defined as the ratio of the probability of an event occuring to the probability of the event not occuring *(pp13-14).*

$$OD(A) = \frac{P(A)}{P(\text{Not } A)} = \frac{P(A)}{1 - P(A)}.$$

In a cohort study it possible to estimate the odds of *disease given exposure,* so $\widehat{OD} (D | E)$ and $\widehat{OD} (D | \text{ Not } E)$ *(pp13).*

$$\widehat{OD} (D | E) = \frac{a}{b}, \hspace{3mm} \widehat{OD} (D | \text{ Not } E) = \frac{c}{d}.$$

Alternatively, case-control studies can estimate the odds of *exposure given disease*, so $\widehat{OD} (E | D)$ and $\widehat{OD} (E | \text{ Not } D)$ *(p27).*

$$\widehat{OD} (E | D) = \frac{a}{c}, \hspace{3mm} \widehat{OD} (E | \text{ Not } D) = \frac{b}{d}.$$

The **odds ratio**, $OR$, is defined as the ratio of the odds of a disease happening given exposure to the odds of the disease happening given no exposure.
It represents the **strength of assocation.**
Like $RR$ a postive value represents a *positive* association, and a negative value represents a *negative* association *(pp13-14).*

It can be shown that

$$\widehat{OR} = \frac{\widehat{OD} (D | E)}{\widehat{OD} (D | \text{ Not } E)} = \frac{\widehat{OD} (E | D)}{\widehat{OD} (E | \text{ Not } D)} = \frac{ad}{bc}.$$

This means that the calculation of the odds ratio is the same for both cohort and case-control studies *(pp27).*

### Comparing the relative risk and odds ratio

!!! Note Review this sub-section.

### Confidence intervals for measures of association

The point estimates for the relative risk and the odds ratio are subject to sampling variability.
A confidence interval can be used to quantify this uncertainty *(pp16).*

This is done using a **binomial model,** with the assumption that the number of disease outcomes for the exposed group are independent of the number of diseased outcome of the control group *(pp17).*

!!! Note Expand this to include some interpretation, specifically when the interval includes 1.

## Multiple exposure categories

Pick an exposure category as an arbitrary **reference** category.
All ratio are then calculated relative to this reference category *(pp29-30).*

## Testing for no association

!!! Note Break this section down futher.

### Chi-squared test for no association

A **chi-squared test for no association** tests the null hypothesis that there is no association between the exposure and the disease.

If there is a need for a reference category, then the test is not affected by the choice of reference category, as all values are taken into account.

#### Expected frequencies

The test requires all expected frequencies to be greater than or equal to **five** for it to be adequate.

#### Chi-squared contributions

!!! Note Missing note

#### Degrees of freedom

The degrees of freedom for the test when using a **2x2** contingency table is **1.**
Otherwise, use $\nu = (r - 1)\hspace{2mm}(c - 1).$

#### The p-value and interpretation

The $p$-value and $\widehat{OR}$ are often reported together:
The $p$-value quantifies the strength of the *evidence;* $\widehat{OR}$ quantifies the strength of *association.*

### Fisher’s exact test

**References:** Book 1 pp40, HB pp11.8

## Implementation in `opyn`

Cohort studies and case-control studies are implemented in

```{python}
opyn.stats.observationalstudies
```

The example notebooks in this directory make use of the module.
