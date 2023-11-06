<script setup lang="ts">
import {computed} from 'vue';

interface Props {
  tag?: 'button' | 'a' | 'span' | 'div';
  theme?: 'primary' | 'secondary';
  href?: string;
  type?: 'button' | 'reset' | 'submit';
}

const props = withDefaults(defineProps<Props>(), {
  tag: 'button',
  theme: 'primary',
  href: '',
  type: 'button',
});

const classList = computed(() => {
  const baseClass = 'button';

  return {
    [`${baseClass}_${props.theme}`]: props.theme,
  };
});

const component = computed(() => {
  if (props.tag !== 'button') {
    return props.tag;
  }

  if (props.href) {
    return 'a';
  }

  return 'button';
});

const attrs = computed(() => {
  switch (component.value) {
    case 'a':
      return {
        href: props.href,
        rel: 'nofollow noopener',
      };

    case 'button': 
      return {
        type: props.type,
      }

    default:
      return {};
  }
});
</script>

<template>
  <component
    :is="component" 
    :class="['button', classList]"
    v-bind="attrs"
  >
    <span class="button__text">
      <slot />
    </span>
  </component>
</template>

<style scoped lang="scss">
.button {
  $block: &;

  display: flex;
  justify-content: center;
  align-items: center;
	width: 200px;
  height: 60px;
  border-radius: 10px;
  cursor: pointer;
  
  &_primary {
    background-color: rgb(19, 165, 121);
    transition: background-color 0.3s ease;

    @media screen and (any-hover: hover) {

      &:hover {
        background-color: rgb(5, 146, 104);
      }
    }
  }

  &_secondary {
    background-color: rgb(24, 17, 92);
    transition: background-color 0.3s ease;

    @media screen and (any-hover: hover) {

      &:hover {
        background-color: rgb(49, 41, 116);
      }
    }
  }

  &__text {
    font-family: Montserrat, sans-serif;
    font-weight: 700;
    font-size: 16px;
    line-height: 1;
    color: rgb(2, 23, 36);

    #{$block}_secondary & {
      color: #ffffff;
    }
  }
}
</style>
