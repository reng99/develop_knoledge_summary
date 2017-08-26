## 清除 select 的默认的样式

```css

  appearance:none;
  -moz-appearance:none;
  -webkit-appearance:none;

```

这个清除的样式对ie无效，即使加上`-ms-appearance:none;`

要对IE做兼容的话，需要加上`select::-ms-expand { display: none; }  `来清除ie默认的下拉的箭头样式。
