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
          id="search-input"
          title="Input Enter an username..."
          placeholder="Enter an username..."
        />
      </div>
      <button class="btn btn-outline-success my-2 my-sm-0" type="submit">
        Search
      </button>
    </form>
    <div v-if="errorsMsg">
      <p class="alert alert-danger" role="alert">{{ errorsMsg }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: "",
      data: [],
      errorsMsg: "",
    };
  },
  methods: {
    async search() {
      this.errorsMsg = "";
      let data = null;
      const api = `https://api.github.com/users/${this.username}`;

      try {
        let response = await this.axios.get(api);
        data = response.data;
      } catch (error) {
        const { status, statusText } = error.response;
        if (status === 404) {
          this.errorsMsg = "User not found";
        } else {
          this.errorsMsg = "API Error: " + statusText;
        }
      }

      this.$emit("onSearch", data);
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
</style>