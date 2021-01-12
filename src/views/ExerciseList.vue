<template>
  <div class="wrapper">
  <div id="ExerciseList" class="ExerciseList">
    <input id="ExerciseSearch"
      name="ExerciseSearch"
      v-model="exerciseSearchPhrase"
      @input="handleSearch"
    />
    <button id="ListBtn"
      name="ListBtn"
      @click="handleSearch"
      >GO!</button>
  </div>
  <ul>
    <li v-for="item in results" :key="item.doc._id">
      <p>{{ item.doc.title }}</p>
    </li>
  </ul>
  </div>
</template>
<script>
import axios from 'axios';

const SlfTstApi = 'http://192.168.56.115/slftstapi/api/v1';
export default {
  name: 'ExerciseSearch',
  data() {
    return {
      exerciseSearchPhrase: '',
      results: [],
    };
  },
  methods: {
    handleSearch() {
      console.log(this.exerciseSearchPhrase);
      axios.get(`${SlfTstApi}/exercises`)
        .then((response) => {
          console.log(response.data);
          this.results = response.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style lang="scss" scoped>
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
