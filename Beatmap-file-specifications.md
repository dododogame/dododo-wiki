A Dododo beatmap is a `.ddd` file in plain-text format.
The beatmap consists of two parts, the **head** and the list of **row**s.
The two parts are separated by a single `---` line.

The following are just some specifications.
To read these, you are assumed to have enough knowledge about notations in sheet music.

# Header

The header consists of several key-value pairs, each of which lies in a line,
and a key is separated from its corresponding value by `: ` (a colon and a whitespace).

The following items are available:

## `title`

The name of the music.

This item should always be specified to a simple, short, unique, direct string
so that users can identify the music quickly.

## `musicAuthor`

The author of the music (the artist).

The first name and middle name of the author can
be abbreviated as their initial letters for brevity.
If there are multiple authors,
it is recommended to specify them all and connect the names with `&`.
If multiple authors contribute in different ways to composing the music
(composers, lyricists, players, etc.),
it is recommended to specify such information in parentheses.
For example, `W. A. Mozart (Composer) & S. Ligoratti (Player)`.

## `beatmapAuthor`

The author of the beatmap.

You may use your nickname.

## `difficulty`

The difficulty of the beatmap.

It is usually specified as an integer ranging from 1 to 15.
If it is not specified, the difficulty would be "unknown" (without the quotes).
Though not recommended, you can specify the difficulty as
numbers greater than 15 or "???" for extremely hard beatmaps.

Difficulty is intended to be a brief indicator on an ordinal scale
of how hard the beatmap is to beat.

## `audioUrl`

The url of the audio file of the music.

If it is not specified, the user has to upload an audio file
(if playing through uploading files),
or the user will not hear any music when playing.

## `start`

Where to start playing the audio file, in milliseconds.

If it is not specified, the audio file will be played from its very beginning.

