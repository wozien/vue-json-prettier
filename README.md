一个可将json数据转为树形展示界面的vue组件

## 安装

```bash
npm i vue-json-prettier
```

## 使用

```html
<template>
  <div id="app">
    <json-prettier :jsondata="{a:1, b: 'hello'}"></json-prettier>
  </div>
</template>

<script>
import JsonPrettier from 'vue-json-prettier'

export default {
  name: 'app',
  components: {
    JsonPrettier
  }
}
</script>
```