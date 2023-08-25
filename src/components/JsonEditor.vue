<template>
  <div>
    <textarea :value="input" @input="update" class="editor"></textarea>
    <button class="button" @click="showModal = true" :disabled = "!input">Сгенерировать форму</button>
    <ModalWindow v-if="showModal" @close="onClosing()">
      <template v-slot = "{ signal }">
        <FormBuilder :parsedInput="parsedInput" :signal="signal">
        </FormBuilder>
      </template>
    </ModalWindow>
  </div>
</template>

<script>
import ModalWindow from "@/components/ModalWindow";
import FormBuilder from "@/components/FormBuilder";
import { nextTick } from 'vue';

export default {
  name: 'JsonEditor',
  data: () => ({
    input: '',
    showModal: false,
  }),
  computed: {
    parsedInput() {
      return JSON.parse(this.input);
    },
  },
  methods: {
    update(e) {
      this.input = e.target.value;
    },
    onClosing: function() {
      // без nextTick форма будет размонтирована при удалении модального окна из Dom
      // и FormBuilder не сможет обработать событие закрытия модального окна, поэтому перенесем
      // закрытие окна на следующий микротаск
      nextTick(() => {
        this.showModal = false;
      })
    },
  },
  components: {
    ModalWindow,
    FormBuilder,
  }
}
</script>

<style>
.editor {
  min-width: 500px;
  min-height: 600px;
  outline: none;
  margin-bottom: 16px;
}

.button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: block;
  margin: auto;
  font-size: 16px;
}
</style>