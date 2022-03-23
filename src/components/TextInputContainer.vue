<template>
  <div class="flex flex-col justify-between gap-4">
    <InputText
      name="Name"
      id_input="name_search"
      :value="variables.filter.name"
      @update:value="(newValue) => (variables.filter.name = newValue.value)"
    />
    <InputText name="Species"
      id_input="species_search"
      :value="variables.filter.species"
      @update:value="(newValue) => (variables.filter.species = newValue.value)"/>
  </div>
</template>

<script>
import InputText from "./ui/InputText.vue";
export default {
  props: {
    variables: {
      type: Object,
    },
  },
  components: { InputText },
};
</script>

<style lang="postcss" scoped></style>
