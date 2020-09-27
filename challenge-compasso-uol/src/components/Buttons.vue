<template>
  <div>
    <div class="col-12 mt-4 text-center">
      <button @click="ViewRepos" class="btn btn-outline-success">Repos</button>
      <button @click="ViewStarred" class="btn btn-outline-success">
        Starred
      </button>
    </div>
    <Results :repos="repos" v-show="isShowResult" :title="title"></Results>
  </div>
</template>
<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

import Results from "./Results";

Vue.use(VueAxios, axios);

export default {
  components: {
    Results,
  },
  props: {
    username: {
      type: String,
      required: true,
    },
    title: {
      type: String,
    },
  },
  data() {
    return {
      repos: [],
      isShowResult: false,
    };
  },
  methods: {
    ViewRepos() {
      const api = `https://api.github.com/users/${this.username}/repos`;
      Vue.axios.get(api).then((response) => {
        this.repos = response.data;
        this.isShowResult = true;
        this.title = "User Repositories";
      });
      this.$emit("ViewRepos", this.title);
    },
    ViewStarred() {
      console.log(this.username);
      const api = `https://api.github.com/users/${this.username}/starred`;
      Vue.axios.get(api).then((response) => {
        this.repos = response.data;
        this.isShowResult = true;
        this.title = "Starred Repositories";
      });
      this.$emit("ViewStarred", this.title);
    },
  },
};
</script>

<style scoped>
</style>