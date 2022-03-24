<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 58 58"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <circle cx="29" cy="29" r="25" stroke="black" stroke-width="8" />
    <line
      x1="8.21169"
      y1="47.132"
      x2="44.2117"
      y2="12.132"
      stroke="black"
      stroke-width="8"
    />
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 50,
    },
    height: {
      type: Number,
      default: 50,
    },
  },
};
</script>
