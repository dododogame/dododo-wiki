---
layout: wiki-page
lang: en-US
title: Beatmapping from scratch
---

This is a walk-through guide for people who write beatmaps for Dododo for the first time.

If you are unfamiliar with sheet music, search for and read something about sheet music
(such as [this](https://www.simplifyingtheory.com/how-to-read-sheet-music-for-beginners/))
before you continue to read the rest of the guide.

## Step 1: Prepare for you tools of beatmapping

Because Dododo beatmap files are actually plain text files,
you can use any text editor you like to write beatmaps.
If you use a Windows computer, you can use the built-in text editor (notepad.exe).
Some well-known text editors are recommended:
[Sublime Text](https://www.sublimetext.com/), [Visual Studio Code](https://code.visualstudio.com/),
etc., are all good choices.
(Developing plugins for writing Dododo beatmaps for various text editors is in the plan.
You can install such plugins in the future if they come out eventually.)

In addition to the text editor, you also need software for playing the music
that has millisecond-precision and can show the waveform of the audio.
It is better if the software can filter the audio and can change the tempo of playback.
Usually, any audio processing software is capable for this, such as [Audacity](https://www.audacityteam.org/).

## Step 2: Find the music that you would like to create a beatmap for

People have composed many pieces of music, some of which are specially for rhythm games.
You can pick any of them, but you should note about the artist's permission about this use of music.
If the music is licensed under a [Creative Commons](https://creativecommons.org/) license
or the artist claims publicly that the music can be used to create rhythm game charts (for non-commercial purposes),
you are usually free to pick that music.
Otherwise, if the artist has not claimed about the extent to which the use of the music is permitted,
you had better contact the artist for asking whether you can legally create a beatmap for the music.

It is also recommended that you pick a music that has steady tempo.
If the tempo of the music changes frequently, it is hard to create a beatmap for it
(because you need to tweak the tempo frequently to make the music and the notes in the beatmap to synchronize).
Usually, a human-played music (without the auxiliary of a metronome) is not considered to have steady tempo.

It is also not recommended to use a music that is too long.
A typical length of a music for rhythm games is 1.5--3 minutes.
However, nobody forces you not to create a beatmap for a music that is even longer than 5 minutes
(which is usually considered a marathon).

In this guide,
[*Big-D*](https://files.freemusicarchive.org/storage-freemusicarchive-org/tracks/MQ8JO0BqKl2UADzKg74rwoY7mapqBT4uWpQYciTJ.mp3)
(artist: Shaolin Dub) is picked. License of music:
[![CC BY-NC-ND 4.0](https://licensebuttons.net/l/by-nc-nd/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

## Step 3: Create and start editing the beatmap file

The beatmap file is a plain text file with the extension `.ddd`.
Depending on your operating system, there are different ways of creating a new file.

To edit a plain text file, you need a plain text editor.
On Windows, there is a built-in plain text editor called Notepad.
There are also many other plain text editors,
such as [Sublime Text](https://www.sublimetext.com/), [Visual Studio Code](https://code.visualstudio.com/), etc.

## Step 3: Write the header

The [header](beatmap-spec#header)
(go to the link to see the format) is where you write the metadata of the beatmap,
including the title, artist, difficulty, etc.

Here is an example of the header:

```plain
title: Big-D
musicAuthor: Shaolin Dub
beatmapAuthor: UlyssesZhan
difficulty: 6
start: 0
end: 185809
offset: 68
volume: 1.2
---
```

Remember to end the header with three hyphens (`---`).

## Step 4: Write the rows

<!-- TODO -->

## Step 5: Add special effects (optional)

<!-- TODO -->

## Step 6: Play it yourself

<!-- TODO -->

## Step 7: Publish the beatmap

<!-- TODO -->
