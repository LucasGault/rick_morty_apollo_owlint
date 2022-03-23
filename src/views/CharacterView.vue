<template>
  <div class="">
    <div
      v-if="loading"
      class="bg-primary-blue flex text-white w-max items-center rounded-md py-2 px-4 text-xl mx-auto my-8"
    >
      <LoadingIcon />
      Loading...
    </div>
    <div v-else-if="error">Error: {{ error.message }}</div>
    <div v-else-if="character">
      {{ character }}
    </div>
  </div>
</template>

<script>
import { useQuery, useResult } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { reactive } from "vue";
import { useRoute } from "vue-router";
import LoadingIcon from "../components/icons/LoadingIcon.vue";

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
            # location {
            #   created
            #   dimension
            #   id
            #   name
            #   type
            # }
            gender
            # episode {
            #   air_date
            #   created
            #   episode
            #   id
            #   name
            # }
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
  components: { LoadingIcon },
};
</script>

<style></style>
