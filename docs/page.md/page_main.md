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
1. 设置function,只要将ue图的宽度进行修改即可
```
\\ global.scss

$ue-width: 375; /* ue图的宽度 */
$ratio: $ue-width / 10;  /* 缩放比例 */

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

3. 页面中使用js方法设置html的font-size
```
const remSetFun = () => {
  const html = document.querySelector('html')
  let fontSize = window.innerWidth / 10
  fontSize = fontSize > 50 ? 50 : fontSize
  fontSize = fontSize < 12 ? 12 : fontSize
  html.style.fontSize = fontSize + 'px'
}

document.addEventListener('DOMContentLoaded', () => {
  remSetFun()
})

window.addEventListener('orientationchange' in window ? 'orientationchange' : 'resize', remSetFun)

```

4. 设置浏览器禁用js兼容性方案，同时修复body字体
```
html {
  font-size: 37.5px; /* 375/10 */
}
body {
  font-size: 16px; /* 修正字体大小 */
  /* 防止页面过宽 */
  margin: auto;
  padding: 0;
  width: 10rem;
  /* 防止页面过宽 */
  outline: 1px dashed green;
}

/* js被禁止的回退方案 */
@media screen and (min-width: 320px) {
  html {font-size: 32px}
  body {font-size: 16px;}
}
@media screen and (min-width: 481px) and (max-width:640px) {
  html {font-size: 48px}
  body {font-size: 18px;}
}
@media screen and (min-width: 641px) {
  html {font-size: 64px}
  body {font-size: 20px;}
}

noscript {
  display: block;
  border: 1px solid #d6e9c6;
  padding: 3px 5px;
  background: #dff0d8;
  color: #3c763d;
}
/* js被禁止的回退方案 */

.p1, .p2 {
  border: 1px solid red;
  margin: 10px 0;
}

.p1 {
  width: 5rem;
  height: 5rem;

  font-size: 1.2em; /* 字体使用em */
}

.s1 {
  font-size: 1.2em; /* 字体使用em */
}

.p2 {
  width: 4rem;
  height: 4rem;
}
.s2 {
  font-size: 1.2em /* 字体使用em */
}
```