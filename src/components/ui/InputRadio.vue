<template>
  <div class="cursor-pointer">
    <input
      type="radio"
      :id="id_input"
      :name="name"
      :value="value"
      @change="$emit('update:value', $event.target)"
    />
    <label class="radio_container cursor-pointer" :for="id_input">
      <slot></slot>
      <div class="radio_details">
        <span>{{ value || "Reset" }}</span>
      </div>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
    },
    name: String,
    id_input: String,
  },
};
</script>

