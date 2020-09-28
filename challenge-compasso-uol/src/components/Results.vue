<template>
  <div>
    <div v-if="repos.length" class="results mt-5">
      <slot name="title"></slot>
      <hr />
      <ul class="mt-4 list-group list-group-flush">
        <li v-for="repo in repos" class="col-12 m-0">
          <a
            :href="repo.html_url"
            target="_blank"
            class="list-group-item list-group-item-action"
            >{{ repo.name }}</a
          >
        </li>
      </ul>
    </div>
    <div v-else-if="repos.length == 0" class="mt-5">
      <slot name="title">Repositorios</slot>
      <hr />
      <p class="alert alert-danger" role="alert">Repositories not found</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["repos"],
};
</script>

<style scoped>
ul {
  list-style: none;
}
ul li:first-child a {
  border-top: none;
}
</style>