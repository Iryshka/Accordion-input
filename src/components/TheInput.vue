<template>
  <div class="input">
    <input class="input-field" v-model="inputText" type="text" :placeholder="placeholder" />
    <button class="button" @click="onButtonClick">Submit</button>
  </div>
</template>

<script setup>
import { ref, reactive, defineEmits } from 'vue'

const inputText = ref('')
const message = ref('')
const messageArray = reactive([])
const placeholder = ref('Enter your message...')

const emit = defineEmits(['displayMessage'])

function onButtonClick() {
  if (inputText.value.length < 3) {
    console.log('Your must write your message')
    return
  }
  message.value = inputText.value
  messageArray.push(message.value)
  console.log(messageArray)
  inputText.value = ''
  emit('displayMessage', message.value)
}
</script>

<style scoped lang="scss">
.input {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 50px;
}
.input-field {
  width: 230px;
  padding: 11px;
  outline: none;
  border: none;
  margin-right: 10px;
  border-radius: 2px;
}

.button {
  padding: 11px;
  background-color: #2a2020;
  color: white;
  font-weight: bold;
  border: none;
  border-radius: 2px;
  cursor: pointer;
  transition:
    background-color 0.3s ease,
    color 0.3s ease;

  &:hover {
    background-color: white;
    color: #2a2020;
  }
}
</style>
