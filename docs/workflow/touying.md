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