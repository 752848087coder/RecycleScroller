<template>
  <div class="recycle-scroller" ref="recycleScroller" @scroll="update" :style="{'minHeight': `${viewHeight}px`}">
    <div
      class="recycle-scroller-holder" 
      :style="{'minHeight': `${totalHeight}px`}"
    >
      <div 
        class="recycle-scroller-wrapper" 
        :style="{ transform: `translateY(${translate}px)` }"
      >
        <div 
          class="recycle-scroller-item" 
          :style="{'height': `${itemHeight}px`}" 
          v-for="(item, index) in showList" :key="item[itemKey] || index"
        >
          <slot
            :item="item"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecycleScroller',
  props: {
    list: { // 需要渲染的数据
      type: Array,
      default: () => {
        return [];
      },
      require: true
    },
    itemKey: { // 数组的唯一标识字段，可以很大程度提升性能
      type: String,
      default: 'id',
      require: true
    },
    itemHeight: { // 每条数据的高度
      type: Number,
      default: 40     
    },
    viewHeight: { // 可视区域高度
      type: Number,
      default: 600  
    }
  },
  data() {
    return {
      showList: [], // 当前渲染的数据
      translate: 0 // 当前渲染数据区域的Y轴偏移数，需要通过偏移数使滚动过程中渲染数据一直出现在可视区域内
    };
  },
  computed: {
    totalHeight() {
      return this.itemHeight * this.list.length;
    }
  },
  mounted() {
    this.update();
  },
  methods: {
    update() { // 更新当前显示的数组数据
      let scrollTop = this.$refs['recycleScroller'].scrollTop;
      let viewNum = Math.ceil(this.viewHeight / this.itemHeight); // 可视区域可显示的最多条数
      let showStart = Math.floor(scrollTop / this.itemHeight); // 可视区域显示的第一数据下标
      // 利用VUE中Diff算法的复用机制，我们可以截取可视区域的上一屏第一条至下一屏最后一条
      // 这样滚动时可以快速复用，避免滚动后再渲染DOM出现短暂空白。
      let start = showStart - viewNum > 0 ? showStart - viewNum: 0; // 上一屏第一条下标
      let end = showStart + (2 * viewNum) < this.list.length ? showStart + (2 * viewNum) : this.list.length; // 下一屏最后一条下标
      this.showList = this.list.slice(start, end);
      this.translate = start *  this.itemHeight;
    }
  }
}
</script>
<style scoped>
.recycle-scroller{
  position: relative;
  overflow: auto;
}

.recycle-scroller-holder, .recycle-scroller-wrapper{
  position: absolute;
  top: 0;
  width: 100%;
}

.recycle-scroller-item{
  display: flex;
  align-items: center;
}

</style>
