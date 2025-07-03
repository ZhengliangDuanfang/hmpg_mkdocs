[Touying官方介绍](https://touying-typ.github.io/zh/docs/intro)

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

### 不显示一级标题
适用于幻灯片较短的情况。
```typst
#show: universiy-theme.with(
  // ... 前略
  config-common(new-section-slide-fn: none), // 新一级标题不单独成立一页
  header-right: "", // 一级标题不再显示在页面右上角
  // ... 后略
)
```

一级标题页也可以选择重载，参见[文档](https://touying-typ.github.io/zh/docs/code-styles#%E7%BA%A6%E5%AE%9A%E4%BC%98%E4%BA%8E%E9%85%8D%E7%BD%AE)

## （TODO）自定义模板
### 设置进度条宽度
### 调整页面