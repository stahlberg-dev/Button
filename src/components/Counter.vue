<script setup lang="ts">
import Button from './Button.vue'

import { ref } from 'vue'

const count = ref(0);
</script>

<template>
  <div class="image">
    <img src="/images/vue.svg" class="image__icon" alt="Vue" />
  </div>
  <p class="counter">
    Count is&nbsp;&nbsp;<span class="counter__number">{{ count }}</span>
  </p>
  <div class="buttons">
    <Button 
      @click="count++"
      href="#"
    >
      Increment
    </Button>
    <Button 
      @click="count--"
      theme="secondary"
    >
      Decrement
    </Button>
  </div>
</template>
<style scoped lang="scss">
.image {
  width: 100px;
  margin: 0 auto 30px;

  &__icon {
    display: block;
    width: 100%;
  }
}

.counter {
  margin-bottom: 30px;
  text-align: center;
  font-size: 24px;

  &__number {
    font-weight: 500;
    font-size: 26px;
    color: rgb(19, 165, 121);
  }
}

.buttons {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  gap: 30px;
}
</style>