<template>
  <div id="app" class="container">
    <Search @onSearch="handleSearch"></Search>

    <template v-if="user">
      <UserDetails :data="user"></UserDetails>
      <Buttons @clickButton="handleRepos" :username="user.login"></Buttons>
    </template>

    <template v-if="repos">
      <Results :repos="repos" :errors="reposErrorMsg">
        <h2 slot="title">{{ titleBtnClicked }}</h2>
      </Results>
    </template>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import UserDetails from "./components/UserDetails.vue";
import Results from "./components/Results.vue";
import Buttons from "./components/Buttons.vue";

export default {
  name: "App",
  components: {
    Search,
    UserDetails,
    Buttons,
    Results,
  },
  data() {
    return {
      user: null,
      repos: null,
      isShowDetails: false,
      titleBtnClicked: "Repositories",
      reposErrorMsg: "",
    };
  },

  methods: {
    handleSearch(data) {
      this.user = data;
      this.repos = null;
    },
    handleRepos(data) {
      this.titleBtnClicked = data.title;
      this.repos = data.repos;
      this.reposErrorMsg = data.errors;
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
  margin-bottom: 60px;
}
</style>
