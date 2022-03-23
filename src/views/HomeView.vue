<template>
  <main>
    <div class="home_container flex flex-col md:flex-row p-2 md:p-4 my-6 gap-4">
      <div>
        <div class="filter_container space-y-12 bg-white rounded-md p-4 sticky top-12">
          <TextInputContainer :variables="variables" />
          <RadioInputContainer :variables="variables" />
        </div>
      </div>
      <div class="data_container bg-white rounded-md p-4">
        <div
          v-if="loading"
          class="bg-primary-blue flex text-white w-max items-center rounded-md py-2 px-4 text-xl mx-auto my-8"
        >
          <LoadingIcon />
          Loading...
        </div>
        <div v-else-if="error">Error: {{ error.message }}</div>
        <div v-else-if="info && characters">
          <Pagination
            v-if="info"
            :info="info"
            :page="variables.page"
            @selectPage="selectPage"
          />
          <div
            class="list_characters_container flex flex-col md:flex-row md:flex-wrap justify-between space-y-4 gap-2"
          >
            <RouterLink :to="{ name: 'Character', params: { id: character.id} }"
              class="list_character flex items-center justify-between gap-6 py-4 px-2 rounded-xl hover:bg-primary-yellow/50"
              v-for="character of characters"
              :key="character.id"
            >
              
              <img class="w-24 h-24 rounded-full" :src="character.image" alt="" />
              <div class="flex flex-col flex-1">
                <p class="text-2xl font-medium">{{ character.name }}</p>
                <p v-if="character.type" class="text-lg font-normal">
                  Type: {{ character.type }}
                </p>
                <p class="text-lg font-normal">Species : {{ character.species }}</p>
              </div>
              <div class="pr-4 space-y-2">
                <div>
                  <div v-if="character.gender == 'Male'">
                    <MaleIcon width="25" height="25" />
                  </div>
                  <div v-else-if="character.gender == 'Female'">
                    <FemaleIcon width="25" height="25" />
                  </div>
                  <div v-else>
                    <UnknownIcon width="25" height="25" />
                  </div>
                </div>
                <div class="">
                  <div v-if="character.status == 'Alive'">
                    <AliveIcon width="25" height="25" />
                  </div>
                  <div v-else-if="character.status == 'Dead'">
                    <DeadIcon width="25" height="25" />
                  </div>
                  <div v-else>
                    <QuestionIcon width="25" height="25" />
                  </div>
                </div>
              </div>
            </RouterLink>
          </div>
          <Pagination
            v-if="info"
            :info="info"
            :page="variables.page"
            @selectPage="selectPage"
          />
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { RouterLink } from "vue-router";
import { useQuery, useResult } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { reactive } from "vue";
import Button from "@/components/ui/Button.vue";
import Pagination from "@/components/Pagination.vue";
import TextInputContainer from "@/components/TextInputContainer.vue";
import RadioInputContainer from "@/components/RadioInputContainer.vue";
import LoadingIcon from "../components/icons/LoadingIcon.vue";
import MaleIcon from "../components/icons/MaleIcon.vue";
import FemaleIcon from "../components/icons/FemaleIcon.vue";
import UnknownIcon from "../components/icons/UnknownIcon.vue";
import AliveIcon from "../components/icons/AliveIcon.vue";
import DeadIcon from "../components/icons/DeadIcon.vue";
import QuestionIcon from "../components/icons/QuestionIcon.vue";

export default {
  setup() {
    const variables = reactive({
      page: 1,
      filter: {
        name: null,
        gender: null,
        gender: null,
      },
    });
    const { result, loading, error } = useQuery(
      gql`
        query getCharactersByPage($page: Int, $filter: FilterCharacter) {
          characters(page: $page, filter: $filter) {
            results {
              id
              name
              gender
              status
              type
              species
              image
            }
            info {
              prev
              pages
              next
              count
            }
          }
        }
      `,
      variables
    );
    function selectPage(page) {
      variables.page = page;
    }
    const characters = useResult(result, null, (data) => data.characters.results);
    const info = useResult(result, null, (data) => data.characters.info);
    return {
      characters,
      loading,
      error,
      selectPage,
      variables,
      info,
    };
  },
  components: {
    Button,
    Pagination,
    TextInputContainer,
    RadioInputContainer,
    LoadingIcon,
    MaleIcon,
    FemaleIcon,
    UnknownIcon,
    AliveIcon,
    DeadIcon,
    QuestionIcon,
    RouterLink,
  },
};
</script>

<style lang="postcss" scoped>
/* .home_container {
  max-height: 80vh;
} */
.data_container {
  min-width: 60vw;
}
/* .list_characters_container {
  max-height: 100vh;
} */

@screen md {
  .list_character {
    min-width: 45%;
    max-width: 45%;
  }
}
</style>
