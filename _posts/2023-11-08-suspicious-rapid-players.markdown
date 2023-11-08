---
layout: post
title:  "Using Move Timing to Identify Suspicious Players in the chess.com 10+0 Pool"
date:   2023-11-08 10:10:18 -0500
categories:
---
Hello! Online cheating has been a hot topic lately, with GMs, site owners, and us plebeians alike wildly speculating about how widespread cheating is in our matches. I’ve got a lot of free time right now and I don’t like cheating, so I set out to answer that question. As it turns out, that’s a very difficult question to answer, so I quickly gave up on it and picked an easier one: how many sketchy people are there in the chess.com 10+0 pool.
A few recent reddit threads, mostly [A case study of blatant cheating](https://www.reddit.com/r/chess/comments/17lavfo/a_case_study_of_blatant_cheating_from_2200_rapid/ "A case study of blatant cheating") and [Anecdotal evidence of blatant cheating](https://www.reddit.com/r/chess/comments/17m58lw/anecdotal_evidence_of_blatant_cheating_amongst/ "Anecdotal evidence of blatant cheating") have tried to tackle this topic as individuals, but I wanted to do it in a measurable way that can attempt to answer how many cheaters are active across the pool at a given time.

To start, I’m looking for accounts that move like stereotypical engine cheats playing much above their skill level – they never move quickly and never move very slowly. Take a second to copy your opponent’s move into stockfish, wait a second for it to calculate, and then make the move in your game. Moves taking less than 2s I considered fast, moves taking above 10s I considered slow, and if either one of those categories were less than 10% of moves, my algorithm considered you suspicious.[^1] Certainly not all of these accounts are cheating, but this is a start, to identify accounts which look weird and can be followed up by analyzing the moves with engines, looking at the way they play other game modes, etc etc.
I scanned the top 5000 players on the rapid leaderboard, (this required a bit over 2100 rating) going through all of their 10+0 games played in October 2023, throwing out any account with fewer than 10 games. This left me with 1464[^2] accounts, and from there, I identified 149 accounts with suspicious move timings, a little over 10% of the active pool.
## Suspicious Signals
Most, but not all, of these accounts had multiple other signals which makes me strongly suspect them of being cheaters.
- The accounts are relatively new, often made in the second half of 2023. Among accounts that aren’t new, many had established ratings several hundred points below their current rating only to find enormous improvement all at once.
![A player stable at 1300 quickly climbing to 1600, then quickly climbing to 2100](/images/suspicious_example_three.PNG "I don't believe in plateaus")
- The suspicious accounts are much less likely to have premium, although I’m not sure it’s appropriate to use that as a cheating signal and I didn’t measure that.
- The accounts are almost entirely playing in the 10+0 pool. When they do have bullet/blitz/puzzle ratings, they are usually substantially lower. Players should be expected to have different abilities in different time controls, but it seems impossible to be 2300 rapid and 800 blitz simultaneously.

![A player rated 2350 in Rapid but 800 in Blitz](/images/suspicious_example_blitz_vs_rapid.PNG "2350 Rapid but 800 Blitz")
- Their rapid ratings do not appear to be stable. Their win-loss ratio is substantially skewed towards wins, meaning their rating should continue to climb if they play more games. Maybe cheaters are getting bored once they realize winning with engines is unfulfilling, or maybe they get banned and make a new account and get banned again, etc etc.

![A player rated 2200 in Rapid but 1300 in Bullet](/images/suspicious_example_one.PNG "Give them nine extra minutes and they can't be stopped")
- They behave very oddly toward the end of games. They don’t react humanly to time trouble by speeding up their moves, or they play games to mate while still spending 5-10 seconds per move. They seem to lose by resignation much less than known humans, although I have not measured this.
None of these signals individually prove cheating, but combined they paint a picture of someone who has nothing at risk and acts exactly like a 1000 with stockfish on their phone would.


## "Results"
Out of the suspicious accounts, 9 of them have already been banned for fair play reasons. (k0lershmp, mahmoodtah, daviddownunder, srinivasareddy9052, people_55, s_iddh, anil8776, jonaa0loss, rajasheroz) Considering that I only started collecting data Sunday night, it’s alarming. We shouldn’t extrapolate two days of bannings to make a point about how many cheaters there are, since maybe this was a bad day, maybe reports come in over the weekend and get processed on Mondays, etc etc… But .3% of the highly rated 10+0 players got banned on one day just from this subset. 4 other accounts that I didn’t mark as suspicious were banned too (icey0042, super_noname, nielcnt, trixxaroula2), so members of the suspicious group were much more likely to be banned. (a significance test is left as an exercise for the reader) 
I plan to check back again in one month to determine 
There are clearly many cheaters afoot, and it's better that they get banned than they don't
### Questions for the Community
* What are some other simple-ish ways to check if an account is suspicious? I'm looking for some more projects to do
* I’d like to hear from people who play with engine-like cadence and are not using the engine, or are 2100+ rapid and play 1000 or more points weaker in other time controls. What could a cheat-detecting algorithm do to avoid suspecting you?
  * Similarly, if you're an undetected cheater, it'd be interesting to hear how you (think) you're avoiding detection

## Future work

* Formalize what makes accounts suspicious
* Analyze more time controls. About 70% of the rapid leaderboard was ineligible for this analysis, but the most obvious cheaters will have similar move cadences regardless of time control.
* Use engines to analyze the results of their moves. We should be able to notice patterns in blunder rate and move quality, especially as a function of move time. Once we can do this, we can consider approaching the more difficult problem of identifying smarter cheaters.
* Build a training set of accounts that have been banned, and examine them to find more precise metrics to evaluate accounts by in the future. I don’t know of a good way to get those accounts sadly.
* Compare and contrast with lichess 10+0 players

---

[^1]: I benchmarked against 20 titled players to determine these thresholds

[^2]: There's a few duplicates since the leaderboard was not captured all at once