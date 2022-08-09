# Control sentences

*中文 (中国)*: [控制语句](control-sentences-zh-cn)

In the beatmap file, before specifying the notes in a row,
some **control sentence**s can be included for the row.
Each control sentence includes a keyword and one or more parameters,
separated by spaces.
Keywords are case-sensitive and are identifiers of various control sentences.

The following are specifications of the control sentences.
Sometimes these control sentences make use of an expression or an expression without x,
see [Expressions](beatmap-spec#expressions).

## `PERFECT`, `GOOD`, `BAD`

Syntax:

```text
PERFECT <windowRadius>
```

```text
GOOD <windowRadius>
```

```text
BAD <windowRadius>
```

These control sentences accept one parameter, indicating the radius of the judgement window.
The `windowRadius` is NOT in milliseconds but is the ratio of the inaccuracy tolerance for a perfect / good / bad judge
and the total (temporal) length of the row.
Therefore, given the same radius of judgement window, judging will be stricter if the row is shorter (in time).

## `BPM`

(Also alised as `BEATS_PER_MINUTE`.)

Syntax:

```text
BPM <beatNote1> <beatsPerMinute1>[ <position1>[ <beatNote2> <beatsPerMinute2> <position2>[ ... ]]]
```

The `beatNote` is a note specified in the same manner [here](beatmap-spec#notes).
The `beatsPerMinute` is the number of beats per minute,
meaning that one minute is exactly `beatsPerMinute` times as long as the beat note.
The `position` is the position of the BPM change, specified as a rational number in $[0, 1]$,
with the start of the row being 0 and the end of the row being 1.
The position is calculated according to notes' literal length but not their temporal length
(e.g. a quavar in 180 BPM and one in 200 BPM has the same literal length because they are both quavars).

## `MS_PER_WHOLE`

(Also alised as `MILLISECONDS_PER_WHOLE`.)

Syntax:

```text
MS_PER_WHOLE <millisecondsPerWhole>
```

This sets the average temporal length of a whole note in milliseconds.
Usually this can be automatically calculated by the game according to the BPM specified by [`BPM`](#bpm),
or inherit from last row.
However, sometimes it is necessary to specify it manually, especially when using [`TIME`](#time).

## `TIME`

Syntax:

```text
TIME <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [Expressions](beatmap-spec#expressions).

The expression is a mapping from $[0, 1]$ to $[0, 1]$.
It *must* be monotonically increasing (because you cannot travel to the past).
It maps the position in the row to the time at which the position in the row is played.
The position mapped to 0 is played exactly when the row starts being played,
and the position mapped to 1 is played exactly when the row ends being played
(and when the next row starts being played).
For example, with the expression `sqrt(x)` you can have the tempo linearly
(w.r.t. notes' literal lengths) increasing from 0.

Default: `x`.

## `JUDGEMENT_LINE_X`, `NOTE_X`, `HIT_X`, `BAR_LINE_X`

Syntax:

```text
JUDGEMENT_LINE_X <expression>
```

```text
NOTE_X <expression>
```

```text
HIT_X <expression>
```

```text
BAR_LINE_X <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [Expressions](beatmap-spec#expressions).

The expression is a mapping from $[0, 1]$ to $[0, 1]$.
The `JUDGEMENT_LINE_X` sentence maps the position of the row (according to note lengths) to the spatial position.
The position mapped to 0 is drawn at the leftmost place,
and the position mapped to 1 is drawn at the rightmost place.
It is not necessarily monotonically increasing (to possibly make the judgement line move to the left)
or being continuous (to possibly make the judgement line jump suddenly).

`NOTE_X` and `HIT_X` do similar things to what `JUDGEMENT_LINE_X` does,
but `NOTE_X` defines the spatial position of drawn notes
while `HIT_X` defines the spatial position of the hit effects.

<!-- TODO BAR_LINE_X -->

The default setting of `JUDGEMENT_LINE_X` is `x`.
The default setting of `NOTE_X` is to be the same as `JUDGEMENT_LINE_X`.
The default setting of `HIT_X` is to be the same as `NOTE_X`.
The default setting of `BAR_LINE_X` is to be the same as `NOTE_X`.

## `JUDGEMENT_LINE_Y`, `JUDGEMENT_LINE_WIDTH`, `JUDGEMENT_LINE_HEIGHT`

Syntax:

```text
JUDGEMENT_LINE_Y <expression>
```

```text
JUDGEMENT_LINE_WIDTH <expression>
```

```text
JUDGEMENT_LINE_HEIGHT <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [Expressions](beatmap-spec#expressions).

These control sentences are purely for ornamental performance of the judgement line
because they do not affect the (spatial and temporal) arrangement of notes.
The expressions are mappings on $[0, 1]$, and the mapped values are lengths in unit of pixels.

`JUDGEMENT_LINE_Y` is the vertical position of the judgement line.
Positive values mean to place the judgement line at specified number of pixels above the default position.
Default: `0`.

`JUDGEMENT_LINE_WIDTH` is the width of the judgement line. Default: `1`.

`JUDGEMENT_LINE_HEIGHT` is the height of the judgement line. Default: `voicesHeight` times the number of voices.

These control sentences are ineffective if the user disabled ornamental judgement line performances
in the preferences.

## `JUDGEMENT_LINE_RED`, `JUDGEMENT_LINE_GREEN`, `JUDGEMENT_LINE_BLUE`, `JUDGEMENT_LINE_ALPHA`

(`JUDGEMENT_LINE_ALPHA` is also alised as `JUDGEMENT_LINE_OPACITY`.)

Syntax:

```text
JUDGEMENT_LINE_RED <expression>
```

```text
JUDGEMENT_LINE_GREEN <expression>
```

```text
JUDGEMENT_LINE_BLUE <expression>
```

```text
JUDGEMENT_LINE_ALPHA <expression>
```

Here `<expression>` is a single-variable mathematical expression of variable `x`.
See [Expressions](beatmap-spec#expressions).

These control sentences are also purely for ornamental performance of the judgement line.
They are used to change the color of the judgement line.
These expressions are mappings from $[0, 1]$ to $[0, 1]$, and the default of them are all `1`
(pure and non-transparent white).

These control sentences are ineffective if the user disabled ornamental judgement line performances
in the preferences.

## `JUDGEMENT_LINE_ROTATION`

<!-- TODO -->

## `JUDGEMENT_LINE_ANCHOR_X`, `JUDGEMENT_LINE_ANCHOR_Y`

<!-- TODO -->

## `JUDGEMENT_LINE_Z`

<!-- TODO -->
## `JUDGEMENT_LINE_BLEND_MODE`

Syntax:

```text
JUDGEMENT_LINE_BLEND_MODE <blendModeName>
```

This control sentence changes the blend mode of the judgement line.
Available options for `blendModeName` are (alphabetically, case-insensitive)

- `ADD`,
- `ADD_NPM`,
- `COLOR`,
- `COLOR_BURN`,
- `COLOR_DODGE`,
- `DARKEN`,
- `DIFFERENCE`,
- `EXCLUSION`,
- `HARD_LIGHT`,
- `HUE`,
- `LIGHTEN`,
- `LUMINOSITY`,
- `MULTIPLY`,
- `NORMAL`,
- `NORMAL_NPM`,
- `OVERLAY`,
- `SATURATION`,
- `SCREEN`,
- `SCREEN_NPM`,
- `SOFT_LIGHT`.

If the player enables the WebGL render in his preferences,
only `NORMAL`, `ADD`, `MULTIPLY`, and `SCREEN` are supported,
and the other blend modes silently act like `NORMAL`.

(It seems that there lacks documents about how these blend modes work. You can look at
[this document](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/globalCompositeOperation)
as a reference or just play around by yourself.)

Default: `NORMAL`.

## `FAKE_JUDGEMENT_LINE`

Syntax:

```text
FAKE_JUDGEMENT_LINE [<label>]
```

This control sentence creates a new judgement line for this row of beatmap but a fake one
(which does not affect the gameplay but is purely ornamental).
After this control sentence, you can add the following control sentences
to define the behaviors of the new fake judgement line without affecting the judgement lines
defined previously:

- [`JUDGEMENT_LINE_X`](#judgement_line_x-note_x-hit_x),
- [`JUDGEMENT_LINE_Y`](#judgement_line_y-judgement_line_width-judgement_line_height),
- [`JUDGEMENT_LINE_Z`](#judgement_line_z),
- [`JUDGEMENT_LINE_RED`](#judgement_line_red-judgement_line_green-judgement_line_blue-judgement_line_alpha),
- [`JUDGEMENT_LINE_GREEN`](#judgement_line_red-judgement_line_green-judgement_line_blue-judgement_line_alpha),
- [`JUDGEMENT_LINE_BLUE`](#judgement_line_red-judgement_line_green-judgement_line_blue-judgement_line_alpha),
- [`JUDGEMENT_LINE_ALPHA`](#judgement_line_red-judgement_line_green-judgement_line_blue-judgement_line_alpha),
- [`JUDGEMENT_LINE_WIDTH`](#judgement_line_y-judgement_line_width-judgement_line_height),
- [`JUDGEMENT_LINE_HEIGHT`](#judgement_line_y-judgement_line_width-judgement_line_height),
- [`JUDGEMENT_LINE_ANCHOR_X`](#judgement_line_anchor_x-judgement_line_anchor_y),
- [`JUDGEMENT_LINE_ANCHOR_Y`](#judgement_line_anchor_x-judgement_line_anchor_y),
- [`JUDGEMENT_LINE_ROTATION`](#judgement_line_rotation),
- [`JUDGEMENT_LINE_BLEND_MODE`](#judgement_line_blend_mode).

You can create more fake judgement lines by using `FAKE_JUDGEMENT_LINE` again
after finishing defining the previous fake judgement line.
Later created fake judgement lines appear on top of previously created fake judgement lines.
Fake judgement lines appear on top of the real judgement line.

You can also specify the `label` parameter to give the fake judgement line a label for it to be referred to later.
Here, `label` is specified as an expression without x.
If the a judgement line with the specified `label` does not exist in the current row,
a new fake judgement line will be created for the row.
If a judgement line with the specified `label` is already created in the current row,
you can now use those `JUDGEMENT_LINE_*` control sentences to modify the judgement line with the label.

This control sentence is not effective if the user disables ornamental judgement line performances
in the preferences.

## `GENUINE_JUDGEMENT_LINE`

Syntax:

```plain
GENUINE_JUDGEMENT_LINE
```

<!-- TODO -->

## `TEXT`

## `TEXT_TEXT`

## `TEXT_X`, `TEXT_Y`, `TEXT_Z`, `TEXT_ANCHOR_X`, `TEXT_ANCHOR_Y`, `TEXT_ROTATION`, `TEXT_RED`, `TEXT_GREEN`, `TEXT_BLUE`, `TEXT_ALPHA`, `TEXT_BLEND_MODE`

## `TEXT_SCALE_X`, `TEXT_SCALE_Y`

## `LET`

Syntax:

```text
LET <identifier> <expression>
```

`LET` can define a variable in the scope with x.
After a variable is defined by `LET`, it can be referred to in any expression with x,
but it cannot be referred to in any expression without x.
The `identifier` must consist only of digits, letters, or underscores, and not start with a digit (in regexp: `[a-zA-Z_]\w*`).
The rule also applies to the identifier specified to variables defined by [`DEF`](#def), [`VAR`](#var), and [`FUN`](#fun).

Example 1:

```plain
LET y x^2
TIME (x+y)/2
```

In this example, a variable with x `y` is defined using `LET`.
It is then referred to in the `TIME` control sentence.
This is equivalent to

```plain
TIME (x+x^2)/2
```

Example 2:

```plain
LET y x^2
TIME (x+$y)/2
JUDGEMENT_LINE_X (x+y)/2
LET y x^3
```

In this example, the variable `y` is value-lockedly referred to in the `TIME` control sentence
(because it is referred to as `$y` with the dollar symbol).
If the reference of a variable is value-locked, it will not be affected if the variable is overridden in the future.
However, the variable `y` is normally referred to in the `JUDGEMENT_LINE_X` control sentence.
The codes are equivalent to

```plain
TIME (x+x^2)/2
JUDGEMENT_LINE_X (x+x^3)/2
```

## `DEF`

(Also aliased as `DEFINE`.)

Syntax:

```plain
DEF <identifier> <parameters> <expression>
```

`DEF` defines a function in the scope with x.
`parameters` is a list of parameter names seperated by commas (`,` without whitespace).
In `expression`, the parameters can be referred to as independent variables, as well as `x`.

A function defined by `DEF` can be invoked in any expression with x.
When a function defined by `DEF` is invoked, parentheses should be used to specify the value of parameters.
Functions defined by `DEF` cannot be referred to in expressions without x.

The parameters list cannot be empty.
Actually, if the parameters list is empty, it should be defined using [`LET`](#let) instead of `DEF`.

Example 1:

```plain
DEF f m x^m
TIME (x+f(2))/2
```

In this example, the function `f` is defined using `DEF`,
and it has one parameter called `m`.
Then, the function is referred to and invoked in the `TIME` control sentence,
with the parameter `m` having value `2`.
The codes are equivalent to

```plain
TIME (x+x^2)/2
```

Example 2:

```plain
DEF f m (x + x^m) / 2
TIME $f(2)
JUDGEMENT_LINE_X f(3)
DEF f m log(1 + m x) / log(1+m)
```

In this example, the function `f` is value-lockedly referred to in the `TIME` control sentence,
while it is referred to normally in the `JUDGEMENT_LINE_X` control sentence.
The codes are equivalent to

```plain
TIME (x + x^2) / 2
JUDGEMENT_LINE_X log(1 + 3 x) / log(4)
```

## `VAR`

(Also aliased as `VARIABLE`.)

Syntax:

```plain
VAR <identifier> <expressionWithoutX>
```

`VAR` sentences define variables in the scope without x.
Such variables can be referred to in both expressions with x and expressions without x.

Example 1:

```plain
VAR a 2003
VAR b a - 895
VAR a 520

# outputs 520:
DEBUG_LOG a

# outputs 1108:
DEBUG_LOG b
```

Example 2:

```plain
VAR m 2
TIME (x+x^m)/2
JUDGEMENT_LINE_X (x+x^$m)/2
VAR m 4
```

This example illustrates that variables defined by `VAR` can be referred to in a value-locked way.
It is equivalent to

```text
TIME (x+x^4)/2
JUDGEMENT_LINE_X (x+x^2)/2
```

## `FUN`

(Also aliased as `FUNCTION`.)

Syntax:

```plain
FUN <identifier> <parameters> <expressionWithoutX>
```

`FUN` defines functions in the scope without x.
`parameters` is a list of parameters separated by commas (`,` without whitespace).

The parameters list cannot be empty.
However, functions with no parameters cannot be defined by [`VAR`](#var)
(this case is different from how [`DEF`](#def) and [`LET`](#let) can replace each other).
Technically, you cannot define a function with no parameters in the scope without x,
but a workaround is to just ignore what you have put in the parameters list (see example 2).

Example 1:

```plain
FUN pythagoras a,b sqrt(a^2+b^2)

# outputs 5:
DEBUG_LOG pythagoras(3,4)
```

Example 2:

```plain
VAR m 1
FUN f _ $m
FUN g _ m
VAR m 2

# outputs 1:
DEBUG_LOG f()

# outputs 2:
DEBUG_LOG g()
```

## `PROCEDURE`

Syntax:

```plain
PROCEDURE <keyword>
  <block>
END
```

`PROCEDURE` enable you to define your own control sentences (without parameters).
`keyword` specifies the keyword of the new control sentence,
which is case-sensitive and must consist of digits, letters, and underscores and start with capitalized letters or an underscore
(regexp: `[A-Z_]\w*`).
`block` contains a sequence of control sentences which will be executed when the newly-defined control sentence is invoked.

If a control sentence with keyword being the same as the `keyword` here,
the old one will be overridden by the newly-defined one.
The aliases of the old one will not be affected (see [`ALIAS`](#alias)).

Example:

```plain
# This control sentence can calculate the factorial of variable `input` and print it
PROCEDURE PrintFactorialOfInput
  VAR result 1
  VAR i 1
  WHILE i <= input
    VAR result result * i
    VAR i i + 1
  END
  DEBUG_LOG result
END

VAR input 5

# outputs 120:
PrintFactorialOfInput
```

## `UNPROCEDURE`

Syntax:

```plain
UNPROCEDURE <keyword> [<keyword2> [...]]
```

`UNPROCEDURE` can undefine control sentences specified by `keyword` etc.
If the newly-undefined control sentence has any aliases,
the aliases will not be affected (see [`ALIAS`](#alias)).

## `ALIAS`

Syntax:

```plain
ALIAS <newKeyword> [<newKeyword2> [...]] <oldKeyword>
```

`ALIAS` defines new control sentences which have the same effect as the control sentence specified by `oldKeyword`,
but with different keyword specified by `newKeyword` etc.

Example 1:

```plain
ALIAS DL DEBUG_LOG
UNPROCEDURE DEBUG_LOG

# outputs "Hello, world!" (without quotes):
DL 'Hello, world!'
```

Example 2:

```plain
PROCEDURE SomeProcedure
  DEBUG_LOG 'old'
END
ALIAS OldSomeProcedure SomeProcedure
PROCEDURE SomeProcedure
  OldSomeProcedure
  DEBUG_LOG 'new'
END

# outputs "old", and then outputs "new" (without quotes):
SomeProcedure
```

## `IF`

Syntax:

```plain
IF <expressionWithoutX>
  <block>
[ELSE_IF <expressionWithoutX2>
  <block2>]
[...]
[ELSE
  <blockN>]
END
```

`IF` helps you build up control flow of control sentences.

## `WHILE`

Syntax:

```plain
WHILE <expressionWithoutX>
  <block>
END
```

`WHILE` helps you build up control flow of control sentences.
Control sentences in `block` will be executed cyclically while `expressionWithoutX` evaluates true.

In `block`, [`BREAK`](#break) can be used to jump out of the cycle.

Example:

```plain
# This control sentence can calculate the factorial of variable `input` and print it
PROCEDURE PrintFactorialOfInput
  VAR result 1
  VAR i 1
  WHILE i <= input
    VAR result result * i
    VAR i i + 1
  END
  DEBUG_LOG result
END

VAR input 5

# outputs 120:
PrintFactorialOfInput
```

## `FOR`

Syntax:

```plain
FOR <variable>[,<indexVariable>] <expressionWithoutX>
  <block>
END
```
<!-- TODO -->

## `BREAK`

Syntax:

```plain
BREAK[ <layer>]
```

`BREAK` makes the execution of control sentences jump out of cycles.
It can only be used inside blocks of cycles like [`WHILE`](#while).

`layer` is a non-negative integer.
It specifies how many layers out of which this `BREAK` control sentence jumps.
If `layer` is not specified, the default value is `0`, which means jump out of one layer of cycle.

Example 1:

```plain
# outputs 1, 2, 3, 4, 5 one by one:
VAR m 0
WHILE true
  IF m > 5
    BREAK
  END
  DEBUG_LOG m
  VAR m m + 1
END
```

Example 2:

```plain
VAR n 0
WHILE true
  WHILE true
    IF n > 5
      # breaks the outer cycle
      BREAK 1
    END
    VAR n n + 1
  END
END

# outputs 6
DEBUG_LOG n
```

## `DEBUG_LOG`

Syntax:

```plain
DEBUG_LOG <expressionWithoutX>
```

`DEBUG_LOG` is used to output something in the console.
It does not affect anything else.

## `COMMENT`

Syntax:

```plain
COMMENT <anything>
```

This control sentence is of no use.
