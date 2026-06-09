# Visual Image Director

`visual-image-director` 是一个可安装的 Codex skill，用于单张视觉设计和图片修改。它适合制作海报、社媒图、广告图、封面图、Banner、缩略图、产品视觉图，以及对生成结果或已有图片做局部修改。

这个 skill 的核心不是“一句话直接出图”，而是先把想法整理成可确认的设计框架和提示词，再生成缩略图预览，最后才生成最终图片。

## 安装

把这个 repository clone 到 Codex 的 skills 目录即可安装。

### macOS / Linux

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/TedTie/visual-image-director.git ~/.codex/skills/visual-image-director
```

### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills"
git clone https://github.com/TedTie/visual-image-director.git "$env:USERPROFILE\.codex\skills\visual-image-director"
```

如果你设置了自定义 `CODEX_HOME`，请安装到：

```text
<CODEX_HOME>/skills/visual-image-director
```

安装后，确认目录里有这些文件：

```text
visual-image-director/
  SKILL.md
  README.md
  agents/openai.yaml
```

然后重启 Codex，或开启一个新的 Codex 会话，让 skill 被重新发现。

## 更新

进入已安装的 skill 目录后拉取最新版本：

```bash
git pull
```

Windows PowerShell 示例：

```powershell
git -C "$env:USERPROFILE\.codex\skills\visual-image-director" pull
```

## 适合什么时候用

使用它处理这些请求：

- 制作一张海报、广告图、封面、社媒图、Banner、YouTube thumbnail。
- 根据你的想法设计一张完整视觉图。
- 根据参考图提取风格，再制作新图。
- 把文案、主视觉、排版和风格整合成一张图。
- 制作复杂度更高的单张视觉图，并允许用 SVG、HTML、CSS、canvas、浏览器渲染或其他代码方式作为中间制作手段。
- 制作需要精确排版、清晰文字、图表、几何结构、UI 风格布局或混合生成/代码合成的高清 PNG。
- 修改已有图片的局部问题。
- 修改最终生成图，但希望保持原本视觉风格不漂移。

不适合这些情况：

- 你最终只想要 SVG、HTML、CSS 或代码源码，而不是一张高清 PNG。
- 你想要批量制作多页 PPT，这类任务更适合 `visual-style-ppt`。
- 你明确要求直接出图且不需要确认流程。

## 基本调用方式

在 Codex 里直接描述你的需求即可，例如：

```text
用 visual-image-director 帮我做一张小红书封面，主题是 AI 自动化工作流，风格要高级、干净、有科技感。
```

或者：

```text
调用 visual-image-director，把这张图右下角的按钮改成红色，其他部分不要动。
```

安装后，也可以直接说：

```text
我要做一张海报，按 visual-image-director 的流程来。
```

## 标准工作流

### 1. 理解需求

Codex 会先判断任务类型：

- 新设计
- 根据参考图设计
- 修改已有图
- 修改生成后的最终图
- 完整重做

如果缺少关键资料，例如尺寸、用途、必须出现的文字、品牌色、参考图、需要保留的区域，Codex 会先问清楚。

### 2. 生成 `design.md`

`design.md` 是图片的设计框架和排版说明，通常会包含：

- 图片用途
- 尺寸比例
- 制作方式，例如纯图片生成、图片编辑、代码辅助渲染，或混合合成
- 目标受众
- 视觉概念
- 构图和排版
- 文案层级
- 主视觉位置
- 色彩、光影、材质
- 必须保留的内容
- 必须避免的内容
- 自检结果

这一步是为了先确认“设计方向是否正确”。

### 3. 生成 `prompt.md`

`prompt.md` 是给图片模型使用的正式提示词，通常会包含：

- 缩略图 prompt
- 最终图 prompt
- negative prompt
- exact text，明确需要出现在图里的文字
- production method，说明是否需要代码辅助排版、渲染、导出或合成
- 风格锁定规则
- 修改图时不能改变的区域
- 自检结果

这一步是为了确认“生成提示词是否会准确表达设计”。

### 4. 让你确认

在没有得到你确认前，默认不会生成图片。

你可以要求：

- 调整排版
- 改风格
- 减少文字
- 增加某个元素
- 替换主视觉
- 改尺寸比例
- 直接继续生成缩略图

### 5. 生成 `thumbnail-board.png`

确认 `design.md` 和 `prompt.md` 后，Codex 会先生成 `thumbnail-board.png`。

这个缩略图用于确认：

- 大概视觉方向
- 排版结构
- 文案位置
- 主体比例
- 色彩气质
- 整体画面节奏

它不是最终图，所以文字和细节不一定完全准确，重点是看构图和视觉方向。

### 6. 缩略图确认

你可以说：

```text
方向可以，继续生成最终图。
```

或：

```text
整体可以，但是标题太靠下，把主体放大一点。
```

Codex 会根据你的意见更新设计或提示词，然后再继续。

## 代码辅助高清 PNG 工作流

如果任务需要更高设计复杂度，Codex 可以把代码当成中间制作工具，而不是只依赖图片生成模型。

可以使用的中间方式包括：

