<template>
  <div class="main">
    <TheAccordion :user-messages="messages" />
    <TheInput class="input" @display-message="addMessage" />
  </div>
</template>

<script setup>
import { ref } from 'vue'

import TheAccordion from '@/components/TheAccordion.vue'
import TheInput from '@/components/TheInput.vue'

const messages = ref([])

function Message(text) {
  this.text = text
  this.id = Date.now()
  this.createdDate = new Date()
}

function addMessage(messageText) {
  const message = new Message(messageText)
  messages.value.push(message)
}
</script>

<style scoped lang="scss">
.main {
  gap: 20px;
  width: 100%;
  height: 100vh;
  background-color: #e10066;
}

.input {
  position: absolute;
  left: 370px;
  top: 0;
}
</style>
