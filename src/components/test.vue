<script setup>
import { ref } from 'vue'
import { format } from 'date-fns'
import ComponentInput from '@/components/ComponentInput.vue'

const messages = ref([])
const isAccordionVisible = ref(false)
const date = ref(new Date())
const formattedDate = format(date.value, 'd.MM.yyyy HH:mm')
const inputDate = ref(formattedDate)

function toggleAccordionVisible() {
  isAccordionVisible.value = !isAccordionVisible.value
}

function showMessage(message) {
  messages.value.push(message)
}
</script>

<template>
  <div class="main">
    <div @click="toggleAccordionVisible" class="accordion">
      <p class="accordion__text">Your messages</p>
      <img
        class="accordion__img"
        :class="{ 'accordion__img--rotate': isAccordionVisible }"
        src="@/assets/images/plus-svgrepo-com.svg"
        alt=""
      />
    </div>
    <transition name="fade">
      <ul v-show="isAccordionVisible" class="accordion__list">
        <li class="accordion__item" v-for="(message, index) in messages" :key="index">
          {{ message }} {{ inputDate }}
        </li>
      </ul>
    </transition>

    <ComponentInput class="input" @display-message="showMessage" />
  </div>
</template>

<style scoped lang="scss">
.main {
  width: 100%;
  height: 100vh;
  background-color: #e10066;
}

.accordion {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: white;
  cursor: pointer;
  padding: 10px;
  border: 3px solid white;
  width: 350px;

  &__img {
    width: 25px;
    height: 25px;
    transition: transform 0.3s ease;
  }

  &__img--rotate {
    transform: rotate(45deg);
  }

  &__item {
    color: black;
    width: 350px;
    height: 30px;
    margin-bottom: 5px;
    border: 3px solid greenyellow;
  }
}

.box {
  color: black;
  width: 200px;
  height: 30px;
  margin-bottom: 5px;
  border: 3px solid greenyellow;
}
.input {
  position: absolute;
  top: 0;
  left: 370px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
