<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 47 47"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M0 23.5C0 10.5213 10.5213 0 23.5 0V0C36.4787 0 47 10.5213 47 23.5V23.5C47 36.4787 36.4787 47 23.5 47V47C10.5213 47 0 36.4787 0 23.5V23.5Z"
      fill="#BFDAE6"
    />
    <path d="M34 7.99915L9 23.7491L34 39.4991V7.99915Z" fill="#57616D" />
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
