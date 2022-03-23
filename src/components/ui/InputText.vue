<template>
<div class="flex flex-col w-full">
  <label class="font-semibold text-lg" :for="id_input"> {{name}}:</label>
  <input
    class="border-[1px] border-primary-gray py-2 px-4 rounded-lg"
    type="text"
    :placeholder="name"
    :name="name"
    :id="id_input"
    :value="value"
    @input="$emit('update:value', $event.target)"
  />
</div>
</template>

<script>
export default {
  props:{
    value: {
      type: String
    },
    name: String,
    id_input : String
  }
}
</script>

<style lang='postcss' scoped>

</style>