- SVG：适合精确图形、图标、几何结构、路径和清晰边缘。
- HTML/CSS：适合复杂排版、卡片布局、品牌视觉系统、社媒封面和海报结构。
- canvas 或 Three.js：适合程序化图形、粒子、3D 元素、动态截图和特殊视觉效果。
- 浏览器截图或渲染导出：适合把代码画面转换成 PNG。
- 混合合成：代码负责文字、网格、图表和版式，图片生成负责人物、产品、背景、材质或氛围。

关键规则：

- 最终交付仍然必须是高清 PNG，例如 `final.png`、`final-v2.png` 或其他明确命名的 PNG。
- SVG、HTML、CSS、脚本、浏览器截图等都只能作为中间产物，不能直接替代最终 PNG。
- 如果没有指定尺寸，默认应按目标用途选择合理比例，并尽量用 2x 或 3x 的高分辨率导出。
- 如果文字准确性很重要，优先用代码排版或后期合成文字，不要完全依赖图片模型拼写。
- 交付前必须检查导出的 PNG，而不是只检查源码。
- 局部修改时，应该更新中间源码或合成文件，再重新导出 PNG，并确认未要求修改的区域保持一致。

### 7. 生成最终图

只有在缩略图方向确认后，Codex 才会生成最终图片，例如：

- `final.png`
- `final-v2.png`
- `poster-final.png`

生成后 Codex 会自检：

- 是否符合原始需求
- 风格是否一致
- 构图是否延续缩略图
- 文字是否正确
- 是否多了不该出现的东西
- 是否漏掉必须出现的元素
- 最终图是否完成了审美校准：和 thumbnail 保持一致，但细节、层次、光影、材质、排版和整体观赏性更成熟
- 最终图是否避免过度简化：不能像基础模板、随手拼贴、儿童式简单画面，必须有明确设计感和完成度

最终版可以比 thumbnail 更精致、更好看，但不能偏离 thumbnail 已确认的构图、风格和视觉方向。

## 输出文件说明

默认工作目录类似：

```text
output/visual-image-director/<项目名>/
```

常见文件：

```text
design.md
prompt.md
style-used.md
thumbnail-board.png
final.png
revision-log.md
render/
```

文件作用：

- `design.md`：设计框架、排版逻辑、视觉结构。
- `prompt.md`：正式生成提示词和修改提示词。
- `style-used.md`：当前视觉风格锁，确保后续修改保持一致。
- `thumbnail-board.png`：最终图之前的视觉预览。
- `final.png`：最终生成图。
- `revision-log.md`：每次修改的记录。
- `render/`：可选的代码辅助制作文件，例如 SVG、HTML、CSS、canvas 脚本、截图、遮罩或合成素材。

## 局部修改规则

如果你对最终图提出局部修改，Codex 必须先复述它理解的修改范围。

例如你说：

```text
把标题换成红色，其他不要动。
```

Codex 应该先确认：

```text
我理解是只把标题颜色改成红色，其他排版、背景、人物、光影和整体风格都保持不变。
```

然后只修改标题颜色。

局部修改默认保持不变的内容：

- 整体构图
- 主体位置
- 风格和色彩系统
- 光影方向
- 字体气质
- 背景结构
- 其他未提到的文字和元素

只有当你明确说这些词时，才进入整体重做：

- 重新设计
- 整体换风格
- 全部大改
- 换一个方向
- 从头来
- redesign
- full revamp

## 示例

### 制作海报

```text
用 visual-image-director 做一张 4:5 小红书封面。
主题：AI 帮普通人提高工作效率。
标题：普通人也能用 AI 自动化一天的工作
风格：干净、高级、科技感，不要太花。
先给我 design.md 和 prompt.md 确认。
```

### 复杂代码辅助视觉

```text
用 visual-image-director 做一张高清 PNG 信息图。
主题：AI 自动化工作流的 5 个步骤。
希望用 HTML/CSS 或 SVG 做精确排版和图标，再导出 2x PNG。
先给我 design.md 和 prompt.md 确认。
```

### 根据参考图做风格

```text
用 visual-image-director 参考这张图的视觉风格，帮我做一张新品发布海报。
不要复制原图内容，只提取风格、色彩、排版气质。
```

### 修改最终图

```text
只把左上角标题放大一点，其他地方不要变。
```

### 完整重做

```text
这版方向不对，整体重做，改成更强烈的赛博朋克视觉。
```

## 使用原则

这个 skill 的重点是“先设计，再预览，再生成，再局部修正”。

只要不是你明确要求跳过确认，它都应该遵守：

```text
design.md -> prompt.md -> 确认 -> thumbnail-board.png -> 确认 -> final.png -> 局部修改
```

如果使用代码辅助制作，则代码、SVG、HTML/CSS、截图和合成文件都只是中间步骤，最终仍然要导出并检查高清 PNG。

这样可以最大限度避免直接出图导致风格跑偏、排版混乱、修改时越改越不像原来的问题。

交付最终图前，Codex 还必须做一次审美校准：

- 对照已确认的 `thumbnail-board.png`，确保构图和风格一致。
- 可以增强细节、质感、光影、层次、留白和视觉张力。
- 不能为了“干净”而过度简化成低完成度画面。
- 不能交付看起来像模板化、业余拼贴、儿童都能做出来的图片。
- 最终图必须审美在线，有明确的设计判断和视觉完成度。
