<template>
  <input type="date" :name="inputName" v-model="inputValue" :data-value="dataValue" placeholder="дд.мм.гггг" class="datepicker_element">
</template>

<script>
const dateRegex1 = /^[0-9]{4}[-][0-9]{2}[-][0-9]{2}$/;
const dateRegex2 = /^[0-9]{2}[.][0-9]{2}[.][0-9]{4}$/;

export default {
  props: ['code', 'value'],
  data: () => ({
    inputValue: '',
  }),
  mounted() {
    this.inputValue = this.$props.value;
  },
  computed: {
    inputName() {
      return this.$props.code;
    },
    dataValue() {
      return this.formatDate(this.inputValue);
    }
  },
  methods: {
    formatDate(dateString, reformat = false) {
      if (dateRegex1.test(dateString) && dateRegex2.test(dateString)) return '';

      const date = new Date(dateString),
            day = date.getDate(),
            month = date.getMonth() + 1,
            year = date.getFullYear();

      return `${year}-${month < 10 ? "0" + month : month}-${day < 10 ? "0" + day : day}`
    },
  },
}
</script>

<style>
.datepicker_element {
  width: 100%;
  margin-bottom: 5px;
}
</style>