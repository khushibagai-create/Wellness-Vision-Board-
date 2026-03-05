# My Wellness Vision Board — Research Framework

**Document type:** UX Research Framework
**Author:** PM Research Team
**Date:** March 2026
**Status:** Ready for implementation
**Audience:** Khushi (PM), Founders (Saurabh, Trishala, Anshul)

---

## Overview

The "My Wellness Vision Board" tool serves two purposes simultaneously. Members receive a personalised wellness artifact they can save and share. Habuild receives structured research signal on which habits to build next in the product roadmap.

**Data fields captured:**
- `habits_selected` — array of up to 6 habit names chosen by the member
- `theme_chosen` — Energised / Grounded / Calm / Joyful
- `intention_text` — free-text (optional, max 60 chars)
- `q1_answer` — urgency signal: Just started / A few months / Over a year / I've tried before
- `q2_answer` — barrier signal: No time / I forget / No energy / Don't know how / No one to do it with
- `phone_number` — links to member profile (segment, tenure, attendance, paid/unpaid status)

---

## 1. Research Questions

### Primary Research Questions

| # | Research Question | Primary Data Signal | Secondary Signal |
|---|---|---|---|
| RQ1 | Which habit categories do members want beyond yoga? | `habits_selected` frequency distribution | `theme_chosen` correlation |
| RQ2 | Which habits do members feel most urgently unmet? | `q1_answer` = "Over a year" or "I've tried before" | `habits_selected` + `q1_answer` cross-tab |
| RQ3 | What is the primary barrier preventing members from building new habits? | `q2_answer` distribution | Segment x `q2_answer` cross-tab |
| RQ4 | Do habit preferences differ meaningfully by member segment? | `habits_selected` x phone_number → segment lookup | `theme_chosen` x segment |
| RQ5 | Are there distinct habit clusters members naturally group together? | Co-occurrence matrix of `habits_selected` | Segment-level cluster variation |
| RQ6 | What emotional state are members seeking beyond physical fitness? | `theme_chosen` distribution | `intention_text` thematic coding |
| RQ7 | What does the free-text intention reveal about unmet needs? | `intention_text` — NLP/thematic analysis | Correlation with habits_selected |

### Secondary Research Questions

| # | Research Question | Data Signal |
|---|---|---|
| SQ1 | Does attendance pattern correlate with habit ambition breadth? | habits_selected count x attendance rate from profile |
| SQ2 | Do unpaid members choose different habits than paying members? | habits_selected x paid/unpaid status |
| SQ3 | Are there regional habit preferences (India vs. Diaspora)? | habits_selected x location from profile |
| SQ4 | Does habit urgency differ between new vs. long-tenure members? | q1_answer x member tenure |
| SQ5 | Do theme preferences signal which product experience to serve first? | theme_chosen x session type preferences |

---

## 2. Analysis Framework

### 2.1 Habit Frequency Distribution

**What to calculate:** For each habit name, count how many members selected it. Express as a percentage of total respondents.

**What to look for:**
- Top 3 habits by frequency = highest demand signal. These are your "must-build" candidates.
- Bottom 3 habits = either low demand or poor labelling (test whether renaming increases selection in a future iteration).
- The gap between rank 1 and rank 5 matters. A steep drop-off means there is one clear winner. A flat distribution means demand is spread — build modular.

**Segmented frequency:** Run the same distribution separately for each member segment. A habit that ranks #1 overall but #6 for Working Professionals is not a reliable cross-segment build.

**Reporting format:**
```
Habit           | Overall % | Homemaker | Senior | Diaspora | Working Pro | Chronic Pain | YT Migrant
```

### 2.2 Habit Co-occurrence Analysis

**Purpose:** Find which habits members naturally bundle together. This reveals how they conceptualise their wellness day and guides feature packaging decisions.

**Method:**
1. For every pair of habits (A, B), calculate: how many members selected both?
2. Express as a percentage of everyone who selected A.
3. Build a co-occurrence matrix heatmap.

**What combinations mean:**

| Pattern | What it signals | Product action |
|---|---|---|
| Breathing + Meditation always together | Members see these as one category | Bundle into a single "Mind and Breath" tab |
| Nutrition + Movement together | Members want a full-day routine anchor | Consider a "Daily Routine Builder" |
| Pain relief always selected alone | Chronic Pain seekers have a single specific need | Dedicated condition-based track |
| Sleep + Breathing together | Evening wind-down demand is real | Confirms the pre-sleep product bet |

