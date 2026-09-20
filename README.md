<div align="center">

<img src="public/icons/icon128.png" width="76" alt="DeepSeek 伴读图标">

# DeepSeek 伴读

**选中英文，沿着原文读懂它。**

在网页或 PDF 里划选词句，DeepSeek 结合前后文给出直接的中文理解；留在原处追问，或听 Kokoro 读出选中的英文。

Chrome 扩展 · 英文网页与 PDF · DeepSeek 上下文解释 · Kokoro 本地发音

</div>

![网页中选中 calibrated probabilities，伴读卡片在原文旁给出中文解释](docs/screenshots/web-selection.png)

## 它怎样陪你读

**贴着原文解释。** 选中词、短语或句子，回答沿用原文的对象、术语、主语和论述顺序，保留必要的限定与确定性。它用自然中文说明选中内容在当前位置的含义，篇幅随内容变化。继续在卡片中追问，DeepSeek 会接着当前原文和对话回答。

**让选区更完整。** 网页和 PDF 都会补齐漏选的单词边界。PDF 阅读器按栏和段落整理文字，并合并排版造成的跨行断词；从 `detec- / tion` 划到的词会按 `detection` 进入解释。涉及图表或公式的 PDF 查询，可把相关页图像一同提供给支持视觉输入的模型。

**听见选中的英文。** 词旁的扬声器使用 Kokoro Q8 的美式 Heart 音色，在本机生成声音。可以选择点击后生成，或选中后预先生成、点击时播放；音量可单独调节。首次安装会自动下载约 92 MB 的量化模型并缓存，此后发音可离线使用。发音支持最长 240 个字符的英文词句。

![网页中选中 Verifiable problems，并在同一张卡片中查看解释与追问入口](docs/screenshots/web-follow-up.png)

对话历史保存在浏览器本地，最多保留最近 200 条；可以搜索并返回原文。界面随系统切换深浅主题，PDF 阅读区使用中性灰背景。

## 安装

需要 Chrome 116 或更新版本，以及自己的 [DeepSeek API Key](https://platform.deepseek.com/api_keys)。

1. 从[最新版本](https://github.com/zzkws/SideNote/releases/latest)下载 `deepseek-reading-companion.zip`，解压到固定目录。
2. 打开 `chrome://extensions`，开启开发者模式，点击「加载已解压的扩展程序」，选择解压后的目录。
3. 在自动打开的设置页填入 API Key，测试连接并保存。语音包会自动下载，进度可在设置页查看。
4. 在英文网页中划词；阅读论文时，从扩展菜单打开 PDF 阅读器，把 PDF 拖入页面。

升级时用新版本文件替换原安装目录，在 `chrome://extensions` 点击重新加载，并刷新已打开的阅读页面。

也可以从源码构建：

```bash
git clone https://github.com/zzkws/SideNote.git
cd SideNote
npm ci
npm run build
```

然后在 `chrome://extensions` 加载项目生成的 `dist/`。`npm run zip` 可生成安装压缩包。

## 数据与适用范围

- 解释与追问需要联网。选中内容、所需前后文，以及 PDF 查询涉及的页图会发送到设置中的 API 地址，默认是 DeepSeek；API 用量由你的账户承担。
- API Key 与对话历史保存在本机 `chrome.storage.local`。Kokoro 模型从 [GitHub 模型发布页](https://github.com/zzkws/SideNote/releases/tag/kokoro-v1.0-q8)下载，Hugging Face 为备用源；模型文件经过 SHA-256 校验。发音文本在本机处理。
- PDF 文字层采用版面规则恢复。扫描件没有可选择的文字层时暂不能直接划词；复杂公式、表格和特殊排版仍应结合原页核对。网页 iframe 内的选区暂不支持。

更详细的上下文策略、页图选择与验证方式见[阅读链路](docs/reading-pipeline.md)，回答约束见[提示词源码](src/background/prompt.ts)。

## 项目与许可

这是围绕 DeepSeek 模型能力与视觉风格制作的独立开源作品，非 DeepSeek 官方产品。谨以此作品，表达本人对 DeepSeek 的喜爱之情。

项目源码采用 [MIT 许可证](LICENSE)。本地发音组件和模型保留各自的许可，详见[第三方许可说明](THIRD_PARTY_NOTICES.md)。仓库沿用原 SideNote 地址；早期固定模板的[回答样例与截图](docs/archive/README.md)、[海报实验](poster/README.md)仅作历史留存。

<details>
<summary>English</summary>

DeepSeek 伴读 is an independent Chrome reading companion for English webpages and PDFs. Select a word or passage for a Chinese explanation grounded in the surrounding text, ask follow-up questions in place, and play local English pronunciation with Kokoro Q8. Bring your own DeepSeek API key. Explanations require a network connection; pronunciation works offline after the first model download.

</details>
