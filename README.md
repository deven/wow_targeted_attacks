# wow_targeted_attacks
Solve targeted attacks for pet battles in World of Warcraft

This is a quick & dirty Perl script for solving targeted attacks for pet battles in World of Warcraft.

Running the script simply prompts for the initial parameters -- the original health of the target, the low end of the target health and the high end of the target health.  Then it enters a loop, asking for one pet ability at a time -- the expected damage amount of the attack, the name of the pet and the name of the ability.  After entering each new ability, it uses a recursive algorithm to implement a brute-force search for all possible solutions using the given abilities to bring the target's health down to the targeted range.

I wrote this script as a tool while developing a pet battle strategy for Cymre Brightblade:

http://www.wowhead.com/npc=83837/cymre-brightblade#comments:id=2299641

I wanted to find out exactly what the threshold was for Idol of Decay to cast Dark Rebirth.  With a number of attempts using manual calculations, I had managed to narrow the range from 274 (at which point Idol of Decay *does* cast Dark Rebirth) to 277 (at which point Idol of Decay does *not* cast Dark Rebirth).  I figured that the threshold was probably right around 275, but I wanted to know precisely what the threshold value was, so I wrote this quick & dirty Perl script off the top of my head to solve the problem, then decided to post it on github in case it might be useful to someone else.  After testing the solutions, I found that 274 and 275 were the key numbers.

Here are a couple of the solutions this program found for these target values:

* 1769 - 3 * 309 (Arcane Eye/Psychic Blast) - 2 * 207 (Darkmoon Turtle/Grasp) - 1 * 154 (Arcane Eye/Eyeblast) = 274
* 1769 - 2 * 309 (Arcane Eye/Psychic Blast) - 2 * 231 (Arcane Eye/Interrupting Gaze) - 2 * 207 (Darkmoon Turtle/Grasp) = 275

When I tested these in the actual pet battle (having to restart once or twice because of critical strikes that ruined the solution), I used Arcane Eye to hit twice for 309 points with Psychic Blast and twice for 231 points with Interrupting Gaze, and used Darkmoon Turtle to hit twice for 207 points with Grasp.  As planned, this brought the health down to precisely 275 for Idol of Decay.  At this point, I just kept passing turns and observed that the Idol of Decay would *not* cast Dark Rebirth, no matter how many turns I passed.  I then started over and used the other solution to bring the health down to precisely 274.  As expected (and as previously observed during my manual testing), when I passed on the next turn, Idol of Decay did indeed cast Dark Rebirth immediately.

From this, I was able to conclude that the Idol of Decay will *not* cast Dark Rebirth as long as its health is 275 or above, but it will immediately cast Dark Rebirth at 274 or below.  This was the information I was seeking to create the most reliable pet battle strategy that I could devise.
