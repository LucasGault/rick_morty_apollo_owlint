<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 47 47"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M0 23.5009C0 10.5222 10.5213 0.000854492 23.5 0.000854492V0.000854492C36.4787 0.000854492 47 10.5222 47 23.5009V23.5009C47 36.4795 36.4787 47.0009 23.5 47.0009V47.0009C10.5213 47.0009 0 36.4795 0 23.5009V23.5009Z"
      fill="white"
    />
    <path d="M34.5 7L7 24L34.5 41V7Z" fill="#57616D" />
  </svg>
</template>

<script>
export default {
  props: {
    width: {
      type: Number,
      default: 47,
    },
    height: {
      type: Number,
      default: 47,
    },
  },
};
</script>
