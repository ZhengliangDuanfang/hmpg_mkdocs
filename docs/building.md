# 搭建记录

## 主要参考资料

[基础教程](https://squidfunk.github.io/mkdocs-material/publishing-your-site/)

[MkDocs官方教程](https://www.mkdocs.org/user-guide/)

进阶：[咸鱼暄前辈的搭建记录](https://xuan-insr.github.io/%E6%9D%82%E9%A1%B9/%E5%8D%9A%E5%AE%A2%E6%90%AD%E5%BB%BA%E8%AE%B0%E5%BD%95/)

## 杂项

- Windows PowerShell 无法识别 `mkdocs` 相关命令

  解决办法：在每个`mkdocs`相关命令前面加一个`python -m`。参见 [链接](https://www.mkdocs.org/user-guide/installation/)

- GitHub Actions 好用，就不用每次都手动操作了。参考 [链接](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions-material-for-mkdocs)

此时`mkdocs.yml`中仅有如下内容：
```
site_name: ZLDF的个人主页

theme: 
  name: material

nav:
  - 主页: 'index.md'
  - 杂项: 
    - 搭建记录: 'building.md'
```

- 亮暗切换 参考[链接](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/#color-palette-toggle)

`mkdocs.yml`中theme部分改为如下内容（添加palette部分）：

```
theme: 
  name: material

  palette: 

    # Palette toggle for light mode
    - scheme: default
      toggle:
        icon: material/weather-night 
        name: Switch to dark mode

    # Palette toggle for dark mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
```

- 自定义网页顶端与背景颜色 参考 [链接](https://squidfunk.github.io/mkdocs-material/setup/changing-the-colors/#custom-color-schemes)

`mkdocs.yml`中添加了如下两行：
```
extra_css:
  - stylesheets/extra.css
```
`stylesheets/extra.css`中添加：
```
[data-md-color-scheme="default"] {
    --md-primary-fg-color:        #AE7000;
    --md-default-bg-color: #fbe3b8;
  }

[data-md-color-scheme="slate"] {
    --md-primary-fg-color:        #845A23;
  }
```
其中，`default`和`slate`两个选项分别与亮暗切换部分的`scheme`值相对应。

- 更换字体：主要根据[这个链接](https://squidfunk.github.io/mkdocs-material/setup/changing-the-fonts/#regular-font)。
  
一个问题是字体依赖谷歌源，有时会被墙。网上给出的[换源方法](http://zongming.net/read-1426/)并不成功，原因是在对应html文件中找不到字体部分。

- 导航栏：主要根据[这个链接](https://squidfunk.github.io/mkdocs-material/setup/setting-up-navigation/#navigation-expansion-with-expansion)