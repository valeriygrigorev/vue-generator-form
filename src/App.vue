<template>
  <div>
    <JsonEditor>
    </JsonEditor>
  </div>
</template>

<script>
import JsonEditor from '@/components/JsonEditor';
export default {
  name: 'App',
  components: {
    JsonEditor,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  border-width: 1px;
  border-radius: 0;
}
</style>
