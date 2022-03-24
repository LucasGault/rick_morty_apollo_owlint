<template>
  <div>
    <div v-if="gender == 'Male'">
      <MaleIcon :width="25" :height="25" />
    </div>
    <div v-else-if="gender == 'Female'">
      <FemaleIcon :width="25" :height="25" />
    </div>
    <div v-else>
      <UnknownIcon :width="25" :height="25" />
    </div>
  </div>
</template>

<script>
import MaleIcon from "../components/icons/MaleIcon.vue";
import FemaleIcon from "../components/icons/FemaleIcon.vue";
import UnknownIcon from "../components/icons/UnknownIcon.vue";

export default {
  name: "GenderIcon",
  props: {
    gender: String,
  },
  components: {
    MaleIcon,
    FemaleIcon,
    UnknownIcon,
  },
};
</script>

<style lang="scss" scoped></style>
