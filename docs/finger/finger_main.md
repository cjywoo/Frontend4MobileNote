# 手势操作

## 简易版本
通过判断起始的x位置的变动和滑动时间，来判断左滑还是右滑
```
// 绑定touchstart事件
this.rendition.on('touchstart', event => {
  this.touchStartX = event.changedTouches[0].clientX
  this.touchStartTime = event.timeStamp
})

// 绑定touchend事件
this.rendition.on('touchend', event => {
  const offsetX = event.changedTouches[0].clientX - this.touchStartX
  const time = event.timeStamp - this.touchStartTime
  if(time<500 && offsetX > 40){
    //从左边右滑动
  }else if( time<500 && offsetX <-40){
    // 从右往左滑动
  }else{
    //既不是左滑又不是右滑动
  }
  console.log(offsetX, time)
})
```