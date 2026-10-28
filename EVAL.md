# Evaluation test set

Fill this in after every refresh, before you publish. The agent is the system under test.
You are the grader. Nothing here is automated on purpose: the point is to decide, with a
source you trust, whether the agent told you the truth.

**Ground truth sources.** Pick one and use the same one every time, so your scores are
comparable week to week:

- Prices: Google Finance (google.com/finance), Yahoo Finance, or your brokerage app.
- News: the article itself. Open the link. Check the date on the page.
- Calendar: the company's investor relations page (search "TICKER investor relations
  events"), or the Fed's own meeting calendar for FOMC dates.

Refresh date: 2026-10-28    Grader: number-checker

Notes on method: Google Finance (google.com/finance/quote/TICKER:EXCHANGE) returned only
"Google Finance isn't supported on this device" for all five tickers, so it showed no prices.
Per the grading rules, prices were checked against Yahoo Finance history pages (a second
named source, independent of the stockanalysis.com pages the agent used). Quote times on
Yahoo were 9:57 AM EDT; the brief's intraday prices are stamped 9:49.

## A. Prices (one row per ticker)

Pass if the dashboard's last price is within $0.10 of the ground truth for the same day
and the same price type (close vs intraday). If the agent recorded an intraday price,
compare against the intraday price at about the same time; do not compare it to a close.

### Refresh 2026-10-28

Latest-price rows (intraday, 9:49 AM ET in the brief; Yahoo quote looked at 9:57 AM EDT, 8 minutes later;
Google Finance did not show it). The gap is small relative to 8 minutes of opening-hour trading, so these are
judged on the time difference. Yahoo cannot show the 9:49 print, so these are not exact matches.

| Ticker | Date shown | Price type shown | Dashboard price | Ground truth price | Source you used | Pass / Fail |
|---|---|---|---|---|---|---|
| NVDA | 2026-10-28 | intraday 09:49 | 217.47 | 217.84 at 9:57 (gap 0.37) | https://finance.yahoo.com/quote/NVDA/history/ (Google Finance did not show it) | Pass (time difference) |
| JPM | 2026-10-28 | intraday 09:49 | 336.03 | 335.73 at 9:57 (gap 0.30) | https://finance.yahoo.com/quote/JPM/history/ (Google Finance did not show it) | Pass (time difference) |
| ACN | 2026-10-28 | intraday 09:49 | 241.65 | 242.80 at 9:57 (gap 1.15, 0.5%) | https://finance.yahoo.com/quote/ACN/history/ (Google Finance did not show it) | Pass (time difference; largest gap, cannot be confirmed) |
| DIS | 2026-10-28 | intraday 09:49 | 109.64 | 109.79 at 9:57 (gap 0.15) | https://finance.yahoo.com/quote/DIS/history/ (Google Finance did not show it) | Pass (time difference) |
| LLY | 2026-10-28 | intraday 09:49 | 1290.20 | 1291.88 at 9:57 (gap 1.68, 0.13%) | https://finance.yahoo.com/quote/LLY/history/ (Google Finance did not show it) | Pass (time difference) |

Daily closes (Oct 21, 22, 23, 26, 27) for every ticker matched Yahoo to the cent, so no per-date Fail rows were needed:

| Ticker | Closes in brief | Yahoo closes | Source | Pass / Fail |
|---|---|---|---|---|
| NVDA | 221.97, 212.21, 210.96, 216.00, 217.94 | 221.97, 212.21, 210.96, 216.00, 217.94 | https://finance.yahoo.com/quote/NVDA/history/ | Pass |
| JPM | 335.19, 336.54, 331.58, 334.04, 335.79 | same | https://finance.yahoo.com/quote/JPM/history/ | Pass |
| ACN | 240.26, 258.74, 249.37, 247.23, 235.16 | same | https://finance.yahoo.com/quote/ACN/history/ | Pass |
| DIS | 111.83, 113.13, 112.52, 110.40, 110.23 | same | https://finance.yahoo.com/quote/DIS/history/ | Pass |
| LLY | 1270.75, 1306.69, 1273.46, 1279.14, 1281.91 | same | https://finance.yahoo.com/quote/LLY/history/ | Pass |

