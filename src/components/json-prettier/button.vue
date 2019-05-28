<template>
  <span class="json-btn" @click.stop="handleClick">
    <i class="iconfont icon-jia" v-show="showType === 1"></i>
    <i class="iconfont icon-jian" v-show="showType === 2"></i>
  </span>
</template>

<script>
export default {
  name: 'JsonButton',

  props: {
    // 1 => +  2 => -
    showType: {
      type: Number,
      default: 2
    }
  },

  methods: {
    handleClick() {
      const eventName = this.showType === 1 ? 'expand' : 'fold'
      this.$emit(eventName)
    }
  }
}
</script>

<style lang="scss" scoped>
@import "../../assets/styles/iconfont.css";

.json-btn>i {
  display: inline-block;
  vertical-align: middle;
  margin-top: -1px;
  cursor: pointer;
  color: #777;
}
</style>

