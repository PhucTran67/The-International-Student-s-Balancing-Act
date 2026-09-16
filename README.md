# The International Student's Balancing Act

An exploratory analysis of how international and domestic students at the
University of Sydney compare on academic expectations, housing costs and
campus access — framed as a hypothetical pilot study for IDP Education, a
provider of study-abroad counselling and accommodation guidance.

- **Course:** DATA2002, University of Sydney
- **Type:** Group project (6 students)
- **My contribution:** Data wrangling and RQ2 (housing costs)
- **Tools:** R, Quarto (tidyverse, ggplot2)

📄 **[Read the full report](Report.html)** — charts and analysis, no R needed.

---

## About the framing

IDP Education is not conducting this study. The report treats a course
survey of DATA2002/2902 students as a **hypothetical exploratory pilot** —
what a student-insight process might look like before IDP invested in
broader data collection. The point is as much to test whether the survey
measures the right things as to report what it found.

## Data

A voluntary survey of DATA2002/2902 students, covering student status
(international/domestic), desired grade, rent, commute time and lecture
delivery preference. Because participation was voluntary and the cohort is
a single course, findings describe this group rather than Australian
students generally.

## Research questions and methods

Each question got the test that fit its data, rather than defaulting to one
technique:

| Question | Method | Why |
|---|---|---|
| **RQ1.** Do desired grades differ between international and domestic students? | Pearson's chi-squared test of independence | Both variables categorical |
| **RQ2.** Among students paying rent, do international students pay a different mean weekly rent? | Welch's two-sample t-test | Continuous outcome, unequal group variances not assumed |
| **RQ3.** Does commute time differ between students attending remotely and on campus? | Monte Carlo permutation test | Commute-time distribution too skewed to assume normality |

## My contribution: data wrangling and RQ2

**The rent questions contradicted each other.** The survey asked separately
whether a respondent paid rent (yes/no) and how much they paid. Comparing
the two fields surfaced two kinds of contradiction: *Yes* paired with `$0`,
and *No* paired with a positive rent figure.

Rather than silently overwriting either answer to force consistency, I set
a **pre-specified inclusion rule** — RQ2 uses only explicit *Yes*
respondents with a finite positive rent — and reported the contradictions
themselves as a finding about the survey instrument. A pilot study's job is
partly to discover that a question is ambiguous.

**Cleaning was kept analysis-specific.** One unusable answer never removed
a respondent from unrelated questions. A student who gave a contradictory
rent answer still counts toward the RQ1 grade analysis.

**Unusual values were retained.** High rents that were implausible were
excluded by rule; high rents that were merely unusual were kept. Removing
outliers to improve a p-value would have been the wrong call, and the
report says so.

## Findings

- **RQ1:** Both groups report high academic aspirations. Desired-grade
  distributions differ statistically, but the difference shouldn't be
  overstated — desired grade is self-reported aspiration, not ability or
  achievement. Notably, domestic respondents had the higher HD-targeting
  proportion, against an intuition that might have pushed the other way.
- **RQ2:** Rent-paying international respondents reported a substantially
  higher mean weekly rent than domestic respondents. This is the clearest
  practical signal in the report for an organisation offering
  accommodation guidance.
- **RQ3:** The commute-time comparison found insufficient evidence of a
  population mean difference at the 5% level. Reported as a null result
  rather than dropped.

## Limitations

- Voluntary participation from a single course cohort. These are
  associations within this group, not Australian benchmarks.
- All three outcomes are self-reported.
- The rent question doesn't distinguish personal cost from room or
  whole-dwelling cost, or record utilities and living arrangements — which
  is exactly the kind of measurement problem a pilot is meant to catch.
- Observational data throughout; no causal claims.

## Files

```
├── Report.qmd                      # Quarto source: code, analysis and write-up
├── Report.html                     # Rendered report — start here
├── DATA2X02_2026_2_survey_clean.csv # Survey data
├── references.bib                  # Bibliography
└── README.md
```

## Reproducing

Requires R and Quarto.

```r
install.packages(c("tidyverse", "ggplot2", "scales", "knitr", "kableExtra"))
```

```bash
quarto render Report.qmd
```

The permutation test uses a fixed random seed, so results reproduce exactly.

## AI usage

Course module and lab code patterns were adapted where appropriate.
ChatGPT was used during final editing for formatting consistency, figure
styling, code comments, literature discovery and word-count reduction. All
statistical results, code, citations and interpretations were checked
against the data by the group.
