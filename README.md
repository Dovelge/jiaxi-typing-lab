# 嘉西英语跟打台 · English Typing Lab

🌐 **在线直接用：https://dovelge.github.io/jiaxi-typing-lab/**

一个把**小学英语课本做成打字游戏**的单文件网页工具。

打开就能用，不用下载、不用注册、不用联网。孩子看到一句英文（或一张图、一段声音），照着把它敲出来；打对了键盘会响、星星会亮，打错了它会记住是哪个字母总出错。

> 眼睛看、耳朵听、手指打、嘴巴跟 —— 四件事同时发生，比抄十遍记得牢。

---

## 里面有什么

| | |
|---|---|
| 课程 | **66 课**：人教版 PEP 小学英语 **三年级上 → 六年级下，8 册 × 8 课**（共 64 课）+ 演讲 1 课 + 电影台词 1 课 |
| 内容 | **1509 条**：教材单词 1488 + 演讲 12 句 + 台词 9 句 |
| 练法 | **四种**：看图跟打 / 音标跟打 / 听音跟打 / 中文跟打（同一句，四种提示强度） |
| 键盘 | 扁平 / 3D 立体两种风格；键帽厚度、键盘仰角、浮起层次三个滑杆实时可调；跟随框四种样式（描边 / 浮起 / 灯条 / 标签）；按键音色四种 |
| 反馈 | 打对得星（正确率 ≥95% 三星、≥80% 二星）；连击、正确率、速度实时统计 |
| 诊断 | **易错字母本**：自动累计哪个字母打错最多，告诉你下一步该补哪里 |
| 节奏 | 每天打对 6 句就收工，进度条走满 |
| 数据 | 全部存在本机浏览器（localStorage），不上传、不联网也能用 |

## 快速开始

```bash
git clone https://github.com/Dovelge/jiaxi-typing-lab.git
cd jiaxi-typing-lab
```

**双击 `index.html`** 即可，用 Chrome / Edge 打开（按 F11 全屏体验最好）。

没有构建步骤，没有依赖，没有 npm install —— 整个应用就是一个 HTML 文件 + 一个 `assets/` 目录。

### 放到线上

任何静态托管都能跑（GitHub Pages / Vercel / Netlify / 自己的服务器）。

本仓库已开启 **GitHub Pages**：向 `main` 分支推送后，会在一两分钟内自动发布到
https://dovelge.github.io/jiaxi-typing-lab/

想在自己服务器上跑：

```bash
python3 -m http.server 8000
```

## 怎么加自己的内容

所有课程数据都在 `index.html` 里的 `const LESSONS = [ ... ]` 那一段，是纯 JS 对象，改完刷新即可。

**教材课（词/句）**

```js
{
  id:"g3a-words",              // 唯一 id
  no:1,
  title:"全部单词",
  sub:"PEP三上 · 全部单词（共65个）",
  items:[
    {en:"hello", zh:"你好", pos:"感叹词", ipa:"/həˈləʊ/"},
    {en:"name",  zh:"名字", pos:"名词",  ipa:"/neɪm/"}
  ]
}
```

**演讲 / 台词课（带音频、图片、整段视频）**

```js
{
  id:"sp-xxx", cat:"speech", no:1,        // cat: "speech" 或 "dialogue"
  title:"Why Not You",
  sub:"演讲 · Jim Rohn《Why Not You》",
  video:"assets/video/speech.mp4",        // 整段视频（可省略，省略则退回纯音频）
  items:[
    {
      en:"Why not you?", zh:"为什么不能是你？",
      pos:"演讲", cap:"Jim Rohn 演讲",
      audio:"assets/speech/aud-01.mp3",   // 单句音频
      img:"assets/speech/img-01.jpg",     // 配图
      start:0.0, end:2.44                 // 在整段音频里的时间轴（秒）
    }
  ]
}
```

`start` / `end` 用于"播放整段时高亮当前句"，没有整段音频的课可以不写。

## 目录结构

```
.
├── index.html            # 整个应用（HTML + CSS + JS + 课程数据）
└── assets/
    ├── speech/           # 演讲课：img-01..12.jpg、aud-01..12.mp3、full.mp3
    ├── dialogue/         # 台词课：img-01..09.jpg、aud-01..09.mp3、full.mp3
    ├── video/            # 整段视频（已裁掉平台水印）
    └── letters/          # 字母音效 a.mp3 … z.mp3
```

想换成自己的素材：把文件放进对应目录，改 `LESSONS` 里的路径即可。

## 说明与声明

- **数据只在本机**：成绩、星星、易错字母都存在浏览器的 localStorage 里，换设备不同步、也不会上传任何地方。清缓存会清空记录。
- **字体**：页面从 CDN 加载 Baloo 2 + Noto Sans SC，断网时回退系统字体，功能不受影响。
- **第三方素材**：`assets/` 里的演讲音频（Jim Rohn《Why Not You》）与电影台词片段（《当幸福来敲门》）版权归原作者／权利人所有，此处仅作个人学习与教学演示使用，未用于商业用途。**如需商用请自行替换为你拥有授权的素材**。权利人如有异议，请开 issue，我会立即移除对应文件。
- **教材词汇**：单词表依据人教版 PEP 小学英语教材整理，仅含词汇本身（英文 / 中文 / 词性 / 音标），不含课文原文。

## License

代码以 **MIT** 协议开源，可自由使用、修改、商用、再分发（保留版权声明）。
第三方音视频素材不在此协议覆盖范围内，见上方声明。

---

做这个小工具的人叫**嘉西**，平时分享 AI + 教育学习类的小工具。
觉得有用就 Star 一下；想加什么课本、演讲、台词，欢迎开 issue 或者评论区告诉我。
