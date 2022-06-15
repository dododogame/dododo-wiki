# Game modifiers

*中文 (中国)*: [游戏修饰器](game-modifiers-zh-cn)

**Game modifiers** are items in preferences that you can use to adjust the difficulty of the gameplay.
They do not affect the calculation of the score and the accuracy rate.
All enabled game modifiers are shown in the middle left of the game interface.

Here is a list of all the modifiers:
| Code                 | Meaning                     | In-game display (English) | Type     | Default              |
|--------------------------|-------------------------------------|------|----------|----------------------|
| [`playRate`](#playRate)      | Play rate (speed of music)    | %fx speed       | Number   | `1.0`                |
| [`autoPlay`](#autoPlay)      | Auto-play          | Auto-play      | Boolean  | `false`              |
| [`noBad`](#noBad)     | No-bad mode        | No-bad      | Boolean  | `false`              |
| [`noExcess`](#noExcess) | No-excess mode | No-excess | Boolean | `false` |
| [`judgeWindow`](#judgeWindow) | Judgement window (smaller is stricter) | %fx judge | Number | `1.0` |
| [`autoCompleteHolds`](#autoCompleteHolds) | Automatically hold for hold notes | Auto-hold | Boolean | `false` |

Any values of these preferences items different from default values are regarded as
enabling the corresponding game modifier (displayed in-game).
The percent symbol (`%`) in the above table is for [printf format](https://en.wikipedia.org/wiki/Printf_format_string).

## `playRate`

This modifier adjusts the speed of the music to a certain multiple of the original speed.
The pitch of the music will change correspondingly.

Note that judgement windows are divided by the play rate value
because they are proportional to the time duration of each row of the beatmap,
which is shorter when the play rate is higher.

## `autoPlay`

This modifier makes the computer play for you and ignore your inputs.
It does not guarantee an all-perfect play if there are impossible notes in the beatmap.

## `noBad`

This modifier makes your gameplay have no bad hits.
It does not affect the judgement windows for perfect hits and good hits.
Technically, it is equivalent to setting the bad window to be the same as the good window.

This modifier does not necessarily decrease the difficulty of the gameplay
because it will be easier to have excess hits.

## `noExcess`

This modifier makes your gameplay have no excess hits.
Technically, it is equivalent to setting the number of excess hits to zero and
turning off all in-game animations related to excess hits.

## `judgeWindow`

This modifier allows you to make the judge stricter or looser.
The radii of judgement windows are multiplied by the ratio specified by this modifier.

## `autoCompleteHolds`

This modifier makes those holds that are hit perfect or good hold themselves
without requiring the player to continuously press the keys.
