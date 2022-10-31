---
layout: wiki-page
lang: en-US
title: Desktop app
---

## Install the desktop app

You can run the game locally on your Windows / Linux desktop without internet access if you install it as a desktop app.
*MacOS is not supported yet.*
Also, if you want to install the game on a 32-bit machine,
there are no pre-built packages, and you need to [build the app](#build-the-desktop-app) youself.

### Install on Windows

First, download the zip package for Windows from [releases](https://github.com/dododogame/dododo/releases).
Just extract the contents of the zip file to somewhere you want to install the game.
Then, you may launch the game by running the script `launcher.vbs` in the game directory.

Optionally, you may
[create a desktop shortcut](https://support.microsoft.com/en-us/office/create-a-desktop-shortcut-for-an-office-program-or-file-9a8df64b-cd87-4700-95cc-4bc3e2a962da)
for the file `launcher.vbs`.
There are icon files in the `www/icon` folder,
you may
[change the icon](https://support.microsoft.com/en-us/topic/how-to-arrange-or-move-icons-on-the-desktop-70e4d22a-d760-5585-449f-2a14c417f84c)
of the shortcut to the icon of the game.

### Install on Linux

First, download the tar.gz package for Linux from [releases](https://github.com/dododogame/dododo/releases).
Just extract the tar.gz file to somewhere you want to install the game.
Then, you may launch the game by running the script `launcher.sh` in the game directory.

Optionally, you may create a
[desktop entry](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html)
for executing the file `launcher.sh`.
The icon can be specified as the one in the `www/icon` folder.

Here is an example of the desktop entry (you should replace `/path/to/dododo` with the actual absolute path of the game):

```ini
[Desktop Entry]
Type=Application
Name=Dododo
Comment=The open-source community rhythm game with musical notations
Icon=/path/to/dododo/www/icon/icon.png
Exec=/path/to/dododo/launcher.sh
Path=/path/to/dododo/
Terminal=false
Categories=Game;
```

### Update the desktop app

To update the game, download the www-only version of the released package from
[releases](https://github.com/dododogame/dododo/releases),
and extract the `www` folder in it to replace the `www` folder of the old installed version.

## Build the desktop app

There is a Ruby script to wrap the game into a self-contained web app which can be run using [NW.js](https://nwjs.io/).
To build the desktop app, first [install Ruby](https://www.ruby-lang.org/en/documentation/installation/),
and then run

```shell
git clone https://github.com/dododogame/dododo.git
cd dododo
bundle install # and resolve all errors if there are any
rake build
```

You can build for different platforms (Windows or Linux) and for different architectures (ia32 or x64).
By default, the platform and the architecture are determined according to the OS on which you are building the app.
You may provide additional arguments for `rake build` to specify the platform and the architecture.

Currently, only the script for building for Windows and Linux are provided.
There are indeed NW.js releases for MacOS, but using it to build the app requires the toolchain that is only available on MacOS
(so actually you may try building the app without using the Ruby script if you have a MacBook).
Also, because there are no official releases for NW.js for machines of ARM architecture,
if you want to build the app for ARM architecture,
you need to download the community [NW.js ARM binaries](https://github.com/LeonardLaszlo/nw.js-armv7-binaries)
and specify the downloaded NW.js in the command-line argument `nwjs_path` (see the table below).

Here is a full list of available command-line arguments:

| Argument | Default                                                                                                                  | Available values | Description                                               |
|---------|--------------------------------------------------------------------------------------------------------------------------|------------------|-----------------------------------------------------------|
| `platform` | Determined by your OS                                                                                                    | `win`, `linux`   | The platform to build for                                 |
| `architecture` | Determined by your OS                                                                                                    | `ia32`, `x64`     | The architecture to build for                             |
| `quiet` | `false`                                                                                                                   | `true`, `false` | Whether to supress output                                 |
| `target_path` | `./pkg`                                                                                                                  | Any path | The path to the output directory                          |
| `temp_dir` | `~/.cache/dododo`                                                                                                        | Any path | The directory to store some downloaded or extracted files |
| `nwjs_version` | `0.67.1`                                                                                                                 | Any version | The version of NW.js to use if it is to be downloaded     |
| `nwjs_path` | `$temp_dir/nwjs-v$nwjs_version-$platform-$architecture.<ext>`, where `<ext>` is `tar.gz` or `zip` according to `platform` | Any path | The pre-downloaded NW.js to be used; will download for you if non-exist |
| `www_only` | `false`                                                                                                                  | `true`, `false` | Whether to build only the web files; no NW.js if true |
| `package` | `false` | `true`, `false` | Whether to package the app for distribution after building completes; will create a .tar.gz or .zip file according to `platform` |

For example, to build for 32-bit Windows and create a zip file for distribution, run

```shell
rake build platform=win architecture=ia32 package=true
```
