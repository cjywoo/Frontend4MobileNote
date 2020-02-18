# 页面自适应布局

## viewport
首先viewport的配置必须保证页面比例为1，且无法缩放
```
<meta name="viewport"
    content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale=1.0,user-scalable=no">
```

## 页面的根font-size
在app.vue下，用js监听并设置根html的font-size
```
document.addEventListener('DOMContentLoaded', () => {
  const html = document.querySelector('html')
  let fontSize = window.innerWidth / 10
  fontSize = fontSize > 50 ? 50 : fontSize
  fontSize = fontSize < 10 ? 10 : fontSize
  html.style.fontSize = fontSize + 'px'
})
```

## 样式中利用function实现px2rem
1. 设置function
```
\\ global.scss

$ratio: 375 / 10;

@function px2rem($px) {
  @return $px / $ratio + rem;
}
```

2. 样式中引用，并使用px2rem函数
```
<style lang="scss" scoped>
@import "./assets/styles/global.scss";
.text {
  font-family: "Days One";
  font-size: px2rem(20);
}
</style>
```