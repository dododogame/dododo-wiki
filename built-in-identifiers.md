# Built-in identifiers

*中文 (中国)*: [预设标识符](built-in-identifiers-zh-cn)

There is an `if` function that can be used to help express piecewise functions.
Its syntax is
```text
if(<condition1>, <value1>[, <condition2>, <value2>[, ... ]][, <elseValue>])
```
It is the same as
```text
condition1 ? value1 : condition2 ? value2 : ... : elseValue
```
All variables set by the gamer in preferences can be used in the math expressions
(they are also independent of x, so they can also be used in expressions without x):

| Variable                 | Meaning                                      | Type     | Default                                     |
|--------------------------|----------------------------------------------|----------|---------------------------------------------|
| `playRate`               | Play rate (speed of music)                   | Number   | `1.0`                                       |
| `autoPlay`               | Auto-play                                    | Boolean  | `false`                                     |
| `noBad`                  | No-bad mode                                  | Boolean  | `false`                                     |
| `noExcess`               | No-excess mode                               | Boolean  | `false`                                     |
| `judgeWindow`            | Judgement window (smaller is stricter)           | Number   | `1.0`                                       |
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
| `judgementLinePerformances`  | Enable ornamental judgement line effects         | Boolean  | `true`                                      |
| `flashWarningGood`       | Warn by flash the screen at good hits        | Boolean  | `false`                                     |
| `falshWarningMiss`       | Warn by flash the screen at combo breaks     | Boolean  | `true`                                      |
| `showInaccuracyData`     | Show inaccuracy data                         | Boolean  | `true`                                      |
| `comboPopupInterval`     | Interval of combo popups (set 0 to disable)  | Number   | `25`                                        |
| `fadeIn`                 | Fade-in (ratio to resolution, 0 to disable)  | Number   | `0.0`                                       |
| `fadeOut`                | Fade-out (ratio to resolution, 0 to disable) | Number   | `0.0`                                       |
| `reverseVoices`          | Reverse voices                               | Boolean  | `false`                                     |
| `mirror`                 | Mirror (flip horizontally)                   | Boolean  | `false`                                     |
| `mirrorLowerRow` | Mirror the lower row | Boolean | `false` |
| `showKeyboard`           | Show keyboard pressings                      | Boolean  | `false` on mobile devices, otherwise `true` |
| `subtractScore`          | Subtract instead of adding score             | Boolean  | `false`                                     |
| `numbersHUD`             | Show numbers of perfect hits etc. in-game    | Boolean  | `true`                                      |
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
| `barLinesHeight`         | Height of bar lines                           | Number   | `256`                                       |
| `hitEffectRadius`        | Radius of hit effects                        | Number   | `32`                                        |
| `distanceBetweenRows`   | Distance between beatmap rows                | Number   | `384`                                       |
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
| `useWebGL`               | Use WebGL to render (restart to take effect) | Boolean  | `true` if WebGL is supported                |
| `enableHitSound`         | Enable hit sound                             | Boolean  | `true`                                      |
| `hitSound`               | Hit sound                                    | String   | `'snare_drum_1.ogg'`                        |
| `hitSoundWithMusic`      | Hit sound with music instead of input        | Boolean  | `false`                                     |
| `countdownBeats`         | Beat by hit sound when counting down         | Boolean  | `false`                                     |
| `musicVolume`            | Volume of music                              | Number   | `1.0`                                       |
| `hitSoundVolume`         | Volume of hit sound                          | Number   | `2.0`                                       |
| `masterVolume`           | Master volume                                | Number   | `1.0`                                       |
| `language`               | Language                                     | String   | According to browser settings               |

Note that here the strings are 7-character lower-case hexadecimal notation of colors.
To get the RGB values (in $[0, 1]$), you can use the methods `red()`, `green()`, `blue()`.
For example, `'#4c8cff'.red()` returns approximately `0.298`, which is `0x4c / 0xff`. 

The preferences items related to [game modifiers](Game-modifiers) and visuals are not recommended to be used
because they will be different from the actual in-game settings when the user is replaying something.

