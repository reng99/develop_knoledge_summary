## 移动端开发

本文档汇集的是自己在移动端开发的重点汇总。

### viewport

手机浏览器是把页面放在一个虚拟的窗口（viewport），通常这个虚拟的窗口（viewport）比屏幕宽屏幕宽，这样就不用把网页的每个页面挤到
很小的窗口中（这样会破坏没有针对手机浏览器优化的网页布局）。用户可以通过平移和缩放来看网页的不同部分。

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

**相关参考**

- [meta viewport 你真的了解吗？](http://yunkus.com/meta-viewport-usage/)
