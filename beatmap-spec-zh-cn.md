# 谱面文件规范

*English (United States)*: [Beatmap file specifications](beatmap-spec)

Dododo 谱面是 `.ddd` 纯文本格式的文件。谱面文件由两部分组成，**文件头**和**行**的列表。这两个部分由 `---` 分隔。

以下只是一些规则。在阅读以下内容时，我们默认您已经对乐谱及乐谱的符号有一定的了解。

## 文件头

文件头由几个谱面基础设置组成，每个设置对位于一行中，与其对应的信息由 `: ` （冒号和空格）分隔。

以下设置可用：

### `title`

音乐的名称。

此设置应始终设置为为简单、简短、唯一、直接的名称，以便玩家可以快速识别音乐。

### `musicAuthor`

音乐的作者（艺术家）。

为简洁起见，作者的名字和中间名可以缩写为首字母。如果有多个作者，建议全部写出并用 `&` 连接名称。如果多个作者以不同的方式创作音乐（作曲家、作词家、演奏者等），建议在括号中写出此类信息。例如 W. A. Mozart (Composer) & S. Ligoratti (Player)。

### `beatmapAuthor`

谱面的作者（谱师）。

您可以使用您的昵称。

### `difficulty`

谱面的难度。

通常设置为 1 到 15 的整数。如果没有指定，难度就会默认设置为“未知”（不带引号）。虽然不推荐，但对于极其困难的谱面，您可以将难度设定为大于 15 的数字或“？？？”。

难度是用来衡量谱面难度的指标。

### `audioUrl`

音频文件的 url。

如果不设置，则玩家必须上传音频文件（如果通过上传文件播放），否则游玩时玩家将听不到任何音乐。

### `start`

### `end`

### `volume`

### `offset`

## 行

### 控制语句

#### `PERFECT`, `GOOD`, `BAD`

#### `BPM`

#### `MS_PER_WHOLE`

#### `TIME`

#### `SPACE_X`, `NOTE_X`, `HIT_X`

#### `SPACE_Y`, `WIDTH`, `HEIGHT`

#### `RED`, `GREEN`, `BLUE`, `ALPHA`

#### `BLEND_MODE`

#### `FAKE_JUDGE_LINE`

#### 数学表达式

<!-- 翻译者请注意: 翻译此处的表格时对照该文件: https://github.com/UlyssesZh/dododo/blob/master/js/Strings.js -->

### 音符

### 用符杠连接音符, 以及连音

### 小节线
