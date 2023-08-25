<template>
  <div class="container_wrap">
    <div v-for="(field, key) in children" :key="key">
      <div class="element_name">{{field.code}}</div>
      <div class="element_wrap">
        <Container v-if="field.type === 'container'"
                   :children = field.children
        >
        </Container>
        <component v-show="['input', 'datepicker', 'list'].includes(field.type)"
                   :is = field.type
                   :code = field.code
                   :value = field.value
                   :listdata = field.listdata
        >
        </component>
      </div>
    </div>
  </div>
</template>

<script>
import Container from "@/formElements/Container";
import Input from './Input';
import List from "./List";
import Datepicker from "./Datepicker";

export default {
  name: 'Container',
  props: ['children'],
  components: {
    Container,
    Input,
    List,
    Datepicker,
  }
}
</script>

<style>
.container_wrap {
  padding: 8px;
  margin-bottom: 8px;
  border: 1px solid #D3D3D3;
  width: 100%
}

.element_wrap {
  display: flex;
}

.element_name {
  text-align: left;
  padding-left: 4px;
  padding-right: 4px;
}
</style>