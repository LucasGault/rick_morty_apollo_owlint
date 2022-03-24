<template>
  <div class="caroussel_container flex justify-between items-center gap-6">
    <div class="w-16">
      <button v-show="startSlice != 0" class="" @click="seeMore(-3)">
        <ArrowLeft :width="60" :height="60" />
      </button>
    </div>
    <div
      class="card_container flex justify-between"
      v-for="data in carousselArray"
      :key="data.id"
    >
      <RouterLink
        :to="{ name: 'Character', params: { id: data.id } }"
        class="w-32 h-48 p-2 rounded-xl transition-colors  hover:bg-primary-yellow/80"
      >
        <img class="rounded-md" :src="data.image" alt="" />
        <p class="text-lg font-medium text-center">{{ data.name }}</p>
      </RouterLink>
    </div>
    <div class="w-16">
      <button v-show="endSlice <= dataArray.length" class="" @click="seeMore(3)">
        <ArrowRight :width="60" :height="60" />
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";
import ArrowLeft from "./icons/ArrowLeft.vue";
import ArrowRight from "./icons/ArrowRight.vue";

const props = defineProps({
  dataArray: Array,
});

const startSlice = ref(0);
const endSlice = ref(3);
const carousselArray = ref(props.dataArray.slice(startSlice.value, endSlice.value));
const seeMore = (nextSlice) => {
  startSlice.value += nextSlice;
  endSlice.value += nextSlice;
  console.log(endSlice.value);
  console.log(props.dataArray.length);
  var newArr
  if (endSlice.value >= props.dataArray.length) {
    console.log("hh");
    newArr = props.dataArray.slice(-3);
  } else {
    newArr = props.dataArray.slice(startSlice.value, endSlice.value);
  }
  carousselArray.value = [...newArr];
};
</script>

<style lang="postcss" scoped></style>
