<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 47 47"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M47 23.5C47 36.4787 36.4787 47 23.5 47V47C10.5213 47 0 36.4787 0 23.5V23.5C0 10.5213 10.5213 0 23.5 0V0C36.4787 0 47 10.5213 47 23.5V23.5Z"
      fill="#BFDAE5"
    />
    <path d="M13 38.5L37.9999 22.75L13 6.99999V38.5Z" fill="#57616D" />
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
