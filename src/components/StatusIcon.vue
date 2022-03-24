<template>
  <div class="">
    <div v-if="status == 'Alive'">
      <AliveIcon :width="25" :height="25" />
    </div>
    <div v-else-if="status == 'Dead'">
      <DeadIcon :width="25" :height="25" />
    </div>
    <div v-else>
      <QuestionIcon :width="25" :height="25" />
    </div>
  </div>
</template>

<script>
import AliveIcon from "../components/icons/AliveIcon.vue";
import DeadIcon from "../components/icons/DeadIcon.vue";
import QuestionIcon from "../components/icons/QuestionIcon.vue";
export default {
  name: "StatusIcon",
  components: {
    AliveIcon,
    DeadIcon,
    QuestionIcon,
  },
  props: {
    status: String,
  },
};
</script>

<style lang="scss" scoped></style>
