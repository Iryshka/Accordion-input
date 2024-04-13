<template>
  <div class="main">
    <TheAccordion class="accordion" :user-messages="messages" />
    <TheInput class="input" @display-message="addMessage" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import TheAccordion from '@/components/TheAccordion.vue'
import TheInput from '@/components/TheInput.vue'

const messages = ref([])

// why does it work in app.vue and doesn't work in theAccordion?
function Message(text) {
  this.text = text
  this.id = Date.now()
  this.date = new Date().toLocaleString()
}

function addMessage(messageText) {
  const message = new Message(messageText)
  messages.value.push(message)
}
</script>

<style scoped lang="scss">
.main {
  display: block;
  width: 100%;
  height: 100vh;
  background-color: #e10066;
}

.input {
  position: fixed;
  top: 13px; // Adjust this value as needed
  left: 35%;
  transform: translateX(-50%);
}
</style>
