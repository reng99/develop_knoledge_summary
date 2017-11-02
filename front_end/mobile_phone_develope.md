## 移动端开发

本文档汇集的是自己在移动端开发的重点汇总。

### viewport

```html

<meta name = "viewport"
      content = "width=device-width,
                 height=device-height,
                 initial-scale=1.0,
                 maximum-scale=1.0,
                 user-scalable=no"
/>

```

在苹果的规范中，`meta viewport`有6个属性，分别如下，

1.width - viewport的宽度[pixel_value|device-width]

2.height - viewport的高度[pixel_value|device-height]

3.initial-scale - 初始的缩放的比例

4.maximum-scale - 允许用户缩放的最大的比例

5.minimum-scale - 允许用户的最小的缩放比例

6.user-scalable - 用户是否可以手动缩放[yes|no]
