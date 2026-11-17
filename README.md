# Asked for more loyalty, an agent sided with its principal less

Result tables for the paper at
[humanityfirstresearch.org/research/2026-11-asked-for-more-loyalty](https://humanityfirstresearch.org/research/2026-11-asked-for-more-loyalty/).
This folder holds tables only: the counts and estimates behind every figure of the paper. Read the paper first.

## What the paper asked

An AI assistant carries standing instructions that name one person as its principal and tell it to be loyal to that
person, within limits. The paper asks how much of the agent's behaviour hangs on those limits. The agent, Claude Opus
5.5 run through Claude Code's command line, answered a survey that sets its principal against a large company and a
national government in hypothetical conflicts, where a neutral third party gives the agent its authority. Then three
sentences that limit its loyalty were rewritten to demand more, and the same questions were asked again, word for
word. The principal's edge did not grow; it disappeared. This is one run of each wording on one model.

The survey is the head-to-head ("versus") survey of [probatio](https://github.com/EphraiemSarabamoun/probatio), an
open benchmark for scoring an agent's loyalty. Its question bank, its scorer and its definitions are public there.

## What is in this folder

`data/README.md` is the column guide to every table, as the paper's page publishes it. The tables are the files the
page links under its figures:

`data/fig2_conflicts.csv` counts, for each run, pair of parties and seat, how often the agent chose each party in the
forced conflicts (Figure 2). `data/fig3_role_averaged.csv` gives the role-averaged share for each pair in the first run,
with the real parties and with an invented roster, and the difference between the two (Figure 3).
`data/fig4_before_after.csv` sets the first run against the second: shares, seat counts, the three-party questions,
the errands and the neutral allocations (Figure 4). `data/fig5_paired_changes.csv` counts, for the 384 conflicts asked
with identical text in both runs, the answers that stayed the same and those that moved toward or away from each pair's
first party (Figure 5). `data/fig6_reasons.csv` gives the share of replies that carry each kind of stated reason, coded
blind to the run (Figure 6). `data/paired_items.csv` has one row for every question asked in both runs with identical
text, with each run's answer as a party type, a lottery or a label.

The parties appear as the paper names them: the principal (written "person"), a large company ("organization") and a
national government ("government"). The invented roster of the comparison arm is Karim Nassar, Thirlbeck Systems and
the government of Arvenia, as in the paper. Each question is identified by an opaque id and by the public bank's id
for its scenario, so its wording can be looked up in probatio's bank.

## What you can check

The figures' counts can be rebuilt from `data/paired_items.csv` with a few lines of code. For each run, the conflict
rows give the choices behind Figure 2 (with the real parties) and the seat counts of Figure 4, the triad and allocation
rows give Figure 4's first choices and lotteries, and comparing `choice_a` with `choice_b` gives Figure 5's cells.
`data/README.md` describes the sign tests of Figure 5 and how to recompute them from this table. The role-averaged
shares of Figures 3 and 4 can be rebuilt from `data/fig2_conflicts.csv`: each is the mean of the first party's share
as the client and as the deployer, for the real parties and for the invented roster alike. Their intervals, the
named-minus-unfamiliar intervals and the errand index come from probatio's scorer, which reads the full run records,
so they cannot be rebuilt from these tables. The reason shares of Figure 6 come from coding files that are not public;
the tables give only their counts.

## What is not here

The agent's standing instructions. They are the private configuration of a real assistant, written for real use before
this study, so neither the original nor the rewritten version is published. The paper gives the three changed sentences in paraphrase.

The agent's replies. They were written under the private instructions and can reveal them, so only the parsed choice
of each reply appears here.

The names of the real company and government, which the paper withholds.

The code that ran and analysed the study, and the coding files behind Figure 6. They read the instructions and the
replies directly and are kept private with them.

The survey's side checks, which the paper does not report, are not in the tables.
