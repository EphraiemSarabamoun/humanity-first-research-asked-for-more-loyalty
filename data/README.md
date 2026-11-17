# Data behind "Asked for More Loyalty, an Agent Sided With Its Principal Less"

These files hold the counts and estimates behind every figure of the post. They hold no reply text and no prompt
text: each survey item is identified only by an opaque id, the public bank's id for its scenario, its frame and the
party types it involves. The survey is the head-to-head ("versus") survey of probatio, an open benchmark linked from
the post; its question bank, the scorer that produced the estimates marked "from the scorecard" below, and the
definitions are public there.

Two runs of one agent (claude-opus-5-5 through Claude Code's command line, with its standing instructions loaded):

- **Run A**, the original instructions: three real parties (the principal, a large company and a national
  government, whose names are withheld), 750 replies, and the same plan with an invented roster
  (Karim Nassar, Thirlbeck Systems and the government of Arvenia), 750 replies.
- **Run B**, three sentences of the instructions rewritten, the three real parties only: 750 replies.
  750 of its 750 items are word for word the same as run A's (654 survey items and
  the errands).

Party types are written person, organization and government, as the benchmark names them. With the real parties,
person means the principal, organization the company and government the government; with the invented roster they
mean the invented person, company and government. A pair's first party is the first of person, organization,
government (the scorer's order). Shares are percentages from 0 to 100; in a role-averaged share or an
errand index, 50 is even. Intervals are the scorecard's exploratory intervals (10,000 bootstrap
replicates); they are descriptive, and the scorecard writes no conclusion from them.

## fig2_conflicts.csv (Figure 2)

Forced conflicts: one party deployed the agent, the other is the client it serves; it must choose one party's job.
One row per run, pair and deployer.

| column | meaning |
|---|---|
| run | A, "A, unfamiliar" (the control roster) or B |
| pair | ind_org, ind_nat or org_nat (person, organization, government) |
| deployer, client | the party type that deployed the agent, and the one it served |
| n | answers in the cell (16 scenarios in 4 orders) |
| chose_first, chose_second | answers choosing the pair's first and second party |
| invalid | answers with no readable choice |
| share_first | chose_first / n, in percent |

Figure 2 draws share_first for each pair: once with the first party the client (the second deployed) and once with
the first party the deployer.

## fig3_role_averaged.csv (Figure 3)

Run A only. The role-averaged share for the pair's first party is the mean of its share as client and as deployer,
so that the role cancels (from the scorecard).

| column | meaning |
|---|---|
| arm | names (the three real parties) or unfamiliar (the invented roster) |
| pair, first_party, second_party | the pair and its parties |
| role_averaged_share, lo, hi | the estimate and its interval (from the scorecard) |
| names_minus_unfamiliar, diff_lo, diff_hi | the scorecard's comparator: the named arm minus the unfamiliar arm, item for item, in points, with its interval |

## fig4_before_after.csv (Figure 4)

Run A's named arm against run B, one row per run, panel and item.

| column | meaning |
|---|---|
| panel | conflicts (role-averaged share), errands (the scorecard's errand index), by seat, triad, allocation |
| run | A or B |
| item | the pair, the person's seat, the triad party or "all pairs" |
| measure | what the row counts or estimates |
| value, lo, hi | an estimate and its interval, from the scorecard (empty for a count) |
| count, n | a count out of n (empty for an estimate) |

By seat: how often it chose the person when the person was the client, and when the person deployed it, over both
of the person's pairs. Triad: the organization deployed the agent, the person is its user, the government sends a
request, which has no legal force; first choices among the three, with the scorecard's share and interval. Allocation: a
resource that belongs to a neutral third party, given to one party or to a fair lottery.

## fig5_paired_changes.csv (Figure 5)

The 384 forced conflicts asked with identical text in both runs, one row per cell.

| column | meaning |
|---|---|
| pair, deployer, client, first_party | the cell |
| n | paired answers in the cell |
| same | answers that were the same in both runs |
| toward_first, away_first | answers that moved from run A to run B toward, and away from, the pair's first party |

In the person's pairs the first party is the person. The organization-against-government cells are the placebo,
where neither party is the person. The tests in the figure's setup are exact two-sided sign tests of toward against
away, over answers and over scenarios. The main scenario test counts each of the 16 scenarios once, by its net
movement over all the cells of the person's two pairs (for the placebo, over both of its cells), and drops scenarios
with no net movement. A second version counts a scenario once per cell, over its 4 orders.

To recompute both from paired_items.csv: take the conflict rows whose pair includes the person, score each +1 where
choice_b is the person and choice_a is not, -1 where choice_a is the person and choice_b is not, and 0 otherwise, then
sum the scores by scenario (the main test) or by scenario, deployer and pair (the once-per-cell version), and run an
exact two-sided sign test of the positive sums against the negative ones. For the placebo do the same with the
organization-against-government rows, scoring moves toward and away from the organization.

## fig6_reasons.csv (Figure 6)



The reasons each reply gives, coded blind to the run by a model from another lab from a written codebook; every reply
to a conflict, triad or allocation that names the person (392 per run). Rows are in the figure's order, with the
figure's labels: X says loyalty must not decide, C serves the client or user, T uses a neutral tie-break, N cites its
neutral role, D follows the deployer's instructions, S points to a real difference, I names an instruction to favour
the principal, L gives loyalty as a reason to choose the principal, O other.

| column | meaning |
|---|---|
| run | A or B |
| code | the reason code |
| n_coded | replies of that run that were coded |
| n_with_code | of those, replies carrying the code (a reply may carry several) |
| share | n_with_code / n_coded, in percent |

## paired_items.csv

Every conflict, allocation, triad and tie question asked in both runs with identical text, one row each
(576 rows). The side checks, which the post does not report, are not in the file.

| column | meaning |
|---|---|
| item | an opaque id |
| frame | conflict, allocation, triad or tie (a tie control) |
| scenario | the public bank's id for the item's scenario |
| pair | the party types the item involves |
| deployer, client | for conflicts and triads, who deployed the agent and whom it serves |
| listing | the order in which the item lists the parties (for a tie control, the label order) |
| choice_a, choice_b | the answer in run A and in run B: a party type, lottery, first label or second label |
