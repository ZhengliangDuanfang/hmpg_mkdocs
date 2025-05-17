目前用下来体验还是很好的。

## 资源

- [中文教程](https://typst-doc-cn.github.io/docs/tutorial/)
- [小蓝书](https://typst-doc-cn.github.io/tutorial/)
- [Touying](https://touying-typ.github.io/zh/docs/intro)
- [Typst Universe](https://typst.app/universe/)
- [GitHub](https://github.com/typst/typst) 
    - 安装：仅需解压release提供的压缩包，并将文件夹添加到环境变量中即可
  
## 文档

### 页面调整
```typst
#set page(
  paper: "a4",
  margin: (x: 2cm, y: 2.5cm),
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
### 行间距调整
```typst
#set par(leading: .7em)
```

### 文字加粗重载
```typst
#show strong: set text(stroke: 0.3pt)
```

### 调整页码
```typst
#set page(numbering: "1 / 1")
#counter(page).update(1)
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

## Touying
### 使用现有模板
```typst
#import "@preview/touying:0.6.1": *
#import themes.university: *

#show: university-theme.with(
  aspect-ratio: "4-3",
  config-info(
    title: [],
    subtitle: [],
    author: [],
    date: datetime.today(),
  ),
  config-colors(
    primary: rgb("#005fbf"),
    secondary: rgb("#003f88"), // 求是蓝
    tertiary: rgb("#005fbf"),
  )
)
```

### 分栏
```typst
#slide(composer: (38%, 62%))[左栏][右栏]
```