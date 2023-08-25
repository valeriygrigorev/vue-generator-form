<template>
  <select v-model="inputValue" :name = "inputName" :data-value="dataValue" class="select_element">
    <option v-for="(item, key) in listdata" :key = "key">{{item.value}}</option>
  </select>
</template>

<script>
export default {
  name: 'Select',
  props: ['code', 'value', 'listdata'],
  data: () => ({
    inputValue: '',
  }),
  mounted() {
    this.inputValue = this.listdata.find((i)=> i.key === this.value).value;
  },
  computed: {
    inputName() {
      return this.$props.code;
    },
    dataValue() {
      return this.inputValue && typeof this.inputValue === 'string' ? this.listdata.find((i)=> i.value === this.inputValue).key: '';
    }
  },
}
</script>

<style>
.select_element {
  width: 100%;
  margin-bottom: 5px;
}
</style>