**Threshold for meaningful co-occurrence:** If habit B appears in >55% of sessions where habit A was selected, treat them as a natural bundle.

### 2.3 Segment Breakdown Methodology

**Segment definitions for this analysis:**

| Segment Label | CRM Filter |
|---|---|
| Committed Homemaker | Paid, India, Attendance >4x/week, Age 40–60 |
| Health-Driven Senior | Paid, India, Age 60+ |
| Indian Diaspora Woman | Paid, Outside India, Female |
| Working Professional | Paid, India, Attendance <3x/week, Age 30–50 |
| Chronic Pain Seeker | Tagged with condition OR selected Pain Relief habit in first session |
| YT-to-Habuild Migrant | Unpaid, joined <90 days ago |

**Minimum segment size for reportable findings:** 30 responses per segment. Below 30, flag as directional only.

**Analysis steps:**
1. Run all primary analyses at the overall level first.
2. Repeat for each segment.
3. Note where a segment deviates more than 15 percentage points from the overall average — these are the actionable insights.
4. Flag Diaspora insights separately as potential premium tier or international product signals.

### 2.4 Barrier Analysis (q2 Mapping)

| Barrier Selected | Root cause interpretation | Product opportunity |
|---|---|---|
| No time | Schedule doesn't accommodate the habit | In-app scheduling, short-format (<5 min) content |
| I forget | No environmental trigger or cue exists | Notification design, WhatsApp reminder personalisation |
| No energy | Habit feels too effortful at the moment they remember | Micro-habit versions, low-effort entry points |
| Don't know how | Confidence gap, not motivation gap | Onboarding content, starter sessions |
| No one to do it with | Accountability and social proof are missing | Community features, habit buddy pairing |

**Key cross-tab:** Barrier x Habit selected. If "No energy" is the top barrier for members who selected "Evening Meditation," the evening wind-down needs ultra-low-friction entry, not more content.

### 2.5 Urgency Scoring (q1 Mapping)

| Answer | Urgency interpretation | Prioritisation signal |
|---|---|---|
| Just started | Early aspiration, low frustration | Lower urgency |
| A few months | Growing want, mild frustration | Medium urgency |
| Over a year | Sustained unmet need, high frustration | High urgency |
| I've tried before | Maximum urgency — repeated failure | Highest priority |

**Urgency score formula per habit:**

```
Urgency Score = (% "Over a year" × 2 + % "I've tried before" × 3) / 5
```

This gives each habit a 0–100 urgency score. Use this to rank habits when frequency scores are close.

**Combined prioritisation matrix:**

```
                    HIGH URGENCY        LOW URGENCY
HIGH FREQUENCY   → Build now           → Build soon
LOW FREQUENCY    → Research more       → Deprioritise
```

---

## 3. Hypothesis Table

| # | Hypothesis | Data signal that confirms it | Data signal that rejects it |
|---|---|---|---|
| H1 | Breathing / Pranayama will be the most selected non-yoga habit across all segments | Breathing selected by >35% of total respondents | Breathing selected by <20%; another category leads |
| H2 | Evening/sleep habits will rank in the top 3 selections | Sleep, Meditation, or Breathing collectively selected by >40% | These three combined account for <25% of selections |
| H3 | Working Professionals will cite "No time" as their primary barrier more than any other segment | q2 = "No time" selected by >50% of Working Professional respondents | Another barrier leads for Working Pros |
| H4 | Chronic Pain Seekers will select fewer habit categories and cluster on condition-specific ones | Chronic Pain segment selects avg <2.5 habits; Pain Relief is top for >60% | Chronic Pain segment selects 4+ habits across categories |
| H5 | Diaspora members will show higher willingness to explore premium habits (journaling, nutrition) | Diaspora top-3 habits differ from India top-3; Journaling or Nutrition in Diaspora top 3 | Diaspora and India selections are nearly identical |
| H6 | Members who select 5–6 habits will show higher attendance rates | habit_count of 5–6 correlates with attendance >4x/week (r > 0.3) | No correlation between habit count and attendance |
| H7 | "Calm" will be the most chosen theme, reflecting stress as the primary unmet need | theme_chosen = Calm selected by >35% of respondents | "Energised" or another theme leads |
| H8 | Members with tenure >1 year will have higher urgency than new members | Among 12+ month tenure members, >55% select high-urgency q1 responses | Urgency distribution is flat across tenure groups |
| H9 | Unpaid members will select different habits than paid members | At least 2 habits rank in different positions (>10pp gap) between paid and unpaid | Paid and unpaid habit selections are nearly identical |
| H10 | "No one to do it with" will be least selected overall but highest among low-attendance members | Bottom-2 overall but top-2 barrier for members with <2x/week attendance | No correlation with attendance pattern |