In some cases, the audio file used as the music is too long for a rhythm game,
and it cannot be modified easily if it is provided through a url.
Then, you may have to specify a certain portion (segment) of the audio file.
The items `start` and [`end`](#end) offers you the function.

## `end`

Where to end playing the audio file, in milliseconds.

If it is not specified, the audio file will be played until its very end.
Despite that, you should always specify this item in your beatmap
to prevent the game preloading the metadata of the audio file
(for calculating the length) to increase its performance.

## `volume`

The volume for playing the audio file. `1.0` means original volume.

It is intended to be used when the audio file is provided through a url
because the file cannot be modified in that case.

## `offset`

The time (position) in the played audio at which the beatmap starts.
May be negative or positive.

It is different from `start` in that the audio before `offset` will be played.
Note that, if `start` and `offset` are both specified,
audio starts playing at `start` while the beatmap starts at `start + offset`.

# Rows

Different **row**s in the beatmap are separated by an empty line.
Do not include empty lines within a row.

Every row consists of one or several **voice**s.
Each voice consists of several **note**s and **bar line**s and is written within a line.
Every note is specified by its note length and multiplicity (simultaneous note in the same voice)
together with symbols denoting whether the note is hold, tied, beamed, etc.

## Control sentences

Before specifying the notes in a row, some control sentences can be included for the row.
Each control sentence includes a function name and one or more parameters,
separated by spaces.
The function name must start with a capitalized letter, and the rest letters are case-insensitive.

Here is some function names and the corresponding parameters.

### `PERFECT`, `GOOD`, `BAD`

Syntax:

```text
PERFECT <window_radius>
GOOD <window_radius>
BAD <window_radius>
```

These control sentences accept one parameter, indicating the radius of the judge window.
The `window_radius` is NOT in milliseconds but is the ratio of the inaccuracy tolerance for a perfect / good / bad judge
and the total (temporal) length of the row.
Therefore, given the same radius of judge window, judging will be stricter if the row is shorter (in time).

### `BPM`

Syntax:

```text
BPM <beatNote1> <beatsPerMinute1>[ <position1>[ <beatNote2> <beatsPerMinute2> <position2>[ ... ]]]
```

The `beatNote` is a note specified in the same manner in [how to write a note](#how-to-write-a-note).
The `beatsPerMinute` is the number of beats per minute,
meaning that one minute is exactly `beatsPerMinute` times as long as the beat note.
The `position` is the position of the BPM change, specified as a rational number in $[0, 1]$,
with the start of the row being 0 and the end of the row being 1.
The position is calculated according to notes' literal length but not their temporal length
(e.g. a quavar in 180 BPM and one in 200 BPM has the same literal length because they are both quavars).

### `MS_PER_WHOLE`

Syntax:

```text
MS_PER_WHOLE <millisecondsPerWhole>
```

This sets the average temporal length of a whole note in milliseconds.
Usually this can be automatically calculated by the game according to the BPM specified by [`BPM`](#bpm),
or inherit from last row.
However, sometimes it is necessary to specify it manually, especially when using [`TIME`](#time).

### `TIME`

Syntax:

```text
TIME <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [math expressions](#math-expressions).

The expression is a mapping from $[0, 1]$ to $[0, 1]$.
It *must* be monotonically increasing (because you cannot travel to the past).
It maps the position in the row to the time at which the position in the row is played.
The position mapped to 0 is played exactly when the row starts being played,
and the position mapped to 1 is played exactly when the row ends being played
(and when the next row starts being played).
For example, with the expression `sqrt(x)` you can have the tempo linearly
(w.r.t. notes' literal lengths) increasing from 0.

Default: `x`.

### `SPACE_X`, `NOTE_X`, `HIT_X`

Syntax:

```text
SPACE_X <expression>
NOTE_X <expression>
HIT_X <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [math expressions](#math-expressions).

The expression is a mapping from $[0, 1]$ to $[0, 1]$.
The `SPACE_X` sentence maps the position of the row (according to note lengths) to the spatial position.
The position mapped to 0 is drawn at the leftmost place,
and the position mapped to 1 is drawn at the rightmost place.
It is not necessarily monotonically increasing (to possibly make the judge line move to the left)
or being continuous (to possibly make the judge line jump suddenly).

`NOTE_X` and `HIT_X` do similar things to what `SPACE_X` does,
but `NOTE_X` defines the spatial position of drawn notes
while `HIT_X` defines the spatial position of the hit effects.

The default setting of `SPACE_X` is `x`.
The default setting of `NOTE_X` is to be the same as `SPACE_X`.
The default setting of `HIT_X` is to be the same as `NOTE_X`.

### `SPACE_Y`, `WIDTH`, `HEIGHT`

Syntax:

```text
SPACE_Y <expression>
WIDTH <expression>
HEIGHT <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [math expressions](#math-expressions).

These control sentences are purely for ornamental performance of the judge line
because they do not affect the (spatial and temporal) arrangement of notes.
The expressions are mappings on $[0, 1]$, and the mapped values are lengths in unit of pixels.

`SPACE_Y` is the vertical position of the judge line.
Positive values mean to place the judge line at specified number of pixels above the default position.
Default: `0`.

`WIDTH` is the width of the judge line. Default: `1`.

`HEIGHT` is the height of the judge line. Default: `voicesHeight` times the number of voices.

These control sentences are ineffective if the user disabled ornamental judge line performances
in the preferences.

### `RED`, `GREEN`, `BLUE`, `ALPHA`

Syntax:

```text
RED <expression>
GREEN <expression>
BLUE <expression>
ALPHA <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [math expressions](#math-expressions).

These control sentences are also purely for ornamental performance of the judge line.
They are used to change the color of the judge line.
These expressions are mappings from $[0, 1]$ to $[0, 1]$, and the default of them are all `1`
(pure and non-transparent white).

These control sentences are ineffective if the user disabled ornamental judge line performances
in the preferences.

### `FAKE_JUDGE_LINE`

This control sentence creates a new judge line for this row of beatmap but a fake one
(which does not affect the gameplay but is purely ornamental).
After this control sentence, you can add the following control sentences
to define the behaviors of the new fake judge line without affecting the judge lines
defined previously:
- `SPACE_X`,
- `SPACE_Y`,
- `RED`,
- `GREEN`,
- `BLUE`,
- `ALPHA`,
- `WIDTH`,
- `HEIGHT`.

You can create more fake judge lines by using `FAKE_JUDGE_LINE` again
after finishing defining the previous fake judge line.

This control sentence is not effective if the user disables ornamental judge line performances
in the preferences.

### Math expressions

Some of the control sentences above use math expressions as parameters.
Parsing the math expressions are powered by [math.js](https://mathjs.org/).

In these expressions, there should be only one variable `x`, denoting the position in the row.
The position is measured according to notes' literal length but not their temporal length.

There is an `if` function that can be used to help express piecewise functions.
Its syntax is
```text
if(<condition1>, <value1>[, <condition2>, <value2>[, ... ]][, <elseValue>])
```
It is the same as
```text
condition1 ? value1 : condition2 ? value2 : ... : elseValue
```
All variables set by the gamer in preferences can be used in the math expressions:

| Variable                 | Meaning                                      | Type     | Default                                     |
|--------------------------|----------------------------------------------|----------|---------------------------------------------|
| `playRate`               | Play rate (speed of music)                   | Number   | `1.0`                                       |
| `autoPlay`               | Auto-play                                    | Boolean  | `false`                                     |
| `noBad`                  | No-bad mode                                  | Boolean  | `false`                                     |
| `noExcess`               | No-excess mode                               | Boolean  | `false`                                     |
| `judgeWindow`            | Judge window (smaller is stricter)           | Number   | `1.0`                                       |
| `autoCompleteHolds`      | Automatically hold for hold notes            | Boolean  | `false`                                     |
| `offset`                 | Offset (in ms)                               | Number   | `0.0`                                       |
| `countdown`              | Show countdown before resuming               | Boolean  | `true`                                      |
| `autoRestartGood`        | Automatically restart when failing to AP     | Boolean  | `false`                                     |
| `autoRestartMiss`        | Automatically restart when failing to FC     | Boolean  | `false`                                     |
| `F7Pause`                | Press <kbd>F7</kbd> to pause                 | Boolean  | `true`                                      |
| `backtickRestart`        | Press <kbd>`</kbd> to restart                | Boolean  | `true`                                      |
| `autoPause`              | Automatically pause when losing focus        | Boolean  | `true`                                      |
| `recordVisual`           | Record visual preferences to replay          | Boolean  | `true`                                      |
| `FCAPIndicator`          | Full combo / all perfect indicator           | Boolean  | `true`                                      |
| `TPSIndicator`           | Taps per second indicator                    | Boolean  | `true`                                      |
| `judgeLinePerformances`  | Enable ornamental judge line effects         | Boolean  | `true`                                      |
| `flashWarningGood`       | Warn by flash the screen at good hits        | Boolean  | `false`                                     |
| `falshWarningMiss`       | Warn by flash the screen at combo breaks     | Boolean  | `true`                                      |
| `showInaccuracyData`     | Show inaccuracy data                         | Boolean  | `true`                                      |
| `comboPopupInterval`     | Interval of combo popups (set 0 to disable)  | Number   | `25`                                        |
| `fadeIn`                 | Fade-in (ratio to resolution, 0 to disable)  | Number   | `0.0`                                       |
| `fadeOut`                | Fade-out (ratio to resolution, 0 to disable) | Number   | `0.0`                                       |
| `reverseVoices`          | Reverse voices                               | Boolean  | `false`                                     |
| `mirror`                 | Mirror (flip horizontally)                   | Boolean  | `false`                                     |
| `showKeyboard`           | Show keyboard pressings                      | Boolean  | `false` on mobile devices, otherwise `true` |
| `fontSize`               | Font size                                    | Number   | `28`                                        |
| `textHeight`             | Height of text lines                         | Number   | `40`                                        |
| `margin`                 | Margins                                      | Number   | `16`                                        |
| `voicesHeight`           | Height of voices                             | Number   | `64`                                        |
| `stemsLength`            | Lengths of note stems                        | Number   | `25`                                        |
| `headsRadius`            | Radius of note heads                         | Number   | `5`                                         |
| `holdWidth`              | Thickness of hold notes' tails (hold bar)    | Number   | `5`                                         |
| `beamsWidth`             | Thickness of note beams                      | Number   | `6`                                         |
| `beamsSpacing`           | Spacing between note beams                   | Number   | `4`                                         |
| `unconnectedBeamsLength` | Length of unconnected note beams             | Number   | `20`                                        |
| `barlinesHeight`         | Height of barlines                           | Number   | `256`                                       |
| `hitEffectRadius`        | Radius of hit effects                        | Number   | `32`                                        |
| `distanceBetweenLines`   | Distance between beatmap rows                | Number   | `384`                                       |
| `notesColor`             | Color of notes                               | String   | `'#ffffff'`                                 |
| `auxiliariesColor`       | Color of auxiliaries (barlines etc)          | String   | `'#4c4c4c'`                                 |
| `perfectColor`           | Color of perfect hits                        | String   | `'#ffff00'`                                 |
| `goodColor`              | Color of good hits                           | String   | `'#0000ff'`                                 |
| `badColor`               | Color of bad hits                            | String   | `'#008000'`                                 |
| `missColor`              | Color of missed hits                         | String   | `'#ff0000'`                                 |
| `excessColor`            | Color of excess hits                         | String   | `'#ff0000'`                                 |
| `textColor`              | Color of foreground (texts etc)              | String   | `'#ffffff'`                                 |
| `backgroundColor`        | Color of background                          | String   | `'#000000'`                                 |
| `graphicsWidth`          | Resolution (width)                           | Number   | `1024`                                      |
| `graphicsHeight`         | Resolution (height)                          | Number   | `768`                                       |
| `enableHitSound`         | Enable hit sound                             | Boolean  | `true`                                      |
| `hitSound`               | Hit sound                                    | String   | `'snare_drum_1.ogg'`                        |
| `hitSoundWithMusic`      | Hit sound with music instead of input        | Boolean  | `false`                                     |
| `musicVolume`            | Volume of music                              | Number   | `1.0`                                       |
| `hitSoundVolume`         | Volume of hit sound                          | Number   | `2.0`                                       |
| `masterVolume`           | Master volume                                | Number   | `1.0`                                       |
| `language`               | Language                                     | String   | According to browser settings               |
| `save`                   | Save preferences in the web storage          | Boolean  | `false`                                     |

Note that here the strings are 7-character lower-case hexadecimal notation of colors.
To get the RGB values (in $[0, 1]$), you can use the methods `red()`, `green()`, `blue()`.
For example, `'#4c8cff'.red()` returns approximately `0.298`, which is `0x4c / 0xff`. 

The preferences items related to [game modifiers](Game-modifiers) and visuals are not recommended to be used
because they will be different from the actual in-game settings when the user is replaying something.

## How to write a note

The syntax of a note is:

```text
<noteLength><dots><multiplicity><hold><big><tied>
```

| Element        | Possible value (Regexp) | Meaning                                                                  |
|----------------|-------------------------|--------------------------------------------------------------------------|
| `noteLength`   | `[0-9a-z]`              | The note length (without of augmentation dots)                           |
| `dots`         | `\.*`                   | The number of augmentation dots (as many as the number written here)     |
| `multiplicity` | `[0-9a-z]?`             | The multiplicity (number of simultaneous notes) (default 1 if omitted)   |
| `hold`         | `_?`                    | Whether the note is a hold (omitted underscore means a click)            |
| `big`          | `\*?`                   | Whether the note is a big note (double weight when calculating score)    |
| `tied`         | `~?`                    | Whether the note is tied (connected to the next note) (tilde means tied) |

Here the `noteLength` and the `multiplicity` are specified by a single character representing a number.
0–9 are just literally 0–9, and a–z are 10–35 respectively.

The `noteLength` value represents the log2 of the ratio of
the time length of a whole note and that of the specified note. 

The `multiplicity` value represents the number of simultaneous notes in the voices.
A zero multiplicity means that the note is a rest.

Because there are totally 10 digits and 26 letters,
the shortest possible note is `2**35`th note,
and the largest multiplicity is 35.

If a note's previous note is tied to this note, this note's `multiplicity` and `hold`
are useless and are kept consistent with the previous note,
and this note's `big` is forced to be `false`.

## Making notes beamed or grouping (contrametric)

Notes can be **beam**ed (flags are connected) by enclosing them with parentheses.
Parenthesized notes without flags will not be beamed.

Beams can be created across bar lines (by inserting `|` between beamed notes)
but not across rows or voices.

**Grouping**s (tuplets) can be created by specifying a ratio after the closing parenthesis.
The ratio consists of two characters, each of which is within `[0-9a-z]` representing a number.
The first number divided by the second number is
the ratio of the seeming length of the grouping and the actual length of the grouping.
The second number can be omitted, and the default value of it is
$$\mathit{ratio}_2=2\^{\left\lfloor\log\_2\mathit{ratio}\_1\right\rfloor},$$
where $\mathit{ratio}\_1$ is the first number.

Here is an example of some notes and the rhythm they represent:

```text
2 (3 3 3)3 2 (4 4 4 4 4)5 | 2
```
![\new RhythmicStaff {
\clef percussion
\time 4/4
\set Score.tempoHideNote = ##t \tempo 4 = 80
c4 \tuplet 3/2 { c8 c c }
c4 \tuplet 5/4 { c16 c c c c }
c4
}](https://upload.wikimedia.org/score/1/e/1ea3xyusyw770pzh5dli2ezzv76si3k/1ea3xyus.png)

## Writing bar lines

Bar lines are created by inserting a `|` (and spaces for separating it from notes) within a voice.
They can appear within a beamed group of notes.
They can also appear between two tied notes.
It is recommended to write a bar line at the end of each voice.

When calculating [score](Game-mechanics#score), measures are taken into account.
Only the bar lines written in the first voice are effective in creating measures.
Bar lines in other voices are fake (it mainly serves as an auxiliary for the beatmapper).
In order for the game to calculate the number of measures correctly,
beatmappers must add one and only one bar line in the first voice after the very last note.

Every bar line will extend all across the voices in the row
but not just the voice where it is written.
