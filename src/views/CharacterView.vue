<template>
  <div class="character_container flex my-8 mx-4">
    <div
      v-if="loading"
      class="bg-primary-blue self-center flex text-white w-max items-center rounded-md py-12 px-14 text-5xl font-black mx-auto my-8"
    >
      <LoadingIcon />
      Loading...
    </div>
    <div v-else-if="error">
      Error: {{ error.message }}
      {{ result }}
    </div>
    <div v-else-if="character" class="space-y-8 mx-auto pt-8 md:max-w-5xl">
      <div class="flex gap-4">
        <img class="w-44 h-44 rounded-full" :src="character.image" alt="" />
        <div class="flex flex-col gap-2">
          <p class="text-4xl font-medium">{{ character.name }}</p>
          <p v-if="character.type" class="text-2xl font-normal">
            Type: {{ character.type }}
          </p>
          <p class="text-xl font-normal">Species : {{ character.species }}</p>
          <div class="flex gap-4">
            <GenderIcon :gender="character.gender" />
            <StatusIcon :status="character.status" />
          </div>
        </div>
        <!-- <p class="text-xl font-normal mt-2">
          Created : {{ new Date(character.created).toLocaleDateString() }}
        </p> -->
      </div>
      <div
        class="flex flex-col md:flex-row justify-between gap-8 bg-white px-8 py-8 rounded-lg"
      >
        <div class="space-y-4">
          <h3 class="font-semibold text-4xl">Location</h3>
          <div class="space-y-2">
            <p class="font-medium text-2xl">Name: {{ character.location.name }}</p>
            <p class="font-medium text-xl">Type: {{ character.location.type }}</p>
            <p class="font-normal text-xl">
              Dimension: {{ character.location.dimension }}
            </p>
          </div>
        </div>
        <div>
          <h3 class="font-medium text-2xl mb-4">Residents :</h3>
          <Caroussel page_name="Character" :dataArray="character.location.residents" />
        </div>
        <!-- <div class="space-y-4">
          <h3 class="font-semibold text-4xl">Origin</h3>
          <div class="space-y-2">
            <p class="font-medium text-2xl">Name: {{ character.origin.name }}</p>
            <p class="font-medium text-xl">Type: {{ character.origin.type }}</p>
            <p class="font-normal text-xl">Dimension: {{ character.origin.dimension }}</p>
          </div>
          <h3 class="font-medium text-3xl">Residents :</h3>
          <Caroussel v-if="character.origin.residents" page_name="Character" :dataArray="character.origin.residents" />
        </div> -->
      </div>
      <div class="w-full bg-white px-8 py-8 rounded-lg">
        <h3 class="font-semibold text-4xl">Episode :</h3>
        <div class="grid gap-2 md:grid-cols-4 md:gap-4 mt-4">
          <div
            class="flex flex-col w-40 bg-primary-blue/60 p-4 box-content rounded-xl gap-4 mx-auto"
            v-for="episode in character.episode"
            :key="episode.id"
          >
            <img class="rounded-md" src="@/assets/rick_morty_affiche.png" alt="" />
            <p class="text-center text-lg font-medium">{{ episode.name }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useQuery, useResult } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { reactive, watch } from "vue";
import { useRoute } from "vue-router";
import LoadingIcon from "../components/icons/LoadingIcon.vue";
import Caroussel from "../components/Caroussel.vue";
import StatusIcon from "../components/StatusIcon.vue";
import GenderIcon from "../components/GenderIcon.vue";

export default {
  setup() {
    const route = useRoute();
    const variables = reactive({
      characterId: route.params.id.toString(),
    });
    watch(route, (currentValue) => {
      if (currentValue.name == "Character") {
        variables.characterId = currentValue.params.id.toString();
      }
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
      result,
      loading,
      error,
      selectPage,
      variables,
    };
  },
  components: {
    LoadingIcon,
    Caroussel,
    StatusIcon,
    GenderIcon,
  },
};
</script>

<style scoped>
.character_container {
  min-height: 80vh;
}
</style>
