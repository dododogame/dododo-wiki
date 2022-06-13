# 谱面文件规范

*English (United States)*: [Beatmap file specifications](beatmap-spec)

Dododo 谱面是 `.ddd` 纯文本格式的文件。铺面文件由两部分组成，**文件头**和**行**的列表。这两个部分由 `---` 分隔。

以下只是一些规则。在阅读以下内容时，我们默认您已经对乐谱及乐谱的符号有一定的了解。

## 文件头

文件头由几个铺面基础设置组成，每个设置对位于一行中，与其对应的信息由 `: ` （冒号和空格）分隔。

以下设置可用：

### `title`

音乐的名称。

此设置应始终指定为简单、简短、唯一、直接的名称，以便用户可以快速识别音乐。

### `musicAuthor`

### `beatmapAuthor`

### `difficulty`

### `audioUrl`

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
