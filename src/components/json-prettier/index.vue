<template>
  <div class="json-prettier-container">
    <div class="json-item">
      <json-item ref="jsonItem" :value="jsondata" :isend="true"></json-item>
    </div>
  </div>
</template>

<script>
import JsonItem from './item'

export default {
  name: 'JsonPrettier',

  props: ['jsondata'],
  
  methods: {
    // 扩展全部
    expandAll() {
      this.expandChildAll(this.$refs.jsonItem)
    },
    expandChildAll(child) {
      const componentName = child.$options.componentName

      if (componentName !== 'JsonItem' && !child.isObjArr) {
        return
      }

      const childs = child.$children
      for (let i = 0; i < childs.length; i++) {
        this.expandChildAll(childs[i])
      }
      child.handleExpand()
    },
    // 折叠全部
    foldAll() {
      this.foldChildAll(this.$refs.jsonItem)
    },
    foldChildAll(child) {
      const componentName = child.$options.componentName

      if (componentName !== 'JsonItem' && !child.isObjArr) {
        return
      }

      const childs = child.$children
      for (let i = 0; i < childs.length; i++) {
        this.foldChildAll(childs[i])
      }
      child.handleFold()
    }
  },

  components: {
    JsonItem
  }
}
</script>

<style lang="scss" scoped>

  .json-prettier-container {
    box-sizing: border-box;
    font-family: Menlo,Monaco,Consolas,Helvetica Neue,Helvetica,Courier New,微软雅黑,monospace,Arial,sans-serif,黑体;
    text-rendering: optimizeLegibility;
    font-weight: 700;
    line-height: 20px;
    color: #555;
    font-size: 13px;
  }

  .json-prettier-container>.json-item {
    padding-left: 12px;
  }

</style>