---

## 4. Product Signal Mapping

### Move (dance, strength, walking challenges)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select a Move habit | Build a dedicated Move section. Pilot a 7-day walking challenge or dance session. |
| Moderate demand | 20–40% | Add a Move content tab to homescreen. Test a single format before committing. |
| Low demand | <15% | Do not prioritise. Revisit naming ("Active Play" vs. "Move"). |

### Breathe (pranayama, box breathing, breathing for sleep)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select a Breathe habit | Confirms the evening wind-down bet. Build a standalone Breathing module with 3–5 guided techniques. Ship next quarter. |
| Moderate demand | 20–40% | Add breathing content to end-of-session cooldown. Track engagement before building standalone. |
| Low demand | <15% | Audit whether the habit label was clear. Do not deprioritise without qualitative validation. |

### Eat (nutrition, hydration, mindful eating, juice fast)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select an Eat habit | Nutrition is a product line, not a feature. Explore a "Eat with Habuild" program. |
| Moderate demand | 20–40% | Add daily nutrition tips to post-session screen. Test a 5-day juice fast challenge. |
| Low demand | <15% | Members do not associate Habuild with nutrition yet. Light content-only integration. |

### Mind (meditation, journaling, gratitude, affirmations)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select a Mind habit | Build a Meditation section. Daily 5-min guided meditation at 9 PM is viable. |
| Moderate demand | 20–40% | Add a Yog Nidra session to the evening batch. Track if it becomes a retention driver. |
| Low demand | <15% | Test alternative labels ("Stress relief," "Calm") before deprioritising. |

### Body (pain relief, posture, mobility, condition-specific)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select a Body habit | Build condition-specific tracks: Knee Care, Back Relief, Cervical. Add onboarding flow for conditions. |
| Moderate demand | 20–40% | Add a "Therapeutic Yoga" content category to the session library. |
| Low demand | <15% | Pain relief may already feel covered by existing yoga sessions. No separate action needed. |

### Connect (community, accountability partner, family wellness, challenges)

| Signal | Threshold | Product action |
|---|---|---|
| High demand | >40% select a Connect habit | Community is an explicit product need. Build habit accountability features (buddy system, challenge leaderboards). |
| Moderate demand | 20–40% | Strengthen the WhatsApp community layer. Add in-app attendance sharing or streak visibility. |
| Low demand | <15% | Members may not frame accountability as a "habit." Do not cut community investment; re-examine the framing. |

---

## 5. Insight Report Template

### [REPORT TITLE]: My Wellness Vision Board — Research Findings
**Date:** [Month Year]
**Respondents:** [N] total / [N] paid members / [N] unpaid members
**Data collection period:** [Start date] to [End date]
**Prepared by:** Khushi, PM

---

#### Executive Summary (1 page, founder-ready)

**The one-line finding:**
[Single sentence capturing the most important product implication.]

**Top 3 action items for the roadmap:**
1. [Most critical build, with urgency score and % selecting it]
2. [Second build, with supporting data point]
3. [Third build or research follow-up]

**What surprised us:**
[1–2 findings that contradicted expectations. Be direct.]

**What confirmed our existing bets:**
[1–2 findings that validate decisions already in motion.]

---

#### Key Findings

**Finding 1: [Title]**
- Data: X% of respondents selected [habit]. Urgency score: [score]/100.
- Segment split: Strongest among [segment] ([X]%), weakest among [segment] ([X]%).
- Barrier: The top barrier for this habit is [q2 answer] ([X]%), suggesting the entry point must be [implication].
- Recommended action: [Specific product action]

[Repeat for 3–5 key findings]

---

#### Segment Breakdown

| Finding | Homemaker | Senior | Diaspora | Working Pro | Chronic Pain | YT Migrant |
|---|---|---|---|---|---|---|
| Top habit | | | | | | |
| Top barrier | | | | | | |
| Top theme | | | | | | |
| Avg habits selected | | | | | | |
| High urgency % | | | | | | |

---

#### Habit Priority Matrix

| Habit Category | Selection % | Urgency Score | Segment Spread | Recommended Action |
|---|---|---|---|---|
| [Category] | X% | X/100 | High / Medium / Low | Build / Pilot / Defer |

