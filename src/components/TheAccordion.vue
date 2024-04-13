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
        <li class="accordion__item" v-for="message in userMessages" :key="message.id">
          {{ message.text }} <span class="accordion__date">{{ message.date }} </span>
        </li>
      </ul>
    </transition>
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue'

const isAccordionVisible = ref(false)

defineProps(['userMessages'])

// function Message(text) {
//   this.text = text
//   this.id = Date.now()
//   this.date = new Date().toLocaleString()
// }

function toggleAccordionVisible() {
  isAccordionVisible.value = !isAccordionVisible.value
}
</script>

<style scoped lang="scss">
.main {
  display: flex;
  flex-direction: column;
  border: none;
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
    margin: 2px 0;
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
