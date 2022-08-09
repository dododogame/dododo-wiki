# Game mechanics

*中文 (中国)*: [游戏机制](game-mechanics-zh-cn)

In this page, a detailed illustration of the process of gameplay is delivered.

## Notes

**Note**s are the most essential part of the gameplay.

There are two types of notes in Dododo, **click**s and **hold**s.

To hit a note, you should hit a key on the keyboard (on a device with a keyboard)
or touch the screen (on a device with a touchable screen)
within the time at which it should be hit (when the [judgement line](#judgement-line) meets the note)
plus or minus the inaccuracy tolerance (judgement window).
The available keys on the keyboard that can hit notes are

- All keys corresponding to ASCII characters,
- All keys in the numbers pad (including <kbd>NumLock</kbd>),
- Whitespace keys: <kbd>Tab</kbd>, <kbd>Space Bar</kbd>, <kbd>Enter</kbd>,
- Navigation keys: four arrows, <kbd>Home</kbd>, <kbd>End</kbd>, <kbd>PageUp</kbd>, <kbd>PageDown</kbd>,
- Editing keys: <kbd>Insert</kbd>, <kbd>Delete</kbd>, <kbd>Backspace</kbd>, <kbd>Clear</kbd>,
- Modifier keys: <kbd>CapsLock</kbd>, <kbd>Shift</kbd>.

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

Some of the notes have halo drawn around it, and they are called **big notes**.
Big notes are hit in the same way as other notes,
but they affect the calculation of [score](#score).

## Bar lines

**Bar line**s are vertical lines as auxiliaries for reading the beatmap.
They are an imitation of bar lines from sheet music.
They can also be used to ornament the beatmap.
They themselves do not affect the gameplay,
but they can separate the notes into chunks called **measures**.

If all the notes in a measure are hit perfect,
the measure is judged as perfect.
If any of the notes in a measure is hit good while no notes in the measure are hit bad or missed,
then the measure is judged as good.
If any of the notes in a measure is hit bad while no notes in the measure are missed,
then the measure is judged as bad.
If any of the notes in a measure is missed, then the measure is judged as miss.
Excess hits do not affect the judge of measures.
All measures with no hittable notes are not counted and have no judge.

The numbers of measures judged to be in these four categories
are respectively shown in parentheses in the summary of your gameplay
next to the number of perfect, good, bad, and miss notes.
The judge of measures affects the calculation of [score](#score).

Note that the judge of a measure is only related to how the notes are hit
but not necessarily related to how the notes are completed.
If a hold is hit good but is finally missed because it is released to early,
it is still regarded as being hit good when considering the judge of the measure it is in.

## Judgement line

The **judgement line** (or scan line) moves throughout the gameplay.
The perfect time for the player to hit a note is exactly
when the judgement line moves to a position at the center of the note.

The speed of the judgement line can change throughout the gameplay,
and it can even run from right to the left.

## Inaccuracy bar

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

## Combo

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

## Accuracy rate

The **accuracy rate** is set based on your performance in playing a beatmap.
The accuracy rate is shown dynamically during the gameplay
in the bottom-right corner of the gameplay interface.
The calculation of the accuracy rate is
$$\mathit{AccuracyRate}=\frac{\mathit{perfect}+\mathit{good}/4-\mathit{excess}}{\mathit{perfect}+\mathit{good}+\mathit{bad}+\mathit{miss}}.$$

## Score

The game will assign you a **score** based on your performance in playing a beatmap.
The score is shown dynamically during the gameplay, just like the accuracy rate,
at the up-right corner of the gameplay interface.

The score consists of two parts, each of which has a cap of 500000,
and the score is the sum of the two parts, which has a cap of 1000000.

The first part of the score is 500000 times a weighted average of accuracy rates,
with big notes having double weights:
$$S\_1=500000\cdot\frac{p+p\_{\mathrm b}+\left(g+g\_{\mathrm b}\right)/4-e}{N+N\_{\mathrm b}},$$
where

- $S\_1$ is the first part of score;
- $p$ is the total number of perfect hit notes (including big notes);
- $g$ is the total number of perfect hit notes (including big notes);
- $p\_{\mathrm b}$ is the total number of perfect hit big notes;
- $g\_{\mathrm b}$ is the total number of good hit big notes;
- $e$ is the total number of excess hits;
- $N$ is the total number of notes (including big notes);
- $N\_{\mathrm b}$ is the total number of big notes.

The second part of the score is related to your performance of completing measures.
See the explanation of [bar lines](#bar-lines) to know about judging measures.
$$S\_2=500000\cdot\frac{p\_{\mathrm m}+g\_{\mathrm m}/2}{N_{\mathrm m}},$$
where

- $S\_2$ is the second part of score;
- $p\_{\mathrm m}$ is the total number of perfect measures;
- $g\_{\mathrm m}$ is the total number of good measures;
- $N\_{\mathrm m}$ is the total number of measures that have at least one note.

The final score is the sum of the two parts:
$$S=S\_1+S\_2.$$

## Mark

Once a gameplay is finished (the judgement line reaches the end of the beat map),
a mark will be calculated according to the accuracy rate
and shown in the top-middle of the gameplay interface.
The mark is a letter. The mark scale is

| Mark | Accuracy rate |
|------|---------------|
| P    | $=1$          |
| S    | $\ge0.95$     |
| A    | $\ge0.9$      |
| B    | $\ge0.8$      |
| C    | $\ge0.7$      |
| D    | $\ge0.6$      |
| E    | $\ge0.5$      |
| F    | else          |
| G | |

The mark is only related to the accuracy rate
but not related to the score, the game modifiers, etc.

There is a special "G" mark, which is given if the player fails the level,
even if the [`noFail`](game-modifiers#noFail) modifier is on.
See [HP](#hp) for details about failing.

The mark is also shown dynamically next to the accuracy rate during the gameplay
based on your performance so far.

## HP

<!-- TODO -->
