<template>
  <div>
    <h1 class="text-center">Search a GitHub User</h1>
    <form v-on:submit.prevent="search" class="search-box text-center mb-5">
      <div class="form-group has-search">
        <span class="fa fa-search form-control-feedback"></span>
        <input
          type="text"
          v-model="username"
          class="form-control"
          placeholder="Enter an username..."
        />
      </div>
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
        Search
      </button>
    </form>

    <UserDetails :data="data" v-show="isShowDetails"></UserDetails>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";

Vue.use(VueAxios, axios);

//Components

import UserDetails from "./UserDetails.vue";
import Results from "./Results.vue";

export default {
  components: { UserDetails, Results },
  data() {
    return {
      username: "",
      data: [],
      isShowDetails: false,
      isShowResults: false,
      errorsMsg: "",
    };
  },
  methods: {
    search() {
      const api = `https://api.github.com/users/${this.username}`;
      this.isShowResults = true;
      Vue.axios
        .get(api)
        .then((response) => {
          this.data = response.data;
          this.isShowDetails = true;
        })
        .catch((error) => {
          this.errorsMsg = "User not found";
          this.data = [];
          this.isShowDetails = true;
        });
    },
  },
  mounted() {
    this.$nextTick(function () {
      let userSet = window.location.href;
      userSet = userSet.replace("#/", "");
      userSet = userSet.split("/")[3];
      $(".search-box input").val(userSet);
      $(".search-box input").value = userSet;
    });
  },
};
</script>

<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  /* color: #42b983; */
}
</style>