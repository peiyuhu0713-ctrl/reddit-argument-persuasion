# reddit-argument-persuasion
NLP analysis of argument types and persuasion in r/science · PRAW · VADER · Mann-Whitney U · Gephi

**Research Question**: Do evidence-based arguments receive more community 
approval (measured by upvotes) than emotion-based arguments in scientific 
online discussions?

**Context**: Master's project analysing argumentation patterns in r/science 
using computational methods.

---

## Methods

| Step | Tool | Purpose |
|------|------|---------|
| Data collection | PRAW (Reddit API) | Scrape comments from r/science hot posts |
| Argument classification | Rule-based NLP (regex + VADER) | Label comments as evidence-based / emotion-based |
| Hypothesis testing | Mann-Whitney U, Bootstrap CI | Test whether argument type predicts upvote score |
| Regression analysis | OLS (statsmodels) | Control for comment length, thread depth, sentiment |
| Network analysis | NetworkX → Gephi | Map user interaction structure and community clusters |
| Text visualisation | WordCloud | Surface dominant themes in comment corpus |

---

## Dataset

- **Source**: r/science, post ID `12b3qwq`
- **Total comments scraped**: 356
- **Classified comments**: 98 (50 evidence-based, 48 emotion-based)
- **Excluded as neutral**: 258 (insufficient signal in either direction)

---

## Key Findings

**Hypothesis not supported** at α = 0.05 with the current dataset.

| Test | Result | Interpretation |
|------|--------|----------------|
| Mann-Whitney U | U = 972, p = 0.9517 | No significant difference in score distributions |
| Effect size | Rank-biserial r = 0.190 (small) | Negligible practical difference |
| OLS regression (full model) | β = −0.169, p = 0.4691 | Effect disappears after controlling for confounds |
| Bootstrap 95% CI | [−0.6, 0.3] | Interval includes 0, direction unreliable |

Sentiment analysis showed r/science comments skew **neutral to positive**, 
consistent with the subreddit's evidence-first community norms.  
Network analysis revealed **clustered discussion patterns** around a small 
number of high-engagement users (see `/gephi`).

---

## Why the Hypothesis Was Not Confirmed

Three plausible explanations, each worth further investigation:

1. **Selection bias** — r/science moderators enforce sourcing rules, 
   pre-filtering low-quality emotional comments before they enter the dataset. 
   This compresses variance between groups.

2. **Insufficient statistical power** — 98 classified samples from a single 
   post. A power analysis suggests ~300 classified comments are needed to 
   detect a small effect (r ≈ 0.2) at 80% power.

3. **Proxy validity** — Upvote count reflects visibility and timing as much 
   as argument quality. A more direct persuasion measure (e.g. delta awards 
   in r/changemyview) may be more appropriate.

---

## Limitations & Future Work

- [ ] Expand dataset to 10–20 posts (target ≥ 1,000 raw comments)  
- [ ] Replace rule-based classifier with fine-tuned BERT for argument mining  
- [ ] Add inter-rater reliability check (Cohen's κ) on classifier labels  
- [ ] Replicate in r/changemyview where persuasion outcomes are explicitly marked  
- [ ] Complete Gephi community detection and integrate with argument type analysis  

---

## Setup

```bash
git clone https://github.com/peiyuhu0713-ctrl/reddit-argument-persuasion.git
cd reddit-argument-persuasion

pip install -r requirements.txt

cp .env.example .env
# Open .env and fill in your Reddit API credentials
```

Run notebooks in order: `01` → `02`

Reddit API credentials can be obtained free at: 
https://www.reddit.com/prefs/apps

---

## References

- Toulmin, S. (1958). *The Uses of Argument*. Cambridge University Press.
- Tan, C., Niculae, V., Danescu-Niculescu-Mizil, C., & Lee, L. (2016). Winning arguments: Interaction dynamics and persuasion strategies in good-faith online discussions. *Proceedings of WWW 2016*.
- Priniski, J. H., & Horne, Z. (2018). Attitude change on Reddit's ChangeMyView. *Proceedings of CogSci 2018*.
- Hutto, C. J., & Gilbert, E. (2014). VADER: A parsimonious rule-based model for sentiment analysis of social media text. *Proceedings of ICWSM 2014*.

---

## Tools

`Python` · `PRAW` · `VADER` · `scipy` · `statsmodels` · `NetworkX` · `Gephi` · `WordCloud`
