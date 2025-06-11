目前用下来体验还是很好的。使用Typst制作幻灯片详见[Touying](./touying.md)

## 资源

- [中文教程](https://typst-doc-cn.github.io/docs/tutorial/)
- [小蓝书](https://typst-doc-cn.github.io/tutorial/)
- [Touying](https://touying-typ.github.io/zh/docs/intro)
- [Typst Universe](https://typst.app/universe/)
- [GitHub](https://github.com/typst/typst) 
    - 安装：仅需解压release提供的压缩包，并将文件夹添加到环境变量中即可
- VSCode插件：Tinymist
  
## 文档

### 页面调整
```typst
#set page(
  paper: "a4",
  margin: (x: 2cm, y: 2.5cm), // 页边距
  // margin: (left: 2cm, right: 2cm, top: 2.5cm, bottom: 2.5cm), 
  // margin: (inside: 2cm, outside: 1cm)
  // columns: 2 // 分栏
)
```

### 字体调整
```typst
#set text(
  size: 12pt,
  font: "SimSun",
  stroke: 0.005em,
)
```

### 文字加粗重载
```typst
#show strong: set text(stroke: 0.3pt)
```

### 调整页码
```typst
#set page(numbering: "1 / 1")
#counter(page).update(1) // 页码归1
```

### 使用表格进行图片展示
```typst
#align(center)[#table(
  columns: (33%, 33%, 33%),
  stroke: none, 
  align: (center, center+horizon),
  [#image("img1.png")],[#image("img2.png")],[#image("img3.png")],
)]
```

### 调整页眉
```typst
#let remain_page_header = table(columns: (100%), stroke: none, align: (center),
  [页眉文字],
  table.hline(stroke: 0.5pt)
)
#set page(header: context{
  remain_page_header
})
```

### 段落开头空两格
```typst
#set par(first-line-indent: 2em)
```
手动方法：
```typst
#h(2em)内容
```

### 调整标题的样式
```typst
#show heading.where(level: 3): set block(below: 10pt, above: 10pt) // 上下间距
#show heading.where(level: 2): set text(size: 16pt, stroke: 0.1em) // 字体
```