In this page, a detailed illustration of the process of gameplay is delivered.

# Notes

**Note**s are the most essential part of the gameplay.

There are two types of notes in Dododo, **click**s and **hold**s.

To hit a note, you should hit a key on the keyboard (on a device with a keyboard)
or touch the screen (on a device with a touchable screen)
within the time at which it should be hit (when the [judge line](#judge-line) meets the note)
plus or minus the inaccuracy tolerance.

There are three levels of inaccuracies: perfect, good, and bad.
Their judge intervals are to be specified in the beatmap and can change throughout the gameplay.
If a note fails to be hit, it is a miss judge.
The number of perfects, goods, bads, and misses affect
the [score](#score) and the [accuracy rate](#accuracy-rate).

Specially, to hit a hold, throughout its sustaining time
(until its end time minus the inaccuracy tolerance of good judge),
there should be at least one key/touch being pressed.
If there are multiple holds sustaining at the same time,
there should also be multiple keys/touches being pressed at the same time.

At first, notes are colored white (the color can be customized in preferences).
After a note is cleared (hit or missed), the note will be re-colored.
Perfect is yellow; good is blue; bad is green; miss is red (the colors can be customized in preferences).
After a note is hit, there will appear an indicator in the [inaccuracy bar](#inaccuracy-bar).

If a hit cannot correspond to any notes, it is regarded as an excess hit,
which also affects the [score](#score), the [accuracy rate](#accuracy-rate), and the [combo](#combo).

# Bar lines

**Bar line**s are vertical lines as auxiliaries for reading the beatmap.
They are an imitation of bar lines from sheet music.
They can also be used to ornament the beatmap.
They themselves do not affect the gameplay.

# Judge line

The **judge line** (or scan line) moves throughout the gameplay.
The perfect time for the player to hit a note is exactly
when the judge line moves to a position at the center of the note.

The speed of the judge line can change throughout the gameplay,
and it can even run from right to the left.

# Inaccuracy bar

The **inaccuracy bar** is to help indicate how inaccurate the notes are hit.
It is located at the bottom of the gameplay interface.
It is colored symmetrically, with the perfect judge interval being yellow,
the good judge interval being blue, and the bad judge interval being green
(the colors can be customized in preferences).
Note that the inaccuracy tolerances are specific to different beatmaps,
and it can even change during the gameplay.

When a note is hit, according to the inaccuracy,
a small rule will appear at the inaccuracy bar.
The more early it is hit, the more left the small rule will be to.
The small rule then fades out.
With an exact perfect hit, the small rule will appear at the very center of the inaccuracy bar.

Any inaccuracy out of the bad judge interval
will not cause a small rule to appear at the inaccuracy bar.

# Combo

The **combo** refers to the number of consecutive notes the player hits.
It is shown in the bottom-left corner of the gameplay interface.

There are two cases when the combo is interrupted and reset to 0:

- During the time at which a note should be hit plus or minus the good judge interval,
the note is not hit. In other words, a note is badded or missed.
- A key that can possibly be the key of a note is hit mistakenly.
In other words, during the time at which a key is hit plus or minus the bad judge interval,
there are no notes corresponding to the key.

After a gameplay is finished, an FC (full combo) note will appear next to the combo number
if the combo has never been reset during the gameplay.

# Accuracy rate

The **accuracy rate** is set based on your performance in playing a beatmap.
The accuracy rate is shown dynamically during the gameplay
in the bottom-right corner of the gameplay interface.
The calculation of the accuracy rate is
$$\mathit{AccuracyRate}=\frac{\mathit{perfect}+\mathit{good}/4-\mathit{excess}}{\mathit{perfect}+\mathit{good}+\mathit{bad}+\mathit{miss}}.$$

# Score

The game will assign you a **score** based on your performance in playing a beatmap.
The score is shown dynamically during the gameplay, just like the accuracy rate,
at the up-right corner of the gameplay interface.
The calculation of the score involves the number of perfects, goods, bads, misses, and excesses:
$$\mathit{Score} = 1000000\cdot\frac{\mathit{perfect}+\mathit{good}/4-\mathit{excess}}{\mathit{notesCount}}.$$

Unlike some (or most) rhythm games, Dododo does not take combo into account when scoring.

Once a gameplay is finished (the judge line reaches the end of the beat map),
a mark will be calculated and shown in the bottom-right corner of the gameplay interface.
The mark is a letter. The mark scale is

| Mark | Score      |
|------|------------|
| P    | = 1000000  |
| S    | \>= 950000 |
| A    | \>= 900000 |
| B    | \>= 800000 |
| C    | \>= 700000 |
| D    | \>= 600000 |
| E    | \>= 500000 |
| F    | else       |

The mark is also shown dynamically next to the accuracy rate during the gameplay
based on your performance so far.
There is a simple relation between the accuracy rate and the score when the gameplay has been finished:
$$\mathit{Score}=1000000\mathit{AccuracyRate}.$$
