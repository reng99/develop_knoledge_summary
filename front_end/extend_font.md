## 引入的外部字体

在介绍引入外部字体的时候，先来介绍一下`@font-face`

### 浏览器支持情况

Internet Explorer 9+, Firefox, Chrome, Safari, 和 Opera 支持 WOFF (Web Open Font Format) 字体.

Firefox, Chrome, Safari, 和 Opera 支持 .ttf(True Type字体)和.otf(OpenType)字体字体类型）。

Chrome, Safari 和 Opera 也支持 SVG 字体/折叠.

Internet Explorer 同样支持 EOT (Embedded OpenType) 字体.

**注意**Internet Explorer 8 以及更早的版本不支持新的 @font-face 规则。


### 使用的例子

```html

 ...
  <style> 
  @font-face
  {
      font-family: myFirstFont;
      src: url(sansation_bold.woff);
      font-weight:bold;
  }

  div
  {
      font-family:myFirstFont;
  }
  </style>
  ...

```

### css3字体描述

下表列出了所有的字体描述和里面的@font-face规则定义：
