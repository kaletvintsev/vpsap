<script setup lang="ts">
import type { FAQ } from '@/interfaces'
import { ref } from 'vue'
import IconArrow from './icons/IconArrow.vue'

defineProps<{
  question: FAQ
}>()
const isOpen = ref(false)
</script>

<template>
  <div @click="isOpen = !isOpen" class="faq-item">
    <div class="item-header">
      <div class="item-title">{{ question.question }}</div>
      <IconArrow :is-open="isOpen" class="arrow" :class="{ 'arrow--closed': !isOpen }" />
    </div>
    <div
      class="item-faq-description"
      v-html="question.answer"
      :class="{ 'item-faq-description--open': isOpen }"
    ></div>
  </div>
</template>

<style lang="scss" scoped>
.faq-item {
  display: flex;
  flex-flow: column;
  padding: 16px 20px;
  border-radius: 20px;
  color: #ffffff;
  background-color: rgba(0, 0, 0, 0.32);
  cursor: pointer;
  &:last-child {
    margin-bottom: 0;
  }
}

.item-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 40px;
}
.item-title {
  font-size: 20px;
  font-weight: 700;
  line-height: 28px;
  letter-spacing: -0.04em;
}

.arrow {
  min-width: 18px;
  &--closed {
    opacity: 0.4;
  }
}

.item-faq-description {
  color: rgba(255, 255, 255, 0.64);
  font-size: 14px;
  font-weight: 500;
  line-height: 24px;
  padding-top: 16px;
  opacity: 0;
  max-height: 0;
  margin: -5px;
  transition:
    max-height 0.9s ease,
    opacity 0.9s ease;

  &--open {
    opacity: 1;
    max-height: 99em;
    margin: 0;
  }
}

// .v-enter-active,
// .v-leave-active {
//   max-height: 0;
//   transition:
//     transform 0.6s ease,
//     opacity 0.6s ease,
//     max-height 0.6s ease;
//   transform-origin: top;
// }

// .v-enter-from,
// .v-leave-to {
//   transform: scaleY(0);
//   opacity: 0;
//   max-height: 99em;
// }
</style>
