# supermall（适配移动端）

```A Vue project```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### 注意问题
解决Better-Scroll可滚动区域问题

- Better-Scroll在解决有多少区域可以滚动时，是根据scrollerHeight属性决定

- scrollerHeight属性是根据放在Better-Scroll的content中的子组件的高度

- 在计算scrollerHeight属性时，是没有将图片计算在内，所以计算出来的高度是错误的

- 后来图片加载之后有新的高度，但scrollerHeight属性没有进行更新

- 解决

- 监听每一张图片是否加载完成，只要有一张图片加载完成，执行一次refresh（）

- 原始js监听图片加载img.onload()=function(){}

- vue中监听：@load="方法"

- 调用scroll的refresh（）

- 如何将GoodListItem.vue中的事件传入到Home.vue中

- 因为涉及非父子组件的通信，所以选择事件总线

- bus ->总线

- Vue.prototype.$bus = new Vue()

- this.$bus.$emit()

- this.$bus.$on()

- 对于refresh频繁的问题，进行防抖操作

  - 如果直接执行refresh（），那么refresh（）函数会被执行30次
  - 可以将refresh函数传入debound\

- tabControl的吸顶效果

- 获取到tabCcontrol的offsetTop

  - 必须知道滚动到多少时，开始有吸顶效果
  - 在mounted中获取tabControl的offsetTop是不正确的

  - 获取正确的值
  - 监听HomeSwiper中img加载完成
  - 加载完成后，发出事件，在home.vue中获取正确的值 

- 监听滚动，动态改变tabControl的样式

- 动态改变tabControl的样式会出现两个问题

  - 下面的商品内容突然上移
  - tabControl虽然设置fixed，但会随着Better-Scroll一起上移

  解决：

  - 多复制一份tabControl组件对象，利用它实现停留效果
  - 当用户移到到一定位置时，tabControl显示出来
  - 当滚动位置没有达到位置，tabControl消失

- 联动效果
  - 点击标题，滚动到对应的主题
  - 获取所有主题的offsetTop
  - 正确获取offsetTop
  - created肯定不行，获取不到元素
  - mounted也不行，数据还没有获取到
  - 获取到数据的回调中也不行，Dom还没有渲染完
  - $nextTick也不可以，图片的高度没有被计算在内
  - 图片加载完成后，获取的高度才是正确
