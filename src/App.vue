<script>
import { RouterLink, RouterView } from "vue-router";
// import HelloWorld from '@/components/HelloWorld.vue'
// import ButtonVue from "./components/ui/Button.vue";
export default {
  components: {
    RouterLink,
    RouterView,
  },
};
</script>

<template>
  <header>
    <nav class="px-6 py-4">
      <RouterLink :to="{ name: 'Home' }">
        <h1 class="text-4xl font-medium">Rick & Morty</h1>
      </RouterLink>
    </nav>
  </header>
  <RouterView />
</template>

<style lang="postcss">
@import "@/assets/base.css";
/* .filter input[type="radio"] {
  position: absolute;
  opacity: 0;
} */
</style>
