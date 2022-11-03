<template>
  <div>
    <h1>The Breaking Bad</h1>

    <table>
      <tbody>
        <tr v-for="todo in result" :key="todo.char_id">
          {{
            todo.name
          }}
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    result: null,
  }),
  mounted() {
    this.getTodos();
  },
  methods: {
    getTodos() {
      axios
        .get("https://www.breakingbadapi.com/api/characters/1")
        .then((response) => {
          console.log(response);
          this.result = response.data;
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>

<style scoped lang="scss"></style>
