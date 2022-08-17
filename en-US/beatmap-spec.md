---
layout: wiki-page
lang: en-US
title: Beatmap file specifications
---

A Dododo beatmap is a `.ddd` file in plain-text format.
The beatmap consists of two parts, the **head** and the list of **row**s.
The two parts are separated by a single `---` line.

The following are just some specifications.
To read these, you are assumed to have enough knowledge about notations in sheet music.
It is better for you to have knowledge about programming.

## Header

The header consists of several key-value pairs, each of which lies in a line,
and a key is separated from its corresponding value by `: `&nbsp;(a colon and a whitespace).

The following items are available:

### `title`

The name of the music.

This item should always be specified to a simple, short, unique, direct string
so that users can identify the music quickly.

### `musicAuthor`

The author of the music (the artist).

The first name and middle name of the author can
be abbreviated as their initial letters for brevity.
If there are multiple authors,
it is recommended to specify them all and connect the names with `&`.
If multiple authors contribute in different ways to composing the music
(composers, lyricists, players, etc.),
it is recommended to specify such information in parentheses.
For example, `W. A. Mozart (Composer) & S. Ligoratti (Player)`.

### `beatmapAuthor`

The author of the beatmap.

You may use your nickname.

### `difficulty`

The difficulty of the beatmap.

It is usually specified as an integer ranging from 1 to 15.
If it is not specified, the difficulty would be "unknown" (without the quotes).
Though not recommended, you can specify the difficulty as
numbers greater than 15 or "???" for extremely hard beatmaps.

Difficulty is intended to be a brief indicator on an ordinal scale
of how hard the beatmap is to beat.

### `audioUrl`

The url of the audio file of the music.

If it is not specified, the user has to upload an audio file
(if playing through uploading files),
or the user will not hear any music when playing.

### `start`

Where to start playing the audio file, in milliseconds.

If it is not specified, the audio file will be played from its very beginning.

In some cases, the audio file used as the music is too long for a rhythm game,
and it cannot be modified easily if it is provided through a url.
Then, you may have to specify a certain portion (segment) of the audio file.
The items `start` and [`end`](#end) offers you the function.

### `end`

Where to end playing the audio file, in milliseconds.

If it is not specified, the audio file will be played until its very end.
Despite that, you should always specify this item in your beatmap
to prevent the game preloading the metadata of the audio file
(for calculating the length) to increase its performance.

### `volume`

The volume for playing the audio file. `1.0` means original volume.

It is intended to be used when the audio file is provided through a url
because the file cannot be modified in that case.

### `offset`

The time (position) in the played audio at which the beatmap starts.
May be negative or positive.

It is different from [`start`](#start) in that the audio before `offset` will be played.
Note that, if `start` and `offset` are both specified,
audio starts playing at `start` while the beatmap starts at `start + offset`.

## Rows

Different **row**s in the beatmap are separated by empty line(s) and/or control sentences.
Do not include empty lines within a row.

In the rows part of the beatmap file,
any line started with a sharp symbol (`#`) (with possibly padding white characters) is ignored.
They serve as comments and help readers of the beatmap file to understand it.

Every row consists of one or several **voice**s.
Each voice consists of several **note**s and **bar line**s and is written within a line.
Every note is specified by its note length and multiplicity (simultaneous note in the same voice)
together with symbols denoting whether the note is hold, tied, beamed, etc.

### Control sentences

Before specifying the notes in a row, some **control sentence**s can be included for the row.
Each control sentence includes a keyword and one or more parameters,
separated by spaces.
Keywords are case-sensitive and are identifiers of various control sentences.
To find the specifications of control sentences, see [Control sentences](control-sentences).

#### Expressions

Some of the control sentences above use math expressions as parameters.
Parsing the math expressions are powered by [math.js](https://mathjs.org/).

There are two kinds of expressions: **expressions (with x)** and **expressions without x**.
When we say "expression" without indicating whether it is with x or without x,
it is an expression with x.

In expressions with x, there should be only one independent variable `x`, denoting the position in the row.
The position is measured according to notes' literal length but not their temporal length.

In expressions without x, there should be no independent variables.
Variables or functions defined by `LET` and `DEF` cannot appear in expressions without x
because they are dependent to x.

To find a full list of built-in variables that can be used in expressions without defining them yourself before hand,
see [Built-in identifiers](built-in-identifiers).

### Notes

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

### Making notes beamed or grouping (contrametric)

Notes can be **beam**ed (flags are connected) by enclosing them with parentheses.
Parenthesized notes without flags will not be beamed.

Beams can be created across bar lines (by inserting `|` between beamed notes)
but not across rows or voices.

**Grouping**s (tuplets) can be created by specifying a ratio after the closing parenthesis.
The ratio consists of two characters, each of which is within `[0-9a-z]` representing a number.
The first number divided by the second number is
the ratio of the seeming length of the grouping and the actual length of the grouping.
The second number can be omitted, and the default value of it is

$$\mathit{ratio}_2=2^{\left\lfloor\log_2\mathit{ratio}_1\right\rfloor},$$

where $\mathit{ratio}_1$ is the first number.

Here is an example of some notes and the rhythm they represent:

```text
2 (3 3 3)3 2 (4 4 4 4 4)5 | 2
```
<pre class="abc-pre">
X: 1
M: 4/4
K: perc stafflines = 1
V:T stem=up
B2 (3BBB B2 (5B/2B/2B/2B/2B/2 | B2
</pre>

### Bar lines

Bar lines are created by inserting a `|` (and spaces for separating it from notes) within a voice.
They can appear within a beamed group of notes.
They can also appear between two tied notes.
It is recommended to write a bar line at the end of each voice.

When calculating [score](game-mechanics#score), measures are taken into account.
Only the bar lines written in the first voice are effective in creating measures.
Bar lines in other voices are fake (it mainly serves as an auxiliary for the beatmapper).

Every bar line will extend all across the voices in the row
but not just the voice where it is written.
