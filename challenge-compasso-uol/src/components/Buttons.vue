<template>
  <div>
    <div class="col-12 mt-4 text-center">
      <button @click="viewRepos" class="btn btn-outline-success">Repos</button>
      <button @click="viewStarred" class="btn btn-outline-success">
        Starred
      </button>
    </div>
    <!-- <Results :repos="repos" v-show="isShowResult">
      <h2 slot="title">{{ title }}</h2>
    </Results> -->
  </div>
</template>
<script>
export default {
  props: {
    username: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      repos: null,
      errorsMsg: "",
      title: "Repositories",
    };
  },
  methods: {
    async viewRepos() {
      let data = null;
      this.errorsMsg = "";
      const api = `https://api.github.com/users/${this.username}/repos`;
      this.title = "User Repositories";
      try {
        let response = await this.axios.get(api);
        data = response.data;
        if (data.length == 0) {
          this.errorsMsg = "Repositories not found";
        }
      } catch (error) {
        const { status, statusText } = error.response;
        if (status === 404) {
          this.errorsMsg = "User not found";
        } else {
          this.errorsMsg = "API Error: " + statusText;
        }
      }
      this.$emit("clickButton", {
        title: this.title,
        repos: data,
        errors: this.errorsMsg,
      });
    },
    async viewStarred() {
      let data = null;
      this.errorsMsg = "";
      const api = `https://api.github.com/users/${this.username}/starred`;
      this.title = "Starred Repositories";
      try {
        let response = await this.axios.get(api);
        data = response.data;
        if (data.length == 0) {
          this.errorsMsg = "Repositories not found";
        }
      } catch (error) {
        console.log(error.response);
        const { status, statusText } = error.response;
        if (status === 404) {
          this.errorsMsg = "Repositories not found";
        } else {
          this.errorsMsg = "API Error: " + statusText;
        }
      }

      this.$emit("clickButton", {
        title: this.title,
        repos: data,
        errors: this.errorsMsg,
      });
    },
  },
};
</script>

<style scoped>
</style>