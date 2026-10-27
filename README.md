# Problem-Set-2-Econ_3916_PS2.ipynb
# Problem Set 2: The Survey That Wasn't Random

ECON 3916 · Applied Data Analytics · Fall 2026

**Notebook:** [Econ_3916_PS2.ipynb](Econ_3916_PS2.ipynb)

## The question

After an onboarding redesign, the in-app satisfaction survey rose from 3.6 to 4.3 out of 5. The PM's slide said "the redesign worked." I checked whether the survey actually supports that.

## What I did

- **Simulated** 50,000 users per period with a known true improvement of 0.10 points, and a response mechanism where happier users are more likely to answer.
- **Reproduced the PM's numbers:** respondents averaged 3.60 before and 4.30 after, a 0.70 gap, while the true gap was only 0.10. Response rates fell from 27% to 15%.
- **Bootstrapped** intervals by hand and with `scipy.stats.bootstrap`, then ran a **coverage simulation**. Intervals work on random samples but cover the truth 0% of the time on the self-selected survey.
- **Power analysis:** detecting a 0.10 improvement needs about 1,236 respondents per period. A simulation showed that a bigger survey only makes the wrong answer more precise.
- **Inverse-probability weighting** (with AI assistance): weighting on engagement and support tickets removed only about 4% of the bias, because response depends on satisfaction itself.

## Rewritten slide

**Onboarding redesign: what the survey can and can't tell us**

- **Supported:** people who answered after the redesign rated it higher: 4.30 vs 3.60, a gap of **+0.70 points (95% CI 0.68 to 0.73)**.
- **Not supported:** that users got 0.70 points happier. Response fell from 27% to 15%, and mostly happy users answered. In a simulation matching our survey, a true +0.10 shows up as +0.70.
- Adjusting for engagement and tickets barely changes it (0.70 → 0.68).
- **Fix:** survey a random sample of about 1,250 users per period and follow up with non-responders until most answer.
