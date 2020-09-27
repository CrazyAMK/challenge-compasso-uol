<template>
  <div>
    <div v-if="repos.length" class="results mt-5">
      <h2>{{ title }}</h2>
      <hr />
      <ul class="mt-4">
        <li v-for="repo in repos" class="col-12 m-0">
          <a :href="repo.html_url" target="_blank">{{ repo.name }}</a>
        </li>
      </ul>
    </div>
    <div v-else-if="repos.length == 0" class="mt-5">
      <h2>{{ title }}</h2>
      <hr />
      <p class="alert alert-danger" role="alert">Repositories not found</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repos", "title"],
};
</script>

<style scoped>
</style>