---

#### Barrier to Product Opportunity Summary

| Barrier | % Selected | Segment most affected | Product implication |
|---|---|---|---|
| No time | X% | [Segment] | [Action] |
| I forget | X% | [Segment] | [Action] |
| No energy | X% | [Segment] | [Action] |
| Don't know how | X% | [Segment] | [Action] |
| No one to do it with | X% | [Segment] | [Action] |

---

#### Intention Text — Thematic Analysis

**Top themes found:**
1. [Theme] — [X]% of non-empty responses — Example quotes: "[quote]"
2. [Theme] — [X]% — Example quotes: "[quote]"
3. [Theme] — [X]% — Example quotes: "[quote]"

**Unmet needs surfaced NOT in the current habit taxonomy:**
[List habit types members wrote about that were not in the structured options.]

---

#### Recommended Next Builds

**Quarter 1 priority:**
- Build: [Feature name]
- Rationale: [1–2 sentences, data-backed]
- Success metric: [How you will measure if it worked]

**Quarter 2 priority:**
- Build or pilot: [Feature name]
- Rationale: [1–2 sentences]
- Dependency: [Any dependency]

**Defer / Research more:**
- [Feature] — Reason: [Insufficient signal / contradictory data / needs qualitative follow-up]

---

#### Open Questions for Next Research Round

1. [Question this data raised but could not answer]
2. [Qualitative interview topic to validate a finding]
3. [A/B test to run based on a finding]

---

## 6. Sample Size and Confidence

### For habit frequency stats (overall level)

| Confidence need | Minimum N | Notes |
|---|---|---|
| Directional (±10pp margin of error) | 100 | Early product conversations only, not roadmap decisions |
| Moderate confidence (±5pp) | 385 | Suitable for roadmap prioritisation |
| High confidence (±3pp) | 1,067 | Required for large investment decisions |

**Recommendation:** Target 500 responses before presenting to founders. At 500, you achieve approximately ±4.4pp margin of error at 95% confidence. Sufficient for roadmap-level decisions.

### For segment-level findings

| Confidence need | Minimum N per segment | Notes |
|---|---|---|
| Directional only | 30 | Flag explicitly as directional |
| Reportable with caveats | 50 | Acceptable for segment-level insights |
| Reliable segment finding | 100 | Required to claim a segment-specific pattern |

### For co-occurrence analysis

Minimum 200 responses needed before running co-occurrence analysis. A co-occurrence rate of >55% is meaningful at 200+.

### When to draw roadmap conclusions

| Decision type | Minimum evidence required |
|---|---|
| Add a content category to the app | 500 total, habit at >25% selection rate |
| Build a standalone feature | 500 total, habit at >35% + urgency score >60 + in top 3 for 2+ segments |
| Commission a new product line | 1,000+ total, category at >40% + confirmed across 4+ segments |
| Deprioritise a habit category | <15% selection across 500+ AND confirmed low urgency |

---

## 7. Ethical Considerations

- Add consent line at login: "By completing this vision board, you agree to Habuild using your responses to improve our product. Your data is private and will never be sold." — in English and Hindi.
- Store raw responses (phone + intention text) in restricted-access database. PM, analyst, and founding team only.
- Intention text may contain sensitive health/emotional information — handle like support ticket data.
- All reports use aggregated data only. No identifiable quotes without explicit consent.
- Do not present data from segments with fewer than 10 respondents.
- Build data deletion capability before launch (DPDPA 2023 compliance).

---

## Appendix: Quick Reference

**5 questions to answer from this data:**
1. What habit should we build next? → Frequency x Urgency Score matrix
2. Who most needs it? → Segment breakdown of top habits
3. Why haven't they built it already? → q2 barrier analysis
4. How long have they wanted it? → q1 urgency distribution
5. What emotional outcome are they seeking? → theme_chosen + intention_text

**3 numbers to lead with in the founder presentation:**
1. Top habit selected (% and urgency score)
2. Top barrier (% and what product fix it implies)
3. Strongest segment-habit pairing

**Red flags in the data:**
- Top habit at <20% — demand too fragmented, no single clear build
- q2 answers evenly distributed — run qualitative interviews before building
- Segment N below 30 for any finding you are presenting as a conclusion
- High selection + low urgency (q1 = "Just started") — aspiration without urgency; build awareness, not product

---

*Review and update after the first 500 responses are collected.*
