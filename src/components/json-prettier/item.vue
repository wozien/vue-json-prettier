<template>
  <div class="keyval">
    <!-- 值不是对象或者数组 -->
    <template v-if="!isObjArr">
      <span class="key" v-show="field">"{{field}}":</span>
      <span :class="['val', valCls]">{{_formatVal(value)}}<span v-if="!isend">,</span></span>
    </template>

    <!-- 值为对象或者数组 -->
    <template v-if="isObjArr">
      <span class="key" v-show="field">"{{field}}":</span>
      <json-button :showType="showType" @expand="handleExpand" @fold="handleFold"></json-button>
    </template>

    <!-- 值为对象 -->
    <template v-if="_getType(value) === 'Object'">
      <span class="expand-view" v-show="showType === 2">
        <span>{</span>
        <div class="json-item">
          <json-item v-for="(val, key, index) in value" :key="key"
                     :field="key" :value="val" :isend="index===_getObjLength(value)-1"></json-item>
        </div>
        <div class="brace-end">}<span v-if="!isend">,</span></div>
      </span>

      <span class="fold-view" v-show="showType === 1">{{_getType(value)}}{<label class="len" @click.stop="handleExpand">{{_getObjLength(value)}}</label>}<span v-if="!isend">,</span>
      </span>
    </template>

    <!-- 值为数组 -->
    <template v-if="_getType(value) === 'Array'">
      <span class="expand-view" v-show="showType === 2">
        <span>[</span>
        <div class="json-item" v-for="(val, index) in value" :key="index">
          <json-item :value="val" :isend="index === value.length - 1"></json-item>
        </div>
        <div class="brace-end">]<span v-if="!isend">,</span></div>
      </span>
      <span class="fold-view" v-show="showType === 1">{{_getType(value)}}[<label class="len" @click.stop="handleExpand">{{value.length}}</label>]<span v-if="!isend">,</span>
      </span>
    </template>
  </div>
</template>

<script>
import JsonButton from './button'

export default {
  name: 'JsonItem',

  componentName: 'JsonItem',

  props: {
    field: String,
    value: {},
    isend: Boolean
  },

  computed: {
    valCls() {
      return 'val-' + this._getType(this.value)
    },
    isObjArr() {
      return this._isObjectArr(this.value)
    }
  },

  data() {
    return {
      showType: 2
    }
  },

  methods: {
    handleExpand() {
      this.showType = 2
    },
    handleFold() {
      this.showType = 1
    },
    _getType(val) {
      return toString.call(val).split(']')[0].split(' ')[1]
    },
    _isObjectArr(val) {
      return ['Object', 'Array'].indexOf(this._getType(val)) > -1
    },
    _getObjLength(val) {
      return Object.keys(val).length
    },
    _formatVal(val) {
      switch(this._getType(val)) {
        case 'String':
          return `"${val}"`
          break
        case 'Null':
          return 'null'
          break
        default:
          return val 
      }
    }
  },

  components: {
    JsonButton
  }
}
</script>

<style lang="scss" scoped>
  .json-item {
    padding-left: 30px;
  }

  .key {
    color: rgb(19, 158, 170);
  }

  .val-String {
    color: rgb(207, 159, 25);
  }

  .val-Boolean {
    color: rgb(124, 197, 0);
  }  

  .val-Number {
    color: rgb(236, 64, 64);
  }

  .len {
    cursor: pointer;
    display: inline-block;
    padding: 0 2px;
    color: #25aae2;
  }
</style>
