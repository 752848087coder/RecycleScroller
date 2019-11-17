# demo

在线demo:  http://129.226.125.49/RecycleScrollerDemo

博客链接:  https://blog.csdn.net/qq_36259513/article/details/103108221

### 实现原理：

![Image text](http://129.226.125.49/images/recycleScroller.png)

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
