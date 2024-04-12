<template>
  <div class="main">
    <div @click="toggleAccordionVisible" class="accordion">
      <p class="accordion__text">Your messages</p>
      <img
        class="accordion__img"
        :class="
          isAccordionVisible ? 'accordion__img-rotate-forward' : 'accordion__img-rotate-backward'
        "
        src="@/assets/images/plus-svgrepo-com.svg"
        alt=""
      />
    </div>
    <transition name="fade">
      <ul v-show="isAccordionVisible" class="accordion__list">
        <li class="accordion__item" v-for="{ text, id, createdDate } in messages" :key="id">
          {{ text }} <span class="accordion__date">{{ createdDate }} </span>
        </li>
      </ul>
    </transition>

    <ComponentInput class="accordion__input" @display-message="addMessage" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { format } from 'date-fns'
import ComponentInput from '@/components/ComponentInput.vue'

const messages = ref([])
const isAccordionVisible = ref(false)

const date = ref(new Date())

const formattedDate = format(date.value, 'd.MM.yyyy HH:mm')

const inputDate = ref(formattedDate)

function Message(text) {
  this.text = text
  this.id = Date.now()
  this.createdDate = new Date()
}

function toggleAccordionVisible() {
  isAccordionVisible.value = !isAccordionVisible.value
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

.accordion {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: white;
  font-size: 16px;
  text-transform: uppercase;
  font-weight: bold;
  cursor: pointer;
  padding: 10px;
  border-radius: 2px;
  border: 3px solid white;
  width: 350px;

  &__img {
    width: 25px;
    height: 25px;
  }

  &__input {
    position: absolute;
    top: 0;
    left: 370px;
  }

  &__img-rotate-forward {
    transform: rotate(45deg);
    transition: transform 0.3s ease;
  }

  &__img-rotate-backward {
    transform: rotate(0deg);
    transition: transform 0.3s ease;
  }

  &__item {
    display: flex;
    justify-content: space-between;
    color: white;
    width: 350px;
    height: 35px;
    padding: 5px;
    margin: 3px 0;
    border: 3px solid white;
    border-radius: 2px;
  }
}

@keyframes rotate {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(45deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

.accordion__img--rotate {
  animation: rotate 0.5s infinite;
}

.box {
  color: black;
  width: 200px;
  height: 30px;
  margin-bottom: 5px;
  border: 3px solid greenyellow;
}
// TRANSITION

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
