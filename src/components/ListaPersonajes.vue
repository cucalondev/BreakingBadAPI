<template>
  <div>
    <table>
      <tbody>
        <tr v-for="todo in result" :key="todo.char_id">
          <img :src="todo.img" />
          {{
            todo.name
          }}
          <br />
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
        .get("https://www.breakingbadapi.com/api/characters/")
        .then((response) => {
          console.log(response);
          this.result = response.data;
        })
        .catch((e) => console.log(e));
    },
  },
};
</script>
<style>
img {
  height: 150px;
  width: 100px;
  object-fit: cover;
  margin-right: 10px;
  border: 2px solid black;
  border-radius: 3px;
}
</style>
