---
title: "PanSeer cancer blood test: Thinking about interpreting medical test accuracy"
date: 2021-02-11
tags: ['medical testing', 'blogs', 'cancer']
draft: true
---

## Background

I recently saw the an article titled 
[Non-invasive early detection of cancer four years before conventional diagnosis using a blood test](https://www.nature.com/articles/s41467-020-17316-z#Tab1)
. This is obviously an impressive claim and so I skimmed through. The methods
of the test are very interesting; the authors measured methylation of DNA
in blood plasma and then used logistic regression to classify reads as cancerous
or not cancerous in origin based on DNA-methylation patterns extracted from
the cancer genome atlas. 

The paper claims to detect 88% of 5 common cancer types in post-diagnosis
patients with a specificity of 96%. Another way of saying the same thing
is that their test has a false-negative rate of 12% and a false-positive rate
of 4%. 

## What would it actually mean if you where diagnosed with this test?

This is the main question I was thinking about. If you were given this test
and it came back positive, what could you conclude? One way to answer this
question is determine the Positive Predictive Value (PPV) of the test. PPV
effectively asks the question "*To what extend does a positive test result 
predict the presence of disease?*"

$$
PPV = \Pr( Cancer \mid + )
$$

Determining an (very) approximate value for the PPV of this test can give us
a better idea of how useful this test might actually be as a tool for early
cancer diagnosis. To do so, lets consider a concrete example.

Consider a case where 10,000 people are tested with the new PanSeer test. The
National Cancer Institute estimates the incidence rate of cancer in the U.S to be
[442.5 per 100,000 men and women](https://www.cancer.gov/about-cancer/understanding/statistics).
Using this as a rough measure, we might expect ~44 individuals in our 10,000 patient
sample to actually have cancer. 

We can visualize these groups as two blocks, red being the true positives
(those with cancer) and green being the true negatives (no cancer).

![](/posts/images/sample.png)

First we know the test to have a 12% false negative rate, meaning 12%, or ~5
of the 44 patients with cancer will test negative. We also know the test to have
a false positive rate of 4%, so we can expect ~398 patients who do not have
cancer to test positive.

I have showed this in the image below by labeling the false negatives in dark
red and the false positives in yellow.

![](/posts/images/sample_pos_negs.png)

Now we can add take the block representing the true positives and divide it
by the sum of the false-positives and false-negatives to get the PPE.

![](/posts/images/ppe.png)

This gives PPE = 0.096 or 9.6%. This means if you were to receive a positive
test result from the PanSeer blood test you would have (very roughly) a ~9.6%
change of *actually* having cancer. It should be noted though that for
simplicity this is treating the test as predicting the occurrence of cancer
at most one year into the future. However even this approximation paints a 
different picture of the test than just stating the false positive
and negative rates. 

## Conclusions

The results of this new blood based test are extremely impressive, and
hopefully the test becomes even more accurate in the future. Since this article
focused on the new methodology the PanSeer test used and their impressive
preliminary results I think it was appropriate to focus on measures such
as sensitivity and specificity. The purpose of this except was to highlight
how the prevalence of a disease has a huge impact on how we interpret the
results out in the wild. It is also important to note that PPV can be made
arbitrary low by decreasing the prevalence of a disease and that there is a
sort of paradox where even an extremely accurate (in terms of sensitivity and
specificity) test can have low PPV if the prevalence of the disease is also
very low.

I think the broader take away is that medical testing is inheritably,
mathematically difficult endeavour and disease prevalence should be
considered by patients and doctors when reviewing the results of any medical
test. 






