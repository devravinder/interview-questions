# Logical Questions: Basic to Advanced

Read [Logical questions](questions.md) first (water jug, cake cutting, doubling water tank); this file adds new ones. Try each before reading the answer.

## Basic

1. A bat and a ball cost 1.10 in total. The bat costs 1.00 more than the ball. How much is the ball?
   - 0.05. If the ball is x, then x + (x + 1.00) = 1.10.
2. 5 machines make 5 widgets in 5 minutes. How long do 100 machines take to make 100 widgets?
   - 5 minutes. Each machine makes one widget in 5 minutes.
3. What is the angle between the hour and minute hands at 3:15?
   - 7.5 degrees. The hour hand moves 0.5 degrees a minute, so it is at 97.5 and the minute hand at 90.
4. How many times do the hour and minute hands overlap in 12 hours?
   - 11 times (22 in a day), because there is no overlap between 11:00 and 1:00 except at 12:00.
5. A drawer has black and white socks. How many do you take, in the dark, to be sure of a pair?
   - 3. With two colours, the third sock must match one of the first two.
6. 10 people each shake hands with everyone else once. How many handshakes?
   - 45, which is n(n - 1) / 2.
7. You have two ropes that each burn in 60 minutes, unevenly. How do you measure 45 minutes?
   - Light rope A at both ends and rope B at one end. When A is gone (30 minutes), light the other end of B. B finishes 15 minutes later.

## Intermediate

1. 8 balls look the same, but one is heavier. Find it with a balance in two weighings.
   - Weigh 3 against 3. If they balance, weigh the last 2. If not, take the heavier 3 and weigh 1 against 1.
2. 100 doors are closed. On pass k you toggle every k-th door, for k = 1 to 100. Which doors end open?
   - The perfect squares (1, 4, 9 ... 100), so 10 doors. Only squares have an odd number of divisors.
3. Four people cross a bridge at night with one torch. They take 1, 2, 5 and 10 minutes. At most two cross at once. What is the minimum time?
   - 17 minutes: 1 and 2 cross (2), 1 returns (1), 5 and 10 cross (10), 2 returns (2), 1 and 2 cross (2).
4. You have 2 eggs and a 100-floor building. What is the fewest drops that always finds the highest safe floor?
   - 14. Drop from floor 14, then 27, 39 and so on, reducing the step by one each time, since 14 + 13 + ... + 1 >= 100.
5. 25 horses, 5 per race, no timer. How many races to find the 3 fastest?
   - 7: five heats, a race of the heat winners, then one race of the 5 horses that can still be in the top 3.
6. Monty Hall: you pick 1 of 3 doors, the host opens an empty one. Should you switch?
   - Yes. Switching wins 2/3 of the time, because your first pick was right only 1/3 of the time.
7. How many trailing zeros does 100! have?
   - 24. Count the factors of 5: 100/5 + 100/25 = 20 + 4.
8. Three switches outside a closed room control one bulb inside. You can enter once. Which switch is it?
   - Turn on switch 1 for a few minutes, turn it off, turn on switch 2, then enter. On is 2, off and warm is 1, off and cold is 3.
9. 1,000 bottles, one is poisoned, and poison takes 24 hours to act. What is the fewest testers to find it in one day?
   - 10. Number the bottles in binary; tester i drinks from every bottle with bit i set. The pattern of sick testers is the bottle number.
10. A snail climbs 3 m a day and slips 2 m at night in a 10 m well. When does it get out?
    - Day 8. After 7 days it is at 7 m, and on day 8 it climbs to 10 m before slipping.

## Advanced

1. 12 balls, one is heavier or lighter, you don't know which. Find it and say heavier or lighter in three weighings.
   - Weigh 4 against 4. Each result leaves 8 or fewer cases. Rotate balls between the pans in the second weighing so each outcome splits the cases into three.
2. Five pirates of strict rank split 100 coins. The top pirate proposes; if at least half vote yes it passes, otherwise he is thrown overboard. What does he propose?
   - 98, 0, 1, 0, 1. Work backwards from two pirates: each proposer buys the votes of those who would get nothing in the next round.
3. Three ants sit on the corners of a triangle and each walks along an edge in a random direction. What is the chance that none collide?
   - 1/4. Only all clockwise or all anticlockwise avoids a collision: 2 of the 8 cases.
4. How many people do you need for a better than 50% chance that two share a birthday?
   - 23. The number of pairs grows as n squared, which is the same reason hash collisions come early.
5. A train leaves every 10 minutes in each direction. Why do you mostly catch the one going one way?
   - The timetable offsets them, for example east at :00 and west at :01, so a random arrival catches east 9 times out of 10.
6. You can flip a biased coin. How do you get a fair 50/50 result?
   - Flip twice. HT means heads, TH means tails, and HH or TT means start again.
7. Pick a random line from a file of unknown size, reading it once.
   - Reservoir sampling: keep line k with probability 1/k. Every line ends up chosen with equal probability.

## Estimation

Interviewers check your assumptions and arithmetic, not the exact number.

1. How many requests per second does an app with 10 million daily users make if each user makes 20 requests a day?
   - 200 million a day / about 86,400 seconds is about 2,300 a second on average. Plan for 2 to 5 times that at peak.
2. How much storage do 500 million short posts a day need for 5 years?
   - About 300 bytes each with metadata: 150 GB a day, about 55 TB a year, about 275 TB for 5 years before replication.
3. How many servers do you need for 50,000 requests a second if one server handles 2,000?
   - 25, plus headroom for peaks and failure (30 to 40).
4. How long does it take to send 1 TB over a 1 Gbit/s link?
   - 8,000 Gbit / 1 Gbit/s = 8,000 s, a bit over 2 hours.
