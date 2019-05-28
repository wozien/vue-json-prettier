<template>
  <div id="app">
    <json-prettier :jsondata="{a:1, b: 'hello'}"></json-prettier>
  </div>
</template>

<script>
import JsonPrettier from '../src/index'

export default {
  name: 'app',
  components: {
    JsonPrettier
  }
}
</script>
