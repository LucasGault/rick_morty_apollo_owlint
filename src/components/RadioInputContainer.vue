<template>
  <div class="filter flex flex-col justify-between gap-4">
    <div class="w-full">
      <h2 class="text-2xl font-semibold mb-2">Gender :</h2>
      <div class="flex items-center justify-between max-w-xl gap-2 flex-wrap md:flex-nowrap">
        <InputRadio
          id_input="gender_choice_1"
          name="gender"
          value="Male"
          @update:value="(newValue) => (variables.filter.gender = newValue.value)"
        >
          <MaleIcon />
        </InputRadio>
        <InputRadio
          id_input="gender_choice_2"
          name="gender"
          value="Female"
          @update:value="(newValue) => (variables.filter.gender = newValue.value)"
        >
          <FemaleIcon />
        </InputRadio>
        <InputRadio
          id_input="gender_choice_3"
          name="gender"
          value="Unknown"
          @update:value="(newValue) => (variables.filter.gender = newValue.value)"
        >
          <UnknownIcon />
        </InputRadio>
        <InputRadio
          id_input="gender_choice_4"
          name="gender"
          value=""
          @update:value="(newValue) => (variables.filter.gender = newValue.value)"
        >
          <ResetIcon />
        </InputRadio>
      </div>
    </div>
    <div class="w-full">
      <h2 class="text-2xl font-semibold mb-2">Status :</h2>
      <div class="flex items-center justify-between max-w-xl flex-wrap md:flex-nowrap">
        <InputRadio
          id_input="status_choice_1"
          name="status"
          value="Alive"
          @update:value="(newValue) => (variables.filter.status = newValue.value)"
        >
          <AliveIcon />
        </InputRadio>
        <InputRadio
          id_input="status_choice_2"
          name="status"
          value="Dead"
          @update:value="(newValue) => (variables.filter.status = newValue.value)"
        >
          <DeadIcon />
        </InputRadio>
        <InputRadio
          id_input="status_choice_3"
          name="status"
          value="Unknown"
          @update:value="(newValue) => (variables.filter.status = newValue.value)"
        >
          <QuestionIcon/>
        </InputRadio>
        <InputRadio
          id_input="status_choice_4"
          name="status"
          value=""
          @update:value="(newValue) => (variables.filter.status = newValue.value)"
        >
          <ResetIcon />
        </InputRadio>
      </div>
    </div>
  </div>
</template>

<script>
import InputRadio from "./ui/InputRadio.vue";
import MaleIcon from "./icons/MaleIcon.vue";
import FemaleIcon from "./icons/FemaleIcon.vue";
import UnknownIcon from "./icons/UnknownIcon.vue";
import AliveIcon from "./icons/AliveIcon.vue";
import DeadIcon from "./icons/DeadIcon.vue";
import ResetIcon from "./icons/ResetIcon.vue";
import QuestionIcon from "./icons/QuestionIcon.vue";
export default {
  props: {
    variables: Object,
  },
  name: "RadioInputContainer",
  components: {
    InputRadio,
    MaleIcon,
    FemaleIcon,
    UnknownIcon,
    AliveIcon,
    DeadIcon,
    ResetIcon,
    QuestionIcon
},
};
</script>

<style lang="postcss">
.filter input[type="radio"] {
  position: absolute;
  opacity: 0;
  width: 0;
  height: 0;
}
.radio_container {
  @apply flex flex-col items-center px-6 py-4;
  /* box-sizing: border-box; */
  border: 2px solid #e1e2e7;
  border-radius: 10px;
  transition: box-shadow 0.4s;
}

.filter .radio_container:hover {
  box-shadow: 0px 3px 5px 0px #e8e8e8;
}

.filter input[type="radio"]:checked + .radio_container {
  @apply bg-primary-yellow;
  transition: ease-in 0.3s;
}
</style>
