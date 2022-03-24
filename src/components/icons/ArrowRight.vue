<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 47 47"
    fill="none"
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M47 23.5C47 36.4787 36.4787 47 23.5 47V47C10.5213 47 3.89218e-05 36.4787 3.89218e-05 23.5V23.5C3.89218e-05 10.5213 10.5213 8.40425e-06 23.5 8.40425e-06V8.40425e-06C36.4787 8.40425e-06 47 10.5213 47 23.5V23.5Z"
      fill="white"
    />
    <path d="M12.5 40L40 23L12.5 6L12.5 40Z" fill="#57616D" />
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
