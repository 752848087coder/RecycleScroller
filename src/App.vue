<template>
  <div id="app">
    <h1>复用滚动组件demo</h1>
    <RecycleScroller 
      :list="list" 
      itemKey="key"
      :itemHeight = "60"
      :viewHeight = "600"
    >
      <!-- 组件插槽会返回当前内容item，可自定义滚动内容 -->
      <template v-slot="props">
        <div class="scroll-item">
          {{ props.item.value }}
        </div>
      </template>
    </RecycleScroller>
  </div>
</template>

<script>

import RecycleScroller from './components/RecycleScroller.vue'
export default {
  name: 'app',
  components: {
    RecycleScroller
  },
  data() {
    return {
      list: []
    };
  },
  created() { // 生成模拟数据
    this.list = Array.from(Array(1000), (v,k) => {
      return {
        value: k,
        key: k
      }
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.scroll-item{
  height: 50px;
  line-height: 50px;
  width: 100%;
  background: #e8f3fe;
  margin: 10px;
  color: #7dbcfc;
}
</style>
