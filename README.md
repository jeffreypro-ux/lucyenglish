# Lucy 的英语复习站

专为学生 Lucy 做的英语口语复习网站：**每节课可互动笔记 + 四级真人发音单词卡**。零后端、内容驱动，双击 `index.html` 即可打开使用，进度自动存在本机浏览器。

## 目录
- `index.html` — 网站入口（页面骨架 + 导航）
- `assets/app.js` — 全部交互逻辑（路由、发音、测验、单词卡、进度）
- `assets/styles.css` — 自定义样式（翻卡 3D、配色等）
- `data/lessons.js` — **课程笔记数据**（加课就改这里）
- `data/words.js` — **四级单词数据**（加词就改这里）

## 如何预览
- 最简单：双击 `index.html`。
- 或起本地服务器（推荐，避免个别浏览器对本地文件的限制）：
  ```bash
  cd 本目录
  python3 -m http.server 8000
  # 浏览器打开 http://localhost:8000
  ```

## 如何持续更新（一节课一页）
打开 `data/lessons.js`，里面是 `window.LESSONS = [ ... ]` 数组。每加一节课，**复制一个 lesson 对象**改 `id`（不能重复）、`title`、`subtitle`、`lessonDate`、`summary` 和 `blocks` 即可，网站会自动多出一页（网址形如 `#/lesson/2`）。

`blocks` 支持 6 种板块（按需要选用）：
| type | 含义 | content 结构 |
|------|------|------|
| `points` | 知识点 | `{items:[{title, detail}]}` |
| `sentences` | 句型操练 | `{items:[{zh, en, note}]}` |
| `mistakes` | 易错纠正 | `{items:[{wrong, right, tip}]}` |
| `dialogue` | 情景对话 | `{items:[{speaker, text, zh}]}` |
| `vocab` | 课堂生词 | `{items:[{word, meaning, example}]}` |
| `homework` | 课后作业 | `{items:[{title, detail}]}` |

> 句子（`sentences`）和生词（`vocab`）板块会自动生成「本课测验」选择题。

## 如何加四级单词
打开 `data/words.js`，数组里每个对象：
```js
{ word:"abandon", pos:"v.", meaning:"放弃；抛弃",
  exampleEn:"He had to abandon his plan because of the rain.",
  exampleZh:"因为下雨，他不得不放弃计划。" }
```
往里追加即可，单词卡会自动更新。

## 发音说明
- 单词/例句发音来自**有道真人录音**（`dict.youdao.com/dictvoice`），需联网；若失败自动回退到浏览器语音合成。
- 单词卡页面右上角可一键切换 **美音 / 英音**。
- 例句发音为合成音，单词本身为真人录音。

## 部署
纯静态文件，可直接丢到任意静态托管（GitHub Pages / Vercel / 对象存储 / 学校服务器）即可上网访问，无需数据库。
