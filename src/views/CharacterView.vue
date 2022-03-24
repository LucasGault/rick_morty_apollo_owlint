<template>
  <div class="mt-8 mx-4">
    <div
      v-if="loading"
      class="bg-primary-blue flex text-white w-max items-center rounded-md py-2 px-4 text-xl mx-auto my-8"
    >
      <LoadingIcon />
      Loading...
    </div>
    <div v-else-if="error">Error: {{ error.message }}</div>
    <div v-else-if="character" class="space-y-4">
      <div class="flex gap-4">
        <img class="w-48 h-48 rounded-full" :src="character.image" alt="" />
        <div class="flex flex-col gap-2">
          <p class="text-4xl font-medium">{{ character.name }}</p>
          <p v-if="character.type" class="text-2xl font-normal">
            Type: {{ character.type }}
          </p>
          <p class="text-xl font-normal">Species : {{ character.species }}</p>
          <div class="flex gap-4">
            <div>
              <div v-if="character.gender == 'Male'">
                <MaleIcon :width="25" :height="25" />
              </div>
              <div v-else-if="character.gender == 'Female'">
                <FemaleIcon :width="25" :height="25" />
              </div>
              <div v-else>
                <UnknownIcon :width="25" :height="25" />
              </div>
            </div>
            <div class="">
              <div v-if="character.status == 'Alive'">
                <AliveIcon :width="25" :height="25" />
              </div>
              <div v-else-if="character.status == 'Dead'">
                <DeadIcon :width="25" :height="25" />
              </div>
              <div v-else>
                <QuestionIcon :width="25" :height="25" />
              </div>
            </div>
          </div>
        </div>
        <p class="text-xl font-normal mt-2">
          Created : {{ new Date(character.created).toLocaleDateString() }}
        </p>
      </div>
      <div class="flex flex-nowrap gap-8">
        <div class="space-y-4">
          <h3 class="font-semibold text-4xl">Location</h3>
          <div class="space-y-2">
            <p class="font-medium text-2xl">Name: {{ character.location.name }}</p>
            <p class="font-medium text-xl">Type: {{ character.location.type }}</p>
            <p class="font-normal text-xl">
              Dimension: {{ character.location.dimension }}
            </p>
          </div>
          <Caroussel :dataArray="character.location.residents" />
          <!-- <div class="grid grid-cols-3 gap-2">
            <div
              class="flex flex-col justify-center items-center"
              v-for="resident in character.location.residents"
              :key="resident.id"
            >
              <img class="w-24 h-24 rounded-full" :src="resident.image" alt="" />
              <p class="font-medium text-sm">{{ resident.name }}</p>
            </div>
          </div> -->
        </div>
      </div>
      {{ character.location }}
    </div>
  </div>
</template>

<script>
import { useQuery, useResult } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { reactive } from "vue";
import { useRoute } from "vue-router";
import LoadingIcon from "../components/icons/LoadingIcon.vue";
import MaleIcon from "../components/icons/MaleIcon.vue";
import FemaleIcon from "../components/icons/FemaleIcon.vue";
import UnknownIcon from "../components/icons/UnknownIcon.vue";
import AliveIcon from "../components/icons/AliveIcon.vue";
import DeadIcon from "../components/icons/DeadIcon.vue";
import QuestionIcon from "../components/icons/QuestionIcon.vue";
import Caroussel from "../components/Caroussel.vue";

export default {
  setup() {
    const route = useRoute();
    const variables = reactive({
      characterId: route.params.id.toString(),
    });
    const { result, loading, error } = useQuery(
      gql`
        query QuegetCharacterById($characterId: ID!) {
          character(id: $characterId) {
            id
            image
            location {
              created
              dimension
              id
              name
              type
              residents {
                name
                image
                id
              }
            }
            gender
            episode {
              air_date
              created
              episode
              id
              name
            }
            name
            # origin {
            #   created
            #   dimension
            #   id
            #   name
            #   type
            # }
            species
            status
            type
            created
          }
        }
      `,
      variables
    );
    function selectPage(page) {
      variables.page = page;
    }
    const character = useResult(result, null, (data) => data.character);
    return {
      character,
      loading,
      error,
      selectPage,
      variables,
    };
  },
  components: {
    LoadingIcon,
    MaleIcon,
    FemaleIcon,
    UnknownIcon,
    AliveIcon,
    DeadIcon,
    QuestionIcon,
    Caroussel,
  },
};
</script>

<style></style>
