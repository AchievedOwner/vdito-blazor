# `VditorBlazor` 是基于 Vditor 封装的 Markdown 编辑器

## 什么是 Vditor
[Vditor](https://b3log.org/vditor/) 是一款浏览器端的 Markdown 编辑器，支持所见即所得、即时渲染（类似 Typora）和分屏预览模式。它使用 TypeScript 实现，支持原生 JavaScript 以及 Vue、React、Angular 和 Svelte 等框架。
## ✨  特性

* 支持三种编辑模式：所见即所得（wysiwyg）、即时渲染（ir）、分屏预览（sv）
* 支持大纲、数学公式、脑图、图表、流程图、甘特图、时序图、五线谱、[多媒体](https://ld246.com/article/1589813914768)、语音阅读、标题锚点、代码高亮及复制、graphviz 渲染、[plantuml](https://plantuml.com)UML图
* 内置安全过滤、导出、图片懒加载、任务列表、多平台预览、多主题切换、复制到微信公众号/知乎功能
* 实现 CommonMark 和 GFM 规范，可对 Markdown 进行格式化和语法树查看，并支持[10+项](https://ld246.com/article/1549638745630#options-preview-markdown)配置
* 工具栏包含 36+ 项操作，除支持扩展外还可对每一项中的[快捷键](https://ld246.com/article/1582778815353)、提示、提示位置、图标、点击事件、类名、子工具栏进行自定义
* 表情/at/话题等自动补全扩展
* 可使用拖拽、剪切板粘贴上传，显示实时上传进度，支持 CORS 跨域上传
* 实时保存内容，防止意外丢失
* 录音支持，用户可直接发布语音
* 粘贴 HTML 自动转换为 Markdown，如粘贴中包含外链图片可通过指定接口上传到服务器
* 支持主窗口大小拖拽、字符计数
* 多主题支持，内置黑白绿三套主题
* 多语言支持，内置中、英、韩文本地化
* 支持主流浏览器，对移动端友好

## 🍱 语法支持

* 所有 CommonMark 语法：分隔线、ATX 标题、Setext 标题、缩进代码块、围栏代码块、HTML 块、链接引用定义、段落、块引用、列表、反斜杠转义、HTML 实体、行级代码、强调、加粗、链接、图片、行级 HTML、硬换行、软换行和纯文本。
* 所有 GFM 语法：表格、任务列表项、删除线、自动链接、XSS 过滤
* 常用 Markdown 扩展语法：脚注、ToC、自定义标题 ID
* 图表语法
  * 流程图、时序图、甘特图，通过 Mermaid 支持
  * Graphviz
  * 折线图、饼图、脑图等，通过 ECharts 支持
* 五线谱：通过 abc.js 支持
* 数学公式：数学公式块、行级数学公式，通过 MathJax 和 KaTeX 支持
* YAML Front Matter
* 中文语境优化
  * 中西文之间插入空格
  * 术语拼写修正
  * 中文后跟英文逗号句号等标点替换为中文对应标点

## :computer: 支持环境
* .NET 8
## 快速开始
* 安装包
 
`> Install-Package VditorBlazor`

* 添加服务

```cs
builder.Services.AddVditor(options => {
 //... 全局配置
})
```

* 使用控件

在 `_Imports.razor` 添加命名空间 `VditorBlazor`

在 `App.razor` 引用必要脚本和样式

```html
<!-- ⚠️生产环境请指定版本号，如 https://cdn.jsdelivr.net/npm/vditor@x.x.x/dist... -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/vditor/dist/index.css" />
<script src="https://cdn.jsdelivr.net/npm/vditor/dist/index.min.js"></script>
```

使用组件 `Vditor`
```html
<!--全局配置-->
<Vditor @bind-Value="Content" />

<!--局部配置-->
<Vditor @bind-Value="Content" Configure="@(options => options.Theme = Dark)" />

@code{
	[Inject] HttpClient Client { get; set; }

	string? Content { get; set; } = "Hello World!!!";

	protected override async Task OnInitializedAsync()
	{
		Content = await Client.GetStringAsync("demo.md");
	}
}
```

#### 遇到任何问题请提【[ISSUE](https://github.com/AchievedOwner/vditor-blazor/issues)】

