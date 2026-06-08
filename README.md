# Visual Image Director 使用手册

`visual-image-director` 是一个用于单张视觉设计和图片修改的 Codex skill。它适合制作海报、社媒图、广告图、封面图、Banner、缩略图、产品视觉图，以及对生成结果或已有图片做局部修改。

这个 skill 的核心不是“一句话直接出图”，而是先把想法整理成可确认的设计框架和提示词，再生成缩略图预览，最后才生成最终图片。

## 适合什么时候用

使用它处理这些请求：

- 制作一张海报、广告图、封面、社媒图、Banner、YouTube thumbnail。
- 根据你的想法设计一张完整视觉图。
- 根据参考图提取风格，再制作新图。
- 把文案、主视觉、排版和风格整合成一张图。
- 修改已有图片的局部问题。
- 修改最终生成图，但希望保持原本视觉风格不漂移。

不适合这些情况：

- 你只想要纯 SVG、HTML、CSS 或代码生成的图形。
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

如果 Codex 已经安装了这个 skill，也可以直接说：

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
```

文件作用：

- `design.md`：设计框架、排版逻辑、视觉结构。
- `prompt.md`：正式生成提示词和修改提示词。
- `style-used.md`：当前视觉风格锁，确保后续修改保持一致。
- `thumbnail-board.png`：最终图之前的视觉预览。
- `final.png`：最终生成图。
- `revision-log.md`：每次修改的记录。

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

## 安装位置

当前全局安装路径：

```text
C:\Users\Teddy Tie\.codex\skills\visual-image-director
```

仓库路径：

```text
C:\Users\Teddy Tie\Documents\Image Refiner\visual-image-director
```

GitHub repository：

```text
https://github.com/TedTie/visual-image-director
```

## 使用原则

这个 skill 的重点是“先设计，再预览，再生成，再局部修正”。

只要不是你明确要求跳过确认，它都应该遵守：

```text
design.md -> prompt.md -> 确认 -> thumbnail-board.png -> 确认 -> final.png -> 局部修改
```

这样可以最大限度避免直接出图导致风格跑偏、排版混乱、修改时越改越不像原来的问题。
