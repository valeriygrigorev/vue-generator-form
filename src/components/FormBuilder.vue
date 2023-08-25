<template>
  <div v-for="(field, key) in formConfig" :key="key" class="field_name">
    {{field.code}}
    <div style="display: flex">
      <component
          :is = field.type
          :children = field.children
          @change = "updateFormValues($event)"
      >
      </component>
    </div>
  </div>
</template>

<script>
import Container from "@/formElements/Container";

export default {
  name: 'FormBuilder',
  props: ['parsedInput', 'signal'],
  data: () => ({
     formValues: {},
  }),
  mounted() {
    for (let obj of this.parsedInput) {
      this.formValues[obj.code] = obj.value ?? null;
    }
  },
  computed: {
    formConfig() {
      const arr = [];
      let arrayItem = null;

      for (let obj of this.parsedInput) {
        if (obj.type === 'container') {
          obj.children = [];
        }

        if (obj.parent) {
          arrayItem = this.findObjectByName(arr, obj.parent);
          arrayItem.children.push(obj);
        } else {
          obj.children = [];
          arr.push(obj);
        }
      }
      return arr;
    },
    name() {
      return this.signal;
    }
  },
  methods: {
    updateFormValues(event) {
      this.formValues[event.target.attributes.name.value] = event.target.dataset.value;
    },
    //метод для рекурсивного поиска вложенных контейнеров
    findObjectByName(arr, code) {
      for (let obj of arr) {
        if (obj.code === code) {
          return obj;
        }
        if (obj.children?.length) {
          const foundObject = this.findObjectByName(obj.children, code);
          if (foundObject) {
            return foundObject;
          }
        }
      }
      return null;
    },
  },
  watch: {
    //ждем появления признака закрытия модального окна,
    //при наличии которого мы отправляет информацию из формы
    name(n) {
      if (n) {
        console.log(JSON.parse(JSON.stringify(this.formValues)));
      }
    },
  },
  components: {
    Container,
  }
}
</script>

<style>
.field_name {
  text-align: left
}
</style>