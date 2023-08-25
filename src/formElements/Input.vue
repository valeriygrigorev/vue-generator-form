<template>
  <input type="text" :name="inputName" v-model="inputValue" :data-value="dataValue" class="textfield_element">
</template>

<script>
export default {
  props: ['code', 'value'],
  data: () => ({
    inputValue: ''
  }),
  mounted() {
      this.inputValue = this.$props.value;
  },
  computed: {
    inputName() {
      return this.$props.code;
    },
    dataValue() {
      return this.inputValue;
    }
  },
}
</script>

<style>
.textfield_element {
  width: 100%;
  margin-bottom: 5px;
}
</style>