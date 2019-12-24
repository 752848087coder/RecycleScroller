# demo

在线demo:  http://gavincat.cn/RecycleScrollerDemo

博客链接:  https://blog.csdn.net/qq_36259513/article/details/103108221

### 组件参数：

参数 | 说明 | 类型 | 必填 | 默认值 |  
-|-|-|-|-|
list | 需要渲染的数据 | Array | [x] |-|
itemKey | 数组的唯一标识字段，可以很大程度提升渲染性能 | String | [x] |-|
itemHeight | 每条数据的高度 | Number | [ ]  | 40 |
viewHeight | 可视区域高度 | Number | [ ]  | 600 
### 实现原理：

![Image text](http://gavincat.cn:8080/recycleScroller.png)

最外层recycle-scroller节点需要设置一个固定高度，它代表可视区域。

中间层recycle-scroller-holder节点高度为渲染所有数据的总高度，它目的在于撑出recycle-scroller的滚动条。

最内层recycle-scroller-wrapper包裹我们实际渲染的数据，它会预加载上一屏与下一屏的数据，在滚动时进行复用。通过改变recycle-scroller-wrapper的纵向偏移量（translateY的值）使得实际渲染的数据一直出现在可视范围内，不变更新渲染的数据，模拟滚动的效果。


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

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
