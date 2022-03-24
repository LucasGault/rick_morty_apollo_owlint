<template>
  <div class="flex justify-center gap-1 md:gap-2 my-8">
    <Button blue v-if="info.prev != 1 && page != 1" @click="$emit('selectPage', 1)">
      {{ 1 }}
    </Button>
    <div
      v-if="page > 3"
      class="font-bold text-gray-dark py-2 px-2 md:px-4 rounded-lg hover:bg-opacity-80"
    >
      ...
    </div>
    <Button blue v-if="info.prev" @click="$emit('selectPage', info.prev)">
      {{ info.prev }}
    </Button>
    <div class="font-bold text-gray-dark py-2 px-4 rounded-lg hover:bg-opacity-80">
      {{ page }}
    </div>
    <Button
      blue
      v-if="info.next && info.next != info.pages"
      @click="$emit('selectPage', info.next)"
    >
      {{ info.next }}
    </Button>
    <div
      v-if="page < info.pages - 2"
      class="font-bold text-gray-dark py-2 px-2 md:px-4 rounded-lg hover:bg-opacity-80"
    >
      ...
    </div>
    <Button blue v-if="info.pages != page" @click="$emit('selectPage', info.pages)">
      {{ info.pages }}
    </Button>
  </div>
</template>

<script>
import Button from "./ui/Button.vue";
export default {
  name: "Pagination",
  emits: ["selectPage"],
  props: {
    info: {
      type: Object,
    },
    page: {
      type: Number,
    },
  },
  components: { Button },
};
</script>

<style lang="scss" scoped></style>