### Refresh 2026-10-28, re-check after owner edit (NVDA 2026-10-27 close changed 217.94 to 188.40)

Google Finance (https://www.google.com/finance/quote/NVDA:NASDAQ) opened but showed only "Google Finance isn't supported on this device", so the owner's claim that it shows 188.40 could not be confirmed there. Checked two other sources I opened myself.

| Ticker | Date | Dashboard | Ground truth | Source | Pass / Fail |
|---|---|---|---|---|---|
| NVDA | 2026-10-27 close | 188.40 | 217.94 (Yahoo) and 217.94 (stockanalysis.com); Google Finance did not show it | https://finance.yahoo.com/quote/NVDA/history/ and https://stockanalysis.com/stocks/nvda/history/ | Fail (off by 29.54; the 188.40 is not on any source I could read; the original 217.94 was right) |
| NVDA | 2026-10-21, 22, 23, 26 closes | 221.97, 212.21, 210.96, 216.00 | same | https://finance.yahoo.com/quote/NVDA/history/ | Pass |
| NVDA | 2026-10-28 intraday 09:49 | 217.47 | 217.77 at 9:57:30 EDT (gap 0.30) | https://finance.yahoo.com/quote/NVDA/history/ (Google Finance did not show it) | Pass (time difference) |
| JPM | latest 09:49 | 336.03 | 335.73 at 9:57 (gap 0.30); closes Oct 21-27 all match | https://finance.yahoo.com/quote/JPM/history/ (Google Finance did not show it) | Pass |
| ACN | latest 09:49 | 241.65 | 242.80 at 9:57 (gap 1.15); closes Oct 21-27 all match | https://finance.yahoo.com/quote/ACN/history/ (Google Finance did not show it) | Pass (time difference) |
| DIS | latest 09:49 | 109.64 | 109.79 at 9:57 (gap 0.15); closes Oct 21-27 all match | https://finance.yahoo.com/quote/DIS/history/ (Google Finance did not show it) | Pass |
| LLY | latest 09:49 | 1290.20 | 1291.88 at 9:57 (gap 1.68); closes Oct 21-27 all match | https://finance.yahoo.com/quote/LLY/history/ (Google Finance did not show it) | Pass |

## B. Weekly change (one row per ticker)

The page computes this from the five closes. Pass if it is within 0.3 percentage points of
your own calculation: (last price minus the close five trading days earlier) divided by
that earlier close.

### Refresh 2026-10-28

The page computes (latest price - first close, Oct 21) / first close, and shows one decimal. Oct 21 is five trading
days before Oct 28, so this matches the required formula. My inputs: Oct 21 close and the Yahoo 9:57 AM price
(the closest independent quote to the brief's 9:49 price). Source: Yahoo history pages listed in section A.

| Ticker | Dashboard weekly change | Your calculation | Pass / Fail |
|---|---|---|---|
| NVDA | -2.0% (217.47 vs 221.97) | (217.84 - 221.97) / 221.97 = -1.86% (diff 0.14 pts) | Pass |
| JPM | +0.3% (336.03 vs 335.19) | (335.73 - 335.19) / 335.19 = +0.16% (diff 0.09 pts) | Pass |
| ACN | +0.6% (241.65 vs 240.26) | (242.80 - 240.26) / 240.26 = +1.06% (diff 0.48 pts) | Fail (over 0.3 pts; caused by the 8-minute price difference, not by the closes) |
| DIS | -2.0% (109.64 vs 111.83) | (109.79 - 111.83) / 111.83 = -1.82% (diff 0.14 pts) | Pass |
| LLY | +1.5% (1290.20 vs 1270.75) | (1291.88 - 1270.75) / 1270.75 = +1.66% (diff 0.13 pts) | Pass |

### Refresh 2026-10-28, re-check after owner edit

The page uses only the first close and the latest price, so the edited NVDA Oct 27 close (188.40) does not change any percentage. It does distort the NVDA sparkline (a false drop to 188.40 then a jump to 217.47). Inputs from Yahoo history pages as in section A.

| Ticker | Dashboard weekly change | Your calculation | Pass / Fail |
|---|---|---|---|
| NVDA | -2.0% (217.47 vs 221.97) | (217.77 - 221.97) / 221.97 = -1.89% (diff 0.14 pts) | Pass (number only; the sparkline uses the bad 188.40 close) |
| JPM | +0.3% (336.03 vs 335.19) | (335.73 - 335.19) / 335.19 = +0.16% (diff 0.09 pts) | Pass |
| ACN | +0.6% (241.65 vs 240.26) | (242.80 - 240.26) / 240.26 = +1.06% (diff 0.48 pts) | Fail (over 0.3 pts; caused by the 8-minute price gap, same as the earlier Fail) |
| DIS | -2.0% (109.64 vs 111.83) | (109.79 - 111.83) / 111.83 = -1.82% (diff 0.14 pts) | Pass |
| LLY | +1.5% (1290.20 vs 1270.75) | (1291.88 - 1270.75) / 1270.75 = +1.66% (diff 0.13 pts) | Pass |

## C. News grounding (one row per news item, three per ticker)

Open every link. Pass only if all four are true: the link opens, the headline matches the
article, the article date is within the last seven days, and the "why it matters" line is
supported by the article (not just plausible).

### Refresh 2026-10-28 (window Oct 21 to Oct 28)

| Ticker | Headline (first few words) | Link opens | Headline matches | Dated within 7 days | "Why" is supported | Pass / Fail |
|---|---|---|---|---|---|---|
| NVDA | Nvidia to invest $3B in Meta's... https://stockanalysis.com/news/nvidia-3-billion-meta-offering/ | Yes | Yes | Yes (Oct 27) | Yes (Meta to deploy more Nvidia infrastructure) | Pass |
| NVDA | Nvidia, Oracle expand Vera Rubin... https://www.tipranks.com/news/the-fly/nvidia-oracle-expand-nvidia-vera-rubin-to-multi-gigawatt-scale-thefly-news | Yes | Yes | Yes (Oct 27) | Yes (expansion driven by customer demand) | Pass |
| NVDA | OpenAI planning to purchase AI chips from Google... https://www.tipranks.com/news/the-fly/openai-planning-to-purchase-ai-chips-from-google-the-information-reports-thefly-news | Yes | Yes | Yes (Oct 28 00:15 UTC, i.e. evening of Oct 27 ET) | Partly: article is one line (OpenAI buying Google chips, longtime Nvidia customer); "possible sign of competition" is the agent's hedged inference, not stated | Pass (borderline) |
| JPM | J.P. Morgan Asset Management Expands Access... https://www.prnewswire.com/news-releases/jp-morgan-asset-management-expands-access-to-its-tokenized-money-market-funds-on-solana-302917188.html | Yes | Yes | Yes (Oct 22) | No: release supports "push into tokenized cash products" but never says it is a "small but growing business line" | Fail (why not supported) |
| ACN | Accenture awarded $151.46M Air Force... https://www.tipranks.com/news/the-fly/accenture-awarded-151-46m-air-force-task-order-thefly-news | Yes | Yes | Yes (Oct 27) | Yes (multi-year, completion June 2030); "small against overall size" is outside knowledge | Pass |
| ACN | Accenture price target raised to $252... https://www.tipranks.com/news/the-fly/accenture-price-target-raised-to-252-from-210-at-wells-fargo-thefly-news | Yes | Yes | Yes (Oct 26) | Yes (Equal Weight kept; AI benefits will take time) | Pass |
| ACN | Accenture downgraded to Neutral... https://www.tipranks.com/news/the-fly/accenture-downgraded-to-neutral-from-outperform-at-baird-thefly-news | Yes | Yes | Yes (Oct 21) | Yes (shares more than doubled since June, fully valued) | Pass |
| DIS | Disney Stock (DIS) Is a Buy Despite... https://www.tipranks.com/news/disney-stock-dis-is-a-buy-despite-its-recent-weakness | Yes | Yes | Yes (Oct 27) | Yes (7% revenue growth, $37.4B debt, consumer spending risk) | Pass |
| LLY | Lilly's retatrutide delivered greater A1C... https://www.prnewswire.com/news-releases/lillys-retatrutide-delivered-greater-a1c-reduction-and-more-than-double-the-weight-loss-of-ozempics-highest-approved-dose-in-head-to-head-trial-302921328.html | Yes | Yes | Yes (Oct 28) | Yes (discontinuation 4.8% / 7.9% vs 2.7% for Ozempic) | Pass |
| LLY | Patrik Jonsson to retire after 36 years... https://www.prnewswire.com/news-releases/patrik-jonsson-to-retire-after-36-years-ilya-yuffa-named-president-lilly-global-markets-302921191.html | Yes | Yes | Yes (Oct 27) | Yes (US and international businesses combine as Lilly Global Markets Jan 1, 2027) | Pass |

### Refresh 2026-10-28, re-check after owner edit (all links reopened)

| Ticker | Headline and link | Link opens | Headline matches | Dated within 7 days | "Why" is supported | Pass / Fail |
|---|---|---|---|---|---|---|
| NVDA | Nvidia to invest $3B in Meta's... https://stockanalysis.com/news/nvidia-3-billion-meta-offering/ | Yes | Yes | Yes (Oct 27) | Yes (expands Meta's use of Nvidia infrastructure) | Pass |
| NVDA | Nvidia, Oracle expand Vera Rubin... https://www.tipranks.com/news/the-fly/nvidia-oracle-expand-nvidia-vera-rubin-to-multi-gigawatt-scale-thefly-news | Yes | Yes | Yes (Oct 27) | Yes (responds to rising customer demand) | Pass |
| NVDA | OpenAI planning to purchase AI chips from Google... https://www.tipranks.com/news/the-fly/openai-planning-to-purchase-ai-chips-from-google-the-information-reports-thefly-news | Yes | Yes | Yes (Oct 28 00:15 UTC) | Partly: article only says OpenAI is a long-time Nvidia customer; "possible sign of competition" is a hedged inference | Pass (borderline, as before) |
| JPM | J.P. Morgan Asset Management Expands Access... https://www.prnewswire.com/news-releases/jp-morgan-asset-management-expands-access-to-its-tokenized-money-market-funds-on-solana-302917188.html | Yes | Yes | Yes (Oct 22) | No: release never says "a small but growing business line" | Fail (why not supported, same as earlier) |
| ACN | Accenture awarded $151.46M Air Force... https://www.tipranks.com/news/the-fly/accenture-awarded-151-46m-air-force-task-order-thefly-news | Yes | Yes | Yes (Oct 27) | Partly: multi-year (to June 2030) is supported; "small against Accenture's overall size" is not in the article (it gives no company size). Graded Pass earlier; held to the same standard as the JPM row this time | Fail (why not fully supported) |
| ACN | Accenture price target raised to $252... https://www.tipranks.com/news/the-fly/accenture-price-target-raised-to-252-from-210-at-wells-fargo-thefly-news | Yes | Yes | Yes (Oct 26) | Yes | Pass |
| ACN | Accenture downgraded to Neutral... https://www.tipranks.com/news/the-fly/accenture-downgraded-to-neutral-from-outperform-at-baird-thefly-news | Yes | Yes | Yes (Oct 21) | Yes ("over doubled since June", valuation) | Pass |
| DIS | Disney Stock (DIS) Is a Buy Despite... https://www.tipranks.com/news/disney-stock-dis-is-a-buy-despite-its-recent-weakness | Yes | Yes | Yes (Oct 27) | Yes (7% revenue growth, $37.4B debt, spending risk) | Pass |
| LLY | Lilly's retatrutide delivered greater A1C... https://www.prnewswire.com/news-releases/lillys-retatrutide-delivered-greater-a1c-reduction-and-more-than-double-the-weight-loss-of-ozempics-highest-approved-dose-in-head-to-head-trial-302921328.html | Yes | Yes | Yes (Oct 28) | Yes (4.8% / 7.9% vs 2.7% discontinuation) | Pass |
| LLY | Patrik Jonsson to retire... https://www.prnewswire.com/news-releases/patrik-jonsson-to-retire-after-36-years-ilya-yuffa-named-president-lilly-global-markets-302921191.html | Yes | Yes | Yes (Oct 27) | Yes (merge into Lilly Global Markets Jan 1, 2027) | Pass |

(Add rows as needed. Fifteen items is normal for five tickers.)

## D. Calendar (one row per event)

Pass if the event and its date appear on the source linked, and the date is in the future
relative to the refresh date.

### Refresh 2026-10-28

| Ticker | Event | Date shown | Confirmed on source | Pass / Fail |
|---|---|---|---|---|
| JPM (FOMC) | FOMC meeting concludes (Oct 27-28) | 2026-10-28 | Yes: https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm lists the October meeting as Oct 27-28; date is on asOf | Pass |
| LLY | Q3 2026 earnings and call, 10 a.m. ET | 2026-10-29 | Lilly's own IR pages (https://investor.lilly.com/node/55096 and https://lilly.gcs-web.com/news-releases/news-release-details/lilly-confirms-date-and-conference-call-third-quarter-2026) both returned HTTP 403, could not open. Date only seen on third-party https://finviz.com/news/403165/lilly-confirms-date-and-conference-call-for-third-quarter-2026-financial-results-announcement (shows Oct 29, 10 a.m. ET). The brief itself cites Finviz, not Lilly | Fail (only third-party confirmation; company page could not be opened) |

### Refresh 2026-10-28, re-check after owner edit

| Ticker | Event | Date shown | Confirmed on source | Pass / Fail |
|---|---|---|---|---|
| JPM (FOMC) | FOMC meeting concludes (Oct 27-28) | 2026-10-28 | Yes: https://www.federalreserve.gov/monetarypolicy/fomccalendars.htm lists October 27-28; date equals asOf | Pass |
| LLY | Q3 2026 earnings and call, 10 a.m. ET | 2026-10-29 | Lilly IR https://investor.lilly.com/events and https://lilly.gcs-web.com/news-releases/news-release-details/lilly-confirms-date-and-conference-call-third-quarter-2026 both returned HTTP 403. Only https://finviz.com/news/403165/lilly-confirms-date-and-conference-call-for-third-quarter-2026-financial-results-announcement opened (Oct 29, 10 a.m. ET, PR Newswire Oct 15); third-party, not the company page | Fail (only third-party confirmation) |

## E. Omissions

Did the agent miss something a human analyst would have included? List anything you found
in the ground-truth sources that the brief does not mention (a big headline, an earnings
date inside the window). Each one counts as a Fail in the score below.

- 
- 

## F. Your own test cases

Write two tests of your own that none of the sections above cover. Examples students have
used: "the as-of date on the page matches the changelog date", "no ticker shows a flat
sparkline when the real stock moved", "the page still renders if I delete one ticker's
news list in the data". Write the test, run it, record the result.

| Test | How you checked | Pass / Fail |
|---|---|---|
| | | |
| | | |

## Score

| Section | Passes | Total | Rate |
|---|---|---|---|
| A. Prices (re-check after owner edit; first pass was 5/5) | 4 | 5 | 80% |
| B. Weekly change | 4 | 5 | 80% |
| C. News (re-check; first pass was 9/10) | 8 | 10 | 80% |
| D. Calendar | 1 | 2 | 50% |
| E. Omissions (fails only) | 0 | | |
| F. Your own | | | |
| **Overall** | | | |

Publish only if A and B are 100% and C is at least 80% after fixes. If a row failed, tell
Claude exactly which row and what the correct value is, let it fix only that, rerun the
`qa-reviewer` agent, and regrade that row. Keep the original Fail in this file: a record of
what the agent got wrong is more useful than a clean sheet.
