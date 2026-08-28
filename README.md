# 攀山快答 · 教师改编版

一个可以直接拿去改的华文词语游戏。90 秒，看词语选释义，答对往上爬一格，答错扣三秒。

原版是「词山学海」里的攀山快答。这个版本是为了让老师改而重写的：一个 HTML 文件、
一个词语文件、三张图，没有任何外部依赖。

**主线做法：把你的 Excel 词语表交给 Claude，让它改；再用 GitHub 变成一个网址发给学生。**
全程在浏览器里，不必装任何东西，不必碰终端机，不必会编码。

---

## 第一步 · 填一份词语表

用这个仓库里的 **`词语表模板.xlsx`**（或 `词语表模板.csv`）。

两栏：`词语`、`释义`。把内容换成你自己单元的就好，第一行不要动。
至少 8 个词语，越多越好（最少 4 个）。

**错误选项不用你写。** 程序会自动从你其他词语的释义里抓三个当干扰项，
所以词语越多，题目越有挑战性。

---

## 第二步 · 交给 Claude 改

### 2.1 下载这个游戏

页面右上角绿色的 **Code** 按钮 → **Download ZIP** → 解压。

### 2.2 开一个 Claude Project

到 [claude.ai](https://claude.ai) → **Projects** → 新建一个 → 把**整个游戏资料夹**
和**你的词语表**一起上传进去。

Project 的好处是：这些文件会一直留在里面。以后要换单元，回到同一个 Project
再说一句就行，不必重新上传。

### 2.3 贴这段提示词

```
我是中学华文老师，不会编码。
我已经把一个小游戏的资料夹和一份词语表格上传到这个 Project 里。

请帮我做三件事：
1. 读我上传的表格，把里面的词语和释义，照 my-words.js 原本的格式
   重新写成一个完整的 my-words.js 给我下载。格式不要动，只换内容。
2. 把 UNIT_NAME 改成：〔你的单元名称〕
3. 把 SECONDS 改成：〔90〕

改好之后直接给我可以下载的 my-words.js，并告诉我放回哪个位置。

如果我的表格有问题（缺了释义、词语重复、少于 8 个），请先告诉我，不要自己猜。
```

最后那一句是整段里最要紧的：**你要它先报告问题，而不是替你蒙混过去。**
判断它做得对不对，是你的工作，不是它的。

### 2.4 换下来，打开看看

把 Claude 给你的 `my-words.js` 放回资料夹（覆盖原来那个），
双击 `index.html`，就在浏览器里跑起来了。

**改了之后，回到浏览器刷新**（Mac `Cmd + R`，Windows `Ctrl + R`）。

### 2.5 还想改别的，就接着说

```
我想再改几个地方：
- 开始画面的标题改成：〔…〕
- 主色调改成：〔…〕
- 答错扣的秒数改成：〔…〕
- 人爬到画面多高，山壁才开始往下卷：〔…〕

改完请把整个 index.html 给我下载。
```

---

## 第三步 · 变成一个网址，发给学生

**不需要装 Git，也不需要用终端机**，全在网页上点：

1. 到 [github.com/new](https://github.com/new)，取一个仓库名字，选 **Public**，
   点 **Create repository**
2. 在新仓库的页面点 **uploading an existing file**
3. 把你资料夹里的东西**整个拖进去**（记得连 `art` 资料夹一起），
   然后 **Commit changes**
4. **Settings** → **Pages** → Source 选 **Deploy from a branch**
   → 分支选 **main** → 资料夹选 **/ (root)** → **Save**
5. 等一两分钟，打开 `https://你的用户名.github.io/你的仓库名/`

这个网址就可以发给学生了。免费，不限人数，没有广告，学生那边什么都不用装。

**以后要换词语**：在 GitHub 网页上点开 `my-words.js` → 铅笔图标 → 改 →
**Commit changes**。一两分钟后网址上就更新了。改坏了也不怕，
GitHub 每一次改动都留着，随时可以退回去。

---

## 不想用 Claude？也可以自己改

用记事本（Windows）或「文本编辑」（Mac）打开 **`my-words.js`**，只改这一段：

```js
const UNIT_NAME = "中三 单元一";     // 单元名称，会显示在开始画面
const SECONDS   = 90;                // 每局几秒

const VOCAB = [
  { word: "维护", def: "保持、保障，使不受破坏" },
  { word: "策略", def: "为了达到某个目标而定下的计划或方法" },
  // 照这个格式往下加，别忘了行尾的逗号
];
```

三条规则：每一行都是 `{ word: "词语", def: "释义" },`；行尾要有逗号；
至少 4 个词语。

整个资料夹里，你只需要动 `my-words.js` 这一个文件。

> Mac 上请**右键 → 打开方式 → 文本编辑**，不要直接双击，免得被别的程序接手。

---

## 常见问题

**打开是一片空白，或出现「词语表好像有点问题」**

页面会直接告诉你第几行写错了。九成是这三样之一：行尾少了逗号、引号少了一边、
大括号少了一边。照着提示改，刷新就好。**它不会给你一片空白让你猜。**

**Claude 给我的文件下载到哪里去了？**

多半在「下载 / Downloads」资料夹。把它拖回游戏资料夹，覆盖掉原来的
`my-words.js` 就行。

**GitHub Pages 打开是 404**

刚开启 Pages 要等一到两分钟才生效。等一下，然后强制刷新
（Mac `Cmd + Shift + R`，Windows `Ctrl + F5`）。

**学校网络打不开 GitHub 或 claude.ai**

有些学校的网络会挡。用手机热点，或者回家再弄。
「不想用 Claude？」那条路完全不需要网络。

**词语很多会不会太慢？**

不会。几百个词语都没问题，程序每次只抽一个。

---

## 换个角色（选做）

`art/climber.png` 是一张 6 格并排的动作图。用 ChatGPT、Claude 或其他 AI 绘图工具
都能生成一张新的换掉它。规格必须说死，不然做出来的图拼不进游戏里：

```
请帮我生成一张角色动作图。规格必须完全照做：
- 6 格横向并排，每一格等宽等高
- 角色朝右
- 六个动作依序：站立、走A、走B、爬A、爬B、举手庆祝
- 背景纯洋红色 #FF00FF，或直接给我透明背景的 PNG
- 画面上不要有任何文字、字母、数字或标志

角色是：〔描述你想要的角色〕
```

下载后改名为 `climber.png`，放回 `art/` 资料夹，刷新就看得到。

如果新图的格子宽高比跟原来不一样，让 Claude 把 `index.html` 里 `.climber`
那几行的 `width` 和 `height` 调一下就好。

---

## 出处

原版「攀山快答」是[词山学海](https://btvssclunit.github.io/VocabSummit)的一部分。

这个教师改编版由 [Chun Kai Xin 郑凯欣](https://kaixinbuilds.github.io) 为
「2026 AI in Sec CL NLC」工作坊重写。MIT 许可，欢迎自由改编，保留署名即可。

`art/` 里的图片一并提供给老师教学与改编使用。换成自己的当然更好，但不是必须。

做出来了？欢迎让我看看。

---

# VocabClimb Starter (English)

A Chinese vocabulary climbing game teachers can adapt without writing code.
90 seconds, match the word to its meaning, climb one ledge per correct answer,
lose three seconds per mistake.

**The main path:** fill in `词语表模板.xlsx`, upload it together with this folder to a
[claude.ai](https://claude.ai) Project, and ask Claude to rebuild `my-words.js` from your
spreadsheet. Then publish it by dragging the folder into a new GitHub repository and
switching on Pages under Settings → Pages (branch `main`, folder `/ (root)`).
No install, no terminal, no coding.

You can also just edit `my-words.js` by hand in any plain text editor. Wrong answers are
always generated from your other entries, so you never write distractors. A broken word
list names the offending line on screen rather than showing a blank page.

Adapted from 攀山快答 in [VocabSummit](https://btvssclunit.github.io/VocabSummit).
MIT licensed. Art assets included for teaching use and adaptation.
