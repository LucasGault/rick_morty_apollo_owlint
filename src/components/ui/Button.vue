<template>
  <component
    :is="is"
    class="font-bold py-2 px-4 rounded-lg hover:bg-opacity-80 cursor-pointer w-14"
    :class="[
      { ' bg-primary-blue text-white': blue },
      { 'bg-primary-green text-white': green },
      { 'bg-primary-yellow text-gray-dark': yellow },
    ]"
  >
    <slot></slot>
  </component>
</template>

<script>
export default {
  name: "CTAButton",
  props: {
    is: {
      type: String,
      default: "button",
    },
    blue: {
      type: Boolean,
    },
    green: {
      type: Boolean,
    },
    yellow: {
      type: Boolean,
    },
  },
};
</script>
